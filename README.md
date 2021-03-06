# Knwl.js
Knwl.js is a Javascript library that parses through text for dates, times, phone numbers, emails, places, and more. 

Parser plugins are what make Knwl.js tick and give it new parsing abilities. There are many already available under ```./default_plugins``` for a number of tasks.
Soon, you'll be able to browse community created plugins all on one website (we're still working on this). If you're interested in developing plugins for Knwl.js, ```./plugin_development.md``` is a great place to start.

### Check out a quick demo: http://loadfive.com/os/knwl/demo
#### Google+ Community: https://plus.google.com/communities/108874785204246812675

## Installation

Installation instructions are specific to whether you want to run Knwl.js in the browser, or on the server with Node.js.

###For Node.js

#### Install using ```npm```:

```console
	npm install knwl.js
```

1. Load the ```knwl``` module using ```require()```.

	```javascript
		var knwl = require("./knwl.js");
	```

2. Load a parser plugin.

	```javascript
		knwl.register('dates', require('./default_plugins/dates'));
	```
	
	The plugins in the ```./default_plugins``` directory will be loaded automatically.

###For the Browser

These steps require the ```npm``` package.

1. Run ```npm install``` to install dependencies.

2. ```browserify``` may be used to build a Knwl.js project from Node.js for the browser.

	Use the following syntax in the terminal:
	
	```console
		./node_modules/.bin/browserify script.js browser.js > output.js
	```
	
	The ```script.js``` file is the Node.js file you wish to package for the browser. The ```browser.js``` file is included in the Knwl.js parent directory.

## Usage Guide

These steps are the same regardless of whether Knwl.js is running on the server or client.

3. Initiate Knwl.js on a String.

	``` javascript
		knwl.init("This is a string. This was written on the 2nd of June, of 2015.");
	```
	
	This line runs the initial parser functions that
	prepare the String for plugins to use. **Plugins
	will not function without this method first being called
	on the String.**
	
4. Initiate a plugin to parse the String.
	
	``` javascript
		var dates = knwl.get('dates');
	```
	
	The first parameter of ```knwl.get()``` is the
	name of the parser plugin you're trying to access (make sure you've added the plugin's .js file to the header of the page).
	The names of all default parser plugins are provided
	 towards the end of this document. If you're using
	plugins other than the defaults, see their respective
	documentation.
	
	Anyways, if the parser plugin is found, ```knwl.get()``` will return
	an array of this format:
	
	```javascript
	var results = [
		{ //result
			//plugin-specific properties
			"preview": "This was written on the 2nd of June of 2015.", //the sentence of rough location of the data from the String
			"found": integer //the position (in words) of the result in the String
		}
	]
	```
	
	For example, here's what is returned from ```knwl.get('dates')``` when called on the previously mentioned String:
	
	```json
	[
		{
			"year": 2015,
			"month": 6,
			"day": 2,
			"preview": "This was written on the 2nd of June of 2015.",
			"found": 5
		}
	]
	```

## Default Plugins

These are automatically loaded by default.

###dates.js
```javascript
	knwl.get('dates');
	
	//Returns any dates found in the String.
```

###times.js
```javascript
	knwl.get('times');
	
	//Returns any times found in the String.
	
```

###phones.js
```javascript		
knwl.get('phones')

	//Returns any phone numbers found in the String.

```

###links.js
```javascript
knwl.get('links')

	//Returns any links found in the String.

```

###emails.js
```javascript
knwl.get('emails')
	
	//Returns any email addresses found in the String.
```

### places.js
```javascript
knwl.get('places')

	//Returns any places found in the String.
```

## Experimental Plugins

###Notice: These plugins have not been upgraded to the new syntax

These parser plugins are not as accurate as the default plugins. However,
they should be stable (they shouldn't crash the page) to use if you are willing to use them. They are considerably more static and rigid than default plugins.

In the future, some of these plugins may reach a level of accuracy that promotes them
from experimental status to the default plugins. However, some will merely stay
as experiments.

###english.js
```javascript
knwl.get('english')

	//Returns the simple parts (verb, subject, etc.) of basic sentences found in the String.
	//WARNING: this is a rigid and simplistic plugin, thus it is merely an experiment.
```
###units.js
```javascript
knwl.get('units')
	
	//Returns any units (grams, pounds, etc.) found in the String.
```
##Developing Parser Plugins

What's awesome about the new version of Knwl.js is that it makes it much easier
for anyone with a little knowledge of JS to build plugins. These plugins offer new
parsing abilities for Knwl.js that otherwise wouldn't exist.

If you want to try your hand at building plugins for Knwl.js, we've
provided some documentation in ```plugin_development.md```.

## Community Driven

The further development of this project was possible because of the
amazing community behind previous versions. Version 1.0 of Knwl.js marks a significant
change in the direction of Knwl.js to the very code-base.

We've restructured and rewritten portions of the project to facilitate
plugin development, but also to drastically increase the performance. **Knwl.js 1.0 is significantly
 faster and more efficient than the previous iterations.**
Yet, in the process of the relaunch, certain past features have been put on hold. But
don't worry, plugins such as spam detection and emotion will return soon!

We think that overall, this is a step in the right direction.

As always, we invite you to re-engineer any part of Knwl.js (including the provided plugins) in an attempt
to make them better. Let's do this together.

You can reach us at knwl@loadfive.com with any questions, comments,
or raging complaints.

http://loadfive.com/os/knwl