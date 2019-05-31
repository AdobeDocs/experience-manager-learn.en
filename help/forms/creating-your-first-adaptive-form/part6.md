---
title: Using functions and code editor
seo-title: Using functions and code editor
description: null
seo-description: null
uuid: 578e91f8-0d93-4192-b7af-1579df2feaf8
contentOwner: gbedekar
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: forms
topic-tags: adaptive_forms
discoiquuid: f480ef3e-7e38-4a6b-a223-c102787aea7f
---

# Using functions and code editor {#using-functions-and-code-editor}


In this part, we will use custom functions and the code editor to author business rules.

[ClientLib with custom function](assets/helpxclientlibs.zip).
Import and install the package into  crx  using the package manager. The package contains client library. Typically a client library consists of CSS and Javascript file. This client library contains javascript file which exposes a function to populate drop-down list values.


## Function to populate drop down list {#function-to-populate-drop-down-list}

Open the Adaptive Form in edit mode.

From the content hierarchy, select Form Container and click the wrench icon to open the properties sheet.

Set the value in the Client Library Category field to "  helpx ". Save your changes.This is the category defined in the client library that was imported in the earlier step.

Refresh your browser

Bring up the content hierarchy and select "what county do you live in" under the People panel.

Click on the hammer icon to bring up the rule editor.

Click Create to create a new rule.

Click on Form Objects and Functions to display the Form Objects and Functions panel on the left-hand side

Select "Set Options Of" from the drop-down list. The default selected value of the dropdown is "when".

In the select option drop-down list, select service output

Click on the "Functions" tab on the left-hand-side to list the functions.Drag and drop the "getCountyNamesList" on to the drop-down list where service output was selected in the previous step.

Click done to save your changes

Preview your form. "What county do you live in" drop-down list in the form is now populated with the return values of the function.

### Custom function to populate drop down list

>[!VIDEO](https://video.tv.adobe.com/v/22282?quality=9)

## Using code editor to set summary title of asset accordion {#using-code-editor-to-set-summary-title-of-asset-accordion}

Open the form in edit mode

Click on the content hierarchy icon on the left panel to bring up the content hierarchy.

Expand the Assets-&gt;Asset section

Click on "Type of Asset", click the wrench icon to open the properties sheet. Set the name to "assetType" and save your changes.

Similarly, set the name of "Value in Dollars" field to "valueInDollars" and save your changes.

Click on the "Asset" and select the hammer icon to open the rule editor.Click Create to create a new rule. By default visual editor is opened when you are creating a new rule. Switch to code editor by selecting code editor from the drop-down list on the right-hand-side.Since our rule is going to be slightly complex we will use the code editor to author our rule.

click on edit code. Click OK to dismiss the warning.Select "Summary" from the event drop-down list

Type the following code in the code editor. The code editor has code complete, syntax checking among other things.

```
if((assetType.value!==null)&&(valueInDollars.value!==null))
  {
    assetType.value+"-$"+valueInDollars.value;
  }
```

Preview your form. Tab to the Assets tab. Add a couple of assets. Make sure the summary changes accordingly

## Validate panels using rule editor {#validate-panels-using-rule-editor}

Make sure you are in the edit mode

Refresh your browser

Tap the "Next" button to bring up the component toolbar.

Click the "Hammer" icon to open the rule editor.

Click "Create" button to bring up the visual editor.

Switch to "Code Editor" by selecting "Code Editor" from the drop-down list. The drop-down list is on the right-hand side of the screen.

Copy on the **Edit Code** to edit the code

Select "Click" from the event drop-down list. The code we are going to add will be triggered when the next button is clicked.

Copy the following code into the code editor

``` javascript {.line-numbers}
//debugger;
var errors =[];
var currentPanel = guideBridge.getFocus({"focusOption": "navigablePanel"});
window.guideBridge.validate(errors,currentPanel);
console.log("The errors are "+ errors.length);
if(errors.length===0)
{
        window.guideBridge.setFocus(this.panel.somExpression, 'nextItem', true);
}
else
  {
        window.confirm("Please fill out all the required fields");
  }
```

You can uncomment line 1 to  debugg  the code in  browser  window.

Line 3 - Get the current panel

Line 4 - Validate the current panel.

Line 8 - If no errors move to the next panel

Preview the form, and test the newly enabled functionality.
