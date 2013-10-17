# Match

This repo is basically the Meteor [Match module](https://github.com/meteor/meteor/tree/devel/packages/check) violently ripped out and made to work with normal Node.

It's a decent simple, validation module. I couldn't find anything I liked as much that existed for Node.

The docs for the Meteor version of the module can be found here:  [http://docs.meteor.com/#Match](http://docs.meteor.com/#Match)

**Work in progress.** Don't expect it to work correctly, or at all.

## Installation

    $ npm install mtr-match

## Example

    var Match = require("mtr-match");

    Match.test({ name: "J.R. Davis" }, { name: String });
    Match.test("Hello, World", String);

## License

The MIT License (MIT)

Copyright (c) 2013 Meteor Development Group and Josh-Ryan Davis

Permission is hereby granted, free of charge, to any person obtaining a copy of
this software and associated documentation files (the "Software"), to deal in
the Software without restriction, including without limitation the rights to
use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of
the Software, and to permit persons to whom the Software is furnished to do so,
subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS
FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR
COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER
IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN
CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
