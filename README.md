# SVG Icons Embedded
SVG icons library embedded in html


*you can find a version of SVG icons in CSS background image here: [SVG Icons CSS](https://github.com/pierfarrugia/svgiconsEmbedded)* 

To add icons on website, the easiest way is to use an icon font. Simple ref link in style and after html tag in the page.

There are several well known icon fonts like Font-Awesome, or Google Material icons.

First time I searched for a font icon, I was looking for the font with the biggest number of icons (2000, 3000,... more than 5000) to have more choices "in case of" even if I were using 8 or 10 only! Now more and more icons gives a ref file to load bigger and bigger! Could be from 128kB
      to 256kB or even more (384... >750!). That means, even if downloading from a CDN, time will be at best 250ms (fiber
      connection)
      but often 750ms or more than 1 second. And that's just for the icons of the website!

5000 icons loaded, using 8 to 10, not really efficient.

**What about building library, with just icons needed. Those icons would have to be scalable as font, can have their color
changed, and can be used with CSS class and data attributes. In add library has to be easy to setup.**

---


![alt text](https://github.com/pierfarrugia/svgiconsCSS/blob/main/svg_icons.webp)

[Read this on HTML page](https://aonecommunication.ch/dev/creativeprog/blog.html#svgIconsEmbedded)

[See it in action full screen](https://aonecommunication.ch/dev/creativeprog/content/svg_icons_embed.html)





---


### The icon

Type “material icons” in your browser to search Google Material icon, or click here:

[https://fonts.google.com/icons?selected=Material+Icons](https://fonts.google.com/icons?selected=Material+Icons)

![google icon](https://github.com/pierfarrugia/svgiconsCSS/blob/main/materialIcon.webp)

When in Material Icon page, type “menu” in the search, select it, a panel arrive on right. On bottom of the panel, you have 2
buttons: SVG and PNG. Click on SVG, the SVG is downloaded in your computer.

*note: google icons font is now a variable font. You can specify several parameters like Fill. In our case, keep initial parameters*

Open the SVG file in your text editor:

```
<svg xmlns="http://www.w3.org/2000/svg"><path d="M6 36v-3h36v3Zm0-10.5v-3h36v3ZM6 15v-3h36v3Z"/></svg>
```

#### cleaning the svg

We don't really the xmlns definition in this embedded version.

We need a viewbox whichi will mainly gives us a ratio. The variable version is now based on a 48px x 48px (previous version was 24x24px)

For the color we'll add a fill with the magic "currentColor"

``` 
<svg viewBox="0 0 48 48" style="fill:currentColor">
      <path d="M6 36v-3h36v3Zm0-10.5v-3h36v3ZM6 15v-3h36v3Z"/>
</svg> 
```

CSS
---

To define the ico we'll need 1 class:

* ico: to define base values for all ico


```
.ico {
display: inline-block;
width: 1em;
height: 1em;
line-height: 1em;
}
```

All sizes are 1em, and very important the line-height (needed for later vertical alignment).

Display is inline-block. Whatever HTML tag you'll be going to use, div, span, it'll be inline-block to have the size defined.

When we’ll put the class ico in any HTML element it’ll take the size defined for this element. For example if it’s a H4 of 2em,
ico will be 2x1 = 2 em… Same if you are putting font-size to 36px, it'll be 36px x 1em = 36px. Because em is proportional and we
put 1em everywhere, it’ll scaled regarding the element it’s in: exactly what needed.

HTML
---

To have this menu icon in HTML, lets add a DIV with display none at the end of body

```
<div id="icons" style="display: none">

    <div id="ico_menu">
        <svg viewBox="0 0 48 48" style="fill:currentColor">
            <path d="M6 36v-3h36v3Zm0-10.5v-3h36v3ZM6 15v-3h36v3Z"/>
        </svg>
    </div>

    ... other icons...
</div>
```

How to use
----------

You can use it as span or div (“ico” is inline-block).

For 1 icon you add the ico class and a "data-icon" with the name of the icon, here "ico_menu".

```
    <span class="ico" data-icon="ico_menu"</span>
```


Javascript
----------

Yes for this version javascript is needed to put the icon shape everywhere you want an icon in HTML!

```
const icons = () => {
        let eicons = document.querySelectorAll('.ico');
        eicons.forEach(e => {
            let esvg = document.querySelector('#' + e.dataset.icon);
            e.innerHTML = esvg.innerHTML;
        })
    }
window.addEventListener('load', icons);
```

We search in document every ".ico".
For each, we take its data attribute (name of icon).
We search the corresponding ID, and copy the inner HTML.

You can have several same ico.

This very fast and short javascript has to be executed at load.


Conclusion
----------

It's quite easy to build your own svg library this way and to save big amount of loading time.

Regarding the CSS library way, the big pro is that it's lot easier to build (no data URI, no color filter to build).
Color of the element is applied (inherited), and size follow your HTML.

Regarding SVG sprite, it's not more complicated to build (even slightly easier), but SVG sprite always complicated to size with text.


Thanks for reading

_(tested on Chrome, Firefox, Edge, Safari)_