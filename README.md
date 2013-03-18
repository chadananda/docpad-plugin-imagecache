## imageCache - DocPad Rendering Plugin for Images


##### Note: this plugin is not yet function. I just started DocPad yesterday so help is welcome.

<br><br>

Plugin for DocPad which provides image transformation and re-sizing similar to other page transforms

The plugin is named after the most excellent [Drupal ImageCache module](http://drupal.org/project/imagecache) but implemented in a DocPad style


### How it works

You create a file named like this:

```
  logo_64x64.jpg.imagecache
```

Docpad generates a file like:

```
  logo_64x64.jpg
```

The "*.imagecache" file is just a text file with, at minimum, a meta-data "src" value indicating the relative path to a source image to be resized or transformed like so:


```
--
 src: mylogo.svg
--
```

#### Other metadata intended:

* __dst__: ../ico/mybigicon.jpg (destination path overriding file's name)
* __size__: 600x600 (destination size, overriding size parsed from filename or original file)
* __aspect__: ignore|keep
* __style__: polaroid (plugin modules will provide more styles)


#### So how does it know when to rebuild destination file?

The rendering plugin checks the *.imagecache file, source and destination. If the timestamps do not match, the image is re-generated and timestamps of the three files are synchronized to the src file's timestamp.

#### A Cool example: generate all your icons from one SVG:

 You know how annoying it is to have to generate all those precomposed icons and favicons when what you should be able to do is just provide a single SVG file, right?

 Ok, here you go: 

   &nbsp; __1.__  create an SVG file in your __files/img__ directory and name it __logo.svg__
   
   &nbsp; __2.__ create a text file named __favicon_16x16.ico.imagecache__ in your documents directory containing:
 
```
---
src: ../files/img/logo.svg 
---
```

   &nbsp; __3.__ copy that file to __logo_144x144.png.imagecache__, __logo_114x114.png.imagecache__, __logo_72x72.png.imagecache__ and __logo_57x57.png.imagecache__
   
   &nbsp; __4.__ now make sure to update your page template header with the following link tags

```
  <link rel="shortcut icon" href="favicon.ico">
  <link rel="apple-touch-icon-precomposed" sizes="144x144" href="logo_144x144.png">
  <link rel="apple-touch-icon-precomposed" sizes="114x114" href="logo_114x114.png">
  <link rel="apple-touch-icon-precomposed" sizes="72x72" href="logo_72x72.png">
  <link rel="apple-touch-icon-precomposed" href="logo_57x57.png">
```

##### That's it! Now whenever you edit the *logo.svg* file or any of the *.imagecache* files, the destination icons will automatically re-render

