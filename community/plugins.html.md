Here is a listing of all the plugins available for DocPad. If you have created a plugin, be sure to [include it in this listing!](https://github.com/bevry/docpad-documentation/edit/master/community/plugins.html.md) :)


## Installing

To install a plugin, run `docpad install #{thePluginName}` inside your project directory. As an example, to install the [eco](/plugin/eco/) plugin, you would run `docpad install eco`

To uninstall a plugin, run `docpad uninstall #{thePluginName}` inside your project directory.

In older versions of DocPad, you would run `npm install --save docpad-plugin-#{thePluginName}` to install, and `npm uninstall --save docpad-plugin-#{thePluginName}` to uninstall.


## Renderers

These are plugins that add support for extra markups and languages to DocPad:

- [coffeescript](/plugin/coffeescript/) - Supports [CoffeeScript](http://jashkenas.github.com/coffee-script/) to JavaScript `.js.coffee`
- [coffeekup](/plugin/coffeekup/) - Supports [CoffeeKup](http://coffeekup.org/) to anything `.anything.coffee`
- [cson](/plugin/cson/) - Supports [CSON](https://github.com/bevry/cson) to JSON `.json.cson`
- [eco](/plugin/eco/) - Supports [Eco](https://github.com/sstephenson/eco) to anything `.anything.eco`
- [haml](/plugin/haml/) - Supports [HAML](http://haml-lang.com/) to anything `.anything.haml`
- [hamlcoffee](https://github.com/ashnur/docpad-plugin-hamlcoffee/) - Supports [HAML Coffee](https://github.com/netzpirat/haml-coffee/) to HTML `.html.hamlc`
- [handlebars](/plugin/handlebars/) - Supports [Handlebars/Moustache](http://handlebarsjs.com/) to anything `.anything.(hb|hbs|handlebars)`
- [hogan](/plugin/hogan/) - Supports [Hogan/Mustache](http://twitter.github.com/hogan.js/) to anything `.anything.hogan`
- [html2coffee](/plugin/html2coffee/) - Supports HTML to CoffeeKup `.coffee.html`
- [html2jade](/plugin/html2jade) - Supports HTML to [Jade](http://jade-lang.com/) `.jade.html`
- [jade](/plugin/jade/) - Supports [Jade](http://jade-lang.com/) to anything `.anything.jade`
- [js2coffee](/plugin/js2coffee/) - Supports JavaScript to CoffeeScript `.coffee.js`
- [less](/plugin/less/) - Supports [LessCSS](http://lesscss.org/) to CSS `.css.less`
- [livescript](/plugin/livescript/) - Supports [LiveScript](http://livescript.net/) to JavaScript `.js.ls`
- [marked](/plugin/marked/) - Supports [Markdown](http://daringfireball.net/projects/markdown/basics) to HTML `.html.(md|markdown)` via [marked](https://github.com/chjj/marked)
- [move](/plugin/move) - Supports [Move](http://movelang.org/) to JavaScript `.js.move`
- [multimarkdown](https://github.com/takitapart/docpad-plugin-multimarkdown) - Supports [MultiMarkdown](http://fletcherpenney.net/multimarkdown/) to HTML `.html.(md|markdown)` via [node-multimarkdown](https://github.com/dtjm/node-multimarkdown)
- [php](/plugin/php) - Supports [PHP](http://php.net/) to anything `.anything.(php|phtml)`
- [robotskirt](/plugin/robotskirt/) - Supports [Markdown](http://daringfireball.net/projects/markdown/basics) to HTML `.html.(md|markdown)` via [robotskirt](https://github.com/benmills/robotskirt)
- [roole](https://github.com/georgeosddev/docpad-plugin-roole) - Supports [Roole](http://roole.org/) to CSS `.css.roo`
- [ruby](/plugin/ruby) - Supports [Ruby](http://www.ruby-lang.org/) and [ERuby](http://en.wikipedia.org/wiki/ERuby) to anything `.anything.(ruby|erb)`
- [sass](/plugin/sass/) - Supports [SCSS and SASS](http://sass-lang.com/) to CSS (includes [compass](http://compass-style.org/) support) `.css.(sass|scss)`
- [styl](/plugin/styl/) - Supports [Styl](https://github.com/visionmedia/styl) to CSS `.css.styl`
- [stylus](/plugin/stylus/) - Supports [Stylus](http://learnboost.github.com/stylus/) to CSS `.css.(styl|stylus)`
- [nodesass](https://github.com/jking90/docpad-plugin-nodesass) - Supports [SCSS](http://sass-lang.com/) to CSS (using [node-sass](https://github.com/andrew/node-sass)) `.css.scss`
- [teacup](https://github.com/hurrymaplelad/docpad-plugin-teacup/) - Supports [Teacup](http://goodeggs.github.io/teacup/) to HTML `.html.coffee`
- [textile](https://github.com/Greduan/docpad-plugin-textile) - Supports [Textile](http://textile.sitemonks.com/) to HTML `.html.textile`
- [typescript](https://github.com/bpampuch/docpad-plugin-tsc) - Supports [TypeScript](http://www.typescriptlang.org/) to JavaScript `.js.ts`
- [yaml](https://github.com/jeremyfa/docpad-plugin-yamljs) - Supports [YAML](http://en.wikipedia.org/wiki/YAML) to JSON `.json.(yaml|yml)` and JSON to YAML `.(yml|yaml).json`


## Helpers

These are plugins that add extra functionality to DocPad:

- [addthis](https://github.com/mikeumus/docpad-plugin-addthis) - Adds the [AddThis](http://www.addthis.com/) toolbar into your project
- [assets](https://github.com/mcdee/docpad-plugin-assets) - Change URL of asset files to contain hash of contents, allowing for effective caching whilst enabling cache busting when contents change
- [associatedfiles](/plugin/associatedfiles) - Lets you easily associate files to a particular document, and then grab the collection for them
- [basicauth](https://github.com/mikeumus/docpad-plugin-basicauth) - Adds basic authentication to your project
- [buildr](/plugin/buildr/) - Supports bundling scripts and styles (including pre-processors like coffeescript, less, etc) using [Buildr](https://github.com/balupton/buildr.npm)
- [datefromfilename](https://github.com/grassator/docpad-plugin-datefromfilename) - Automaticaly set the date meta-data property by determining it from the document's filename
- [dateurls](https://npmjs.org/package/docpad-plugin-dateurls) - Automatically add `/YEAR/MONTH/DAY/NAME` routes for your posts
- [cachr](/plugin/cachr/) - Allows you to cache remote urls locally from within your templates
- [cleanurls](/plugin/cleanurls/) - Adds support for urls like `/blog/hello` as well as the original url `/blog/hello.html`
- [coffeelint](https://github.com/jking90/docpad-plugin-coffeelint) - Prints [coffeelint](http://www.coffeelint.org/) errors to the console
- [csv](https://github.com/CycoPH/docpad-plugin-csv/) - Adds support for CSV data mapping. The comma seperated data files work just like a database, map from column 1 to column 2
- [dateurls](https://github.com/mgroves84/docpad-plugin-dateurls/) - Adds support for date based urls like `/2013/04/27/hello.html`
- [facebookcomments](https://github.com/mikeumus/docpad-plugin-facebookcomments) - Adds the [Facebook Comment Widget](https://developers.facebook.com/docs/reference/plugins/comments/) to your project
- [feedr](/plugin/feedr/) - Allows you to render remote feeds within your templates
- [frontend](https://npmjs.org/package/docpad-plugin-frontend) - CSS and JavaScript asset manager and compiler for DocPad
- [gist](/plugin/gist/)  - Pulls in gists into your document
- [highlightjs](/plugin/highlightjs/) - Adds [Highlight.js](https://github.com/isagalaev/highlight.js) syntax highlighting to code snippets
- [jshint](https://github.com/jking90/docpad-plugin-jshint) - Prints [JSHint](http://www.jshint.com/) errors to the console
- [jsexc](https://github.com/JeffreyZhao/docpad-plugin-jscexc) - Adds the ability to apply AOT compilation to JavaScript files
- [livereload](/plugin/livereload) - Automatically reloads the page whenever a regeneration is performed
- [lunr](https://github.com/brockfanning/docpad-plugin-lunr) - Client-side full-text and faceted search using [Lunr.js](http://lunrjs.com)
- [menu](https://github.com/sergeche/docpad-plugin-menu) - Automatically generates menu from documents folder
- [nativecomments](/plugin/nativecomments/) - Adds support for native comments to DocPad
- [paged](/plugin/paged/) - Adds multiple page support to documents allowing you to render one document out to many pages
- [partials](/plugin/partials/) - Adds the ability to create re-usable partials for your templates within DocPad
- [pygments](/plugin/pygments/) - Adds [Pygments](http://pygments.org/) syntax highlighting to code snippets
- [related](/plugin/related/) - Scans your documents `tags: 'tag1', 'tag2'` metadata to produce a listing of related documents
- [rss](https://github.com/hurrymaplelad/docpad-plugin-rss) - Generates an RSS feed for a configurable collection
- [services](/plugin/services/) - Adds support for many 3rd party services to DocPad
- [sitemap](https://github.com/benjamind/docpad-plugin-sitemap) - Generates a `sitemap.xml` file for your site from the `html` documents collection
- [text](/plugin/text/) - Render templateData properties without needing template engine, useful for abstraction in configuration files
- [tableofcontents](https://github.com/takitapart/docpad-plugin-tableofcontents) - Automatically generate table of contents
- [thumbnails](https://github.com/rantecki/docpad-plugin-thumbnails) - Manages thumbnail generation of your image files
- [umd](/plugin/umd/) - Wrap specified JavaScript documents in the Universal Module Definition (UMD) allowing them to run in AMD, Require.js, CommonJS/Node.js and Vanilla environments automatically
- [jsonfragment](https://github.com/field/docpad-plugin-jsonfragment) - Writes each documents content without layout and its meta data into a separate .json file for quick loading via AJAX.
- [navlinks](https://github.com/lucor/docpad-plugin-navlinks) - Adds the ability to generate a navigation bar for documents with links to the next and previous document of a specified collection.


## Deployers

These are plugins that make [deploying](/docpad/deploy) to particular services even easier:

- [ghpages](/plugin/ghpages) - Deploy to [GitHub Pages](http://pages.github.com/) as easy as `docpad deploy-ghpages`
- [sunny](https://github.com/bobobo1618/docpad-plugin-sunny) - Uploads site to cloud (AWS, Google Storage) after generation



## Admin Interfaces

[DocPad's plan from the very beginning has been to be interface agnostic.](https://github.com/bevry/docpad/issues/123) This means that we will be able to utilise existing interfaces, customer interfaces, and decoupled interfaces. Allowing us to always utilise the best experiences for everyone involved.


### Existing Interfaces
<a id="importers"></a>

DocPad's plugin/extension infrastructure supports existing coupled interfaces by importing their data directly into the DocPad Database. So if you love using Tumblr, WordPress, Medium, MongoDB or GitHub Repos for your content, you don't have to give them up. Just install the importer plugin for them, and DocPad will import the data from that service into the DocPad database for rendering.

- [downloader](/plugin/downloader/) - Download (and optionally extract) files into your project, used in the [Twitter Bootstrap Skeleton](https://github.com/docpad/twitter-bootstrap.docpad) to pull in [Twitter Boostrap](http://twitter.github.io/bootstrap/)
- [repocloner](/plugin/repocloner/) - Clone repos into your project, awesome for [creating wikis](https://gist.github.com/balupton/5519403)
- [tumblr](/plugin/tumblr/) - Imports Tumblr data directly into your DocPad Database, used in the [Syte Skeleton](https://github.com/docpad/syte.docpad) to pull in Tumblr data


### Custom Interfaces

DocPad's plugin/extension infrastructure supports custom Admin Interfaces tightly coupled to the DocPad experience. So far we have the following extensions that add Admin Interfaces to DocPad:

- [DocPad Collections Editor](https://github.com/cauld/docpad-collections-editor) - A simple WYSIWYG editor for DocPad Collections
- [MiniCMS](https://npmjs.org/package/docpad-plugin-minicms) - Adds an admin interface to DocPad


### Decoupled Interfaces

DocPad's plugin/extension infrastructure supports existing decoupled interfaces by providing plugin/extension adapters to the interface allowing the interface to interact directly with the DocPad Database, or theoritically any backend providing an interface was made for it. So far we have the following extensions that add Decoupled Interfaces to DocPad:

- [Use Prose with DocPad to create a Wiki](https://gist.github.com/balupton/5519403) - Tutorial on how to use [Prose.io](http://prose.io/about.html) as an Admin Interface for DocPad
- [WebWrite's InlineGUI](/plugin/inlinegui) (not yet ready) - Edit your content from any backend with this inline editing interface



## Guides

These are miscellaneous things that you can do with DocPad:

- [Localising and formatting dates](https://gist.github.com/4166882)
- [Automatically set custom meta data for collections](https://gist.github.com/4166806)
- [Absolute URL Helper](https://gist.github.com/3939146)
- [Benchmarking DocPad](https://gist.github.com/3906050)
- [Sitemap Generation](https://gist.github.com/3898935)
- [Concatenate your scripts with Browserify](https://gist.github.com/4398093)
- [Minify your assets with Grunt](https://gist.github.com/3898915)
- [Minify your assets automatically post-deployment with Cloudflare](http://blog.cloudflare.com/an-all-new-and-improved-autominify)
- [Custom Routing](https://gist.github.com/3695936)
- [Paging Solutions](https://gist.github.com/3695876)
- [Responsive Layouts in Stylus](https://gist.github.com/1549029)
- [Thoughts on a DocPad GUI](https://gist.github.com/2906284)
- [Getting Ruby, SASS and DocPad working on Heroku](https://gist.github.com/4342818)
- [Respond with JSON when asked to](https://github.com/lzrski/docpad-plugin-json)
- [Require authentication to view certain documents](http://stackoverflow.com/q/14327676/130638)
- [Use DocPad and GitHub as a Wiki](https://gist.github.com/balupton/5519403)



## Complete Plugin Listing

You can find a [complete listing of all DocPad Plugins on the NPM Registry using the `docpad-plugin` keyword.](https://npmjs.org/browse/keyword/docpad-plugin) Though note, this listing is not curated by the DocPad Team, so be careful.



## Create Your Own!

It's easy to write plugin for DocPad. [Get started now on our Write a Plugin Page!](/docpad/plugin-write)



## Requested

[Here is a list of plugins waiting to be coded up :-)](/issues?labels=plugin&sort=created&direction=desc&state=open&page=1)
