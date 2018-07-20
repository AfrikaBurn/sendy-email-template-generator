
# General

Most email clients cannot apply external CSS stylesheets to the HTML code that makes up an email. Thus, we have to apply all styles inline. That is to say, by adding a `style` attrinute to every element that we would like to style. For example:

    <td data-editable="text" style="background: #ede9df; font-family: courier; line-height: 150%; padding: 10px 20px 10px 20px;">
      First of all, we at African Burns Transformational Desert Experiences...
    </td>

Doing this directly would be a complete pain in the ass. Life is too short to spend that much time copying and pasting. This node application allows you to create an HTML template with an external stylesheet, so you can write dynamic CSS in an external stylesheet, and it will apply them inline to every HTML element when you run the script.

# Files and folders structure

Create a folder in the root of the email template folder, and name it what the template is named. Don't use spaces!

Inside this, create 2 folders. One named `img` and the other named `thumbnails`.

The `img` folder is where you place any images you would like to use in the template.

The `thumbnails` folder is where you place one 250px wide `png` image for each module. This is used in the email builder UI to show an image for each module, which acts as a preview for the person creating the email.

Each thumbnail must be named as the lowercase version of the `id` that is assinged to the module in `template.html` (See below).

For example if the module looks like this:

    <table cellpadding="0" cellspacing="0" class='module' id='Heading_4'>

    </table>

The thumbnail for this module should be named `heading-4.png`, that being the lowercase version of `Heading_4`.

--baardskeerder
----template.html
----img
----thumbnails
--new-template
----template.html
----img
----thumbnails

# Layout

The Sendy email builder requires the layout to be implemented with tables and table cells. Floating divs do not work.

# template.json

This is the file that we ultimately upload to the server, and it results in the drag and drop template that people can then use to create newsletters.

The template is split into modules. In the UI, each module is shown in a panel on the left, and they can be dragged into the email you are building, and then edited.

These modules, along with their HTML, styles and some default content are contained in `template.json`.

# template.html

This is the file that you will create. The script takes this file and uses it to spit out `template.json`.

You can add a `<style>` element at the top of the file, and write dynamic CSS styles there.

Beneath this, create a `<div>` element with the class `container`. It must have that class, as well as an `id` which is the name of the template.

This must not be the same as the name of any other template.

    <div class='container' id='Baardskeerder'>

    </div>

Inside this, create a `<table>` element for each module that you would like to add to the template.

Each one of these tables must have a unique `id` attribute and the class `module`. This will become the title of the module in the UI.

    <table align="center" cellpadding="0" cellspacing="0" class='module' id='Banner'>

    </table>

    <table cellpadding="0" cellspacing="0" class='module' id='Heading_4'>

    </table>

# Images

Don't apply a width of 100% to images in the CSS if you want them to be resizeable.

To ensure that an image can be resized in the template, set the width and height attributes in the HTML:

    <img alt="" src="img/test-image.jpg" width="660" height="372">

# Editable elements

Text, images and links need to be editable in the email builder. To add editablility to any element in your HTML template, use the `data-editable` attribute.

## Text

Add `data-editable="text"` to the relevant `<td>` element.

    <td data-editable="text">
      Dear AfrikaBurn Community Member...
    </td>

## Images

Add `data-editable="image"` to the `<td>` element which contains the `<img>` element.

    <td data-editable="image">
      <img alt="" src="img/test-image.jpg" width="660" height="372">
    </td>

## Links

Add `data-editable="link"` to the container `<a>` element.

    <a class='link-button' data-editable="link" href='#'>Link button</a>

# Browser testing

It is not necessary to upload template.json to the email builder each time you make an edit. Simply open `template.html` in your browser in order to view your progress as you work.

# Running the script

In the terminal, navigate to the email template directory and run:

`node index.js template-name`
