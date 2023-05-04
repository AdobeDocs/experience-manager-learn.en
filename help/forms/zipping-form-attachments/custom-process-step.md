---
title: Custom process step to zip file attachments
description: Custom process step to add the adaptive form attachments to a zip file and store the zip file into a workflow variable
feature: Adaptive Forms
version: 6.5
topic: Development
role: Developer
level: Beginner
kt: kt-8049
exl-id: 1131dca8-882d-4904-8691-95468fb708b7
---
# Custom Process Step


A custom process step was implemented to create the zip file containing the form attachments. If you are not familiar with creating OSGi bundle, please [follow these instructions](https://experienceleague.adobe.com/docs/experience-manager-learn/forms/creating-your-first-osgi-bundle/create-your-first-osgi-bundle.html?lang=en)

The code in the custom process step does the following

* Query for all the adaptive form attachments under the payload folder. Folder name is passed as a process argument to the process step.

* Create a zip file containing the form attachments and store it under the payload folder.
* Set the value of workflow variable (no_of_attachments)





```java

 package com.aemforms.formattachments.core;
import javax.jcr.Binary;
import javax.jcr.Node;
import javax.jcr.RepositoryException;
import javax.jcr.Session;
import javax.jcr.ValueFactory;

import javax.jcr.Node;
import javax.jcr.Session;

import org.osgi.framework.Constants;
import org.osgi.service.component.annotations.Component;
import org.osgi.service.component.annotations.Reference;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

import com.adobe.aemfd.docmanager.Document;
import com.adobe.granite.workflow.WorkflowException;
import com.adobe.granite.workflow.WorkflowSession;
import com.adobe.granite.workflow.exec.WorkItem;
import com.adobe.granite.workflow.exec.WorkflowProcess;
import com.adobe.granite.workflow.metadata.MetaDataMap;
import com.day.cq.search.PredicateGroup;
import com.day.cq.search.Query;
import com.day.cq.search.QueryBuilder;
import com.day.cq.search.result.Hit
import com.day.cq.search.result.SearchResult;


@Component(property = {
        Constants.SERVICE_DESCRIPTION + "=Zip form attachments",
        Constants.SERVICE_VENDOR + "=Adobe Systems",
        "process.label" + "=Zip form attachments"
})


public class ZipFormAttachments implements WorkflowProcess {

     private static final Logger log = LoggerFactory.getLogger(ZipFormAttachments.class);
     @Reference
     QueryBuilder queryBuilder;

     @Override
     public void execute(WorkItem workItem, WorkflowSession workflowSession, MetaDataMap processArguments) throws WorkflowException
     {
             String payloadPath = workItem.getWorkflowData().getPayload().toString();
             log.debug("The payload path  is" + payloadPath);
             MetaDataMap metaDataMap = workItem.getWorkflow().getWorkflowData().getMetaDataMap();
             Session session = workflowSession.adaptTo(Session.class);
             Map < String, String > map = new HashMap < String, String > ();
             map.put("path", workItem.getWorkflowData().getPayload().toString() + "/" + processArguments.get("PROCESS_ARGS", "string").toString());
             map.put("type", "nt:file");
             Query query = queryBuilder.createQuery(PredicateGroup.create(map), workflowSession.adaptTo(Session.class));
             query.setStart(0);
             query.setHitsPerPage(20);
             SearchResult result = query.getResult();
             log.debug("Get result hits " + result.getHits().size());
             ByteArrayOutputStream baos = new ByteArrayOutputStream();
             ZipOutputStream zipOut = new ZipOutputStream(baos);
             int no_of_attachments = result.getHits().size();
             for (Hit hit: result.getHits())
             {
                     try
                     {
                             String attachmentPath = hit.getPath();
                             log.debug("The hit path is" + hit.getPath());
                             Node attachmentNode = session.getNode(attachmentPath + "/jcr:content");
                             InputStream attachmentStream = attachmentNode.getProperty("jcr:data").getBinary().getStream();
                             ByteArrayOutputStream buffer = new ByteArrayOutputStream();
                             int nRead;
                             byte[] data = new byte[1024];
                             while ((nRead = attachmentStream.read(data, 0, data.length)) != -1)
                             {
                                     buffer.write(data, 0, nRead);
                             }

                             buffer.flush();
                             byte[] byteArray = buffer.toByteArray();
                             ZipEntry zipEntry = new ZipEntry(hit.getTitle());
                             zipOut.putNextEntry(zipEntry);
                             zipOut.write(byteArray);
                             zipOut.closeEntry();

                     } 
                     catch (Exception e)
                     {
                             log.debug("The error message is " + e.getMessage());
                     }
             }
             try
             {
                    zipOut.close();
                    Node payloadNode = session.getNode(payloadPath);
                    Node zippedFileNode =  payloadNode.addNode("zipped_attachments.zip", "nt:file");
                    javax.jcr.Node resNode = zippedFileNode.addNode("jcr:content", "nt:resource");
                
                    ValueFactory valueFactory = session.getValueFactory();
                    Document zippedDocument = new Document(baos.toByteArray());

                    Binary contentValue = valueFactory.createBinary(zippedDocument.getInputStream());
                    metaDataMap.put("no_of_attachments", no_of_attachments);

                    workflowSession.updateWorkflowData(workItem.getWorkflow(), workItem.getWorkflow().getWorkflowData());
                    log.debug("Updated workflow");
                    resNode.setProperty("jcr:data", contentValue);
                    session.save();
                    zippedDocument.close();



             }
             catch (IOException | RepositoryException e)
             {
                     
                     log.error("Error in closing zipout", e);
             }
             
            
             

     }

}

```

>[!NOTE]
>
> Please make sure you have a variable called  *no_of_attachments* of type Double in your workflow for this code to work.

## Next Steps

[Populate ArrayList workflow variables with Attachments and Attachment Name](./custom-process-step.md)
