# Svelte Starter

**NOTE**: This uses Svelte 5
### Features

- [Lucide Icons](https://lucide.dev/) for simple/easy svg icons
- [ArchieML](http://archieml.org/) for micro-CMS powered by Google Docs and Sheets
- [Style Dictionary](https://amzn.github.io/style-dictionary/) for CSS/JS style parity
- CSV, JSON, and SVG imports
- SSR static-hosted builds by default

#### Installation
* In your local repo run `pnpm install` or `npm install`

## Development

```bash
npm run dev
```

Change the script in `package.json` to `"dev": "svelte-kit dev --host"` to test on your local network on a different device.

## Deploy
```bash
npm run build
```

This generates a directory called `build` with the statically rendered app.

A shortcut for github pages:
```bash
make github
```

Deploying to Pudding AWS:
```bash
make pudding
```

## Style

There are a few stylesheets included by default in `src/styles`. Refer to them in `app.css`, the place for applying global styles.

For variable parity in both CSS and JS, modify files in the `properties` folder using the [Style Dictionary](https://amzn.github.io/style-dictionary/) API.

Run `npm run style` to regenerate the style dictionary.

#### Some css utility classes in reset.css
* `.sr-only`: makes content invisible available for screen reader
* `.text-outline`: adds a psuedo stroke to text element

### Custom Fonts
For locally hosted fonts, simply add the font to the `static/assets` folder and include a reference in `src/styles/font.css`, making sure the url starts with `"assets/..."`.

## Google Docs and Sheets

* Create a Google Doc or Sheet
* Click `Share` -> `Advanced` -> `Change...` -> `Anyone with this link`
* In the address bar, grab the ID - eg. "...com/document/d/**1IiA5a5iCjbjOYvZVgPcjGzMy5PyfCzpPF-LnQdCdFI0**/edit"
* paste in the ID above into `google.config.js`, and set the filepath to where you want the file saved
* If you want to do a Google Sheet, be sure to include the `gid` value in the url as well

Running `npm run gdoc` at any point (even in new tab while server is running) will fetch the latest from all Docs and Sheets.

## Structural Overview

### Pages
The `src/routes` directory contains pages for your app. For a single-page app (most cases) you don't have to modify anything in here. `+page.svelte` represents the root page, think of it as the `index.html` file. It is prepopulated with a few things like metadata and font preloading. It also includes a reference to a blank slate component `src/components/Index.svelte`. This is the file you want to really start in for your app.

### Embedding Data
For smaller datasets, it is often great to embed the data into the HTML file. If you want to use data as-is, you can use normal import syntax (e.g., `import data from "$data/file.csv"`). If you are working with data but you want to preserve the original or clean/parse just what you need to use in the browser to optimize the front-end payload, you can load it via `+page.server.js`, do some work on it, and return just what you need. This is passed automatically to `+page.svelte` and accessible in any component with `getContext("data")`.


## Pre-loaded helpers

### Components

Located in `src/components`.

```js
```

*Available*
* `Scrolly.svelte`: Scrollytelling.


### Headless Components

[bits UI](https://www.bits-ui.com/docs/introduction) comes pre-installed. It is recommended to use these for any UI components.

### Actions

Located in `src/actions`.

```js
// Usage
import example from "$actions/action.js";
```

* `canTab.js`: enable/disable tabbing on child elements.
* `checkOverlap.js`: Label overlapping detection. Loops through selection of nodes and adds a class to the ones that are overlapping. Once one is hidden it ignores it.
* `focusTrap.js`: Enable a keyboard focus trap for modals and menus.
* `keepWithinBox.js`: Offsets and element left/right to stay within parent.
* `inView.js`: detect when an element enters or exits the viewport.
* `resize.js`: detect when an element is resized.

```
*Available*
* `viewport`: returns an object `{ width, height }` of the viewport dimensions. It is debounced for performance.


### Utils

Located in `src/utils/`.

```js
// Usage
import example from "$utils/example.js";
```
* `checkScrollDir.js`: Gets the user's scroll direction ("up" or "down")
* `csvDownload.js`: Converts a flat array of data to CSV content ready to be used as an `href` value for download.
* `generateId.js`: Generate an alphanumeric id.
* `loadCsv.js`: Loads and parses a CSV file.
* `loadImage.js`: Loads an image.
* `loadJson.js`: Loads and parses a JSON file.
* `loadPixels.js`: Loads the pixel data of an image via an offscreen canvas.
* `localStorage.js`: Read and write to local storage.
* `mapToArray.js`: Convenience function to convert a map to an array.
* `move.js`: transform translate function shorthand.
* `transformSvg.js`: Custom transition lets you apply an svg transform property with the in/out svelte transition. Parameters (with defaults):
* `translate.js`: Convenience function for transform translate css.
* `urlParams.js`: Get and set url parameters.

## Tips

### Image asset paths
For `img` tags, use relative paths:

```html
<img src="assets/demo/test.jpg" alt="cat" />
```

For CSS background images, use absolute paths:

```css
background: url("/assets/demo/test.jpg");
```

View example code in the preloaded demo.
