# Good Practices:
- reset template:
```css
*,
*::after,
*::before {
  margin: 0;
  padding: 0;
  box-sizing: inherit;
  /* inherit will do that every component will inherit from parent*/
}

html{
    /**default font size in browser is 16px*/
    /*we want to set the html default font to 10px*/
    /* divide wantedSize/16 * 100 = percent */
    /* 10/16 = 0.625... */
    font-size: 62.5%;
}

body {
  box-sizing: border-box;
  /*declare that the box-sizing to be inherited will be border-box*/
}
```
- use rem always.
- give classes to all components.
- classses by BEM (block element modifier)
```css
.block{}
.block__element{}
.block__element--modifier{}
```
## architect:
separate folders for partial CSS files
one main file into compiled css stylesheet

## Sass & SCSS
 ### install sass:
 - make sure you have node.js in you pc. type in the root of your file:
 ```shell
 npm init
 ```
 - next lets install sass by typing:
 ```shell
 npm install node-sass --save-dev
 ```
 ```shell
  npm install concat --save-dev
 ```
 ```shell
  npm install autoprefixer --save-dev
 ```

  ```shell
  npm install postcss-cli --save-dev
 ```
  ```shell
  npm install npm-run-all --save-dev
 ```

 - in the package.json file create a script saying what file you want to compile and where is the css file where you want it to be compiled:
 ```json
   "scripts": {
    "watch-sass": "node-sass sass/main.scss css/style.css -w",
    "devserver":"live-server",
    "start":"npm-run-all --parallel devserver watch-sass",
    "compile-sass": "node-sass sass/main.scss css/style.comp.css",
    "concat-css":"concat -o css/style.concat.css css/icon-font.css css/style.comp.css",
    "prefix-css": "postcss --use autoprefixer -b 'last 10 versions' css/style.concat.css -o css/style.prefix.css",
    "compress-css":"node-sass css/style.prefix.css css/style.css --output-style compressed",
    "build-css":"npm-run-all compile-sass concat-css prefix-css compress-css"
  },
 ```
 - notice -w for watch.

```shell
npm install live-server --save-dev
```
- from the commandline: //not working for me
```shell
live-server
```

##sass structure/architecture

inside sass folder type:
```shell
mkdir base
cd base
edit _base.scss _animations.scss _typogrphy.scss _utilities.scss

mkdir abstracts
cd abstracts
edit _functions.scss _mixins.scss _variables.scss

mkdir pages
cd pages
edit _home.scss

mkdir components
mkdir layout
mkdir themes
mkdir vendors
```

## Mobile first design

- ignore devices all toguether and only look at your design.
- you begin at one size and start increasing your viewport width.
- when the design breaks then you insert a breakpoint.

### perfect break points phones max 600, tablet portrait max 900, tablets landscape max 1200, desktops max 1800, big desktops over 1800px


# Responsive Img
### density switching in html:

```html
<img
  srcset="./img/logo-green-1x.png 1x, ./img/logo-green-2x.png 2x"
  alt="full logo"
  class="footer__logo"
/>
```

### art direction:
```html
  <picture class="footer__logo">
      <source srcset="./img/logo-green-1x.png 1x, ./img/logo-green-2x.png 2x" media="(max-width: 37.5em)">
      <img srcset="./img/logo-green-1x.png 1x, ./img/logo-green-2x.png 2x" alt="full logo" class="footer__logo" />
  </picture>
```

### resolution switching
```html
  <img 
    srcset="./img/nat-1.jpg 300w, ./img/nat-1-large.jpg 1000w" 
    sizes="(max-width:900px) 20vw, (max-width:600px) 30vw, 300px", 
    alt="photo 1"
    class="composition__photo composition__photo--p1"
    src="./img/nat-1-large.jpg"
  >
```

### responsive img in CSS
```css
    @media (min-resolution:192dpi) and (min-width:600px){
      background-image: linear-gradient(
      to right bottom,
      rgba($color-secundary-ligth, 0.8),
      rgba($color-secundary-dark, 0.8), url(../img/hero.jpg));
    }
```

### browser support

```css
@support (-webkit-backdrop-filter:blur(10px))
```


## Build process:

