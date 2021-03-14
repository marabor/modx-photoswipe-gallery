# modx-photoswipe-gallery

Combine MODX Gallery Extra and PhotoSwipe Gallery to create a Gallery Album and when clicked
on a thumb inside the album the picture is shown with PhotoSwipe Gallery.

We need the following to implement that.

    MODX Gallery Extra
    MODX phpThumbOf Extra
    getImageProperties Snippet
    PhotoSwipe Gallery
    photoswipeIntegration Snippet (optional)

<h2>Before beginning</h2>

The first thing to do is installing the MODX Gallery Extra and make sure that at least one album was created and a few pictures were loaded into it. To avoid confusion, give the uploaded images a short description. Any questions? A quick reference for setting up your gallery could be found in the [documentation](https://docs.modx.com/current/en/extras/gallery/gallery.setting-up-your-gallery).

<h2>Usage</h2>

Step 1: Creating a template based overview of the albums. In this case is use the Gallery Snippet and the GalleryAlbums Snippet wich both comes with the MODX Gallery Extra.

<h2>MODX Gallery Extra</h2>

The Gallery Snippet and the GalleryAlbums Snippet can be called using this tags. To make things easier you can also put in there the optional photoswipeIntegration Snippet.

Create a new Resource or Template and add following.

`gallery-extra`

<h2>Templating</h2>

For templating use the following two Chunks.

<h2>Chunk getImagePropertiesTpl</h2>

Create Chunk "getImagePropertiesTpl" and add the following.

`getImagePropertiesTpl`

<h2>Chunk albumItemTpl</h2>

This is to build an array of slides from a list of links. For resizing the image items i use the MODX phpThumbOf Extra, make sure you installed it.

Create Chunk "albumItemTpl" and add the following.

`albumItemTpl`

Step 2: PhotoSwipe integration

<h2>Snippet getImageProperties</h2>

The getImageProperties Snippet fetch the width and height from each Gallery Album Item. It's necessary because PhotoSwipe requires predefined image dimensions for html data-size attribute.

Create Snippet "getImageProperties" and add the following.

`getImageProperties`

<h2>PhotoSwipe Gallery</h2>

Next add the PhotoSwipe code to your Resource or Template. For getting startet with PhotoSwipe please visit the documentation. Alternatively you can use the optional photoswipeIntegration Snippet, which you can find below.
