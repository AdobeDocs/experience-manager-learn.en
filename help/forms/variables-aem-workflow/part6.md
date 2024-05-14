---
title: Logging Variables in AEM Workflow[Part6]
description: Log the value of AEM workflow variables
version: 6.5
topic: Development
feature: Adaptive Forms, Workflow
role: Developer
level: Beginner
jira: KT-13783
exl-id: 6afb3a52-9879-4393-8efd-ec3e5c303063
duration: 84
---
# Log the variables value in AEM Workflow

Logging the value of variables is a common practice in software development. It helps developers track and understand how a AEM workflow is executing,diagnose issues and montior the flow of the data within an AEM workflow.



The following code asscociated with a custom process step logs the value of all types of variables except of type FormDataModel.

```java
package com.variablelogger.core;
import com.adobe.aemfd.docmanager.Document;
import com.adobe.granite.workflow.WorkflowException;
import com.adobe.granite.workflow.WorkflowSession;
import com.adobe.granite.workflow.exec.WorkItem;
import com.adobe.granite.workflow.exec.WorkflowProcess;
import com.adobe.granite.workflow.metadata.MetaDataMap;
import com.adobe.granite.workflow.model.VariableTemplate;
import org.osgi.framework.Constants;
import org.osgi.service.component.annotations.Component;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import java.io.File;
import java.io.IOException;
import java.util.Iterator;
import java.util.Map;

@Component(property = {
        Constants.SERVICE_DESCRIPTION + "=Log workflow process variables",
        Constants.SERVICE_VENDOR + "=Adobe Systems",
        "process.label" + "=Log workflow process variables"
})
public class LogWorkflowVariables implements WorkflowProcess {
    Logger log = LoggerFactory.getLogger(this.getClass());
    private void writeListOfString(String[] stringArray)
    {

        for (int i = 1; i <= stringArray.length; i++)
        {
            log.debug("Got String " + stringArray[i]);
        }

    }
    private void writeListOfDocuments(Object[] documentsArray)
    {
        log.debug(" Got "+documentsArray.length+" files to write to file system");

        for(int i=0;i<documentsArray.length;i++)
            {
                Document attachment = (Document) documentsArray[i];
                try
                    {
                        String[] path = attachment.getAttribute("adobe.docmanager.attribute.filename").toString().split("/");
                        log.debug("The attachment name is "+ path[1]);
                        attachment.copyToFile(new File(path[1]));
                        attachment.close();
                    }
                    catch (IOException e)
                    {
                        throw new RuntimeException(e);
                    }
            }

    }
    private void writeDocument(Document documentToWrite,String key)
    {
        log.debug(" Writing Document  "+key);

        if (documentToWrite!=null)
        {
            try
                {

                        documentToWrite.copyToFile(new File(key + ".pdf"));
                        documentToWrite.close();
                }
             catch (IOException e)
                 {
                    throw new RuntimeException(e);
                }

        }

    }
    
    @Override
    public void execute(WorkItem workItem, WorkflowSession workflowSession, MetaDataMap metaDataMap) throws WorkflowException
    {
            log.debug("Logging variable info for "+ workItem.getWorkflow().getWorkflowModel().getTitle()+" workflow ");
            log.debug("Logging variable info for payload path "+ workItem.getWorkflowData().getPayload().toString());
            MetaDataMap metaMap = workItem.getWorkflow().getWorkflowData().getMetaDataMap();
            Map <String,com.adobe.granite.workflow.model.VariableTemplate>variableTemplateMap = workItem.getWorkflow().getWorkflowModel().getVariableTemplates();
            Iterator<String> templateIterator = variableTemplateMap.keySet().iterator();
            while(templateIterator.hasNext())
                {
                    String key = templateIterator.next();
                    VariableTemplate vt = variableTemplateMap.get(key);
                    log.debug("The variable  "+key+" is of type "+vt.getType()+" and its sub type is  "+vt.getSubType());
                    if(vt.getType().equalsIgnoreCase("com.adobe.aemfd.docmanager.Document"))
                        {
                            Document documentToWrite = metaMap.get(key, Document.class);
                            if(documentToWrite!=null)
                                writeDocument((Document) metaMap.get(key),key);
                        }
                    if(vt.getType().equalsIgnoreCase("java.util.ArrayList"))
                        {
                            if(vt.getSubType().equalsIgnoreCase("com.adobe.aemfd.docmanager.Document"))
                                {
                                    log.debug("Got Array List " + key);
                                    Document[] documentsArray = metaMap.get(key, Document[].class);
                                    if(documentsArray!=null)
                                        writeListOfDocuments(documentsArray);
                                }
                            if(vt.getSubType().equalsIgnoreCase("java.lang.String"))
                                {
                                    log.debug("Got Array List of Strings " + key);
                                    String[] stringArray = metaMap.get(key, String[].class);
                                    if(stringArray!=null)
                                        writeListOfString(stringArray);
                                }
                        }
                    if(vt.getType().equalsIgnoreCase("java.util.Date"))
                    {
                        log.debug("Got Date  "+key);
                        java.util.Date dateVariable = metaMap.get(key,java.util.Date.class);
                        if(dateVariable!=null)
                            log.debug("The value of  "+key+ " is  "  +dateVariable.toString());
                    }
                    if(vt.getType().equalsIgnoreCase("java.lang.Boolean"))
                    {
                        log.debug("Got Boolean "+key);
                        Boolean booleanVariable = metaMap.get(key,java.lang.Boolean.class);
                        if(booleanVariable!=null)
                            log.debug("The value of "+key+" is  "+String.valueOf(booleanVariable));
                    }
                    if(vt.getType().equalsIgnoreCase("org.w3c.dom.Document"))
                        {
                            log.debug("Got XML Document "+key);
                            String xmlDocument = metaMap.get(key,String.class);
                            if(xmlDocument!=null)
                                log.debug("The value of xml Document is  "+xmlDocument);
                        }
                if( (vt.getType().equalsIgnoreCase("com.google.gson.JsonObject") )|| (vt.getType().equalsIgnoreCase("java.lang.String")))
                        {
                            log.debug("Got String/Json variable");
                            if(metaMap.get(key)!=null)
                                log.debug("The value of  "+key+" is  "+metaMap.get(key));
                        }

                }
        log.debug("Finished logging variable info for "+ workItem.getWorkflow().getWorkflowModel().getTitle()+" workflow ");
        log.debug("Finished logging variable info for  payload path "+ workItem.getWorkflowData().getPayload().toString());

    }

}

```

>[!NOTE]
>
>The documents are saved  in the root folder of your AEM server installation.

## Deploy the sample bundle

[Deploy the variable logger bundle](assets/VariableLogger.core-1.0.0-SNAPSHOT.jar) using the Felix web console.
Associate this bundle with a process step in your AEM workflow to log the value of the String and Document variable.
