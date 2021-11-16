# GRID AREAS

Class reference:
https://codepen.io/kevinpowell/pen/rzGJBJ/

To create Grid-areas you have first to declare them according to the layout you want.
In this example we have 4 columns (the 2 at the side are like small margins for the main area...) 
We have also 4 rows as for the header, a hero section, the main content section (with the cards) and a footer.

``` css
grid-template-columns: 1fr 5fr 2fr 1fr; 
/* 4 columns */
grid-template-rows: 3em 20vh auto 3em;  
/*4 rows, main content auto */
grid-template-areas:
    "header header header header"
    "hero hero hero hero"
    ". main sidebar ."
    "footer footer footer footer";
```

The next step is to assign the areas to the correct DIV/CLASS block in the CSS

``` css
.hero {
    grid-area: hero;
}
footer {
    grid-area: footer;
}
aside {
    grid-area: sidebar;
}
.main-content {
    grid-area: main;
}
```
<div class="page"/>

# Content Alignment

The hero section for example has 2 lines, on h1 and one normal paragraph.
If I want to align it so that the 2 lines are behaving into rows in a FLEX way I have to do the following (this will avoid to have them sticked together one next to the others)
``` css
.hero {
    grid-area: hero;
    background: url(http://yoururl/filename.png);
    display: flex;
    flex-direction: column;

```

# Section alignment
When you DIV or SECTION is displayed in **FLEX** mode you can play with vertical and horizontal alignment:

this one is aligning the text <u>horizontally</u>
``` css
.header {
    display: flex;
    justify-content: center;
}       
```
this one is aligning <mark>vertically</mark> in the allocated space
``` css
    align-items: center;
```
<div class="page"/>

# CARDS (Grid areas in existing grid areas...)
In reality you can create sub-grid areas for example if you have CARDs in your main content area.
It is important to have a good semantic HTML or at least sections ready for it
For example if in the main text area of the cards you have multiple lines (description, tags references, a link..) you to setup a dedicated DIV for it.
### Here the HTML
``` html
<div class="card">
    <img src="https://s3-us-west-2.amazonaws.com/s.cdpn.io/308367/gridarea-card-img-01.jpg" alt="" class="card-img">
    <h2 class="card-title">Blog post title</h2>
    <div class="card-content">
      <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Aenean posuere semper urna, ut pellentesque sem fermentum vel. Mauris luctus quis lectus nec luctus. Donec ut diam et neque eleifend varius sed quis erat.</p>
      <a href="">Read more</a>
    </div>
  </div>
  ```
  ### Here the CSS
  ``` css
// Cards

.card {
  display: grid;
  grid-template:
    "img title" min-content
    "img content" auto / 1fr 3fr;
  grid-column-gap: 1.5em;
  box-shadow: 0 0 1em rgba(0, 0, 0, 0.5);
  padding: 1.5em;
  margin-bottom: 1.5em;
}

.card-img {
  grid-area: img;
  max-width: 100%;
}

.card-title {
  grid-area: title;
  margin: 0;
  font-weight: 300;
}

.card-content {
  grid-area: content;
  
  a {
    color: $yellow;
    font-size: 1.1em;
  }
}

  ```

  The grid areas can also be created in the standard way as already illustrated above:
  ``` css
.card {
  display: grid;
  grid-template-columns: 1fr 3fr;
  grid-template-rows: min-content auto;
  grid-template-areas:
    "img title" 
    "img content";
  grid-column-gap: 1.5em;
  [...]
  .card-img {
  grid-area: img;
  max-width: 100%;
  [...]
  .card-title {
  grid-area: title;
  [...]  
  .card-content {
  grid-area: content;  
  ```
<div class="page"/>

# How to use CSS variables
Using global setting varibles in CSS is a powerful tool you need to know. You can set them and then you can change in on single place to rearrange your project

