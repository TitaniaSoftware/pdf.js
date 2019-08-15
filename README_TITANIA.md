# Titania PDF.js 

[Titania PDF.js](https://github.com/TitaniaSoftware/pdf.js) is a fork of [PDF.js](https://github.com/mozilla/pdf.js/) customized for use in [Titania](http://titaniasoftware.com) portal themes.

## Getting the Code

To get a local copy of the current code, clone it using git:

    $ git clone https://github.com/TitaniaSoftware/pdf.js.git
    $ cd pdf.js

Next, install Node.js via the [official package](https://nodejs.org) or via
[nvm](https://github.com/creationix/nvm). You need to install the gulp package
globally (see also [gulp's getting started](https://github.com/gulpjs/gulp/blob/master/docs/getting-started.md#getting-started)):

    $ npm install -g gulp-cli

If everything worked out, install all dependencies for PDF.js:

    $ npm install

## Building Titania PDF.js

To build a web distribution of Titania PDF.js for use in a portal theme, run:

    $ gulp dist-install

This will generate `build`, `image_decoders`, and `web` directories in the `build/minified/` directory. Copy these 3 directories into a suitable location under the portal theme's `static/` directory. (Perhaps `static/scripts/lib/pdfjs`.)

## Using Titania PDF.js in a portal theme

The built file, `web/viewer.html`, is the container for the PDF viewer. It can be the top document in a browser window, or put in an `iframe`. It will load all required pdfjs scripts and activate the PDF viewing functionality.

To invoke the viewer for a PDF file, use the portal themeFileUrl of the `web/viewer.html` and append the query, `file=/path/to/project-item.pdf`. For example, in a portal named 'scratch':

    <iframe src="/scratch/_theme/scripts/lib/pdfjs/web/viewer.html?file=/scratch/my-new-project/ESGN-C-S-PL_0000069612.pdf">

To activate the fragment metadata sidebar view, define a javascript variable named `pdfFragmentMetadata`. This variable can be either in the top window scope, or an iframe scope. If it is defined, the PDF viewer will show an extra sidebar view button. The `pdfFragmentMetadata` variable must be an array of outline items, as defined in the PDF.js source file, `src/display/api.js`, for the `getOutline()` function.

    [
      {
        title: string,
        bold: boolean,
        italic: boolean,
        color: rgb Uint8ClampedArray,
        count: integer or undefined (count of descendants),
        dest: dest obj, either 'page=n' or named destination
        url: string or undefined,
        items: array of more items like this (empty array if no children)
      },
      ...
    ]

