# [Uppy](https://uppy.io)

<img src="https://uppy.io/images/logos/uppy-logo-2019.svg" width="120" alt="Uppy logo: a superman puppy in a pink suit" align="right">

<a href="https://www.npmjs.com/package/uppy"><img src="https://img.shields.io/npm/v/uppy.svg?style=flat-square"></a>
<a href="https://travis-ci.org/transloadit/uppy"><img src="https://img.shields.io/travis/transloadit/uppy/master.svg?style=flat-square" alt="Build Status"></a>

Uppy is a sleek, modular JavaScript file uploader that integrates seamlessly with any application. It’s fast, easy to use and lets you worry about more important problems than building a file uploader.

- **Fetch** files from local disk, remote URLs, Google Drive, Dropbox, Instagram or snap and record selfies with a camera
- **Preview** and edit metadata with a nice interface
- **Upload** to the final destination, optionally process/encode

<img src="https://github.com/transloadit/uppy/raw/master/assets/uppy-demo-oct-2018.gif">

**[Read the docs](https://uppy.io/docs)** | **[Try Uppy](https://uppy.io/examples/dashboard/)**

<a href="https://transloadit.com" target="_blank"><img width="185" src="https://github.com/transloadit/uppy/raw/master/assets/developed-by-transloadit.png"></a>

Uppy is being developed by the folks at [Transloadit](https://transloadit.com), a versatile file encoding service.

## Example

Code used in the above example:

```js
const Uppy = require('@uppy/core')
const Dashboard = require('@uppy/dashboard')
const GoogleDrive = require('@uppy/google-drive')
const Instagram = require('@uppy/instagram')
const Webcam = require('@uppy/webcam')
const Tus = require('@uppy/tus')

const uppy = Uppy({ autoProceed: false })
  .use(Dashboard, { trigger: '#select-files' })
  .use(GoogleDrive, { target: Dashboard, companionUrl: 'https://companion.uppy.io' })
  .use(Instagram, { target: Dashboard, companionUrl: 'https://companion.uppy.io' })
  .use(Webcam, { target: Dashboard })
  .use(Tus, { endpoint: 'https://master.tus.io/files/' })
  .on('complete', (result) => {
    console.log('Upload result:', result)
  })
```

**[Try it online](https://uppy.io/examples/dashboard/)** or **[read the docs](https://uppy.io/docs)** for more details on how to use Uppy and its plugins.

## Features

- Lightweight, modular plugin-based architecture, easy on dependencies :zap:
- Resumable file uploads via the open [tus](https://tus.io/) standard, so large uploads survive network hiccups
- Supports picking files from: Webcam, Dropbox, Google Drive, Instagram, bypassing the user’s device where possible, syncing between servers directly via [@uppy/companion](https://uppy.io/docs/companion)
- Works great with file encoding and processing backends, such as [Transloadit](https://transloadit.com), works great without (just roll your own Apache/Nginx/Node/FFmpeg/etc backend)
- Sleek user interface :sparkles:
- Optional file recovery (after a browser crash) with [Golden Retriever](https://uppy.io/docs/golden-retriever/)
- Speaks multiple languages (i18n) :earth_africa:
- Built with accessibility in mind
- Free for the world, forever (as in beer 🍺, pizza 🍕, and liberty 🗽)
- Cute as a puppy, also accepts cat pictures :dog:

## Installation

``` bash
$ npm install @uppy/core @uppy/dashboard @uppy/tus
```

We recommend installing from npm and then using a module bundler such as [Webpack](https://webpack.js.org/), [Browserify](http://browserify.org/) or [Rollup.js](http://rollupjs.org/).

Add CSS [uppy.min.css](https://transloadit.edgly.net/releases/uppy/v1.13.0/uppy.min.css), either to your HTML page's `<head>` or include in JS, if your bundler of choice supports it — transforms and plugins are available for Browserify and Webpack.

Alternatively, you can also use a pre-built bundle from Transloadit's CDN: Edgly. In that case `Uppy` will attach itself to the global `window.Uppy` object.

> ⚠️ The bundle currently consists of most Uppy plugins, so this method is not recommended for production, as your users will have to download all plugins when you are likely using just a few.

```html
<!-- 1. Add CSS to `<head>` -->
<link href="https://transloadit.edgly.net/releases/uppy/v1.13.0/uppy.min.css" rel="stylesheet">

<!-- 2. Add JS before the closing `</body>` -->
<script src="https://transloadit.edgly.net/releases/uppy/v1.13.0/uppy.min.js"></script>

<!-- 3. Initialize -->
<div class="UppyDragDrop"></div>
<script>
  var uppy = Uppy.Core()
  uppy.use(Uppy.DragDrop, { target: '.UppyDragDrop' })
  uppy.use(Uppy.Tus, { endpoint: '//master.tus.io/files/' })
</script>
```

## Documentation

- [Uppy](https://uppy.io/docs/uppy/) — full list of options, methods and events
- [Plugins](https://uppy.io/docs/plugins/) — list of Uppy plugins and their options
- [Companion](https://uppy.io/docs/companion/) — setting up and running a Companion instance, which adds support for Instagram, Dropbox, Google Drive and remote URLs
- [React](https://uppy.io/docs/react/) — components to integrate Uppy UI plugins with React apps
- [Architecture & Writing a Plugin](https://uppy.io/docs/writing-plugins/) — how to write a plugin for Uppy

## Plugins

[List of plugins and their common options](https://uppy.io/docs/plugins/)

### UI Elements

- [`Dashboard`](https://uppy.io/docs/dashboard/) — universal UI with previews, progress bars, metadata editor and all the cool stuff. Required for most UI plugins like Webcam and Instagram
- [`Progress Bar`](https://uppy.io/docs/progress-bar/) — minimal progress bar that fills itself when upload progresses
- [`Status Bar`](https://uppy.io/docs/status-bar/) — more detailed progress, pause/resume/cancel buttons, percentage, speed, uploaded/total sizes (included by default with `Dashboard`)
- [`Informer`](https://uppy.io/docs/informer/) — send notifications like “smile” before taking a selfie or “upload failed” when all is lost (also included by default with `Dashboard`)

### Sources

- [`Drag & Drop`](https://uppy.io/docs/drag-drop/) — plain and simple drag and drop area
- [`File Input`](https://uppy.io/docs/file-input/) — even plainer “select files” button
- [`Webcam`](https://uppy.io/docs/webcam/) — snap and record those selfies 📷
- ⓒ [`Google Drive`](https://uppy.io/docs/google-drive/)
- ⓒ [`Dropbox`](https://uppy.io/docs/dropbox/)
- ⓒ [`Instagram`](https://uppy.io/docs/instagram/)
- ⓒ [`Facebook`](https://uppy.io/docs/facebook/)
- ⓒ [`OneDrive`](https://uppy.io/docs/onedrive/)
- ⓒ [`Import From URL`](https://uppy.io/docs/url/) — support picking files from remote providers or direct URLs from anywhere on the web

The ⓒ mark means that [`@uppy/companion`](https://uppy.io/docs/companion), a server-side component, is needed for a plugin to work.

### Destinations

- [`Tus`](https://uppy.io/docs/tus/) — resumable uploads via the open [tus](http://tus.io) standard
- [`XHR Upload`](https://uppy.io/docs/xhr-upload/) — regular uploads for any backend out there (like Apache, Nginx)
- [`AWS S3`](https://uppy.io/docs/aws-s3/) — uploader for AWS S3
- [`AWS S3 Multipart`](https://uppy.io/docs/aws-s3-multipart/) — upload to AWS S3

### File Processing

- [`Robodog`](https://uppy.io/docs/robodog/) — user friendly abstraction to do file processing with Transloadit
- [`Transloadit`](https://uppy.io/docs/transloadit/) — support for [Transloadit](http://transloadit.com)’s robust file uploading and encoding backend

### Miscellaneous

- [`Golden Retriever`](https://uppy.io/docs/golden-retriever/) — restores files after a browser crash, like it’s nothing
- [`Thumbnail Generator`](https://uppy.io/docs/thumbnail-generator/) — generates image previews (included by default with `Dashboard`)
- [`Form`](https://uppy.io/docs/form/) — collects metadata from `<form>` right before an Uppy upload, then optionally appends results back to the form
- [`Redux`](https://uppy.io/docs/redux/) — for your emerging [time traveling](https://github.com/gaearon/redux-devtools) needs

## React

- [React](https://uppy.io/docs/react/) — components to integrate Uppy UI plugins with React apps
- [React Native](https://uppy.io//docs/react/native/) — basic Uppy component for React Native with Expo

## Browser Support

<a href="https://saucelabs.com/u/transloadit-uppy">
  <img src="https://saucelabs.com/browser-matrix/transloadit-uppy.svg" alt="Sauce Test Status"/>
</a>

We aim to support IE11 and recent versions of Safari, Edge, Chrome, Firefox and Opera.

We still run end-to-end tests with IE10, but we are not actively supporting it or fixing visual / minor issues.

### Polyfills

Uppy heavily uses Promises. If your target environment [does not support Promises](https://caniuse.com/#feat=promises), use a polyfill like `es6-promise` before initializing Uppy.

When using remote providers like Google Drive or Dropbox, the Fetch API is used. If your target environment does not support the [Fetch API](https://caniuse.com/#feat=fetch), use a polyfill like `whatwg-fetch` before initializing Uppy. The Fetch API polyfill must be loaded _after_ the Promises polyfill, because Fetch uses Promises.

With a module bundler, you can use the required polyfills like so:

```shell
npm install es6-promise whatwg-fetch
```
```js
require('es6-promise/auto')
require('whatwg-fetch')
const Uppy = require('@uppy/core')
```

If you're using Uppy from CDN, `es6-promise` and `whatwg-fetch` are already included in the bundle, so no need to include anything additionally:

```html
<script src="https://transloadit.edgly.net/releases/uppy/v1.13.0/uppy.min.js"></script>
```

## FAQ

### Why not just use `<input type="file">`?

Having no JavaScript beats having a lot of it, so that’s a fair question! Running an uploading & encoding business for ten years though we found that in cases, the file input leaves some to be desired:

- We received complaints about broken uploads and found that resumable uploads are important, especially for big files and to be inclusive towards people on poorer connections (we also launched [tus.io](https://tus.io) to attack that problem). Uppy uploads can survive network outages and browser crashes or accidental navigate-aways.
- Uppy supports editing meta information before uploading (and e.g. cropping is planned).
- There’s the situation where people are using their mobile devices and want to upload on the go, but they have their picture on Instagram, files in Dropbox or just a plain file URL from anywhere on the open web. Uppy allows to pick files from those and push it to the destination without downloading it to your mobile device first.
- Accurate upload progress reporting is an issue on many platforms.
- Some file validation — size, type, number of files — can be done on the client with Uppy.
- Uppy integrates webcam support, in case your users want to upload a picture/video/audio that does not exist yet :)
- A larger drag and drop surface can be pleasant to work with. Some people also like that you can control the styling, language, etc.
- Uppy is aware of encoding backends. Often after an upload, the server needs to rotate, detect faces, optimize for iPad, or what have you. Uppy can track progress of this and report back to the user in different ways.
- Sometimes you might want your uploads to happen while you continue to interact on the same single page.

Not all apps need all of these features. An `<input type="file">` is fine in many situations. But these were a few things that our customers hit / asked about enough to spark us to develop Uppy.

### Why is all this goodness free?

Transloadit’s team is small and we have a shared ambition to make a living from open source. By giving away projects like [tus.io](https://tus.io) and [Uppy](https://uppy.io), we’re hoping to advance the state of the art, make life a tiny little bit better for everyone and in doing so have rewarding jobs and get some eyes on our commercial service: [a content ingestion & processing platform](https://transloadit.com).

Our thinking is that if just a fraction of our open source userbase can see the appeal of hosted versions straight from the source, that could already be enough to sustain our work. So far this is working out! We’re able to dedicate 80% of our time to open source and haven’t gone bankrupt yet. :D

### Does Uppy support React?

Yep, we have Uppy React components, please see [Uppy React docs](https://uppy.io/docs/react/).

### Does Uppy support S3 uploads?

Yes, there is an S3 plugin, please check out the [docs](https://uppy.io/docs/aws-s3/) for more.

### Do I need to install a special service/server for Uppy? Can I use it with Rails/Node/Go/PHP?

Yes, whatever you want on the backend will work with `@uppy/xhr-upload` plugin, since it just does a `POST` or `PUT` request. Here’s a [PHP backend example](https://uppy.io/docs/xhr-upload/#Uploading-to-a-PHP-Server).

If you want resumability with the Tus plugin, use [one of the tus server implementations](https://tus.io/implementations.html) 👌🏼

And you’ll need [`@uppy/companion`](https://uppy.io/docs/companion) if you’d like your users to be able to pick files from Instagram, Google Drive, Dropbox or via direct URLs (with more services coming).

## Contributions are welcome

- Contributor’s guide in [`.github/CONTRIBUTING.md`](.github/CONTRIBUTING.md)
- Changelog to track our release progress (we aim to roll out a release every month): [`CHANGELOG.md`](CHANGELOG.md)

## Used by

Uppy is used by: [Photobox](http://photobox.com), [Issuu](https://issuu.com/), [Law Insider](https://lawinsider.com), [Cool Tabs](https://cool-tabs.com), [Soundoff](https://soundoff.io), [Scrumi](https://www.scrumi.io/), [Crive](https://crive.co/) and others.

Use Uppy in your project? [Let us know](https://github.com/transloadit/uppy/issues/769)!

## Contributors

<!--contributors-->
[<img alt="arturi" src="https://avatars2.githubusercontent.com/u/1199054?v=4&s=117" width="117">](https://github.com/arturi) |[<img alt="goto-bus-stop" src="https://avatars1.githubusercontent.com/u/1006268?v=4&s=117" width="117">](https://github.com/goto-bus-stop) |[<img alt="kvz" src="https://avatars2.githubusercontent.com/u/26752?v=4&s=117" width="117">](https://github.com/kvz) |[<img alt="ifedapoolarewaju" src="https://avatars1.githubusercontent.com/u/8383781?v=4&s=117" width="117">](https://github.com/ifedapoolarewaju) |[<img alt="hedgerh" src="https://avatars2.githubusercontent.com/u/2524280?v=4&s=117" width="117">](https://github.com/hedgerh) |[<img alt="AJvanLoon" src="https://avatars0.githubusercontent.com/u/15716628?v=4&s=117" width="117">](https://github.com/AJvanLoon) |
:---: |:---: |:---: |:---: |:---: |:---: |
[arturi](https://github.com/arturi) |[goto-bus-stop](https://github.com/goto-bus-stop) |[kvz](https://github.com/kvz) |[ifedapoolarewaju](https://github.com/ifedapoolarewaju) |[hedgerh](https://github.com/hedgerh) |[AJvanLoon](https://github.com/AJvanLoon) |

[<img alt="nqst" src="https://avatars0.githubusercontent.com/u/375537?v=4&s=117" width="117">](https://github.com/nqst) |[<img alt="lakesare" src="https://avatars1.githubusercontent.com/u/7578559?v=4&s=117" width="117">](https://github.com/lakesare) |[<img alt="kiloreux" src="https://avatars0.githubusercontent.com/u/6282557?v=4&s=117" width="117">](https://github.com/kiloreux) |[<img alt="sadovnychyi" src="https://avatars3.githubusercontent.com/u/193864?v=4&s=117" width="117">](https://github.com/sadovnychyi) |[<img alt="samuelayo" src="https://avatars1.githubusercontent.com/u/14964486?v=4&s=117" width="117">](https://github.com/samuelayo) |[<img alt="richardwillars" src="https://avatars3.githubusercontent.com/u/291004?v=4&s=117" width="117">](https://github.com/richardwillars) |
:---: |:---: |:---: |:---: |:---: |:---: |
[nqst](https://github.com/nqst) |[lakesare](https://github.com/lakesare) |[kiloreux](https://github.com/kiloreux) |[sadovnychyi](https://github.com/sadovnychyi) |[samuelayo](https://github.com/samuelayo) |[richardwillars](https://github.com/richardwillars) |

[<img alt="zcallan" src="https://avatars0.githubusercontent.com/u/13760738?v=4&s=117" width="117">](https://github.com/zcallan) |[<img alt="tim-kos" src="https://avatars1.githubusercontent.com/u/15005?v=4&s=117" width="117">](https://github.com/tim-kos) |[<img alt="janko" src="https://avatars2.githubusercontent.com/u/795488?v=4&s=117" width="117">](https://github.com/janko) |[<img alt="wilkoklak" src="https://avatars1.githubusercontent.com/u/17553085?v=4&s=117" width="117">](https://github.com/wilkoklak) |[<img alt="oliverpool" src="https://avatars0.githubusercontent.com/u/3864879?v=4&s=117" width="117">](https://github.com/oliverpool) |[<img alt="mcallistertyler95" src="https://avatars1.githubusercontent.com/u/14939210?v=4&s=117" width="117">](https://github.com/mcallistertyler95) |
:---: |:---: |:---: |:---: |:---: |:---: |
[zcallan](https://github.com/zcallan) |[tim-kos](https://github.com/tim-kos) |[janko](https://github.com/janko) |[wilkoklak](https://github.com/wilkoklak) |[oliverpool](https://github.com/oliverpool) |[mcallistertyler95](https://github.com/mcallistertyler95) |

[<img alt="DJWassink" src="https://avatars3.githubusercontent.com/u/1822404?v=4&s=117" width="117">](https://github.com/DJWassink) |[<img alt="taoqf" src="https://avatars3.githubusercontent.com/u/15901911?v=4&s=117" width="117">](https://github.com/taoqf) |[<img alt="bertho-zero" src="https://avatars0.githubusercontent.com/u/8525267?v=4&s=117" width="117">](https://github.com/bertho-zero) |[<img alt="ap--" src="https://avatars1.githubusercontent.com/u/1463443?v=4&s=117" width="117">](https://github.com/ap--) |[<img alt="dependabot[bot]" src="https://avatars0.githubusercontent.com/in/29110?v=4&s=117" width="117">](https://github.com/apps/dependabot) |[<img alt="bambii7" src="https://avatars3.githubusercontent.com/u/1826459?v=4&s=117" width="117">](https://github.com/bambii7) |
:---: |:---: |:---: |:---: |:---: |:---: |
[DJWassink](https://github.com/DJWassink) |[taoqf](https://github.com/taoqf) |[bertho-zero](https://github.com/bertho-zero) |[ap--](https://github.com/ap--) |[dependabot[bot]](https://github.com/apps/dependabot) |[bambii7](https://github.com/bambii7) |

[<img alt="tranvansang" src="https://avatars1.githubusercontent.com/u/13043196?v=4&s=117" width="117">](https://github.com/tranvansang) |[<img alt="MikeKovarik" src="https://avatars0.githubusercontent.com/u/3995401?v=4&s=117" width="117">](https://github.com/MikeKovarik) |[<img alt="pauln" src="https://avatars3.githubusercontent.com/u/574359?v=4&s=117" width="117">](https://github.com/pauln) |[<img alt="toadkicker" src="https://avatars1.githubusercontent.com/u/523330?v=4&s=117" width="117">](https://github.com/toadkicker) |[<img alt="gavboulton" src="https://avatars0.githubusercontent.com/u/3900826?v=4&s=117" width="117">](https://github.com/gavboulton) |[<img alt="mrbatista" src="https://avatars0.githubusercontent.com/u/6544817?v=4&s=117" width="117">](https://github.com/mrbatista) |
:---: |:---: |:---: |:---: |:---: |:---: |
[tranvansang](https://github.com/tranvansang) |[MikeKovarik](https://github.com/MikeKovarik) |[pauln](https://github.com/pauln) |[toadkicker](https://github.com/toadkicker) |[gavboulton](https://github.com/gavboulton) |[mrbatista](https://github.com/mrbatista) |

[<img alt="manuelkiessling" src="https://avatars2.githubusercontent.com/u/206592?v=4&s=117" width="117">](https://github.com/manuelkiessling) |[<img alt="nndevstudio" src="https://avatars2.githubusercontent.com/u/22050968?v=4&s=117" width="117">](https://github.com/nndevstudio) |[<img alt="ogtfaber" src="https://avatars2.githubusercontent.com/u/320955?v=4&s=117" width="117">](https://github.com/ogtfaber) |[<img alt="dargmuesli" src="https://avatars2.githubusercontent.com/u/4778485?v=4&s=117" width="117">](https://github.com/dargmuesli) |[<img alt="sunil-shrestha" src="https://avatars3.githubusercontent.com/u/2129058?v=4&s=117" width="117">](https://github.com/sunil-shrestha) |[<img alt="yonahforst" src="https://avatars3.githubusercontent.com/u/1440796?v=4&s=117" width="117">](https://github.com/yonahforst) |
:---: |:---: |:---: |:---: |:---: |:---: |
[manuelkiessling](https://github.com/manuelkiessling) |[nndevstudio](https://github.com/nndevstudio) |[ogtfaber](https://github.com/ogtfaber) |[dargmuesli](https://github.com/dargmuesli) |[sunil-shrestha](https://github.com/sunil-shrestha) |[yonahforst](https://github.com/yonahforst) |

[<img alt="stephentuso" src="https://avatars2.githubusercontent.com/u/11889560?v=4&s=117" width="117">](https://github.com/stephentuso) |[<img alt="mskelton" src="https://avatars3.githubusercontent.com/u/25914066?v=4&s=117" width="117">](https://github.com/mskelton) |[<img alt="sksavant" src="https://avatars1.githubusercontent.com/u/1040701?v=4&s=117" width="117">](https://github.com/sksavant) |[<img alt="btrice" src="https://avatars2.githubusercontent.com/u/4358225?v=4&s=117" width="117">](https://github.com/btrice) |[<img alt="Burkes" src="https://avatars2.githubusercontent.com/u/9220052?v=4&s=117" width="117">](https://github.com/Burkes) |[<img alt="craigjennings11" src="https://avatars2.githubusercontent.com/u/1683368?v=4&s=117" width="117">](https://github.com/craigjennings11) |
:---: |:---: |:---: |:---: |:---: |:---: |
[stephentuso](https://github.com/stephentuso) |[mskelton](https://github.com/mskelton) |[sksavant](https://github.com/sksavant) |[btrice](https://github.com/btrice) |[Burkes](https://github.com/Burkes) |[craigjennings11](https://github.com/craigjennings11) |

[<img alt="davekiss" src="https://avatars2.githubusercontent.com/u/1256071?v=4&s=117" width="117">](https://github.com/davekiss) |[<img alt="frobinsonj" src="https://avatars3.githubusercontent.com/u/16726902?v=4&s=117" width="117">](https://github.com/frobinsonj) |[<img alt="geertclerx" src="https://avatars0.githubusercontent.com/u/1381327?v=4&s=117" width="117">](https://github.com/geertclerx) |[<img alt="jasonbosco" src="https://avatars3.githubusercontent.com/u/458383?v=4&s=117" width="117">](https://github.com/jasonbosco) |[<img alt="jedwood" src="https://avatars0.githubusercontent.com/u/369060?v=4&s=117" width="117">](https://github.com/jedwood) |[<img alt="Mactaivsh" src="https://avatars0.githubusercontent.com/u/12948083?v=4&s=117" width="117">](https://github.com/Mactaivsh) |
:---: |:---: |:---: |:---: |:---: |:---: |
[davekiss](https://github.com/davekiss) |[frobinsonj](https://github.com/frobinsonj) |[geertclerx](https://github.com/geertclerx) |[jasonbosco](https://github.com/jasonbosco) |[jedwood](https://github.com/jedwood) |[Mactaivsh](https://github.com/Mactaivsh) |

[<img alt="maferland" src="https://avatars3.githubusercontent.com/u/5889721?v=4&s=117" width="117">](https://github.com/maferland) |[<img alt="Martin005" src="https://avatars0.githubusercontent.com/u/10096404?v=4&s=117" width="117">](https://github.com/Martin005) |[<img alt="martiuslim" src="https://avatars2.githubusercontent.com/u/17944339?v=4&s=117" width="117">](https://github.com/martiuslim) |[<img alt="uxitten" src="https://avatars0.githubusercontent.com/u/1549069?v=4&s=117" width="117">](https://github.com/uxitten) |[<img alt="msand" src="https://avatars2.githubusercontent.com/u/1131362?v=4&s=117" width="117">](https://github.com/msand) |[<img alt="richartkeil" src="https://avatars0.githubusercontent.com/u/8680858?v=4&s=117" width="117">](https://github.com/richartkeil) |
:---: |:---: |:---: |:---: |:---: |:---: |
[maferland](https://github.com/maferland) |[Martin005](https://github.com/Martin005) |[martiuslim](https://github.com/martiuslim) |[uxitten](https://github.com/uxitten) |[msand](https://github.com/msand) |[richartkeil](https://github.com/richartkeil) |

[<img alt="richmeij" src="https://avatars0.githubusercontent.com/u/9741858?v=4&s=117" width="117">](https://github.com/richmeij) |[<img alt="rosenfeld" src="https://avatars1.githubusercontent.com/u/32246?v=4&s=117" width="117">](https://github.com/rosenfeld) |[<img alt="ThomasG77" src="https://avatars2.githubusercontent.com/u/642120?v=4&s=117" width="117">](https://github.com/ThomasG77) |[<img alt="zhuangya" src="https://avatars2.githubusercontent.com/u/499038?v=4&s=117" width="117">](https://github.com/zhuangya) |[<img alt="allenfantasy" src="https://avatars1.githubusercontent.com/u/1009294?v=4&s=117" width="117">](https://github.com/allenfantasy) |[<img alt="Zyclotrop-j" src="https://avatars0.githubusercontent.com/u/4939546?v=4&s=117" width="117">](https://github.com/Zyclotrop-j) |
:---: |:---: |:---: |:---: |:---: |:---: |
[richmeij](https://github.com/richmeij) |[rosenfeld](https://github.com/rosenfeld) |[ThomasG77](https://github.com/ThomasG77) |[zhuangya](https://github.com/zhuangya) |[allenfantasy](https://github.com/allenfantasy) |[Zyclotrop-j](https://github.com/Zyclotrop-j) |

[<img alt="fortrieb" src="https://avatars0.githubusercontent.com/u/4126707?v=4&s=117" width="117">](https://github.com/fortrieb) |[<img alt="muhammadInam" src="https://avatars1.githubusercontent.com/u/7801708?v=4&s=117" width="117">](https://github.com/muhammadInam) |[<img alt="rettgerst" src="https://avatars2.githubusercontent.com/u/11684948?v=4&s=117" width="117">](https://github.com/rettgerst) |[<img alt="jukakoski" src="https://avatars0.githubusercontent.com/u/52720967?v=4&s=117" width="117">](https://github.com/jukakoski) |[<img alt="MatthiasKunnen" src="https://avatars3.githubusercontent.com/u/16807587?v=4&s=117" width="117">](https://github.com/MatthiasKunnen) |[<img alt="ajschmidt8" src="https://avatars0.githubusercontent.com/u/7400326?v=4&s=117" width="117">](https://github.com/ajschmidt8) |
:---: |:---: |:---: |:---: |:---: |:---: |
[fortrieb](https://github.com/fortrieb) |[muhammadInam](https://github.com/muhammadInam) |[rettgerst](https://github.com/rettgerst) |[jukakoski](https://github.com/jukakoski) |[MatthiasKunnen](https://github.com/MatthiasKunnen) |[ajschmidt8](https://github.com/ajschmidt8) |

[<img alt="superhawk610" src="https://avatars1.githubusercontent.com/u/18172185?v=4&s=117" width="117">](https://github.com/superhawk610) |[<img alt="adamelmore" src="https://avatars2.githubusercontent.com/u/2363879?v=4&s=117" width="117">](https://github.com/adamelmore) |[<img alt="adamvigneault" src="https://avatars2.githubusercontent.com/u/18236120?v=4&s=117" width="117">](https://github.com/adamvigneault) |[<img alt="asmt3" src="https://avatars1.githubusercontent.com/u/1777709?v=4&s=117" width="117">](https://github.com/asmt3) |[<img alt="alexnj" src="https://avatars0.githubusercontent.com/u/683500?v=4&s=117" width="117">](https://github.com/alexnj) |[<img alt="amitport" src="https://avatars1.githubusercontent.com/u/1131991?v=4&s=117" width="117">](https://github.com/amitport) |
:---: |:---: |:---: |:---: |:---: |:---: |
[superhawk610](https://github.com/superhawk610) |[adamelmore](https://github.com/adamelmore) |[adamvigneault](https://github.com/adamvigneault) |[asmt3](https://github.com/asmt3) |[alexnj](https://github.com/alexnj) |[amitport](https://github.com/amitport) |

[<img alt="functino" src="https://avatars0.githubusercontent.com/u/415498?v=4&s=117" width="117">](https://github.com/functino) |[<img alt="Botz" src="https://avatars3.githubusercontent.com/u/2706678?v=4&s=117" width="117">](https://github.com/Botz) |[<img alt="radarhere" src="https://avatars2.githubusercontent.com/u/3112309?v=4&s=117" width="117">](https://github.com/radarhere) |[<img alt="superandrew213" src="https://avatars3.githubusercontent.com/u/13059204?v=4&s=117" width="117">](https://github.com/superandrew213) |[<img alt="andychongyz" src="https://avatars0.githubusercontent.com/u/12697240?v=4&s=117" width="117">](https://github.com/andychongyz) |[<img alt="arthurdenner" src="https://avatars0.githubusercontent.com/u/13774309?v=4&s=117" width="117">](https://github.com/arthurdenner) |
:---: |:---: |:---: |:---: |:---: |:---: |
[functino](https://github.com/functino) |[Botz](https://github.com/Botz) |[radarhere](https://github.com/radarhere) |[superandrew213](https://github.com/superandrew213) |[andychongyz](https://github.com/andychongyz) |[arthurdenner](https://github.com/arthurdenner) |

[<img alt="bochkarev-artem" src="https://avatars2.githubusercontent.com/u/11025874?v=4&s=117" width="117">](https://github.com/bochkarev-artem) |[<img alt="ayhankesicioglu" src="https://avatars2.githubusercontent.com/u/36304312?v=4&s=117" width="117">](https://github.com/ayhankesicioglu) |[<img alt="azeemba" src="https://avatars0.githubusercontent.com/u/2160795?v=4&s=117" width="117">](https://github.com/azeemba) |[<img alt="bducharme" src="https://avatars2.githubusercontent.com/u/4173569?v=4&s=117" width="117">](https://github.com/bducharme) |[<img alt="Quorafind" src="https://avatars1.githubusercontent.com/u/13215013?v=4&s=117" width="117">](https://github.com/Quorafind) |[<img alt="cellvinchung" src="https://avatars2.githubusercontent.com/u/5347394?v=4&s=117" width="117">](https://github.com/cellvinchung) |
:---: |:---: |:---: |:---: |:---: |:---: |
[bochkarev-artem](https://github.com/bochkarev-artem) |[ayhankesicioglu](https://github.com/ayhankesicioglu) |[azeemba](https://github.com/azeemba) |[bducharme](https://github.com/bducharme) |[Quorafind](https://github.com/Quorafind) |[cellvinchung](https://github.com/cellvinchung) |

[<img alt="chao" src="https://avatars2.githubusercontent.com/u/55872?v=4&s=117" width="117">](https://github.com/chao) |[<img alt="csprance" src="https://avatars0.githubusercontent.com/u/7902617?v=4&s=117" width="117">](https://github.com/csprance) |[<img alt="Aarbel" src="https://avatars2.githubusercontent.com/u/25119847?v=4&s=117" width="117">](https://github.com/Aarbel) |[<img alt="cbush06" src="https://avatars0.githubusercontent.com/u/15720146?v=4&s=117" width="117">](https://github.com/cbush06) |[<img alt="czj" src="https://avatars2.githubusercontent.com/u/14306?v=4&s=117" width="117">](https://github.com/czj) |[<img alt="ardeois" src="https://avatars0.githubusercontent.com/u/1867939?v=4&s=117" width="117">](https://github.com/ardeois) |
:---: |:---: |:---: |:---: |:---: |:---: |
[chao](https://github.com/chao) |[csprance](https://github.com/csprance) |[Aarbel](https://github.com/Aarbel) |[cbush06](https://github.com/cbush06) |[czj](https://github.com/czj) |[ardeois](https://github.com/ardeois) |

[<img alt="sercraig" src="https://avatars3.githubusercontent.com/u/24261518?v=4&s=117" width="117">](https://github.com/sercraig) |[<img alt="danmichaelo" src="https://avatars1.githubusercontent.com/u/434495?v=4&s=117" width="117">](https://github.com/danmichaelo) |[<img alt="mrboomer" src="https://avatars0.githubusercontent.com/u/5942912?v=4&s=117" width="117">](https://github.com/mrboomer) |[<img alt="tuoxiansp" src="https://avatars1.githubusercontent.com/u/3960056?v=4&s=117" width="117">](https://github.com/tuoxiansp) |[<img alt="davilima6" src="https://avatars0.githubusercontent.com/u/422130?v=4&s=117" width="117">](https://github.com/davilima6) |[<img alt="DennisKofflard" src="https://avatars2.githubusercontent.com/u/8669129?v=4&s=117" width="117">](https://github.com/DennisKofflard) |
:---: |:---: |:---: |:---: |:---: |:---: |
[sercraig](https://github.com/sercraig) |[danmichaelo](https://github.com/danmichaelo) |[mrboomer](https://github.com/mrboomer) |[tuoxiansp](https://github.com/tuoxiansp) |[davilima6](https://github.com/davilima6) |[DennisKofflard](https://github.com/DennisKofflard) |

[<img alt="dominiceden" src="https://avatars2.githubusercontent.com/u/6367692?v=4&s=117" width="117">](https://github.com/dominiceden) |[<img alt="efbautista" src="https://avatars3.githubusercontent.com/u/35430671?v=4&s=117" width="117">](https://github.com/efbautista) |[<img alt="yoldar" src="https://avatars3.githubusercontent.com/u/1597578?v=4&s=117" width="117">](https://github.com/yoldar) |[<img alt="eliOcs" src="https://avatars1.githubusercontent.com/u/1283954?v=4&s=117" width="117">](https://github.com/eliOcs) |[<img alt="lowsprofile" src="https://avatars1.githubusercontent.com/u/11029687?v=4&s=117" width="117">](https://github.com/lowsprofile) |[<img alt="fgallinari" src="https://avatars1.githubusercontent.com/u/6473638?v=4&s=117" width="117">](https://github.com/fgallinari) |
:---: |:---: |:---: |:---: |:---: |:---: |
[dominiceden](https://github.com/dominiceden) |[efbautista](https://github.com/efbautista) |[yoldar](https://github.com/yoldar) |[eliOcs](https://github.com/eliOcs) |[lowsprofile](https://github.com/lowsprofile) |[fgallinari](https://github.com/fgallinari) |

[<img alt="FWirtz" src="https://avatars1.githubusercontent.com/u/6052785?v=4&s=117" width="117">](https://github.com/FWirtz) |[<img alt="geoffappleford" src="https://avatars2.githubusercontent.com/u/731678?v=4&s=117" width="117">](https://github.com/geoffappleford) |[<img alt="gjungb" src="https://avatars0.githubusercontent.com/u/3391068?v=4&s=117" width="117">](https://github.com/gjungb) |[<img alt="roenschg" src="https://avatars2.githubusercontent.com/u/9590236?v=4&s=117" width="117">](https://github.com/roenschg) |[<img alt="HughbertD" src="https://avatars0.githubusercontent.com/u/1580021?v=4&s=117" width="117">](https://github.com/HughbertD) |[<img alt="HussainAlkhalifah" src="https://avatars1.githubusercontent.com/u/43642162?v=4&s=117" width="117">](https://github.com/HussainAlkhalifah) |
:---: |:---: |:---: |:---: |:---: |:---: |
[FWirtz](https://github.com/FWirtz) |[geoffappleford](https://github.com/geoffappleford) |[gjungb](https://github.com/gjungb) |[roenschg](https://github.com/roenschg) |[HughbertD](https://github.com/HughbertD) |[HussainAlkhalifah](https://github.com/HussainAlkhalifah) |

[<img alt="huydod" src="https://avatars2.githubusercontent.com/u/37580530?v=4&s=117" width="117">](https://github.com/huydod) |[<img alt="ishendyweb" src="https://avatars1.githubusercontent.com/u/10582418?v=4&s=117" width="117">](https://github.com/ishendyweb) |[<img alt="JacobMGEvans" src="https://avatars1.githubusercontent.com/u/27247160?v=4&s=117" width="117">](https://github.com/JacobMGEvans) |[<img alt="jdssem" src="https://avatars0.githubusercontent.com/u/978944?v=4&s=117" width="117">](https://github.com/jdssem) |[<img alt="jcjmcclean" src="https://avatars3.githubusercontent.com/u/1822574?v=4&s=117" width="117">](https://github.com/jcjmcclean) |[<img alt="janklimo" src="https://avatars1.githubusercontent.com/u/7811733?v=4&s=117" width="117">](https://github.com/janklimo) |
:---: |:---: |:---: |:---: |:---: |:---: |
[huydod](https://github.com/huydod) |[ishendyweb](https://github.com/ishendyweb) |[JacobMGEvans](https://github.com/JacobMGEvans) |[jdssem](https://github.com/jdssem) |[jcjmcclean](https://github.com/jcjmcclean) |[janklimo](https://github.com/janklimo) |

[<img alt="vith" src="https://avatars1.githubusercontent.com/u/3265539?v=4&s=117" width="117">](https://github.com/vith) |[<img alt="jessica-coursera" src="https://avatars1.githubusercontent.com/u/35155465?v=4&s=117" width="117">](https://github.com/jessica-coursera) |[<img alt="theJoeBiz" src="https://avatars1.githubusercontent.com/u/189589?v=4&s=117" width="117">](https://github.com/theJoeBiz) |[<img alt="jderrough" src="https://avatars3.githubusercontent.com/u/1108358?v=4&s=117" width="117">](https://github.com/jderrough) |[<img alt="jonathanly" src="https://avatars3.githubusercontent.com/u/13286473?v=4&s=117" width="117">](https://github.com/jonathanly) |[<img alt="jorgeepc" src="https://avatars3.githubusercontent.com/u/3879892?v=4&s=117" width="117">](https://github.com/jorgeepc) |
:---: |:---: |:---: |:---: |:---: |:---: |
[vith](https://github.com/vith) |[jessica-coursera](https://github.com/jessica-coursera) |[theJoeBiz](https://github.com/theJoeBiz) |[jderrough](https://github.com/jderrough) |[jonathanly](https://github.com/jonathanly) |[jorgeepc](https://github.com/jorgeepc) |

[<img alt="julianocomg" src="https://avatars1.githubusercontent.com/u/7483557?v=4&s=117" width="117">](https://github.com/julianocomg) |[<img alt="dogrocker" src="https://avatars0.githubusercontent.com/u/8379027?v=4&s=117" width="117">](https://github.com/dogrocker) |[<img alt="firesharkstudios" src="https://avatars1.githubusercontent.com/u/17069637?v=4&s=117" width="117">](https://github.com/firesharkstudios) |[<img alt="kyleparisi" src="https://avatars0.githubusercontent.com/u/1286753?v=4&s=117" width="117">](https://github.com/kyleparisi) |[<img alt="larowlan" src="https://avatars2.githubusercontent.com/u/555254?v=4&s=117" width="117">](https://github.com/larowlan) |[<img alt="dviry" src="https://avatars3.githubusercontent.com/u/1230260?v=4&s=117" width="117">](https://github.com/dviry) |
:---: |:---: |:---: |:---: |:---: |:---: |
[julianocomg](https://github.com/julianocomg) |[dogrocker](https://github.com/dogrocker) |[firesharkstudios](https://github.com/firesharkstudios) |[kyleparisi](https://github.com/kyleparisi) |[larowlan](https://github.com/larowlan) |[dviry](https://github.com/dviry) |

[<img alt="galli-leo" src="https://avatars3.githubusercontent.com/u/5339762?v=4&s=117" width="117">](https://github.com/galli-leo) |[<img alt="leods92" src="https://avatars0.githubusercontent.com/u/879395?v=4&s=117" width="117">](https://github.com/leods92) |[<img alt="lucaperret" src="https://avatars1.githubusercontent.com/u/1887122?v=4&s=117" width="117">](https://github.com/lucaperret) |[<img alt="mperrando" src="https://avatars2.githubusercontent.com/u/525572?v=4&s=117" width="117">](https://github.com/mperrando) |[<img alt="marcusforsberg" src="https://avatars0.githubusercontent.com/u/1009069?v=4&s=117" width="117">](https://github.com/marcusforsberg) |[<img alt="mattfik" src="https://avatars2.githubusercontent.com/u/1638028?v=4&s=117" width="117">](https://github.com/mattfik) |
:---: |:---: |:---: |:---: |:---: |:---: |
[galli-leo](https://github.com/galli-leo) |[leods92](https://github.com/leods92) |[lucaperret](https://github.com/lucaperret) |[mperrando](https://github.com/mperrando) |[marcusforsberg](https://github.com/marcusforsberg) |[mattfik](https://github.com/mattfik) |

[<img alt="hrsh" src="https://avatars3.githubusercontent.com/u/1929359?v=4&s=117" width="117">](https://github.com/hrsh) |[<img alt="mkabatek" src="https://avatars0.githubusercontent.com/u/1764486?v=4&s=117" width="117">](https://github.com/mkabatek) |[<img alt="achmiral" src="https://avatars0.githubusercontent.com/u/10906059?v=4&s=117" width="117">](https://github.com/achmiral) |[<img alt="mnafees" src="https://avatars1.githubusercontent.com/u/1763885?v=4&s=117" width="117">](https://github.com/mnafees) |[<img alt="shahimclt" src="https://avatars3.githubusercontent.com/u/8318002?v=4&s=117" width="117">](https://github.com/shahimclt) |[<img alt="naveed-ahmad" src="https://avatars2.githubusercontent.com/u/701567?v=4&s=117" width="117">](https://github.com/naveed-ahmad) |
:---: |:---: |:---: |:---: |:---: |:---: |
[hrsh](https://github.com/hrsh) |[mkabatek](https://github.com/mkabatek) |[achmiral](https://github.com/achmiral) |[mnafees](https://github.com/mnafees) |[shahimclt](https://github.com/shahimclt) |[naveed-ahmad](https://github.com/naveed-ahmad) |

[<img alt="olemoign" src="https://avatars3.githubusercontent.com/u/11632871?v=4&s=117" width="117">](https://github.com/olemoign) |[<img alt="leftdevel" src="https://avatars3.githubusercontent.com/u/843337?v=4&s=117" width="117">](https://github.com/leftdevel) |[<img alt="cryptic022" src="https://avatars2.githubusercontent.com/u/18145703?v=4&s=117" width="117">](https://github.com/cryptic022) |[<img alt="phillipalexander" src="https://avatars0.githubusercontent.com/u/1577682?v=4&s=117" width="117">](https://github.com/phillipalexander) |[<img alt="Pzoco" src="https://avatars0.githubusercontent.com/u/3101348?v=4&s=117" width="117">](https://github.com/Pzoco) |[<img alt="eman8519" src="https://avatars2.githubusercontent.com/u/2380804?v=4&s=117" width="117">](https://github.com/eman8519) |
:---: |:---: |:---: |:---: |:---: |:---: |
[olemoign](https://github.com/olemoign) |[leftdevel](https://github.com/leftdevel) |[cryptic022](https://github.com/cryptic022) |[phillipalexander](https://github.com/phillipalexander) |[Pzoco](https://github.com/Pzoco) |[eman8519](https://github.com/eman8519) |

[<img alt="luarmr" src="https://avatars3.githubusercontent.com/u/817416?v=4&s=117" width="117">](https://github.com/luarmr) |[<img alt="phobos101" src="https://avatars2.githubusercontent.com/u/7114944?v=4&s=117" width="117">](https://github.com/phobos101) |[<img alt="scherroman" src="https://avatars3.githubusercontent.com/u/7923938?v=4&s=117" width="117">](https://github.com/scherroman) |[<img alt="fortunto2" src="https://avatars1.githubusercontent.com/u/1236751?v=4&s=117" width="117">](https://github.com/fortunto2) |[<img alt="samuelcolburn" src="https://avatars2.githubusercontent.com/u/9741902?v=4&s=117" width="117">](https://github.com/samuelcolburn) |[<img alt="sergei-zelinsky" src="https://avatars2.githubusercontent.com/u/19428086?v=4&s=117" width="117">](https://github.com/sergei-zelinsky) |
:---: |:---: |:---: |:---: |:---: |:---: |
[luarmr](https://github.com/luarmr) |[phobos101](https://github.com/phobos101) |[scherroman](https://github.com/scherroman) |[fortunto2](https://github.com/fortunto2) |[samuelcolburn](https://github.com/samuelcolburn) |[sergei-zelinsky](https://github.com/sergei-zelinsky) |

[<img alt="SpazzMarticus" src="https://avatars0.githubusercontent.com/u/5716457?v=4&s=117" width="117">](https://github.com/SpazzMarticus) |[<img alt="waptik" src="https://avatars1.githubusercontent.com/u/1687551?v=4&s=117" width="117">](https://github.com/waptik) |[<img alt="steverob" src="https://avatars2.githubusercontent.com/u/1220480?v=4&s=117" width="117">](https://github.com/steverob) |[<img alt="tajchumber" src="https://avatars3.githubusercontent.com/u/16062635?v=4&s=117" width="117">](https://github.com/tajchumber) |[<img alt="Tashows" src="https://avatars2.githubusercontent.com/u/16656928?v=4&s=117" width="117">](https://github.com/Tashows) |[<img alt="twarlop" src="https://avatars3.githubusercontent.com/u/2856082?v=4&s=117" width="117">](https://github.com/twarlop) |
:---: |:---: |:---: |:---: |:---: |:---: |
[SpazzMarticus](https://github.com/SpazzMarticus) |[waptik](https://github.com/waptik) |[steverob](https://github.com/steverob) |[tajchumber](https://github.com/tajchumber) |[Tashows](https://github.com/Tashows) |[twarlop](https://github.com/twarlop) |

[<img alt="tomsaleeba" src="https://avatars0.githubusercontent.com/u/1773838?v=4&s=117" width="117">](https://github.com/tomsaleeba) |[<img alt="tvaliasek" src="https://avatars2.githubusercontent.com/u/8644946?v=4&s=117" width="117">](https://github.com/tvaliasek) |[<img alt="vially" src="https://avatars1.githubusercontent.com/u/433598?v=4&s=117" width="117">](https://github.com/vially) |[<img alt="nagyv" src="https://avatars2.githubusercontent.com/u/126671?v=4&s=117" width="117">](https://github.com/nagyv) |[<img alt="willycamargo" src="https://avatars1.githubusercontent.com/u/5041887?v=4&s=117" width="117">](https://github.com/willycamargo) |[<img alt="xhocquet" src="https://avatars2.githubusercontent.com/u/8116516?v=4&s=117" width="117">](https://github.com/xhocquet) |
:---: |:---: |:---: |:---: |:---: |:---: |
[tomsaleeba](https://github.com/tomsaleeba) |[tvaliasek](https://github.com/tvaliasek) |[vially](https://github.com/vially) |[nagyv](https://github.com/nagyv) |[willycamargo](https://github.com/willycamargo) |[xhocquet](https://github.com/xhocquet) |

[<img alt="YehudaKremer" src="https://avatars3.githubusercontent.com/u/946652?v=4&s=117" width="117">](https://github.com/YehudaKremer) |[<img alt="agreene-coursera" src="https://avatars0.githubusercontent.com/u/30501355?v=4&s=117" width="117">](https://github.com/agreene-coursera) |[<img alt="alfatv" src="https://avatars2.githubusercontent.com/u/62238673?v=4&s=117" width="117">](https://github.com/alfatv) |[<img alt="arggh" src="https://avatars3.githubusercontent.com/u/17210302?v=4&s=117" width="117">](https://github.com/arggh) |[<img alt="avalla" src="https://avatars1.githubusercontent.com/u/986614?v=4&s=117" width="117">](https://github.com/avalla) |[<img alt="c0b41" src="https://avatars1.githubusercontent.com/u/2834954?v=4&s=117" width="117">](https://github.com/c0b41) |
:---: |:---: |:---: |:---: |:---: |:---: |
[YehudaKremer](https://github.com/YehudaKremer) |[agreene-coursera](https://github.com/agreene-coursera) |[alfatv](https://github.com/alfatv) |[arggh](https://github.com/arggh) |[avalla](https://github.com/avalla) |[c0b41](https://github.com/c0b41) |

[<img alt="canvasbh" src="https://avatars3.githubusercontent.com/u/44477734?v=4&s=117" width="117">](https://github.com/canvasbh) |[<img alt="craigcbrunner" src="https://avatars3.githubusercontent.com/u/2780521?v=4&s=117" width="117">](https://github.com/craigcbrunner) |[<img alt="darthf1" src="https://avatars2.githubusercontent.com/u/17253332?v=4&s=117" width="117">](https://github.com/darthf1) |[<img alt="dkisic" src="https://avatars2.githubusercontent.com/u/32257921?v=4&s=117" width="117">](https://github.com/dkisic) |[<img alt="franckl" src="https://avatars0.githubusercontent.com/u/3875803?v=4&s=117" width="117">](https://github.com/franckl) |[<img alt="green-mike" src="https://avatars1.githubusercontent.com/u/5584225?v=4&s=117" width="117">](https://github.com/green-mike) |
:---: |:---: |:---: |:---: |:---: |:---: |
[canvasbh](https://github.com/canvasbh) |[craigcbrunner](https://github.com/craigcbrunner) |[darthf1](https://github.com/darthf1) |[dkisic](https://github.com/dkisic) |[franckl](https://github.com/franckl) |[green-mike](https://github.com/green-mike) |

[<img alt="jarey" src="https://avatars1.githubusercontent.com/u/5025224?v=4&s=117" width="117">](https://github.com/jarey) |[<img alt="johnmanjiro13" src="https://avatars1.githubusercontent.com/u/28798279?v=4&s=117" width="117">](https://github.com/johnmanjiro13) |[<img alt="magumbo" src="https://avatars3.githubusercontent.com/u/6683765?v=4&s=117" width="117">](https://github.com/magumbo) |[<img alt="ninesalt" src="https://avatars2.githubusercontent.com/u/7952255?v=4&s=117" width="117">](https://github.com/ninesalt) |[<img alt="luntta" src="https://avatars0.githubusercontent.com/u/14221637?v=4&s=117" width="117">](https://github.com/luntta) |[<img alt="rhymes" src="https://avatars3.githubusercontent.com/u/146201?v=4&s=117" width="117">](https://github.com/rhymes) |
:---: |:---: |:---: |:---: |:---: |:---: |
[jarey](https://github.com/jarey) |[johnmanjiro13](https://github.com/johnmanjiro13) |[magumbo](https://github.com/magumbo) |[ninesalt](https://github.com/ninesalt) |[luntta](https://github.com/luntta) |[rhymes](https://github.com/rhymes) |

[<img alt="rlebosse" src="https://avatars0.githubusercontent.com/u/2794137?v=4&s=117" width="117">](https://github.com/rlebosse) |[<img alt="rtaieb" src="https://avatars2.githubusercontent.com/u/35224301?v=4&s=117" width="117">](https://github.com/rtaieb) |[<img alt="thanhthot" src="https://avatars0.githubusercontent.com/u/50633205?v=4&s=117" width="117">](https://github.com/thanhthot) |[<img alt="tinny77" src="https://avatars2.githubusercontent.com/u/1872936?v=4&s=117" width="117">](https://github.com/tinny77) |[<img alt="yoann-hellopret" src="https://avatars3.githubusercontent.com/u/46525558?v=4&s=117" width="117">](https://github.com/yoann-hellopret) |[<img alt="olitomas" src="https://avatars0.githubusercontent.com/u/6918659?v=4&s=117" width="117">](https://github.com/olitomas) |
:---: |:---: |:---: |:---: |:---: |:---: |
[rlebosse](https://github.com/rlebosse) |[rtaieb](https://github.com/rtaieb) |[thanhthot](https://github.com/thanhthot) |[tinny77](https://github.com/tinny77) |[yoann-hellopret](https://github.com/yoann-hellopret) |[olitomas](https://github.com/olitomas) |

[<img alt="akizor" src="https://avatars1.githubusercontent.com/u/1052439?v=4&s=117" width="117">](https://github.com/akizor) |
:---: |
[akizor](https://github.com/akizor) |


<!--/contributors-->

## Software

We use Browserstack for manual testing
<a href="https://www.browserstack.com" target="_blank">
  <img align="left" width="117" alt="BrowserStack logo" src="https://i.ibb.co/HDRDHmx/Browserstack-logo-2x.png">
</a>

## License

[The MIT License](LICENSE).