in <code><mark>**:root**</mark></code> you have to put them.<br>
See the example below
``` css
:root {
    --width: 650px;
    --cols2width: 320px;
    --cols3width: 212px;
    --cols2gap: 10px;
    --cols3gap: 7px;
    --ff-text:  'Open Sans', sans-serif;
    --ff-title: 'Lato', sans-serif;
    --color1 : rgba(252,176,69,1);
    --color2: rgba(253,29,29,1);
    --color3: rgba(131,58,180,1);
    --color4:  rgba(3,111,250,1);
    --color21: rgb(251,28,70);
    --color22: rgb(159,0,29);
}
```
Then you can use them in the CSS element calling <code><mark>**var(--varname)**</mark></code>.<br>
See the example
``` css
body {
    width: var(--width);
    font-family: var(--ff-text);

``` css
.sect-2 {
    width: var(--width);
    display: grid;
 ```   grid-template-columns: var(--cols2width) var(--cols2width);
    column-gap: var(--cols2gap);
    padding-bottom: 2em;
}
```
<div class="page"/>

# How to use FontAwsome (Glyphicon)
In the <code><mark>**\<head>**</mark></code> section include the call to the CDN
``` html
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/4.7.0/css/font-awesome.css" integrity="sha512-5A8nwdMOWrSz20fDsjczgUidUBR8liPYU+WymTZP1lmY9G6Oc7HlZv156XqnsgNUzTyMefFTcsFH/tnJE/+xBg==" crossorigin="anonymous" referrerpolicy="no-referrer" />
```
Once done you can reference the fa FontAwesome in the <code><mark>**\<i>**</mark></code> tag as follows:
``` html
<i class="fa fa-dot-circle-o" aria-hidden="true"></i>
```
Examples for version 4.7 are here https://fontawesome.com/v4.7/examples/

### Fixed width
Use fa-fw to set icons at a fixed width. Great to use when different icon widths throw off alignment. Especially useful in things like nav lists & list groups.
``` html
<div class="list-group">
  <a class="list-group-item" href="#"><i class="fa fa-home fa-fw" aria-hidden="true"></i>&nbsp; Home</a>
  <a class="list-group-item" href="#"><i class="fa fa-book fa-fw" aria-hidden="true"></i>&nbsp; Library</a>
  <a class="list-group-item" href="#"><i class="fa fa-pencil fa-fw" aria-hidden="true"></i>&nbsp; Applications</a>
  <a class="list-group-item" href="#"><i class="fa fa-cog fa-fw" aria-hidden="true"></i>&nbsp; Settings</a>
</div>
```
### Use as bullets replacement
You can also use them instead of the default bullets in unordered lists
``` html
<ul class="fa-ul">
  <li><i class="fa-li fa fa-check-square"></i>List icons</li>
  <li><i class="fa-li fa fa-check-square"></i>can be used</li>
  <li><i class="fa-li fa fa-spinner fa-spin"></i>as bullets</li>
  <li><i class="fa-li fa fa-square"></i>in lists</li>
</ul>
```
### Animated Icons
Use the fa-spin class to get any icon to rotate, and use fa-pulse to have it rotate with 8 steps. Works well with fa-spinner, fa-refresh, and fa-cog.
``` html
<i class="fa fa-spinner fa-spin fa-3x fa-fw"></i>
<span class="sr-only">Loading...</span>

<i class="fa fa-circle-o-notch fa-spin fa-3x fa-fw"></i>
<span class="sr-only">Loading...</span>

<i class="fa fa-refresh fa-spin fa-3x fa-fw"></i>
<span class="sr-only">Loading...</span>

<i class="fa fa-cog fa-spin fa-3x fa-fw"></i>
<span class="sr-only">Loading...</span>

<i class="fa fa-spinner fa-pulse fa-3x fa-fw"></i>
<span class="sr-only">Loading...</span>
```
### All icons list
You can find the entire list by sections in the lin below
https://fontawesome.com/v4.7/icons/


<div class="page"/>

# Quotes

> Perfection is achieved, not when there is nothing more to add, but when there is nothing left to take away.<br>
><div style="text-align: right"><i>Antoine de Saint-Exupéry</i><div>
<br>

# Keyboard Keys in MarkDown
<kbd>Ctrl</kbd> + <kbd>Alt</kbd> + <kbd>Space</kbd>

``` markdown
<kbd>Ctrl</kbd> + <kbd>Alt</kbd> + <kbd>Space</kbd>

left arrow: ← &#8592;
upward arrow: ↑ &#8593;
right arrow: → &#8594;
downward arrow: ↓ &#8595;

<kbd>&uarr;</kbd>

<kbd>shift</kbd>+<kbd>command</kbd>+<kbd>3</kbd> will work if you have escaped your VirtualBox and places the screen shot on your Mac's desktop. You could also use or <kbd>shift</kbd>+<kbd>command</kbd>+<kbd>4</kbd> which gives you a cross-hair to select the area you want to capture.

⌥ Option ⌥ <kbd>⌥ Option</kbd> <kbd>⌥</kbd>
⌃ Control ⌃ <kbd>⌃ Control</kbd> <kbd>⌃</kbd>
⇧ Shift ⇧ <kbd>⇧ Shift</kbd> <kbd>⇧</kbd>
⌘ Command ⌘ <kbd>⌘ Command</kbd> <kbd>⌘</kbd>
⎋ Escape ⎋ <kbd>⎋ Escape</kbd> <kbd>⎋</kbd>
⇪ Caps lock ⇪ <kbd>⇪ Caps lock</kbd> <kbd>⇪</kbd>
⇥ Tab ⇥ <kbd>⇥ Tab</kbd> <kbd>⇥</kbd>
⏏︎ Eject ⏏︎ <kbd>⏏︎ Eject</kbd> <kbd>⏏︎</kbd>
⌫ Delete ⌫ <kbd>⌫ Delete</kbd> <kbd>⌫</kbd>
```
<div class="page"/>

<kbd>Alt</kbd> + <kbd>Enter</kbd><br>
<kbd>&uarr;</kbd><br>

<kbd>shift</kbd>+<kbd>command</kbd>+<kbd>3</kbd> will work if you have escaped your VirtualBox and places the screen shot on your Mac's desktop. You could also use or <kbd>shift</kbd>+<kbd>command</kbd>+<kbd>4</kbd> which gives you a cross-hair to select the area you want to capture.

⌥ Option ⌥ <kbd>⌥ Option</kbd> <kbd>⌥</kbd>
⌃ Control ⌃ <kbd>⌃ Control</kbd> <kbd>⌃</kbd>
⇧ Shift ⇧ <kbd>⇧ Shift</kbd> <kbd>⇧</kbd>
⌘ Command ⌘ <kbd>⌘ Command</kbd> <kbd>⌘</kbd>
⎋ Escape ⎋ <kbd>⎋ Escape</kbd> <kbd>⎋</kbd>
⇪ Caps lock ⇪ <kbd>⇪ Caps lock</kbd> <kbd>⇪</kbd>
⇥ Tab ⇥ <kbd>⇥ Tab</kbd> <kbd>⇥</kbd>
⏏︎ Eject ⏏︎ <kbd>⏏︎ Eject</kbd> <kbd>⏏︎</kbd>
⌫ Delete ⌫ <kbd>⌫ Delete</kbd> <kbd>⌫</kbd>

You can always access these symbols via Character Viewer on a Mac:

Edit > Emoji & Symbols <kbd>⌃</kbd> <kbd>⌘</kbd> <kbd>Space</kbd>
You'll find these under the Symbols > ⌘ Technical Symbols list

<div class="page"/>

# Emoji

``` 
:smile:   :bell:
```

:smile: :bell:
use as reference the complete list here
https://gist.github.com/rxaviers/7360908
<br>not all MD renders them...<br>

# Markdown to PDF rendering
When rendering for PDF export use the following tags to identify a page break

``` html
<div class="page"/>
```

