# DisplayAnything 3.0b2 AKA 'nearly there' #

## About ##
A file and image gallery module for Silverstripe 3.0b2, forked from <a href="http://github.com/codem/displayanything">DisplayAnything</a>.

This module is only compatible with <a href="http://www.silverstripe.org/silverstripe-3-beta-2/">the Silverstripe 3.0b2 release</a>.

## State ##
This is a highly experimental fork of <a href="http://github.com/codem/displayanything">DisplayAnything</a> based on SilverStripe 3.0b2.

Don't expect it to work consistently in a production environment. It may eat your files or worse. Backup your files if you are testing.

If you would like to contribute to the development of this module, please fork it and hack away. If you would like to use a spiffy multi-file uploader and gallery module in SilverStripe 2.4.x, please look at <a href="http://github.com/codem/displayanything">DisplayAnything</a>.

To assist with version identification this module will be versioned the same as the pre-release version of SS3.0 it has been tested against.

## Changes ##
<ul>
<li>The field now extends GridField rather than ComplexTableField</li>
<li>Updated JS upload handling to bind on new CMS events</li>
<li>Worked through deprecation notices to get compatibility with method changes between 3.0a2 and 3.0b2</li>
<li>Remove 2.4 JS handlers such as lightbox loading</li>
<li>Update drop zone styles to match UploadField</li>
<li>General CSS updates</li>
<li>Deprecate getComponentInfo() compat layer and remove calls to it</li>
<li>Update example page content</li>
<li>Layout updates in FieldHolder</li>
<li>CleanFileName() now hits up FileNameFilter</li>
<li>Change WatermarkedImageDecorator to WatermarkedImageExtension and use DataExtension</li>
<li>Change behaviour of OrderedGalleryItems for use as default DataList</li>
</ul>

## TODO / Known issues ###
<ul>
<li>File edit link currently hits up the asset admin, we'd rather this went to a specific view to remain in gallery context (fork and hack if you want to help with this. Hint:FileEditorLink())</li>
<li>Drop support for single file UploadAnythingField, this will become an abstract class, use UploadField instead</li>
<li>General testing as required</li>
</ul>


## Installing ##
<ol>
<li>Download and <a href="http://www.silverstripe.org/silverstripe-3-0-alpha-2-is-here/">install SilverStripe 3.0b2</a></li>
<li>cd /path/to/your/silverstripe/site</li>
<li>Grab the source:
	<dl>
		<dt>Git</dt>
		<dd><code>git clone git@github.com:codem/DisplayAnything3.git display_anything</code></dd>
		<dt>Bzr (requires bzr-git) - note the / in the path</dt>
		<dd><code>bzr branch git://git@github.com/codem/DisplayAnything3.git display_anything</code></dd>
		<dt>Download</dt>
		<dd><code>wget --output-document=display_anything.zip https://github.com/codem/DisplayAnything3/zipball/master</code></dd>
	</dl>
	<br />In all cases the module source code should be located in a directory called 'display_anything'
</li>
<li>run /dev/build (admin privileges required) and possibly a ?flush=1</li>
<li>implement in the CMS (see 'CMS' below)</li>
<li>log into the CMS and start editing</li>
</ol>

## Migrating items from the ImageGallery gallery module ##

Note: this functionality is experimental in this version of the module.

If DisplayAnything detects an  ImageGallery Album associated with the current page it will provide an Image Gallery Migration tab containing migration options. Migrated images are copied rather than moved.
You can choose a albums from the list of album(s) provided and save the page, successfully imported items will appear in the file list. You can retry the migration at any time.

Once migration is complete you can remove the Image Gallery module as and when you wish.

## CMS implementation ##
View the <a href="./DisplayAnything3/examples">example directory</a> for some sample page, dataobject and template implementations.

## Templates ##
Innumerable gallery plugins with varying licenses exist for image & file lists and viewing of images in a lightbox (Fancybox is good and open source).

By design, DisplayAnything avoids being a kitchen sink, stays light and does not bundle any of these plugins. It's up to you to implement the gallery the way you want it (this saves you having to undo & override any defaults DisplayAnything may set).

View the <a href="./DisplayAnything3/examples/templates">example directory</a> for some sample layouts related to the pages in the examples section.

### Ordered Gallery Items ###
You can implement ordered galleries in your frontend template to match yours or someone else's drag and drop admin work on the Gallery. Simply change "GalleryItems" to "OrderedGalleryItems" in the template example above.

## Watermarking ##
To implement watermarking, use the following image template/html snippet within your gallery control:

```php
<li class="$EvenOdd $FirstLast"><a href="$URL" rel="page-gallery">$WatermarkCroppedImage(90,90)</a></li>
```

You can use any Silverstripe image resizing method supported (SetHeight, SetWidth, CroppedImage, PaddedImage, SetSize) but prefixed with "Watermark".

The module ships with a watermark image called "_wm.png". To implement your own, add an image called "_wm.png" to a directory named the same as your theme. For example, if your theme is "green", add a file of that name to document_root/green/images/.

Watermarking is only enabled if you use the Watermark prefixed template controls.

## Watermark configuration options ###
Use the following in your site config:
+ WatermarkedImage::$opacity (0-100)
+ WatermarkedImage::$position (tr, tl, br, bl). Example br anchors the watermark image to the bottom right of the source image.
+ WatermarkedImage::$padding_x (pixel padding from image edge in the x-axis)
+ WatermarkedImage::$padding_y (pixel padding from image edge in the y-axis)

## Watermark notes ###
+ Uses GD
+ 8 bit PNGs only
+ The watermark source image is not resized
+ The original image is not watermarked
+ WatermarkedImageDecorator decorates Image

## Support ##
+ No support is available for this version of DisplayAnything. The intended audience is developers who want to hack away and get it working alongside SS3 releases.

## Licenses ##
DisplayAnything is licensed under the Modified BSD License (refer license.txt)

This library links to Ajax Upload (http://valums.com/ajax-upload/) which is released under the GNU GPL and GNU LGPL 2 or later licenses

+ DisplayAnything is linking to Ajax Upload as described in Section 6 of the LGPL2.1 (http://www.gnu.org/licenses/lgpl-2.1.html)
+ You may modify DisplayAnything under the terms described in license.txt
+ The Copyright holder of DisplayAnything is Codem
+ The Copyright holder of Ajax Upload is Andrew Valums
+ Refer to javascript/file-uploader/license.txt for further information regarding Ajax Upload

