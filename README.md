# Match

[![Build Status](https://travis-ci.org/jrdavis/match.png?branch=master)](https://travis-ci.org/jrdavis/match) [![NPM version](https://badge.fury.io/js/mtr-match.png)](https://npmjs.org/package/mtr-match) [![Dependency Status](https://gemnasium.com/jrdavis/match.png)](https://gemnasium.com/jrdavis/match)

[![NPM](https://nodei.co/npm/mtr-match.png)](https://nodei.co/npm/mtr-match/)


Match is a lightweight library for checking that arguments and other values are of the expected type.

This package was originally the [Match module](https://github.com/meteor/meteor/tree/devel/packages/check) in Meteor. This repo is the code for that package violently ripped out and made to work with normal Node.

**Work in progress.** Don't expect it to work correctly, or at all.

The docs for the original Meteor version of the module can be found here:  [http://docs.meteor.com/#match](http://docs.meteor.com/#match)

## Installation

    $ npm install mtr-match

## Example

    var Match = require("mtr-match");
    
    // Returns true
    var valid = Match.test("testing", String); 
    
    Match.check({ name: "Danny Dyer" }, { name: String });
    Match.check("Hello, World", String);

Methods
-------

##### ```Match.check(value, pattern)```

Checks that a value matches a pattern. If the value does not match the pattern, throws a Match.Error.

**Arguments:**

**value**: The value to check

**pattern**: The pattern to match value against

##### ```Match.test(value, pattern)```

Returns true if the value matches the pattern.

**Arguments:**

**value**: The value to check

**pattern**: The pattern to match value against

---

If the match fails, check throws a Match.Error describing how it failed.

Match Patterns
--------------

The following patterns can be used as pattern arguments to check and Match.test:

##### ```Match.Any```

Matches any value.

##### ```String```, ```Number```, ```Boolean```, ```undefined```, ```null```

Matches a primitive of the given type.

##### ```Match.Any```

Matches a signed 32-bit integer. Doesn't match ```Infinity```, ```-Infinity```, or ```NaN```.

##### ```[pattern]```

A one-element array matches an array of elements, each of which match pattern. For example, [```Number```] matches a (possibly empty) array of numbers; [```Match.Any```] matches any array.

##### ```{key1: pattern1, key2: pattern2, ...}```

Matches an Object with the given keys, with values matching the given patterns. If any pattern is a Match.Optional, that key does not need to exist in the object. The value may not contain any keys not listed in the pattern. The value must be a plain Object with no special prototype.

##### ```Match.ObjectIncluding({key1: pattern1, key2: pattern2, ...})```

Matches an Object with the given keys; the value may also have other keys with arbitrary values.

##### ```Object```

Matches any plain Object with any keys; equivalent to ```Match.ObjectIncluding({})```.

##### ```Match.Optional(pattern)```

Matches either ```undefined``` or something that matches pattern. If used in an object this matches only if the key is not set as opposed to the value being set to ```undefined```.
    
    // In an object
    var pat = { name: Match.Optional(String) };
    Match.check({ name: "something" }, pat) // OK
    Match.check({}, pat) // OK
    Match.check({ name: undefined }, pat) // Throws an exception
    
    // Outside an object
    Match.check(undefined, Match.Optional(String)); // OK

##### ```Match.OneOf(pattern1, pattern2, ...)```

Matches any value that matches at least one of the provided patterns.

##### Any constructor function (eg, Date)

Matches any element that is an instance of that type.

##### ```Match.Where(condition)```

Calls the function condition with the value as the argument. If condition returns true, this matches. If condition throws a Match.Error or returns false, this fails. If condition throws any other error, that error is thrown from the call to check or Match.test. 

Examples:
    
    Match.check(buffer, Match.Where(EJSON.isBinary));
    
    NonEmptyString = Match.Where(function (x) {
      check(x, String);
      return x.length > 0;
    });
    Match.check(arg, NonEmptyString);

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
