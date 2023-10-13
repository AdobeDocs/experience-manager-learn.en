---
title: Fetch the JSON of the Adaptive Form to embed
description: Use the API to fetch the json of the adaptive form
feature: Adaptive Forms
version: 6.5
kt: 13285
topic: Development
role: User
level: Intermediate
exl-id: ee534724-54ea-48e1-8c92-de1c56a928d4
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
