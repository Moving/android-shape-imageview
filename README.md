# Shape Image View 
[![](http://img.shields.io/travis/siyamed/android-shape-imageview.svg?branch=master&&style=flat)](https://travis-ci.org/siyamed/android-shape-imageview/) 
[![Maven Central](https://maven-badges.herokuapp.com/maven-central/com.github.siyamed/android-shape-imageview/badge.svg?style=flat)](https://maven-badges.herokuapp.com/maven-central/com.github.siyamed/android-shape-imageview)

Provides a set of custom shaped android imageview components, and a framework to define more shapes. Implements both **shader** and **bitmap mask** based image views. 

[Shader]: http://developer.android.com/reference/android/graphics/BitmapShader.html
[Path.addPath]: http://developer.android.com/reference/android/graphics/Path.html#addPath(android.graphics.Path)
[Path]: http://developer.android.com/reference/android/graphics/Path.html
[xfermode]: http://developer.android.com/reference/android/graphics/Xfermode.html
[svg_location]: library/src/main/res/raw
[svg_rectangle]: http://www.w3schools.com/svg/svg_rect.asp 
[svg_circle]: http://www.w3schools.com/svg/svg_circle.asp 
[svg_ellipse]: http://www.w3schools.com/svg/svg_ellipse.asp
[svg_polygon]: http://www.w3schools.com/svg/svg_polygon.asp
[svg_path]: http://www.w3schools.com/svg/svg_path.asp
[svg_group]: https://developer.mozilla.org/en-US/docs/Web/SVG/Element/g
[svg_transformations]: https://developer.mozilla.org/en-US/docs/Web/SVG/Attribute/transform


* [Shader][Shader] based one uses *canvas draw methods* and *[Path][Path]* class, 
* Mask based one uses [xfermode][xfermode] to draw image on bitmaps defined by android shape XML's or resource bitmaps.

<div>
<a href="images/shader-buble.png" style="float:left;">
<img src="images/shader-buble.png" alt="Chat Bubble Image" height="600px"/>
</a>
<a href="images/all-samples.png" >
<img src="images/all-samples.png" alt="Shape Image View" height="600px"/>
</a>
</div>

There are many projects online implementing such components, however one goal of this project is to provide a 
performant/smooth scrolling **image view component framework** to define different shapes for imageviews. 

**For use with recycling view such as ListView or GridView please use shader based implementations.**

## How to use

Gradle dependency:
```Groovy
compile 'com.github.siyamed:android-shape-imageview:0.9.+@aar'
```

###Shader Based ImageView's
####BubbleImageView
![Android Bubble ImageView](images/small-bubble.png)
```XML
<com.github.siyamed.shapeimageview.BubbleImageView
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:src="@drawable/neo"
    app:arrowPosition="right"
    app:square="true"/>
```

Attributes:
* `triangleHeight` the height of the bubble pointer in dp  
* `arrowPosition` where to point the arrow, currently `left|right`
* `square` set width and height to the minimum of the given values `true|false`

####RoundedImageView
![Android Rounded Rectangle ImageView](images/small-rounded.png)
```XML
<com.github.siyamed.shapeimageview.RoundedImageView
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:src="@drawable/neo"
    app:radius="6dp"
    app:borderWidth="6dp"
    app:borderColor="@color/darkgray"
    app:square="true"/>
```

Attributes:
* `borderColor` border color 
* `borderWidth` border width in dp
* `borderAlpha` alpha value of the border between 0.0-1.0
* `radius` corner radius in dp
* `square` set width and height to the minimum of the given values `true|false`

####CircularImageView
![Android Circular ImageView](images/small-circle.png)
```XML
<com.github.siyamed.shapeimageview.CircularImageView
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:src="@drawable/neo"
    app:borderWidth="6dp"
    app:borderColor="@color/darkgray"/>
```

Attributes:
* `borderColor` border color 
* `borderWidth` border width in dp
* `borderAlpha` alpha value of the border between 0.0-1.0

####ShapeImageView
This view has the capability to process a provided SVG file (for a limited set of SVG elements), build a 
[Path][Path] object and draw it on the shader. The library includes SVG files defining a set of basic shapes and 
ShapeImageView subclasses using those files. You can use whatever SVG you want to have a wonderful 
and creatively shaped images in your application. The included SVG files are under [library/src/main/res/raw][svg_location]


| DiamondImageView                                       | PentagonImageView                                        | HexagonImageView                                         |
| ------------------------------------------------------ | -------------------------------------------------------- | -------------------------------------------------------- |
| ![Android Diamond ImageView](images/small-diamond.png) | ![Android Pentagon ImageView](images/small-pentagon.png) | ![Android Hexagon ImageView](images/small-hexagon.png)   |


| OctogonImageView                                       | StarImageView                                            | HeartImageView                                       |
| ------------------------------------------------------ | -------------------------------------------------------- | ---------------------------------------------------- |
| ![Android Octogon ImageView](images/small-octogon.png) | ![Android Start ImageView](images/small-star.png)        | ![Android Heart ImageView](images/small-heart.png)   |


```XML
<com.github.siyamed.shapeimageview.{ClassName}
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:layout_margin="8dp"
    android:src="@drawable/neo"
    app:borderWidth="8dp"
    app:borderColor="@color/darkgray"/>
```

Attributes:
* `borderColor` border color 
* `borderWidth` border width in dp
* `borderAlpha` alpha value of the border between 0.0-1.0
* `strokeCap` border stroke cap type `butt|round|square`
* `strokeJoin` border stroke join type `bevel|miter|round`
* `square` set width and height to the minimum of the given values `true|false`
* `shape` a reference to an SVG. This is used by ShapeImageView, not the subclasses of it. 


SVG elements that are supported are: [rectangle][svg_rectangle], [circle][svg_circle], 
[ellipse][svg_ellipse], [polygon][svg_polygon], [path][svg_path], [group][svg_group]. [Transformations][svg_transformations] on those elements are also supported. 

The system converts an SVG file into a Path. For each element including the parent element `<svg>` a new Path is created, and all the children Path's are [added][Path.addPath] to their parent path. 

###Bitmap Mask Based ImageViews 

This view uses extra bitmaps for bitmap masks. Therefore it would be good to use them for very custom shapes, 
possibly not in a recycling view. 

* With [mask bitmap](sample/src/main/res/drawable/star.png): 

![Android Star Shape ImageView ](images/small-mask-star.png)
```XML
<com.github.siyamed.shapeimageview.shape.PorterShapeImageView
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    app:shape="@drawable/star"
    android:src="@drawable/neo"
    app:square="true"/>
```

* With [shape XML](sample/src/main/res/drawable/shape_rounded_rectangle.xml):

![Android Star Shape ImageView ](images/small-xmlshape-rounded.png)

```XML
<com.github.siyamed.shapeimageview.shape.PorterShapeImageView
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    app:shape="@drawable/shape_rounded_rectangle"
    android:src="@drawable/neo"
    app:square="true"/>
```

rounded rectangle shape definition in XML: 

```XML
<shape android:shape="rectangle" xmlns:android="http://schemas.android.com/apk/res/android">
    <corners
        android:topLeftRadius="18dp"
        android:topRightRadius="18dp"
        android:bottomLeftRadius="18dp"
        android:bottomRightRadius="18dp" />
    <solid android:color="@color/black" />
</shape>
```

Attributes:
* `shape` the bitmap mask shape, either a shape drawable or a bitmap  
* `square` set width and height to the minimum of the given values `true|false`

This method reads a shape file (either bitmap or an android shape xml), creates a bitmap object using this shape, and finally combines the bitmap of the real image to be shown and the mast bitmap using xfermode. 

## Sample

See/execute the [sample](sample) for a demonstration of the components.

If you are lazy check [this youtube video](http://youtu.be/6fCkptmwxtQ) demonstrating scrolling in the sample app

## References
* [MostafaGazar/CustomShapeImageView](https://github.com/MostafaGazar/CustomShapeImageView): Used this project a basis for bitmap masks  
* [geosolutions-it/mapsforge/svg-android](https://github.com/geosolutions-it/mapsforge/tree/master/svg-android): Used and modified to create a path from a svg file 

[![Android Shape Image View on Android Arsenal](https://img.shields.io/badge/Android%20Arsenal-android--shape--imageview-brightgreen.svg?style=flat)](https://android-arsenal.com/details/1/932) [![Analytics](https://ga-beacon.appspot.com/UA-54885408-1/android-shape-imageview/home?pixel)](https://github.com/igrigorik/ga-beacon)
