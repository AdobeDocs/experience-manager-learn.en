---
title: Displaying inline images in Adaptive Forms
description: Display uploaded images inline in Adaptive Forms
feature: Adaptive Forms
topics: development
version: 6.3,6.4,6.5
topic: Development
role: Developer
level: Experienced
exl-id: 4a69513d-992c-435a-a520-feb9085820e7
---
# Inline images in Adaptive Forms

A common use case is to display the uploaded image as an inline image in Adaptive Form. By default, the uploaded image is shown as a link and this experience can be enhanced by displaying the image in Adaptive Form. This article will walk you through the steps involved in displaying inline image.

[Live example of this capability](https://forms.enablementadobe.com/content/samples/samples.html?query=0#collapse1)

## Add placeholder image

The first step is to prepend a placeholder div to the file attachment component. In the code below the file attachment component is identified by its CSS class name of photo-upload. The JavaScript function is part of client library that is associated with the adaptive forms. This function is called in initialize event of the file attachment component.

```javascript

/**
* Add Placeholder Image
* @return {string} 
 */
function addTempImage(){
  $(".photo-upload").prepend(" <div class='preview'' style='border:2px solid;height:225px;width:175px;text-align:center'><br><br><div class='text'>3.5mm * 4.5mm<br>2Mb max<br>Min 600dpi</div></div><br>");

}

```

### Display inline image

After the user has uploaded the image, the function listed below is invoked in commit event of the file attachment component. The function receives the uploaded file object as an argument.

```javascript
/**
* Consume Image
* @return {string} 
 */
function consumeImage (file) {
  var reader = new FileReader();
    console.log("Reading file");
  reader.addEventListener("load", function (e) {
    console.log("in the event listener");
    var image  = new Image();
    $(".photo-upload .preview .imageP").remove();
    $(".photo-upload .preview .text").remove();
    image.width = 170;image.height = 220;
    image.className = "imageP";
    image.addEventListener("load", function () {
      $(".photo-upload .preview")[0].prepend(this);
    });
    image.src = window.URL.createObjectURL(file);
  });
  reader.readAsDataURL(file); 
}

```

### Deploy on your server

* Download and install the [client library](assets/inline-image-client-library.zip) on your AEM instance using AEM package manager.
* Download and install the [sample form](assets/inline-image-af.zip) on you your AEM instance using AEM package manager.
* Point your browser to [Add Inline Image](http://localhost:4502/content/dam/formsanddocuments/addinlineimage/jcr:content?wcmmode=disabled)
* Click the "Attach your photo" button to add image
