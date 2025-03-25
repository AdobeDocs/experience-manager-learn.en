---
title: Displaying DAM images inline in Adaptive Forms
description: Display DAM images inline in Adaptive Forms
feature: Adaptive Forms
version: Experience Manager 6.4, Experience Manager 6.5
topic: Development
role: Developer
level: Experienced
last-substantial-update: 2022-10-20
thumbnail: inline-dam.jpg
kt: kt-11307
exl-id: 339eb16e-8ad8-4b98-939c-b4b5fd04d67e
duration: 60
---
# Display DAM image in Adaptive Forms

A common use case is to display the image(s) residing in the crx repository inline in an Adaptive Form. 

## Add placeholder image

The first step is to prepend a placeholder div to the panel component. In the code below the panel component is identified by its CSS class name of photo-upload. The JavaScript function is part of client library that is associated with the adaptive forms. This function is called in initialize event of the file attachment component.

```javascript
/**
* Add Placeholder Div
*/
function addPlaceholderDiv(){

     $(".photo-upload").prepend(" <div class='preview'' style='border:1px dotted;height:225px;width:175px;text-align:center'><br><br><div class='text'>The Image will appear here</div></div><br>");
}
```

### Display inline image

After the user has selected the image, the hidden field ImageName is populated with the selected image name. This image name is then passed to the damURLToFile function which invokes the createFile function to  convert a URL to a Blob for FileReader.readAsDataURL(). 

```javascript
/**
* DAM URL to File Object
* @return {string} 
 */
 function damURLToFile (imageName) {
   console.log("The image selected is "+imageName);
     createFile(imageName);
}

```

``` javascript
async function createFile(imageName){
  let response = await fetch('/content/dam/formsanddocuments/fieldinspection/images/'+imageName);
  let data = await response.blob();
    console.log(data);
  let metadata = {
    type: 'image/jpeg'
  };
  let file = new File([data], "test.jpg", metadata);
     let reader = new FileReader();
    reader.readAsDataURL(file);
     reader.onload = function() {
    console.log("finished reading ...."+reader.result);
    
  };
    var image  = new Image();
    $(".photo-upload .preview .imageP").remove();
    $(".photo-upload .preview .text").remove();
    image.width = 484;image.height = 334;
    image.className = "imageP";
    image.addEventListener("load", function () {
      $(".photo-upload .preview")[0].prepend(this);
    });
    
    console.log(window.URL.createObjectURL(file));
    image.src = window.URL.createObjectURL(file);

  }

```

### Deploy on your server

* Download and install the [client library and sample images](assets/InlineDAMImage.zip) on your AEM instance using AEM Package Manager.
* Download and install the [sample form](assets/FieldInspectionForm.zip) on you your AEM instance using AEM package manager.
* Point your browser to [FielInspectionForm](http://localhost:4502/content/dam/formsanddocuments/fieldinspection/fieldinspection/jcr:content?wcmmode=disabled)
* Select one of the fixture
* You should see the image displayed in the form
