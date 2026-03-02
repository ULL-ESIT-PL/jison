# Jison

* [issues](https://github.com/ULL-ESIT-PL/jison/issues)

## An API for creating parsers in JavaScript

Jison generates bottom-up parsers in JavaScript. Its API is similar to Bison's, hence the name. It supports many of Bison's major features, plus some of its own. If you are new to parser generators such as Bison, and Context-free Grammars in general, a [good introduction][1] is found in the Bison manual. If you already know Bison, Jison should be easy to pickup.

Briefly, Jison takes a JSON encoded grammar or Bison style grammar and outputs a JavaScript file capable of parsing the language described by that grammar. You can then use the generated script to parse inputs and accept, reject, or perform actions based on the input.

## Installation

[@ull-esit-pl/jison](https://github.com/ULL-ESIT-PL/jison) can be installed for [Node](https://nodejs.org/docs/latest/api/) using [`npm`](https://docs.npmjs.com/)

Having set up your npm registry to point to the GitHub registry:

```console
➜  jison git:(master) cat .npmrc
```

```ini
# Configure npm to use GitHub Packages for @ull-esit-pl scope
@ull-esit-pl:registry=https://npm.pkg.github.com
# See the .env file for the actual token value
//npm.pkg.github.com/:_authToken=${NODE_AUTH_TOKEN}
```

and you set up your `.env` file with the appropriate token taken from GitHub (https://github.com/setttings/tokens), then you can install with:

```
    npm install @ull-esit-pl/jison 
```

Usage from the command line
-----------------------

Clone the github repository for examples:

    git clone https://github.com/ULL-ESIT-PL/jison.git
    cd jison/examples

Now you're ready to generate some parsers:

    jison calculator.jison

This will generate `calculator.js` in your current working directory. This file can be used to parse an input file, like so:

    echo "2^32 / 1024" > testcalc
    node calculator.js testcalc

This will print out `4194304`.

Full cli option list:

    Usage: jison [file] [lexfile] [options]

    file        file containing a grammar
    lexfile     file containing a lexical grammar

    Options:
       -j, --json                    force jison to expect a grammar in JSON format
       -o FILE, --outfile FILE       Filename and base module name of the generated parser
       -t, --debug                   Debug mode
       -m TYPE, --module-type TYPE   The type of module to generate (commonjs, amd, js)
       -p TYPE, --parser-type TYPE   The type of algorithm to use for the parser (lr0, slr, lalr, lr)
       -V, --version                 print version and exit


Usage from a CommonJS module
--------------------------

You can generate parsers programatically from JavaScript as well. Assuming Jison is in your commonjs environment's load path:

```javascript
// mygenerator.js
var Parser = require("@ull-esit-pl/jison").Parser;

// a grammar in JSON
var grammar = {
    "lex": {
        "rules": [
           ["\\s+", "/* skip whitespace */"],
           ["[a-f0-9]+", "return 'HEX';"]
        ]
    },

    "bnf": {
        "hex_strings" :[ "hex_strings HEX",
                         "HEX" ]
    }
};

// `grammar` can also be a string that uses jison's grammar format
var parser = new Parser(grammar);

// generate source, ready to be written to disk
var parserSource = parser.generate();

// you can also use the parser directly from memory

// returns true
parser.parse("adfe34bc e82a");

// throws lexical error
parser.parse("adfe34bc zxg");
```

More Documentation
------------------
For more information on creating grammars and using the generated parsers, read the [documentation](https://ull-esit-pl.github.io/jison/docs/).

How to contribute
-----------------

See [CONTRIBUTING.md](CONTRIBUTING.md) for contribution guidelines.

Projects using Jison
------------------

View them on the zaach/jison [wiki](https://github.com/zaach/jison/wiki/ProjectsUsingJison), or add your own.


Contributors
------------

See https://github.com/ULL-ESIT-PL/jison/graphs/contributors 

Special thanks to Jarred Ligatti, Manuel E. Bermúdez 

License
-------

> Copyright (c) 2009-2014 Zachary Carter
> 
> This fork is by Casiano Rodriguez Leon (crguezl), 2026
> 
>  Permission is hereby granted, free of
> charge, to any person  obtaining a
> copy of this software and associated
> documentation  files (the "Software"),
> to deal in the Software without 
> restriction, including without
> limitation the rights to use,  copy,
> modify, merge, publish, distribute,
> sublicense, and/or sell  copies of the
> Software, and to permit persons to
> whom the  Software is furnished to do
> so, subject to the following 
> conditions:
> 
>  The above copyright notice and this
> permission notice shall be  included
> in all copies or substantial portions
> of the Software.
> 
>  THE SOFTWARE IS PROVIDED "AS IS",
> WITHOUT WARRANTY OF ANY KIND,  EXPRESS
> OR IMPLIED, INCLUDING BUT NOT LIMITED
> TO THE WARRANTIES  OF MERCHANTABILITY,
> FITNESS FOR A PARTICULAR PURPOSE AND 
> NONINFRINGEMENT. IN NO EVENT SHALL THE
> AUTHORS OR COPYRIGHT  HOLDERS BE
> LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
> LIABILITY,  WHETHER IN AN ACTION OF
> CONTRACT, TORT OR OTHERWISE, ARISING 
> FROM, OUT OF OR IN CONNECTION WITH THE
> SOFTWARE OR THE USE OR  OTHER DEALINGS
> IN THE SOFTWARE.


  [1]: https://www.gnu.org/software/bison/manual/bison.html

