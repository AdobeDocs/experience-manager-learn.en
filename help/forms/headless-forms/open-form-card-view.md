---
title: Click on card to display the form
description: Drill down on form from card view
feature: Adaptive Forms
version: 6.5
kt: 13372
topic: Development
role: User
level: Intermediate
exl-id: c8684cd9-b9c5-4b5b-b990-27c5700cea9f
---
# Displaying the form on card click

The following code was used to display the form when the user clicks on a card. The path of the form to display is extracted from the url using the useParams function.

``` javascript
import Form from './components/Form';
import PlainText from './components/plainText';
import TextField from './components/TextField';
import Button from './components/Button';
import Panel from './components/Panel';
import { useState,useEffect } from "react";
import {Link, useParams} from 'react-router-dom';
import { AdaptiveForm } from "@aemforms/af-react-renderer";
export default function DisplayForm()
{
   const [selectedForm, setForm] = useState("");
   const params = useParams();
   const extendMappings =
    {
        'plain-text' : PlainText,
        'text-input' : TextField,
        'button' : Button,
        'form': Form
    };
    
    
   const getAFForm = async () =>
    {
           
        const resp = await fetch(`/adobe/forms/af/${params.formID}`);
        let formJSON = await resp.json();
        console.log("The contact form json is "+formJSON);
        setForm(formJSON.afModelDefinition)
    }
    
    useEffect( ()=>{
        getAFForm()
        

    },[]);
    return(
       <div>
           <AdaptiveForm mappings={extendMappings} formJson={selectedForm}/>
        </div>
    )
}
```

## Next Steps

[Display thank you message on form submission](./display-thank-you-message.md)
