---
title: Some useful UI tips and tricks
description: Document to demonstrate some useful user interface tips
feature: Adaptive Forms
type: Tutorial
version: 6.5
topic: Development
role: Developer
level: Beginner
jira: KT-9270
exl-id: 13b9cd28-2797-4da9-a300-218e208cd21b
last-substantial-update: 2019-07-07
duration: 62
---
# Toggle password field visibility

A common use case is to allow the form fillers to toggle to visibility of the text entered in the password field.
To accomplish this use case, I have used the eye icon from the [Font Awesome Library](https://fontawesome.com/). The required CSS and the eye.svg are included in the client library created for this demonstration.



## Sample code

The adaptive form has a field of type PasswordBox called **ssnField**.

The following code gets executed when the form is loaded

``` javascript
$(document).ready(function() {
    $(".ssnField").append("<p id='fisheye' style='color: Dodgerblue';><i class='fa fa-eye'></i></p>");

    $(document).on('click', 'p', function() {
        var type = $(".ssnField").find("input").attr("type");

        if (type == "text") {
            $(".ssnField").find("input").attr("type", "password");
        }

        if (type == "password") {
            $(".ssnField").find("input").attr("type", "text");
        }

    });

});
```

The following CSS was used to position the **eye** icon inside the password field

``` javascript
.svg-inline--fa {
    /* display: inline-block; */
    font-size: inherit;
    height: 1em;
    overflow: visible;
    vertical-align: -.125em;
    position: absolute;
    top: 45px;
    right: 40px;
}

```

## Deploy the toggle password sample

* Download the [client library](assets/simple-ui-tips.zip)
* Download the [sample form](assets/simple-ui-tricks-form.zip)
* Import the client library using the [package manager UI](http://localhost:4502/crx/packmgr/index.jsp)
* Import the sample form using the [Forms and Document](http://localhost:4502/aem/forms.html/content/dam/formsanddocuments)
* [Preview the form](http://localhost:4502/content/dam/formsanddocuments/simpleuitips/jcr:content?wcmmode=disabled)
