# Google Mobile WebDev
## Responsive Web Design

### Pixels
- Screen Resolution / Hardware Pixel
- CSS pixel - Viewport
    - CSS=SR/DPR
- DPR - Device pixel ratio
    - DPR=SR/CSS

### Set Viewport
- `<meta name="viewport" content="width=device-width, initial-scale=1">`

### Relative width
- in Css
- `img, embed, object, video { max-width: 100%; }`

### Tap Target
- button should be 48px by 48px with 40px space
- in Css `min-width: 48px; min-height: 48px;`
- add `padding: 1.5em`

### Start Small
- prioritize content and add from Phone -> Tablet -> Laptop -> Desktop
- performance: how much Data for Phone

### Breakpoints
- choose breakpoints for different screen size
- `@media screen and (min-width: 601px) and (max-width: 992px){...}`

### Flexbox
- use `div class="container"` in html
- use `.container {display: flex;}` in css
- use `order:1 ; width:100%;` in css

### Patterns
- use responsive patterns
- fluid, etc
![img](Google_dev/Responsive_Patterns.png)

### Tables
- Hide no essential columns
    - `display:none;` removed from flow
    - `visibility: hidden;` space still in the flow
- No more Tables
    - `@media screen and (max-width: 500px) { table, thead, tbody, th, td, tr { display: block; } }`
    - add css formatting `position, padding`
    - `content: attr(data-th);`
- Contained Scrolling

### Fonts
- line length ~65 cpl
- use measures for breakpoints 
- `font-size:16px;`
- `line-height: 1.25em;`

### Minor breakpoints
- adjust margin
- change font-size

---
## Responsive Images
### Goal
- Highest quality images with fewest bytes possible!

### Units, Formats, Environments
- total bits= pixels x bits per pixels
- fixed size, width 100%, max-width: 100%

### Request and Revenue
![img](Google_dev/Revenue.png)

### Relative sizing
- use calc()
    - `img {
    margin-right: 10px;
    max-width: 426px;`
        - `width: calc((100% - 10px)/2);
    }`
    - `img:last-of-type {
    margin-right: 0;
    }`

### Landscape and Portrait
- landscape on desktop
- portrait on mobile and tablet
- screen rotation
- never assume screen width

### Viewport max min
- resize images according to viewport height / width
- `height: 100vh;`
- `width: 100vmax`
- `width: 100vmin;`

### Raster Vector
- Raster for pictures, points in canvas .png .jpg .webp
- Vector for logo anysize .svg

### File formats
- don't send pictures with higher natural resolution than display
    - except for high DPI devices
- use compression to reduce file size

