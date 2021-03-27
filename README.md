<h1>MODX PhotoSwipe Gallery</h1>

Combine [MODX Gallery Extra](https://docs.modx.com/current/en/extras/gallery/index) and [PhotoSwipe Gallery](http://www.photoswipe.com/) to create a Gallery Album and when clicked
on a thumb inside the album the picture is shown with PhotoSwipe Gallery.

Download [PDF](https://github.com/marabor/modx-photoswipe-gallery/raw/main/MODX-PhotoSwipe-Gallery.pdf)

<h2>Required things</h2>

We need the following to implement that.

- [MODX Gallery Extra](https://docs.modx.com/current/en/extras/gallery/index)
- [MODX phpThumbOf Extra](https://docs.modx.com/current/en/extras/phpthumbof/index)
- getImageProperties Snippet ↓
- [PhotoSwipe Gallery](http://www.photoswipe.com/)
- photoswipeIntegration Snippet (optional) ↓

<h2>Before beginning</h2>

The first thing to do is installing the MODX Gallery Extra and make sure that at least one album was created and a few pictures were loaded into it. To avoid confusion, give the uploaded images a short description. Any questions? A quick reference for setting up your gallery could be found in the [documentation](https://docs.modx.com/current/en/extras/gallery/gallery.setting-up-your-gallery).

<h2>Usage</h2>

Step 1: Creating a template based overview of the albums. In this case is use the Gallery Snippet and the GalleryAlbums Snippet wich both comes with the MODX Gallery Extra.

<h2>MODX Gallery Extra</h2>

The [Gallery Snippet](https://docs.modx.com/current/en/extras/gallery/gallery) and the [GalleryAlbums Snippet](https://docs.modx.com/current/en/extras/gallery/gallery.galleryalbums)  can be called using this tags. To make things easier you can also put in there the optional photoswipeIntegration Snippet.

Create a new Resource or Template and add following. [modx-gallery-extra](example/modx-gallery-extra)

<h2>Templating</h2>

For templating use the following two Chunks.

<h2>Chunk getImagePropertiesTpl</h2>

Create Chunk "getImagePropertiesTpl" and add the following. [getImagePropertiesTpl](chunks/getImagePropertiesTpl)

```html
[[!getImageProperties? &ia=`[[+image_absolute]]`]]
```

<h2>Chunk albumItemTpl</h2>

This is to build an array of slides from a list of links. For resizing the image items i use the MODX phpThumbOf Extra, make sure you installed it.

Create Chunk "albumItemTpl" and add the following. [albumItemTpl](chunks/albumItemTpl)

```html
<figure>
  <a href="[[+image_absolute]]" data-size="[[+image_absolute_width]]x[[+image_absolute_height]]">
    <img title="[[+description]]" src="[[+image_absolute:phpthumbof=`w=768&h=576&zc=1&q=98`]]" alt="[[+description]]"/>
  </a>
  <figcaption>[[+description]]</figcaption>
</figure>
```

Step 2: PhotoSwipe integration

<h2>#Snippet getImageProperties</h2>

The getImageProperties Snippet fetch the width and height from each Gallery Album Item. It's necessary because PhotoSwipe requires predefined image dimensions for html data-size attribute.

Create Snippet "getImageProperties" and add the following. [getImageProperties](snippets/getImageProperties)

```javascript
<?php
/**
 * getImageProperties
 *
 * DESCRIPTION
 *
 * This Snippet fetch the width and height from a Gallery Album Item using the "image_absolute" Placeholder
 *
 * It's necessary to combine MODX Gallery Extra and PhotoSwipe gallery script
 * PhotoSwipe requires predefined image dimensions for html data-size attribute
 *
 * PROPERTIES:
 * 
 * &ia string is required
 *
 * USAGE:
 *
 * [[!getImageProperties? &ia=`[[+image_absolute]]`]]
 *
 */

$ia = $modx->getOption('ia', $scriptProperties);

if (!isset($scriptProperties['ia'])) {
  $modx->log(modX::LOG_LEVEL_ERROR, '[getImageProperties] missing required properties &ia!');
  return;
}

// to use PHP getimagesize properly in some cases it is necessary to remove the leading slash
$l = strlen($ia)-1;
$ian=substr($ia,1,$l);  

list($iawidth, $iaheight) = getimagesize($ian);

// templating
$tpl = $modx->getOption('tpl',$scriptProperties,'albumItemTpl'); // default property
$output = $modx->getChunk($tpl,array(
  'image_absolute_width' => $iawidth,
  'image_absolute_height' => $iaheight
));

return $output;
```

<h2>PhotoSwipe Gallery</h2>

Next add the PhotoSwipe code to your Resource or Template. For getting startet with PhotoSwipe please visit the [documentation](https://photoswipe.com/documentation/getting-started.html). Alternatively you can use the optional photoswipeIntegration Snippet, which you can find below.

<h2>#Snippet photoswipeIntegration</h2>

This Snippet includes PhotoSwipe JS and CSS files, add PhotoSwipe (.pswp) element to DOM and initialize and execute (pure Vanilla JS implementation). It's optional, but it is to make things easier. Integration can of course also be done manually.

Create Snippet "photoswipeIntegration" and add the following. [photoswipeIntegration](snippets/photoswipeIntegration)

<h2>PhotoSwipe files</h2>

Complete the integration with upload the required PhotoSwipe files, get them at [GitHub](https://github.com/dimsemenov/photoswipe). Create "photoswipe" directory in your assets directory and put the css, js and skin files in there.

That should be it. Note: This is not a reference, it should only illustrate what is possible when you combine the MODX Gallery Extra with other third party components like PhotoSwipe Gallery.
