---
title: Populate adaptive form using the setData method
description: Send the uploaded pdf file for data extraction and populate the adaptive form with the extracted data
feature: Adaptive Forms
version: 6.5
topic: Development
role: Developer
level: Beginner
jira: KT-14196
exl-id: f380d589-6520-4955-a6ac-2d0fcd5aaf3f
duration: 53
---
# Make Ajax Call

When the user has uploaded the pdf file, we need to make a POST call to a servlet and pass the uploaded PDF document in the POST request. The POST request returns a path to the exported data in the crx repository

```javascript
$("#fileElem").on('change', function (e) {
           console.log("submitting files");
           var filesUploaded = e.target.files;
           var ajaxData = new FormData($("#myform").get(0));
           for (var i = 0; i < filesUploaded.length; i++) {
               ajaxData.append(filesUploaded[i].name, filesUploaded[i]);
           }

           handleFiles(ajaxData);

       });

function handleFiles(formData) {
    console.log("File uploaded");

    $.ajax({
        type: 'POST',
        data: formData,
        url: '/bin/ExtractDataFromPDF',
        contentType: false,
        processData: false,
        cache: false,
        success: function (filePath) {
            console.log(filePath);
            guideBridge.setData({
                dataRef: filePath,
                error: function (guideResultObject) {
                    console.log("Error");
                }
            })
            

        }
    });
}

```

The servlet mounted on **_/bin/ExtractDataFromPDF_** extracts the data from the PDF file and returns the path of the crx node where the extracted data is stored.
The [GuideBridge setData](https://developer.adobe.com/experience-manager/reference-materials/6-5/forms/javascript-api/GuideBridge.html#setData__anchor) method is then used to set the data of the adaptive form.

## Next Steps

[Deploy the sample assets](./test-the-solution.md)
