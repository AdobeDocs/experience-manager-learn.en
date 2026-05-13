---
title: Fetch the JSON of the Adaptive Form to embed
description: Use the API to fetch the json of the adaptive form
feature: Adaptive Forms
version: Experience Manager 6.5
jira: KT-13285
topic: Development
role: User
level: Intermediate
exl-id: ee534724-54ea-48e1-8c92-de1c56a928d4
duration: 50
TQID: https://experienceleague.adobe.com/WUK7WRf-Ej-esPMzMZXfDRzYGr63RWs3JcaES6fLFfM
product_v2:
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
---
# Fetch the JSON of the Form

Login to your AEM Forms author instance and create a new adaptive using the **Blank with Core Components** template. Publish your form to your publish instance.

To embed the form, we first fetch the json of the adaptive form by making a get call against our publish server.

The following code snippet fetches the json of the adaptive form called **contactus**

``` javascript
const getForm = async () => {
        
        const resp = await fetch('/adobe/forms/af/L2NvbnRlbnQvZm9ybXMvYWYvZmlyc3RoZWFkbGVzcw==');
        // Get the form id manually using the listform api
        let formJSON = await resp.json();
        console.log("The contact form json is "+formJSON);
        setForm(formJSON.afModelDefinition)
      }
```

The complete code of the Contact function component is given below

``` javascript
import Form from './components/Form';
import PlainText from './components/plainText';
import TextField from './components/TextField';
import Button from './components/Button';
import Panel from './components/Panel';
import { useState,useEffect } from "react";
import { AdaptiveForm } from "@aemforms/af-react-renderer";

export default function Contact(){
   const [selectedForm, setForm] = useState("");
   const extendMappings = {
        'plain-text' : PlainText,
        'text-input' : TextField,
        'button' : Button,
        'form': Form
      };
    const getForm = async () => {
        
        const resp = await fetch('/adobe/forms/af/dor/L2NvbnRlbnQvZm9ybXMvYWYvcmlzaGk=');
        let formJSON = await resp.json();
        setForm(formJSON.afModelDefinition)
      
      }
      useEffect( ()=>{
        getForm();
        

    },[]);
    return(
        
        <div>
            <h1>Get in touch with us!!!!</h1>
            <AdaptiveForm mappings={extendMappings} formJson={selectedForm} />
      
          
        </div>
    )
}
```

The above code uses native html components which are mapped to the components used in the adaptive form. For example we are mapping the text-input adaptive form component to TextField component. The native components used in the article [can be downloaded from here](./assets/native-components.zip)

## Next Steps

[Select a form from drop-down list](./select-form-from-drop-down-list.md)
