# cordova-minify-obfuscate

Cordova hook that uglifies and minifies your app's Javascript, CSS and HTML files, as well as compresses your image files. It is a modification of the work of [Ross Martin's original cordova-uglify](https://github.com/rossmartin/cordova-uglify), [Alastair Paragas' modified version](https://github.com/alastairparagas/cordova-minify), [adamerny' modified version](https://github.com/adamerny/cordova-minify-v2) and [Timofey Kachalov's Javascript-obfuscator](https://github.com/javascript-obfuscator/javascript-obfuscator) with the added default parsing of your top-level app folder `www` as well as minifying of HTML files.

This DOES NOT compress the assets in your www folder, but rather, on your respective platform's www folders, so your development environment isn't touched, and your apps stay fast and slim!

## Install
Install this package inside of your app's root folder with this command.
```
npm install git+https://github.com/yeejfe/cordova-minify-obfuscate --save-dev
```
The `--save-dev` flag is important! If you decide to work on another environment, cordova-minify cannot run without the original package and its dependencies! After install, an `after_prepare` folder will be added to your `hooks` folder with the `cordova-minify-obfuscate.js` script in it.

## Usage
Once you have this hook installed it will compress your app's JavaScript and CSS when you run a `cordova prepare <platform>` or `cordova build <platform>` command.  This hook does not change your assets that live in the root www folder; it will uglify the assets that get outputted to the platforms folder after a `prepare` or `build`.

By default the hook will uglify the JavaScript, CSS, HTML, and images in the `<platform>` `www/js`, `www/css`, `www/img`, `www/javascript`, `www/style`, `www/html`, and `www/media` folders of your project recursively (If they exist) as well as the top-level `www` folder (not recursively) to account for minifying the index.html and any other files that may reside there.

Obfuscation would be done to the JavaScript files.

[Take a look at this line in the hook to add more folders to be minified - optional](https://github.com/yeejfe/cordova-minify-obfuscate/blob/master/after_prepare/cordova-minify-obfuscate.js#l221).

You can configure the hook to uglify/minify only for a release build, [see here](https://github.com/yeejfe/cordova-minify-obfuscate/blob/master/after_prepare/cordova-minify-obfuscate.js#l43).
If you would like to have verbose logging, [set `debug` to true here](https://github.com/yeejfe/cordova-minify-obfuscate/blob/master/after_prepare/cordova-minify-obfuscate.js#l22).

To disable parsing of the `www` folder, [set `processRoot` to false here](https://github.com/yeejfe/cordova-minify-obfuscate/blob/master/after_prepare/cordova-minify-obfuscate.js#l42).

Options for HTML minification [can be changed here](https://github.com/yeejfe/cordova-minify-obfuscate/blob/master/after_prepare/cordova-minify-obfuscate.js#l23) and a list of all available options [can be found here](https://github.com/kangax/html-minifier#options-quick-reference).

Javascript uglify options [can be changed here](https://github.com/yeejfe/cordova-minify-obfuscate/blob/master/after_prepare/cordova-minify-obfuscate.js#l77) and a list of all available options [can be found here scattered throughout the page](https://github.com/mishoo/UglifyJS2).

CSS minification options [can be changed here](https://github.com/yeejfe/cordova-minify-obfuscate/blob/master/after_prepare/cordova-minify-obfuscate.js#l13) and a list of all available options [can be found here](https://github.com/jakubpawlowicz/clean-css#how-to-use-clean-css-api).

## Requirements
Out of the box this hook requires Cordova 3.3.1-0.4.2 and above but it can work with versions 3.0.0 thru 3.3.0 if you manually indicate the path for the platforms directories on Android and iOS [see here](https://github.com/yeejfe/cordova-minify-obfuscate/blob/master/after_prepare/cordova-minify-obfuscate.js#l18).  This is because the `CORDOVA_PLATFORMS` environment variable was not added until version 3.3.1-0.4.2 ([see this post by Dan Moore](http://www.mooreds.com/wordpress/archives/1425)).

## Dependencies:
* [javascript-obfuscator](https://www.npmjs.com/package/javascript-obfuscator)
* [uglify-js](https://github.com/mishoo/UglifyJS2)
* [clean-css](https://github.com/jakubpawlowicz/clean-css)
* [imagemin](https://github.com/imagemin/imagemin) (**not** image-min)
* [imagemin-svgo](https://github.com/imagemin/imagemin-svgo)
* [imagemin-jpegtran](https://github.com/imagemin/imagemin-jpegtran)
* [imagemin-gifsicle](https://github.com/imagemin/imagemin-gifsicle)
* [imagemin-optipng](https://github.com/imagemin/imagemin-optipng)
* [html-minifier](https://github.com/kangax/html-minifier)

## Quirks:
* On Linux and OSX: `hooks` folder needs to have permissions modified.  Perform a `chmod -R 755 /hooks` to resolve this issue.

## Original Work:
* [Ross Martin](https://github.com/rossmartin/cordova-uglify)
* [Alastair Paragas](https://github.com/alastairparagas/cordova-minify)
* [adamerny](https://github.com/adamerny/cordova-minify-v2)

## License
[MIT](https://github.com/yeejfe/cordova-minify-obfuscate/blob/master/LICENSE)