### Tools
- Grunt
    - `sudo npm install -g grunt-cli`
    - in folder `npm install`
    - 2 files 
        - `package.json` used by npm
        - `Gruntfile.js` configure tasks and load Grunt plugins
    - [Gruntjs.com](https://gruntjs.com/getting-started)

- ImageMagick, ImageOptim

### Performance
- latency
![latency](Google_dev/latency.png)
- reduce images files
- reduce number of requests

### Text Problems
- use text over images rather the text in images
    - `div {font-size: 10vw; position: absolute; text-align: center; width : 100vw;}`
    - `img {position: absolute; width: 100%;}`
- Css effects on text ie border, box-shadow, animation, etc.
- careful css cost
    - [Fast Mobile Website](https://www.smashingmagazine.com/2013/04/build-fast-loading-mobile-website/)

### Css background images
- use elaborate background with only Css
- use conditional background image display
- use alternative images for different devices
    - full image vs crop/close up
- use `image-set()` or `srcset` in html see 'Respond to screen'
    - `div {
      background-image: url(icon1x.png);
      background-image: -webkit-image-set(url(icon1x.png) 1x, url(icon2x.png) 2x);
      background-image: image-set(url(icon1x.png) 1x, url(icon2x.png) 2x);
      height: 128px;
      width: 128px;
    }`
- `background-size: cover;` image as small as possible while filling its container
    - fit the smaller side of image overfill the other
- `background-size: contain;` image as large as possible while completely visible inside its container
    - fit the larger side of image repeat the other

### Symbol character
- use unicode character or glyphs instead of image
    - `<meta charset="utf-8">`
    - `&#160;` for no-break space

### Icon fonts
- vector file for resize, change color, add shadow, etc.
- use Zocial icon for social
- [Css tricks](https://css-tricks.com/examples/IconFont/)

### Inline images
- inline svg
- data uri
- in html or css to reduce http requests

### Image handling technique
![techniques](Google_dev/ImgTech.png)
- inline less request Vs external with caching for reuse
- raster for photos Vs vector for icon & small animation

### Respond to screen 
- use `srcset` 
    - Width `<img src="small.jpg" srcset="small.jpg 500w, medium.jpg 1000w, large.jpg 1500w" alt="Wallaby">`
    - DPR `<img src="small.jpg" srcset="small_1x.jpg , medium_2x.jpg 2x" alt="Wallaby">`
- add size attribute in html for charging the right image at parse time but match with css
    - Html : `<img src="small.jpg" srcset="small.jpg 500w, medium.jpg 1000w, large.jpg 1500w" sizes="(max-width: 250px) 100vw, 50vw" alt="Wallaby">`
    - Css : `img {width: 50vw;} `
        - `@media screen and (max-width: 250px){ img {width: 100vw;}}`
- [device pixel density](http://pixensity.com/list/phone/)

### Picture Element
- `<picture>` requires `<img>` as its last child. Without that, nothing is displayed. This is good for accessibility as there is just one traditional place for your alternate text, and it’s great for fallback content in old browsers, which just show the `<img>` element.
- fallback alternative
    - `<picture>`
        - `<source srcset="kittens.webp" type="image/webp">`
        - `<source srcset="kittens.jpg" type="image/jpeg">`
        - `<img src="kittens.jpg" alt="Two grey tabby kittens">`
    - `</picture>`
- with media queries
    - `<picture>`
        - `<source
            media="(min-width: 1000px)"
            srcset="kookaburra_large_1x.jpg 1x, kookaburra_large_2x.jpg 2x">`
        - `<source
            media="(min-width: 500px)"
            srcset="kookaburra_medium_1x.jpg 1x, kookaburra_medium_2x.jpg 2x">`
        - `<img src="kookaburra_small.jpg"
            alt="The kookaburra: a terrestrial tree kingfisher native to Australia and New Guinea (according to Wikipedia)">`
    - `</picture>`
- add polyfill [Picturefill](http://scottjehl.github.io/picturefill/) for compatibility
    - `<script src="picturefill.min.js"></script>`
- see [article](https://dev.opera.com/articles/responsive-images/)
    - Do I want my image sizes to change depending on my responsive design rules?
    - Do I want to optimize for high-dpi screens?
    - Do I want to serve images with different mime types to browsers that support them?
    - Do I want to serve different art depending on certain contextual factors?

### Accessibility
- `alt` attributes should 
    - be descriptive of important images
    - empty for images used as decoration
    - set on every images
- `<img src="kittens.jpg" alt="Two grey tabby kittens">`
---
## Accessibility
[WCAG](https://www.w3.org/TR/WCAG20/), [Checklist](https://webaim.org/standards/wcag/checklist)

- Perceivable
    - 1 Provide text alternatives for any non-text content so that it can be changed into other forms people need, such as large print, braille, speech, symbols or simpler language.
    - 2 Provide alternatives for time-based media.
    - 3 Create content that can be presented in different ways (for example simpler layout) without losing information or structure.
    - 4 Make it easier for users to see and hear content including separating foreground from background.
- Operable
    - 1 Make all functionality available from a keyboard.
    - 2 Provide users enough time to read and use content.
    - 3 Do not design content in a way that is known to cause seizures.
    - 4 Provide ways to help users navigate, find content, and determine where they are.
- Understandable
    - 1 Make text content readable and understandable.
    - 2 Make Web pages appear and operate in predictable ways.
    - 3 Help users avoid and correct mistakes.
- Robust
    - Maximize compatibility with current and future user agents, including assistive technologies.

### Focus
- `TAB` : forward, `Shift TAB` : backward, `Arrows` : navigate inside component
- Tab order for `input`, `button`, `select` implicitly focusable
- Not all elements focusable : headers, paragraphs, images no interactivity
- Ordered by the dom not the css 
    - WCAG 1.3.2 The reading and navigation order (determined by code order) is logical and intuitive.
- use `tabindex` to add focus to an element for interactivity
    - with '0' it enters the order flow
        - `<div tabindex="0" > Focus me! </div>`
    - with '-1' make it accessible via javascript (with `focus()`method) but no part of the order flow
        - `document.querySelector('#modal').focus()`

### Semantics Basics
### Navigation Content
### ARIA
### Style

---
## Offline First
### Benefits
- The *Problem*
- What slow down
- Techniques
    - Deliver the page's header (and the content) from a cache on the device, the attempt to fetch updated content from the network.
### Service Worker
### IndexedDB & Caching

---
## ES 6
### Syntax
### Functions
### Built-ins
### Pro Dev-fu

---
## Extra

### Git

### GitHub
