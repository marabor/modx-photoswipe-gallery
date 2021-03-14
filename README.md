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

The first thing to do is installing the MODX Gallery Extra and make sure that at least one album was created and a few pictures were loaded into it. To avoid confusion, give the uploaded images a short description. Any questions? A quick reference for setting up your gallery could be found in the documentation.

<h2>Usage</h2>

__Step 1:__ Creating a template based overview of the albums. In this case is use the Gallery Snippet and the GalleryAlbums Snippet wich both comes with the MODX Gallery Extra.

<h2>MODX Gallery Extra</h2>

The Gallery Snippet and the GalleryAlbums Snippet can be called using this tags. To make things easier you can also put in there the optional photoswipeIntegration Snippet.

_gallery-extra_

<h2>Templating</h2>

For templating use the following two Chunks.
