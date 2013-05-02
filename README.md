# CSSSelector


A fully CSS3 compilant selector for [htmlparse-node](https://github.com/tautologistics/node-htmlparser) parses.



## Requirements

Uses components from [js-library](https://github.com/debonet/js-library)


## Usage

~~~

var fCSSSelector = require("fCSSSelector");

fCSSSelector(parsedhtml, selector);

~~~

Where `parsedhtml` is the output docuement from node-htmlparser, and `selector` is any valid CSS3 selector.


## Supported selectors

Rather than provide a complete BNF, suffice it to say that all of the forms suggested below are supported

~~~
selector = element.class[attribute=val]:pseudo(argument),selector
~~~


### Pseudo selectors:

All the standard CSS3 pseudo selectors are supported, as well as some non-standard ones. Here's a compelete list:

* first-child
* last-child
* nth-child
* nth-last-child
* first-of-type
* last-of-type
* only-of-type
* nth-of-type
* nth-last-of-type
* empty
* not
* contains


### A complete example

~~~
var nsHtmlparser = require("htmlparser");
var fCSSSelector = require("fCSSSelector");

// --------------------------------------------------------------------------------
// fFindMatchingElements
//   find the elements within an html string which match the provided selector
//
// Params:
//   shtml := string containing html
//   sSelector := css selector of interest
//   fCallback := function(err, ve), called with array of matching elements
//
function fFindMatchingElements = function (shtml, sSelector, fCallback){
	(new nsHtmlparser.Parser(
		new nsHtmlparser.DefaultHandler(
			function(err, veDocument){
				if (err){return fCallback(err);	}
				var veSelection = fCSSSelector(veDocument, selector);
				fCallback(null, veSelection);
			}
		)
	)).parseComplete(shtml);
};


// --------------------------------------------------------------------------------
// fPrintElements
//   A callback function which does something with the results
//
var fPrintElements = function(err, ve){
	console.log(err || ve);
};


// --------------------------------------------------------------------------------
// some examples
// --------------------------------------------------------------------------------

// readFile() is a much better idea, but readFileSync() is used for clarity
var shtml = require("fs").readFileSync("my.html").toString();

// find all the links
fFindMatchingElements(shtml, "a", fPrintElements);

// find all the headers
fFindMatchingElements(shtml, "h1,h2,h3,h4,h5,h6,h7", fPrintElements);

// find all elements of class foo which are the 2nd child 
// or of class bar, but not of class baz
fFindMatchingElements(shtml, ".foo:nth-child(2n),.bar:not(.baz)", fPrintElements);


~~~

## Inspiration

Inspired by [soupselect](https://github.com/harryf/node-soupselect)

## License

The MIT License (MIT)

Copyright (c) 2013 Jeremy S. De Bonet

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

