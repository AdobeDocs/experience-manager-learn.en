---
title: Create Client Library
description: Client library code to fetch the next form to sign
feature: Adaptive Forms
version: 6.4,6.5
kt: 6907
thumbnail: 6907.jpg
topic: Development
role: Developer
level: Intermediate
---
# Create a Client Library

Create a custom Client Library, clientlib for short, to extract the url parameters pass those parameters in the GET call. The GET call is made to a servlet mounted on /bin/getnextformtosign which returns the url of the next form to sign in the package.

The following is the code used in the clientlib javascript function


```java
function getUrlVars()
{
    var vars = {};
    var parts = window.location.href.replace(/[?&]+([^=&]+)=([^&]*)/gi, function(m, key, value)
    {
        vars[key] = value;
    });
    return vars;
}

function navigateToNextForm()
{
    
    console.log("The id is " + guidelib.runtime.adobeSign.submitData.agreementId);
    var guid = getUrlVars()["guid"];
    var customerID = getUrlVars()["customerID"];
    console.log("The customer Id is " + customerID);
    $.ajax(
    {
        type: 'GET',
        url: '/bin/getnextformtosign?guid=' + guid + '&customerID=' + customerID,
        contentType: false,
        processData: false,
        cache: false,
        success: function(response)
        {
            console.log(response);
            var jsonResponse = JSON.parse(JSON.stringify(response));
            console.log(jsonResponse.nextFormToSign);
            var nextFormToSign = jsonResponse.nextFormToSign;
            if (nextFormToSign != "AllDone")
            {
                window.open(nextFormToSign, '_self');
            }
            else
            {
                window.open("http://localhost:4502/content/forms/af/formsandsigndemo/alldone.html", '_self');
            }

}
    });
}
$(document).ready(function()
{
    $(document).on("click", ".nextform", navigateToNextForm);
});

```

## Assets

[The clientlib can be downloaded from here](assets/get-next-form-client-lib.zip)
