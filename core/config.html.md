```
title: "Configuration"
```

## Configuration Files

The DocPad configuration file sits within the root of your DocPad project and be named as one of the following. Each name provides a special meaing. Here are the valid names:

- `docpad.js` a node javascript file, will generally look like: `module.exports = {/*the configuration*/}`
- `docpad.json` a json file, does not allow functions, will generally look like: `{/*the configuration*/}`
- `docpad.coffee` a node coffeescript file, will generally look like: `module.exports = /*the configuration*/`
- `docpad.cson` a [cson](https://github.com/bevry/cson) file, will generally look like: `/*the configuration*/`

The advantage of `docpad.js` and `docpad.coffee` over `docpad.json` and `docpad.cson` is that they allow us to declare functions, as well as call functions. However, for instances where we cannot trust the contents of the configuration files you would want to use the `docpad.json` or `docpad.cson` as they can't do anything naughty.

The advantage of `docpad.coffee` and `docpad.cson` over `docpad.js` and `docpad.json` is that they allow us to use the CoffeeScript syntax which is a lot more lenient.

Generally, you'll usually always find either a `docpad.coffee` file or a `docpad.cson` file.


### Example `docpad.coffee` file

``` coffee
# The DocPad Configuration File
# It is simply a CoffeeScript Object which is parsed by CSON
docpadConfig = {

	# =================================
	# DocPad Configuration
	
	# Change the port DocPad uses from the default 9778 to 8080
	port: 8080

	
	# =================================
	# Template Data
	# These are variables that will be accessible via our templates

	templateData:

		# Specify some site properties
		site:
			# The production url of our website
			url: "http://website.com"

			# The default title of our website
			title: "Your Website"

			# The website description (for SEO)
			description: """
				When your website appears in search results in say Google, the text here will be shown underneath your website's title.
				"""

			# The website keywords (for SEO) separated by commas
			keywords: """
				place, your, website, keywoards, here, keep, them, related, to, the, content, of, your, website
				"""


		# -----------------------------
		# Helper Functions

		# Get the prepared site/document title
		# Often we would like to specify particular formatting to our page's title
		# we can apply that formatting here
		getPreparedTitle: ->
			# if we have a document title, then we should use that and suffix the site's title onto it
			if @document.title
				"#{@document.title} | #{@site.title}"
			# if our document does not have it's own title, then we should just use the site's title
			else
				@site.title

		# Get the prepared site/document description
		getPreparedDescription: ->
			# if we have a document description, then we should use that, otherwise use the site's description
			@document.description or @site.description

		# Get the prepared site/document keywords
		getPreparedKeywords: ->
			# Merge the document keywords with the site keywords
			@site.keywords.concat(@document.keywords or []).join(', ')


	# =================================
	# Plugins

	# Enable Unlisted Plugins
	# If set to false (defaults to true), we will only enable plugins that have been explicitly set to true inside enabledPlugins
	enabledUnlistedPlugins: true

	# Enabled Plugins
	enabledPlugins:
		# Disable the Pokemon Plugin
		pokemon: false

		# Enable the Digimon Plugin
		# Unless, enableUnlistedPlugins is set to false, all plugins are enabled by default
		digimon: true

	# Configure Plugins
	# Should contain the plugin short names on the left, and the configuration to pass the plugin on the right
	plugins:

		# Disable NIB within the Stylus Plugin
		stylus:
			useNib: false


	# =================================
	# DocPad Events

	# Here we can define handlers for events that DocPad fires
	# You can find a full listing of events on the DocPad Wiki
	events:

		# Server Extend
		# Used to add our own custom routes to the server before the docpad routes are added
		serverExtend: (opts) ->
			# Extract the server from the options
			{server} = opts
			docpad = @docpad

	# =================================
	# Environments

	environments:
	
		development:

			# anything here will be merged with the top-level (production) configuration if we are running inside the development environment
}

# Export our DocPad Configuration
module.exports = docpadConfig
```


## Environment Configuration File

We also support `.env` environment configuration file, the format works like so:

```
KEY=VALUE
KEY2=VALUE2
```

With all key value pairs being added to the `process.env` environment variable.

It is useful for setting sensitive information such as API keys and database information etc - if using for this purpose, then be sure to add the `.env` file to your `.gitignore` file.

