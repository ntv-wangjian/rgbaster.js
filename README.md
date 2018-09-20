# <img src="https://rawgithub.com/briangonzalez/rgbaster.js/master/demo/baster.svg" width=25 style="margin-right: 10px"> RGBaster 

从一副图片中提取主题特征色，可用于对图片周边环境进行渲染。在有些网站中，随着图片的滚动周边配色也会变，基本原理就是对图片进行色彩提权，使用获取的主题颜色值对周边环境进行渲染。
### 对原版的改进： 支持对图片的部分区域进行取值，避免整副图片计算量过大造成的卡顿。例如可以只对图片边缘进行取值。
### 原始项目位置 https://github.com/briangonzalez/rgbaster.js
### 感谢 Brian Gonzalez

### Usage

Usage is simple. Create an image (or grab an image URL), then get its dominant color & palette.

```javascript
var img = document.getElementById('image');
// or
var img = 'http://example.com/path-to-image.jpg'

RGBaster.colors(img, {
  success: function(payload) {
    // You now have the payload.
    console.log(payload.dominant);
    console.log(payload.secondary);
    console.log(payload.palette);
  }
});
```


### Configuration options

The `colors` function takes an object as optional second parameter, with the following options:

#### `paletteSize`
Type: `int`
Default: `10`

Maximum number of palette colors to return. Only the top palette colors will be returned.

#### `exclude`
Type: `array`
Default: `[]`

RGB colors to exclude when counting colors.<br>
For example to exclude white and black use: `[ 'rgb(255,255,255)', 'rgb(0,0,0)' ]`

#### `success`
Type: `function`
Default: `undefined`

Function to call after image processing has completed.<br>The function will receive one `payload` argument with the following structure:

```javascript
{
    // {string} dominant rgb color
    dominant:  'rgb(0,0,0)',

    // {string} secondary rgb color
    secondary: 'rgb(0,0,1)',

    // {array} list of colors in the image (limited by paletteSize)
    palette:   [ 'rgb(0,0,1)', 'rgb(0,0,2)' ]
}
```

### Full example

```javascript
RGBaster.colors(img, {
    // return up to 30 top colors from the palette
    paletteSize: 30,

    // don't count white
    exclude: [ 'rgb(255,255,255)' ],

    // do something when done
    success: function(payload){
        console.log('Dominant color:', payload.dominant);
        console.log('Secondary color:', payload.secondary);
        console.log('Palette:', payload.palette);
    }
})
```

### Browser support

rgbaster.js depends on the following browser functionality:

* [Canvas](http://caniuse.com/#feat=canvas)
* [CORS](http://caniuse.com/#feat=cors)
* Array.prototype.map ([can i use](http://caniuse.com/#feat=es5), [compatibility table](http://kangax.github.io/es5-compat-table/#Array.prototype.map))

Check the linked resources above to determine current level of browser support.


Author
-------
| ![twitter/brianmgonzalez](http://gravatar.com/avatar/f6363fe1d9aadb1c3f07ba7867f0e854?s=70](http://twitter.com/brianmgonzalez "Follow @brianmgonzalez on Twitter") |
|---|
| [Brian Gonzalez](http://briangonzalez.org) |

About
-----
RGBaster was created to modularize a feature of another plugin I built called [adaptive backgrounds](http://briangonzalez.github.io/jquery.adaptive-backgrounds.js/). Check it out.

License
-------
MIT
