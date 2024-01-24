---
title: Combining selected newsletters into one file
description: Combine selected newsletters using assembler service
feature: Adaptive Forms
version: 6.5
topic: Development
role: User
level: Beginner
last-substantial-update: 2023-01-01
exl-id: 3a64315f-f699-4538-b999-626e7a998c05
duration: 102
---
# Combine selected newsletters into one pdf

  The user's selections are stored in a hidden field. The value of this hidden field is passed to the servlet which will combine the selections into one pdf using [Forms Assembler service](https://developer.adobe.com/experience-manager/reference-materials/6-5/forms/javadocs/com/adobe/fd/assembler/service/AssemblerService.html).
  

## Servlet to assemble pdf files

 The following code does the assembling of the selected newsletters. The code creates map of documents from the user's selections. From this map a DDX is created and this DDX along with the map of documents is passed to the invoke method of Assembler service to get the combined document. The assembled pdf is stored in the repository and its path is returned to the calling application.

 ```java
 protected void doPost(SlingHttpServletRequest request,SlingHttpServletResponse response)
    {
    
        String []newsletters = request.getParameter("selectedNewsLetters").split(",");
        Map<String, Object> mapOfDocuments = new HashMap<String, Object>();
        for(int i= 0;i<newsletters.length;i++)
        {
            Resource resource = request.getResourceResolver().getResource(newsletters[i]);
            
            log.debug("The resource name is "+resource.getName());
            Document newsletter = new Document(resource.getPath());
            mapOfDocuments.put(resource.getName(), newsletter);
        }
        log.debug("The newsletters selected: "+newsletters);
        Document ddxDocument = createDDXFromMapOfDocuments(mapOfDocuments);
        AssemblerOptionSpec aoSpec = new AssemblerOptionSpec();
        aoSpec.setFailOnError(true);
        AssemblerResult ar = null;
        try {
                ar = assemblerService.invoke(ddxDocument, mapOfDocuments, aoSpec);
                Document assembledPDF = ar.getDocuments().get("GeneratedPDF.pdf");
                // This is my custom code to get fd-service user
                ResourceResolver formsServiceResolver = getResolver.getFormsServiceResolver();
                
                Resource nodeResource = formsServiceResolver.getResource("/content/newsletters");
            
                UUID uuid = UUID.randomUUID();
                String uuidString = uuid.toString();
                javax.jcr.Node assembledNewsletters = nodeResource.adaptTo(Node.class);
                javax.jcr.Node assembledNewsletter =  assembledNewsletters.addNode(uuidString + ".pdf", "nt:file");
                javax.jcr.Node resNode = assembledNewsletter.addNode("jcr:content", "nt:resource");
                ValueFactory valueFactory = formsServiceResolver.adaptTo(Session.class).getValueFactory();
                Binary contentValue = valueFactory.createBinary(assembledPDF.getInputStream());
                resNode.setProperty("jcr:data", contentValue);
                formsServiceResolver.commit();
                PrintWriter out = response.getWriter();
                response.setContentType("application/json");
                response.setCharacterEncoding("UTF-8");
                JsonObject asset = new JsonObject();
           
                asset.addProperty("assetPath", assembledNewsletter.getPath());
                out.print(new Gson().toJson(asset));
                out.flush();  
                
            } 
            catch (IOException | OperationException | RepositoryException e)
            {
            
                log.error("Error is "+e.getMessage());
            }
    }


 ``` 

## Utility functions

The following utility functions were used in assembling the newsletters. These utility functions create DDX from map of documents and convert the org.w3c.dom.Document into AEMFD document object.


```java
public Document createDDXFromMapOfDocuments(Map<String, Object> mapOfDocuments)
     {
         
        final DocumentBuilderFactory docFactory = DocumentBuilderFactory.newInstance();
        org.w3c.dom.Document ddx = null;
        try
               {
                   DocumentBuilder docBuilder = docFactory.newDocumentBuilder();
                   ddx = docBuilder.newDocument();
                   Element rootElement = ddx.createElementNS("http://ns.adobe.com/DDX/1.0/", "DDX");
                ddx.appendChild(rootElement);
                Element pdfResult = ddx.createElement("PDF");
                pdfResult.setAttribute("result","GeneratedPDF.pdf");
                rootElement.appendChild(pdfResult);
                for (String key : mapOfDocuments.keySet())
                    {
                        log.debug(key + " " + mapOfDocuments.get(key));
                        Element pdfSourceElement = ddx.createElement("PDF");
                        pdfSourceElement.setAttribute("source", key);
                        pdfSourceElement.setAttribute("bookmarkTitle",key);
                        pdfResult.appendChild(pdfSourceElement);
                    }
                return orgw3cDocumentToAEMFDDocument(ddx);
            }
            catch (ParserConfigurationException e)
                {
                    log.debug("Error:"+e.getMessage());
                }
            return null;
     }

```

```java
public Document orgw3cDocumentToAEMFDDocument( org.w3c.dom.Document xmlDocument)
     {
         final ByteArrayOutputStream outputStream = new ByteArrayOutputStream();
         DOMSource source = new DOMSource(xmlDocument);
         log.debug("$$$$In orgW3CDocumentToAEMFDDocument method");
         StreamResult outputTarget = new StreamResult(outputStream);
         try
             {
               TransformerFactory.newInstance().newTransformer().transform(source, outputTarget);
               InputStream is1 = new ByteArrayInputStream(outputStream.toByteArray());
               Document xmlAEMFDDocument = new Document(is1);
               if (log.isDebugEnabled())
                   {
                    xmlAEMFDDocument.copyToFile(new File("dataxmldocument.xml"));
                }
             return xmlAEMFDDocument;
            }
            catch (Exception e)
                 {
                    log.error("Error in generating ddx " + e.getMessage());
                    return null;
                 }
        }
```

## Next Steps

[Deploy the sample assets on your system](./deploy-on-your-system.md)