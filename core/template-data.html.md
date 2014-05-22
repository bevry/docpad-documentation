```
title: "Template Data & Helpers"
```

## Standard Template Data

- `site` &mdash; an object of several site-specific properties, contains:
	- `date` &mdash; a JavaScript date object for the time that the website was last generated
- `document` &mdash; a JavaScript Object containing the serialised values of our `documentModel` (e.g., `documentModel.toJSON()`)
- `req` &mdash; dynamic documents will also have this available to the, it is a reference to the current request object created by the [ExpressJS](http://expressjs.com) framework
- `content` &mdash; when rendering layouts the `content` template data variable contains the contents of the rendered child content to be injected into the current layout for rendering

## Standard Template Helpers

- `include(relativePath)` return the content of another file at the given path
- `getEnvironment()` &mdash; a string of the current environment(s) we are running under
- `getEnvironments()` &mdash; an array of the current environments we are running under
- `referencesOthers()` &mdash; when called, will set the document’s `referenceOthers` [meta data](/docpad/meta-data) property to `true`
- `getDocument()` &mdash; a reference to the current document we are rendering, documents are defined by the [Document Class][] which extends the [File Class][] which extends a [Backbone Model][]
- `getBlock(blockName)` &mdash; valid block names are:
	- `scripts` &mdash; a collection of scripts to be outputted
	- `styles` &mdash; a collection of styles to be outputted
	- `meta` &mdash; a collection of meta to be outputted
- `getPath(path,parentPath)` get a path with respect to the path of the current document

### Querying

- `getDatabase()` &mdash; a [Query-Engine][] collection of all our documents
- `getCollection(collectionName)` &mdash; a [Query-Engine][] collection of a particular sub collection, built in collections are:
	- `documents` &mdash; for all documents
	- `files` &mdash; for all files
	- `layouts` &mdash; for all files
	- `html` &mdash; for all documents and files that result in an HTML file
	- `stylesheet` &mdash; for all stylesheet files (includes stylesheet pre-processor files)
- `getFiles(query, sorting, paging)` get all files that match the arguments, caches the result collection
- `getFile(query, sorting, paging)` get a single file that matches the arguments
- `getFilesAtPath(relativePath)` get a file at the given path, path is processed through `getPath`
- `getFileAtPath(path, sorting, paging)` get a single file at the given path, path is processed through `getPath`
- `getFileById(id, sorting, paging)` get a single file that has the specified id

[Document Class]: https://github.com/bevry/docpad/blob/master/src/lib/models/document.coffee
[File Class]: https://github.com/bevry/docpad/blob/master/src/lib/models/file.coffee
[Backbone Model]: http://documentcloud.github.com/backbone/#Model
[Query-Engine]: https://github.com/bevry/query-engine