# Contributing to Jison

Fork, make your changes, run tests and/or add tests 
and then send your issues to https://github.com/ULL-ESIT-PL/jison/issues
and pull requests to https://github.com/ULL-ESIT-PL/jison/pulls.

## Running tests

Prerequesites: `node` and `npm`.

First run:

    npm install

Then run tests with:

    npm test

## Building the site

To build the site, as well as the Browserified web version of Jison, run:

    make site
    
Then you can also preview the site by doing:

    make preview
    
Note that you will need `nanoc` and `adsf` in order to build/preview the site. `gem install` them if you haven't.
