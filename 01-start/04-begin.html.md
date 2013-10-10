```
title: "Beginner Guide"
cssClasses: ['compact']
```

## Introduction

Welcome to the Beginner Guide for DocPad. By the end, you'll have all the knowledge necessary to create amazing powerful websites and applications with DocPad. You won't need any special training, and if you are a web developer then you'll already feel right at home.

For this guide we'll create a [blog](http://en.wikipedia.org/wiki/Blog) and explain step-by-step how it's done. A blog is just a listing of posts/articles as well as some pages. Posts are intended to allow regular new content, like status updates, to be published, whereas Pages are more permanent, usually providing general background information.

Great, let's get started! Oh, and if you ever get stuck, you have a question or need help, then jump onto any of our [official support channels](/support) and we'll be right with you. Cheers!

<iframe width="420" height="315" src="//www.youtube.com/embed/5wFYW6v0Y34" frameborder="0" allowfullscreen></iframe>


## Creating the Standard Project Structure

Before we get hacking away on content, we have to create our project and set it up with [DocPad's standard structure](/docpad/overview). To do this, we'll run the following:

``` bash
mkdir my-new-website
cd my-new-website
docpad run
```

When prompted for a skeleton, select `No Skeleton`, which will set up our standard directory structure automatically. The `docpad run` command will also keep running once the action has completed successfully. This is because it also watches for changes and will regenerate our website when they occur. It'll also start a web server on [http://localhost:9778](http://localhost:9778) so that we can view our website as we go.

For now, we'll keep `docpad run` running but, whenever you want to stop it, just hit `CTRL+C` on your keyboard to exit it.


## Adding the Home Page

Let's create our first document; the _Homepage_ for our website. Create the document `src/documents/index.html` and give it the following content:

``` erb
<html>
<head>
	<title>Welcome! | My Website</title>
</head>
<body>
	<h1>Welcome!</h1>
	<p>Welcome to My Website!</p>
</body>
</html>
```

Once you've saved it, open up [http://localhost:9778](http://localhost:9778) (or refresh if you already had it open) and you'll notice that DocPad has already regenerated your website and see the page we created rendered inside the browser. Fantastic!











## Adding the About Page and a Layout

Now that's done, we'll want to add our "About Me" page so that people browsing our website will know who we are. To do this, let's create a new document at `src/documents/about.html` and give it the content:

``` erb
<html>
<head>
	<title>About Me | My Website</title>
</head>
<body>
	<h1>About Me</h1>
	<p>I like long walks on the beach. <strong>Plus I rock at DocPad!</strong></p>
</body>
</html>
```

Now if we go to [http://localhost:9778/about.html](http://localhost:9778/about.html), we'll be able to see that page in our browser. Awesome!

However, duplicating that layout information inside our _Homepage_ and our _About_ page is pretty redundant. For instance, if we wanted to change the contents of `<head>` to something else, then we'll have to change it in two places! This is where layouts come in.

Layouts wrap around our documents, so we can define the surrounding areas of a document only once. Let's move the wrapper stuff of our two documents into a new layout located at `src/layouts/default.html.eco`, so that we end up with the following:

- `src/layouts/default.html.eco`

	``` erb
	<html>
	<head>
		<title><%= @document.title %> | My Website</title>
	</head>
	<body>
		<h1><%= @document.title %></h1>
		<%- @content %>
	</body>
	</html>
	```

- `src/documents/index.html`

	``` erb
	---
	title: "Welcome!"
	layout: "default"
	isPage: true
	---

	<p>Welcome to My Website!</p>
	```

- `src/documents/about.html`

	``` erb
	---
	title: "About Me"
	layout: "default"
	isPage: true
	---

	<p>I like long walks on the beach. <strong>Plus I rock at DocPad!</strong></p>
	```

However, if you go to either the _Homepage_ or the _About_ page on our web server, you'll notice that their content is just the layout, and don't actually contain any of the document content. This is because we haven't installed the templating engine for our layout yet.

We've also added a new `isPage` attribute, this is our own custom attribute and has no special meaning in DocPad. However, we will give it special meaning later on when we add our menu listings :)


### Installing the Templating Engine

_Templating Engines_ allow us to embed abstractions inside our documents - which is why we have to use them for layouts, as a layout is an abstraction, an abstraction that wraps around a document and outputs the document's content in a specific way :)

For this guide, the templating engine we'll be using is [eco](https://github.com/sstephenson/eco) and is available to us via the [eco plugin](/plugin/eco). So let's install that now by quitting DocPad (`CTRL+C`), and running:

``` bash
docpad install eco
```

Once installed, if we run DocPad again (`docpad run`) and then go our _Homepage_ or _About_ page, we'll see that the content actually contains the document content. In other words, it has rendered correctly through our eco templating engine. Woot woot!

Now, why did we use `<%=` for the document's title, but `<%-` for the document's content? The reason for this is that `<%=` will escape the data we give it before outputting the data, which allows special characters to be interpretted as normal characters. On the other hand, `<%-` will output without performing any escaping, leaving special characters intact. So, why should we escape some things but not others? Generally, whenever the data we want to output is HTML (e.g. the document's content) we want to output it "as is", without any escaping. On the other hand, if we didn't escape document titles, titles such as `3 is > 2` would end up as `<title>3 is > 2</title>`, which is invalid HTML due to the superfluous closing element character, `>`. Thus, using escaping would result in `<title>3 is &gt; 2</title>`, which uses the [HTML entity code](http://www.ascii.cl/htmlcodes.htm) to represent the special character. This is valid HTML and looks exactly the same to the user :)


### A note on Plugins

Even though we have chosen to use the eco templating engine in this guide, there are plenty of others we could use too! We find eco is the very friendly for beginners, as it is the most like HTML. However, after experimenting with some of the others, you may find you'd like to use them instead. Adding support for a new templating engine, pre-processor or whatever is as simple as installing the plugin for it.

DocPad also supports more than just templating engines, though. We have a whole range of different plugins to do all sorts of things, so be sure to check them out!

You can find the full listing of plugins we have on the [Plugins](/docpad/plugins) page.


### A note on Rendering

Now, the reason we can support multiple templating engines is because of the way DocPad renders things, file extension by extension. Thus, by creating the file `default.html.eco`, we can render from `eco` to `html`. Conversely, if we tried `default.eco.html`, we'd be trying to render from `html` to `eco`, which wouldn't actually be very useful or even possible. However, other combinations can be rendered in both directions, such as CoffeeScript to JavaScript and JavaScript to CoffeeScript, provided you have the right plugins installed. You can also mix and match extensions, such as `default.html.md.eco`, which renders from `eco` to `md` (markdown) and then `md` to `html`. This allows you to apply abstractions with eco to your markdown documents. Awesome! For now, though, it's way out of our scope, so let's get back on track!


### A note on Meta Data

What on earth was with the stuff between the `---` at the top of our documents? That stuff is our _meta data_. It is where we can define extra information about our document, such as its title, layout, date, whatever. You are not limited to what you can define here; it's up to you. However, there are some pre-defined properties that serve special purposes (such as layout, which we just used).

You can learn more about meta data and all the special properties on our [Meta Data](/docpad/meta-data) page.


## Adding the Live Reload Plugin and Blocks

### Adding the Live Reload Plugin

Sweet, so we're doing well so far! We've got two documents, and a layout to abstract them. As we are making changes, it sure would be nice if our browser refreshed the page automatically! We can do this with the [Live Reload Plugin](/plugin/livereload), so let's install that now:

``` bash
docpad install livereload
```

Once you've restarted DocPad, whenever you make a change to the files, you'll notice the browser still doesn't refresh automatically to show the changes! Why? The reason is that we have to add our _Blocks_.

### Adding the Blocks

_Blocks_ are a way for plugins and even ourselves to be able to easily add scripts, styles and meta elements to our pages. In the instance of the Live Reload Plugin, it needs the _Script Block_ to be able to inject the needed scripts into the page that refresh the browser.

So to add the three default blocks to our layout, we'll update our `default.html.eco` layout to become:

- `src/layouts/default.html.eco`

``` erb
<html>
<head>
	<title><%= @document.title %> | My Website</title>
	<%- @getBlock("meta").toHTML() %>
	<%- @getBlock("styles").toHTML() %>
</head>
<body>
	<h1><%= @document.title %></h1>
	<%- @content %>
	<%- @getBlock("scripts").toHTML() %>
</body>
</html>
```

Saving that, and manually reloading our browser, we'll notice that our page now has the necessary scripts for the Live Reloaded Plugin automatically injected right where the scripts block has been output. Now if we make a change to any of the files, we'll notice the browser will automatically refresh. Amazing!

In the next part, we'll work with blocks some more by adding our assets to them.












## Adding Assets

It's time to start adding some assets. Before proceeding with this section, please read the [DocPad Overview Page](/docpad/overview) so you know what each of the directories inside our website structure are for.


### Images

Let's add our logo to our layout's header. We'll download the [DocPad logo](http://d.pr/i/cfmt+) and place it in our `files` directory at `src/files/images/logo.gif` (binary files should _always_ go in the `files` directory). Then, we'll add it to the body of our layout, to show our logo on each page:

- `src/layouts/default.html.eco`

``` html
<body>
  <img src="/images/logo.gif" />
  <h1><%= @document.title %></h1>
  <%- @content %>
  <%- @getBlock("scripts").toHTML() %>
</body>
```

If you are downloading the file directory into the specified location, you may have to restart DocPad. We're working on this.


### Stylesheets

Now let's make all of our `h1` headers red, by adding a stylesheet file in our documents directory at `src/documents/styles/style.css` that contains:

``` css
h1 {
	color: red;
}
```

Then, to include it in our pages, we'll update the _styles Block_ in our `default.html.eco` layout to:

``` erb
<%- @getBlock("styles").add(["/styles/style.css"]).toHTML() %>
```

Upon saving, we'll notice that our browser will automatically reload, and that our css file will be injected into the layout making our header red!



### Scripts

Now let's add a nifty loading effect using JavaScript and the [jQuery JavaScript Library](http://jquery.com). As always, there's plenty of other JavaScript Libraries you can use, but in this guide we'll go with jQuery.

 To do this, we'll first download the [jQuery library](http://code.jquery.com/jquery.js) file and put it in our `files` directory at `src/files/vendor/jquery.js`.

 The reason we use the `files` directory for vendor files is that it is extremely unlikely we'll ever want to render any vendor files, so having them there is a good choice for consistency and speed. Whereas, we will probably eventually want to render our own scripts and styles with something, so generally we'll just put them in the documents directory to make the transition to rendering engines easier.

 Now that we have included jQuery in our project, we'll add our nifty loading effect by adding a script file at `src/documents/scripts/script.js` that contains:

``` javascript
(function(){
	$("body").hide().fadeIn(1000);
})();
```

Now that's done, let's add those files to our _scripts Block_ in our `default.html.eco` layout:

``` erb
<%- @getBlock("scripts").add(["/vendor/jquery.js","/scripts/script.js"]).toHTML() %>
```

Upon saving, we'll notice that our content will fade in over a duration of two seconds. Nifty!

Now, some of you may wonder why we omitted the [jQuery onDomReady](http://api.jquery.com/ready/) handler in our script file. While off-topic for DocPad, the reasoning for this is that only code that requires the entire DOM to be loaded needs it. For instance, if your script requires a DOM element that is positioned after our script tag, then it would be useful. In this instance, as we inject our scripts into our body element, we already have access to the body element, and therefore can start our `fadeIn` animation immediately. This avoids the page loading, then, the DOM loading after a delay, followed by our fade-in with an undesirable "popping" effect.











## Getting the benefits of Pre-Processors
_Pre-Processors_ are amazing things. They allow us to write documents in one language (the source language), and export them to a different language (the target language). This is extremely beneficial, as it allows you to use the syntax that you enjoy, instead of the syntax that you are sometimes forced to work with. Most importantly, however, pre-processors often offer more robust and clean functionality than the target language supports out of the box, allowing you to make use of modern developers while still working with old languages.


### Using Markdown, an HTML Pre-Processor
HTML's verbose syntax is terrible for writing content that is more text than markup (e.g. articles, comments, etc). Fortunately, [Markdown](http://daringfireball.net/projects/markdown/) (one of the many HTML Pre-Processors available to us as [Plugins](/docpad/plugins)) comes to the rescue!

Install the [Marked Markdown Plugin](/plugin/marked) by running `docpad install marked`.

Then, rename the _About_ page we created earlier from (`documents/about.html`) to (`documents/about.html.md`), to indicate that we want to render from Markdown to HTML, and open it. Writing in Markdown, update its content (leave the existing meta data section as it is) to become:

``` markdown
I like long walks on the beach. **Plus I rock at DocPad!**
```

Which gives us the same result, but with all the benefits of Markdown!

This simple procedure can be followed irrespective of your desired HTML pre-processor.

Sweet, you're now ready to party, Markdown-style! ;)


### Using Stylus, a CSS Pre-Processor
Open the Stylesheet document we created earlier (`documents/styles/style.css`). CSS really hasn't come that far over the years and, thus, it has absolutely no abstractions available to us, making it incredibly verbose and painful to write. Fortunately, [Stylus](http://learnboost.github.com/stylus/) (one of the many [CSS Pre-Processors](/docpad/plugins) available to us) is our saviour!

Install the [Stylus Plugin](/plugin/stylus) by running `docpad install stylus`.

Then, rename `src/files/styles/style.css` to `src/files/styles/style.css.styl`, to indicate we want to render from Stylus to CSS, and open it. 

Using Stylus syntax, update the stylesheet's content to become:

``` stylus
h1
	color: red
```

Which gives us the same result as before, but with all the benefits of Stylus.

This simple procedure can be followed irrespective of your desired CSS pre-processor.

Sweet, you're now ready to rock the house with Stylus!


### Using CoffeeScript, a JavaScript Pre-Processor
Sometimes people can get quite irritated with JavaScript's verbosity, and very annoyed at its nit-picking, such as when they forget a single comma somewhere and their entire app breaks. Fortunately, [CoffeeScript](http://coffeescript.org/) (one of the many [JavaScript Pre-Processors](/docpad/plugins) available to us) restores our sanity!

Install the [CoffeeScript Plugin](/plugin/coffeescript) by running `docpad install coffeescript`.

Then rename `documents/scripts/script.js` to `documents/scripts/script.js.coffee`, to indicate we want to render from CoffeeScript to JavaScript, and open it.

Using CoffeeScript, we can update our file's content to become:

``` coffeescript
$("body").hide().fadeIn(1000)
```

Which gives us the same result, but with all the benefits of CoffeeScript.

This simple procedure can be followed irrespective of your desired JavaScript pre-processor.

Sweet, you're now ready to relax, with a rich cup of CoffeeScript.











## Adding some Template Data and Template Helpers via a Configuration File

### Purpose of a Configuration File

The [DocPad Configuration File](/docpad/config) allows us to configure our DocPad instance, listen to events and perform some nifty abstractions.

Consider the case where our document title is empty. With our current solution, the title of the page would be ` | My Website`. A page title of `My Website` would look far better when our document doesn't have a title.

To handle this, we update our title code in our `default.html.eco` layout template to become:

``` erb
<title><%= if @document.title then "#{@document.title} | My Website" else "My Website" %></title>
```

Which would achieve the immediate goal, but then would mean that we would have to update the website title in two places if we want to use anything other than `My Website`. Considering this a common requirement, it would be nice if we could abstract it out, say, into a configuration file!

DocPad should have created an application-wide configuration file for us at `/docpad.coffee` (in the project root) when we initialized the project. If not, let's create it, with the following contents:

``` coffee
# Define the Configuration
docpadConfig = {
	# ...
}

# Export the Configuration
module.exports = docpadConfig
```

Notice that the `docpadConfig` object is written in CoffeeScript's version of a JSON object.

You'll have to restart DocPad so that DocPad can become aware of the configuration file. From then on, DocPad will automatically reload your configuration when changes occur.

The first part of this configuration is where we actually define our configuration (where the `# ...` is located), and the second part is a [node convention](http://nodejs.org/docs/latest/api/modules.html#modules_module_exports) for exporting data from one file to another. Whenever we add some configuration, you'll want to add it to the `docpadConfig` object we just defined.

For more information on configuration files and what configuration is available to your, refer to our [Configuration Page](/docpad/config).


### Using TemplateData for Abstractions

Everything that is available to our templates is called [TemplateData](/docpad/template-data). For instance, `@document` is part of our template data. To be able to abstract out something that our templates will use, we will need to extend our template data. We can do this by modifying our template data configuration property in `/docpad.coffee` like so:

``` coffee
docpadConfig = {
	templateData:
		site:
			title: "My Website"
}
```

With that, our website title is now abstracted and we can update our title element in the `default.html.eco` template:

``` erb
<title><%= if @document.title then "#{@document.title} | #{@site.title}" else @site.title %></title>
```

However, if we really wanted to (and we probably do) we can abstract out that logic into a function inside our template data.


### Abstracting Logic into Template Helpers

When using `.coffee` or `.js` files to define our Configuration File, we are allowed to define functions. Doing so allows us to use functions within our template data, which we call _Template Helpers_.

When calling a template helper, the scope of the template helper is exactly the same as the scope of whatever is calling it. This makes abstracting out logic really easy. Let's see what our object in `/docpad.coffee` would look like:

``` coffee
docpadConfig = {
	templateData:
		site:
			title: "My Website"

		getPreparedTitle: -> if @document.title then "#{@document.title} | #{@site.title}" else @site.title
}
```

And the title of our layout template, `default.html.eco`, would become:

``` erb
<title><%= @getPreparedTitle() %></title>
```

Now that is awesome! While this was a simple example, we can use it to do some really cool stuff. For instance, [here](https://gist.github.com/4166882) is an example of it being used to localize dates into French.

If you're writing a plugin, you can use the [extendTemplateData](/docpad/events) event to extend the template data.











## Adding a Menu Listing for our Pages

Remember our _About_ page? Wouldn't it be nice if, when we list more pages, our menu updates automatically? It sure would, so let's do that!


### Updating our Layout

Open your default layout and, before the `h1`, add the following:

- `src/layouts/default.html.eco`

``` erb
<ul>
	<% for page in @getCollection("html").findAll({isPage:true}).toJSON(): %>
		<li class="<%= if page.id is @document.id then 'active' else 'inactive' %>">
			<a href="<%= page.url %>">
				<%= page.title %>
			</a>
		</li>
	<% end %>
</ul>
```

Save it, and bang, now we've got our navigation menu on each page! Wicked. So what does that do? Well first it uses the `getCollection` [template helper](/docpad/template-data) to fetch the `html` collection, which is a pre-defined collection by DocPad that contains all the HTML documents in our website. Then, with that collection, we find everything that has a `isPage` attribute set to `true`, which is the attribute we defined earlier when first applying our layout to our pages. We then convert the result from a [Backbone Collection](http://backbonejs.org/#Collection) / [QueryEngine](/queryengine/guide) into a standard JavaScript Array using [`toJSON`](http://backbonejs.org/#Collection-toJSON).

That's a bit of a mouthful, but give it a while and you'll be a pro in no time. There is one major inefficiency with the above approach. Can you guess it?

Performing the query every single time we render a layout is a bit silly, as the results won't change each time. What we ought to do is query once and provide access to the results of our collection. Let's do it!


### Creating Custom Collections via the Configuration File

Let's go back to our [DocPad Configuration File](/docpad/config) (`docpad.coffee`) and open it up. This time we want to add the following:

``` coffee
docpadConfig = {
	collections:
		pages: ->
			@getCollection("html").findAllLive({isPage:true})
}
```

In our default layout, `default.html.eco`, we'll update the `getCollection` line to become:
	
``` erb
<% for page in @getCollection("pages").toJSON(): %>
```

Much better, and way more efficient. Did you spot the difference with the call we used? When performing our query, we used the `findAllLive` instead of the `findAll` method. The reasoning behind this is that `findAllLive` utilizes [QueryEngine's Live Collections](/queryengine/guide), which allows us to define our criteria once and then, throughout time, keep our collection up-to-date. It works by creating a live child collection of the parent collection (in this case, the `html` collection is the parent collection and our `pages` collection is the child collection). The child collection then subscribes to `add`, `remove` and `change` events of the parent collection and tests the model that the event was for against our child collection's criteria. If it passes the collection, it adds it, and if it doesn't pass then it removes it. This performs much better than querying everything every single time.

So then, what about sorting? That's easy enough! We can sort by changing `@getCollection('html').findAllLive({isPage:true})` to add a second argument, which is the sorting argument; `@getCollection('html').findAllLive({isPage:true},[{filename:1}])` that, in this case, will sort by the filename in ascending order. To sort in descending order, we would change the `1` to become `-1`. Now we can sort by any attribute available on our models, which means that we could even add an `order` attribute to our document meta data and then sort by that if we wanted to. There is also a third parameter for paging. To learn about this, as well as what type of queries are available to you, you can refer to the [QueryEngine Guide](/queryengine/guide).


### Setting Default Meta Data Attributes for our Pages

Considering we'd probably like all our pages to use the default layout, we may be lazy enough to want to set this by default for all our pages, so we don't always have to add `layout: default` to the [meta data](/docpad/meta-data) of each page. Just like everything, it's pretty darn easy, if you know how. And here's how:

``` coffee
docpadConfig = {
	collections:
		pages: ->
			@getCollection("html").findAllLive({isPage:true}).on "add", (model) ->
				model.setMetaDefaults({layout:"default"})
}
```

So, what does this do? It's exactly the same as before, but we use the `add` event automaticaly fired by [backbone](http://backbonejs.org/#Collection-add) whenever a model (a page, file, document, whatever) is added to our collection. Then, inside our event, we say we want to set our default meta data attributes for the model; in this case, setting the layout to `"default"`.

This ability is priceless when doing more complicated things with DocPad. For instance, we use it for this documentation, to allow us to base the navigation structure of our documentation files on their physical location in our file system. Thus, if we have a file `docs/docpad/01-start/04-begin.html.md`, we can detect that the project is `docpad`, and assign `project: "docpad"` to the meta data accordingly. As the section is "start" and it is order first, we set `category: "start"` and `categoryOrder: 1`, and also see that our file is `begin` and ordered 4th. This is just one nifty example. There's plenty more you'll discover on your own epic journey! :)











## Adding the Blog Posts

As you now have all the tools and knowledge required to be able to create the blog post section, we've left that part as an exercise for you! We've done this to help you retain and make best use of all the awesomeness you've just learned.

- If you need a few pointers to help you get started, here you go :)
	- Create a new layout called `post` that will use the default layout. Use it to perform custom styling for your blog post (e.g. `<div class="post"><%- @content %></div>`).
	- When creating your blog posts, we recommend giving them a `date` meta data attribute in the format of `date: 2012-12-25`, so you can sort your blog posts in descending date order.
	- Create a new directory called `posts` that contains all of your blog posts, and use the query `relativeOutDirPath: 'posts'` for your custom collection in order to retrieve all documents in the `posts` output directory (`/my-new-website/out/posts`). You can refer to the [Meta Data Page](/docpad/meta-data) for more information about the attributes already available to you.
	- Create a new page called `posts.html.eco` that lists all your blog posts. This will be, more or less, the same as our navigation menu. If you would like to display descriptons of the blog posts, just add that as a meta data attribute for the blog posts, and then output that meta data attribute. If you want to show the rendered content of the data, you can use `post.contentRenderedWithoutLayouts`. You can refer to the [Meta Data Page](/docpad/meta-data) for more information about the attributes already available to you.

- If you're stuck and need some help, just hop on over to the [DocPad IRC Support Channel](http://webchat.freenode.net/?channels=docpad) (#docpad on freenode) and someone will be with you soon enough. :) You can also discover all of our available Support Channels via our [Support Page](/support).

By the way, congratulations! You now possess all the foundations required to be able to write amazing and powerful web applications like those already in our [Showcase](/docpad/showcase). To recap, you now know how to:

- write documents in any language, markup, pre-processor, templating engine, whatever you wish, by installing the necessary plugin for it and changing the extensions of the document
- perform powerful abstractions using layouts, meta data, template data and configuration files
- create incredibly efficient custom collections, filtered and sorted by your own criteria
- do your own custom listings of content

But it doesn't stop there; these were just the foundations! If you can imagine it, then you will be able to accomplish it with DocPad. Really, there are no limits - that's why DocPad sets you free!

So, farewell and enjoy your epic journey. The power is yours!








## Deployment

[Deployment is the next page of this guide.](/docpad/deploy)
