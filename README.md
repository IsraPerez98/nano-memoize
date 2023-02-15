[![Codacy Badge](https://api.codacy.com/project/badge/Grade/30ce201484754fa5b0a6c6046abb842d)](https://www.codacy.com/app/syblackwell/nano-memoize?utm_source=github.com&amp;utm_medium=referral&amp;utm_content=anywhichway/nano-memoize&amp;utm_campaign=Badge_Grade)
# Faster than fast, smaller than micro ... nano-memoize.

[![Maintainability](https://api.codeclimate.com/v1/badges/76cb5396753d151cfdd8/maintainability)](https://codeclimate.com/github/anywhichway/nano-memoize/maintainability)

# Introduction

Version 3.x.x of nano-memoize was modified to use newer versions of JavaScript built-in classes and take advantage of current v8 loop optimizations. As a result, the minified/brotli size of 3.0.4 at 487 bytes is 30% smaller and is slightly faster that v2.x.x and v1.x.x. 

Tests show 'nano-memoize' is overall the smallest and fastest openly available JavaScript memoizer for single and multiple argument functions accepting primitives and objects. However, I have found that benchmarks can vary dramatically from O/S to O/S or Node version to Node version, so I could be wrong. These tests were run on a Windows 10 Pro 64bit 2.8ghz i7 machine with 16GB RAM and Node v18.13.0. Garbage collection was forced between each sample run to minimize its impact on results.

The speed tests are below.
 
* For single primitive argument functions `nano-memoize` is typically 2% faster than `fast-memoize` and `micro-emoize`. However, all three are almost always within the margins of error of the other.
 
* For single object argument functions `nano-memoize` is consistently at least 15% faster than its closest competitor `fast-memoize`.

* For multiple primitive argument functions `nano-memoize` is typically 2% faster than `fast-memoize` and `micro-emoize`. However, all three are frequently within the margin of error of the other.

* For multiple object argument functions `micro-memoize` is always at least 5% faster than its closest competitors `moize` and `nano-memoize` which alternate in second place typically within each other's margin of error.

* For custom equality functions 'nano-memoize` and `micro-memoize vary in speed depending on the equality function used. `nano-memoize` is always first by at least 15% using `hash-it` and `micro-memoize` is always second using `hash-it` or `lodash`. See the table below.

The `planetheidea/moize` library (which claims to be the fastest on average) does not include `nano-memoize` for comparison and the repository is not accepting comments or a pull request for some technical reason. The repository has been forked and its own benchmarking has been updated and run to confirm the results below.


Starting cycles for functions with a single primitive parameter...
┌───────────────┬─────────────┬──────────────────────────┬─────────────┐
│ Name          │ Ops / sec   │ Relative margin of error │ Sample size │
├───────────────┼─────────────┼──────────────────────────┼─────────────┤
│ nano-memoize  │ 150,014,960 │ ± 1.26%                  │ 88          │
├───────────────┼─────────────┼──────────────────────────┼─────────────┤
│ fast-memoize  │ 148,920,057 │ ± 1.37%                  │ 88          │
├───────────────┼─────────────┼──────────────────────────┼─────────────┤
│ micro-memoize │ 148,405,982 │ ± 1.46%                  │ 90          │
├───────────────┼─────────────┼──────────────────────────┼─────────────┤
│ iMemoized     │ 117,844,380 │ ± 1.65%                  │ 88          │
├───────────────┼─────────────┼──────────────────────────┼─────────────┤
│ moize         │ 96,796,008  │ ± 1.80%                  │ 85          │
├───────────────┼─────────────┼──────────────────────────┼─────────────┤
│ underscore    │ 54,815,804  │ ± 1.28%                  │ 87          │
├───────────────┼─────────────┼──────────────────────────┼─────────────┤
│ lodash        │ 54,617,110  │ ± 1.30%                  │ 87          │
├───────────────┼─────────────┼──────────────────────────┼─────────────┤
│ lru-memoize   │ 41,426,130  │ ± 1.16%                  │ 87          │
├───────────────┼─────────────┼──────────────────────────┼─────────────┤
│ memoizee      │ 31,747,590  │ ± 1.52%                  │ 85          │
├───────────────┼─────────────┼──────────────────────────┼─────────────┤
│ addy-osmani   │ 14,848,551  │ ± 1.76%                  │ 82          │
├───────────────┼─────────────┼──────────────────────────┼─────────────┤
│ memoizerific  │ 12,835,863  │ ± 1.84%                  │ 85          │
└───────────────┴─────────────┴──────────────────────────┴─────────────┘

Starting cycles for functions with a single object parameter...
┌───────────────┬─────────────┬──────────────────────────┬─────────────┐
│ Name          │ Ops / sec   │ Relative margin of error │ Sample size │
├───────────────┼─────────────┼──────────────────────────┼─────────────┤
│ nano-memoize  │ 149,402,848 │ ± 1.20%                  │ 90          │
├───────────────┼─────────────┼──────────────────────────┼─────────────┤
│ fast-memoize  │ 121,117,510 │ ± 2.41%                  │ 86          │
├───────────────┼─────────────┼──────────────────────────┼─────────────┤
│ iMemoized     │ 98,480,257  │ ± 3.36%                  │ 85          │
├───────────────┼─────────────┼──────────────────────────┼─────────────┤
│ micro-memoize │ 97,781,728  │ ± 1.36%                  │ 87          │
├───────────────┼─────────────┼──────────────────────────┼─────────────┤
│ moize         │ 94,370,945  │ ± 4.58%                  │ 84          │
├───────────────┼─────────────┼──────────────────────────┼─────────────┤
│ lodash        │ 41,298,824  │ ± 2.60%                  │ 84          │
├───────────────┼─────────────┼──────────────────────────┼─────────────┤
│ lru-memoize   │ 39,315,541  │ ± 1.55%                  │ 86          │
├───────────────┼─────────────┼──────────────────────────┼─────────────┤
│ underscore    │ 33,803,044  │ ± 1.66%                  │ 87          │
├───────────────┼─────────────┼──────────────────────────┼─────────────┤
│ memoizee      │ 27,298,946  │ ± 2.40%                  │ 86          │
├───────────────┼─────────────┼──────────────────────────┼─────────────┤
│ addy-osmani   │ 16,003,489  │ ± 1.72%                  │ 87          │
├───────────────┼─────────────┼──────────────────────────┼─────────────┤
│ memoizerific  │ 12,502,443  │ ± 1.33%                  │ 86          │
└───────────────┴─────────────┴──────────────────────────┴─────────────┘

Starting cycles for functions with multiple parameters that contain only primitives...
┌───────────────┬────────────┬──────────────────────────┬─────────────┐
│ Name          │ Ops / sec  │ Relative margin of error │ Sample size │
├───────────────┼────────────┼──────────────────────────┼─────────────┤
│ nano-memoize  │ 57,333,928 │ ± 1.83%                  │ 85          │
├───────────────┼────────────┼──────────────────────────┼─────────────┤
│ micro-memoize │ 51,539,993 │ ± 2.07%                  │ 83          │
├───────────────┼────────────┼──────────────────────────┼─────────────┤
│ moize         │ 49,918,411 │ ± 3.30%                  │ 81          │
├───────────────┼────────────┼──────────────────────────┼─────────────┤
│ lru-memoize   │ 29,594,676 │ ± 2.83%                  │ 79          │
├───────────────┼────────────┼──────────────────────────┼─────────────┤
│ memoizee      │ 17,895,742 │ ± 2.08%                  │ 87          │
├───────────────┼────────────┼──────────────────────────┼─────────────┤
│ iMemoized     │ 12,263,731 │ ± 1.99%                  │ 85          │
├───────────────┼────────────┼──────────────────────────┼─────────────┤
│ memoizerific  │ 7,804,227  │ ± 1.81%                  │ 84          │
├───────────────┼────────────┼──────────────────────────┼─────────────┤
│ addy-osmani   │ 4,190,503  │ ± 2.03%                  │ 84          │
├───────────────┼────────────┼──────────────────────────┼─────────────┤
│ fast-memoize  │ 1,101,952  │ ± 2.87%                  │ 81          │
└───────────────┴────────────┴──────────────────────────┴─────────────┘


Starting cycles for functions with multiple parameters that contain objects...
┌───────────────┬────────────┬──────────────────────────┬─────────────┐
│ Name          │ Ops / sec  │ Relative margin of error │ Sample size │
├───────────────┼────────────┼──────────────────────────┼─────────────┤
│ micro-memoize │ 51,551,926 │ ± 2.10%                  │ 82          │
├───────────────┼────────────┼──────────────────────────┼─────────────┤
│ nano-memoize  │ 40,243,156 │ ± 3.75%                  │ 82          │
├───────────────┼────────────┼──────────────────────────┼─────────────┤
│ moize         │ 37,285,146 │ ± 16.13%                 │ 65          │
├───────────────┼────────────┼──────────────────────────┼─────────────┤
│ lru-memoize   │ 27,946,905 │ ± 3.41%                  │ 79          │
├───────────────┼────────────┼──────────────────────────┼─────────────┤
│ memoizee      │ 17,209,457 │ ± 1.96%                  │ 84          │
├───────────────┼────────────┼──────────────────────────┼─────────────┤
│ memoizerific  │ 7,609,760  │ ± 4.26%                  │ 76          │
├───────────────┼────────────┼──────────────────────────┼─────────────┤
│ addy-osmani   │ 1,212,045  │ ± 1.85%                  │ 86          │
├───────────────┼────────────┼──────────────────────────┼─────────────┤
│ fast-memoize  │ 563,610    │ ± 26.34%                 │ 69          │
└───────────────┴────────────┴──────────────────────────┴─────────────┘

Starting cycles for alternative cache types...
┌─────────────────────────────────────────────────────┬─────────────┬──────────────────────────┬─────────────┐
│ Name                                                │ Ops / sec   │ Relative margin of error │ Sample size │
├─────────────────────────────────────────────────────┼─────────────┼──────────────────────────┼─────────────┤
│ nanomemoize deep equals (hash-it isEqual)           │ 112,560,448 │ ± 1.35%                  │ 85          │
├─────────────────────────────────────────────────────┼─────────────┼──────────────────────────┼─────────────┤
│ micro-memoize deep equals (lodash isEqual)          │ 83,402,392  │ ± 2.88%                  │ 80          │
├─────────────────────────────────────────────────────┼─────────────┼──────────────────────────┼─────────────┤
│ micro-memoize deep equals (hash-it isEqual)         │ 70,493,317  │ ± 2.46%                  │ 83          │
├─────────────────────────────────────────────────────┼─────────────┼──────────────────────────┼─────────────┤
│ nanomemoize deep equals (lodash isEqual)            │ 63,040,211  │ ± 1.61%                  │ 84          │
├─────────────────────────────────────────────────────┼─────────────┼──────────────────────────┼─────────────┤
│ nanomemoize fast equals (fast-equals deepEqual/ES6) │ 61,878,364  │ ± 1.73%                  │ 84          │
├─────────────────────────────────────────────────────┼─────────────┼──────────────────────────┼─────────────┤
│ micro-memoize deep equals (fast-equals deepEqual)   │ 56,841,180  │ ± 3.10%                  │ 80          │
├─────────────────────────────────────────────────────┼─────────────┼──────────────────────────┼─────────────┤
│ nanomemoize fast deep equals (fast-deep-equal/ES6)  │ 41,010,681  │ ± 2.44%                  │ 82          │
└─────────────────────────────────────────────────────┴─────────────┴──────────────────────────┴─────────────┘

If you want similar performance for intersection, union or Cartesian product also see:

- https://github.com/anywhichway/intersector
- https://github.com/anywhichway/unionizor
- https://github.com/anywhichway/cxproduct


# Usage

`npm install nano-memoize`

The code is hand-crafted to run across all browsers all the way back to IE 11. No transpiling is necessary.


# API

The API is a subset of the `moize` API.

```javascript
const memoized = nanomemoize(sum(a,b) => a + b);
memoized(1,2); // 3
memoized(1,2); // pulled from cache
```

`nanomemoize(function,options) returns function`

The shape of options is:

```javascript
{
  // only use the provided maxArgs for cache look-up, useful for ignoring final callback arguments
  maxArgs: number,
  // call last argument of memoized multi-args functions after a number of milliseconds via a timeout after the 
  // cached result has been returned, perhaps to ensure that callbacks are invoked, does not cache the timemout result
  // e.g. nanomemoize(function(a,b,callback) { var result = a + b; callback(result); return result; },{maxArgs:2,callTimeout:0});
  callTimeout: number,
  // number of milliseconds to cache a result, set to `Infinity` or `-1` to never create timers or expire
  maxAge: number, 
  // the serializer/key generator to use for single argument functions (optional, not recommended)
  // must be able to serialize objects and functions, by default a Map is used internally without serializing
  serializer: function,
  // the equals function to use for multi-argument functions (optional, try to avoid) e.g. deepEquals for objects
  equals: function, 
  // forces the use of multi-argument paradigm, auto set if function has a spread argument or uses `arguments` in its body.
  vargs: boolean 
}
```

The returned function will also have these methods:

`.clear()` clears the cache for the function.

`.keys()` returns an array of arrays with each array being the arguments provided on a call of the function.

`.values()` returns an array of arrays with each array being the results of a function call with the same index position as the keys.


# Release History (reverse chronological order)

2022-02-15 v3.0.5 Documentation updates.

2022-02-04 v3.0.4 A code walkthrough revealed an opportunity to remove unused code from v2.x.x.

2022-02-02 v3.0.3 Added unit test for `maxAge`. Adjusted varArg unit tests for more accuracy. Slight optimizations to multi argument memoized functions. Slight improvement to cache clearing that may reduce GC. Updated license file for copyright period. Updated docs on `callTimeout` for clarity.

2022-02-01 v3.0.2 Fixed https://github.com/anywhichway/nano-memoize/issues/52 with custom equals functions not consistently working. `fast-equals` or `lodash.isEqual` now work. Slight performance degradation, but still generally the fastest.

2022-01-29 v3.0.1 Fixed build issue where root index.js was not getting updated.

2022-01-28 v3.0.0 Slight size optimization. 25% speed improvement. Moved to module format. There is a known issue with providing `fast-equals` or `lodash.isEqual` as an optional comparison function. Unit tests pass, but the functions fail under load. The `hash-it` object equivalence function does work. A formerly undocumented method `.keyValues()` has been deprecated since it is no longer relevant with the new optimizations.

2022-12-08 v2.0.0 Removed callTimeout from TypeScript typings since it was not implemented and there are no plans to implement. Bumped version to 2.0.0 since this may break some users.

2022-10-20 v1.3.1 Bumping version for https://github.com/anywhichway/nano-memoize/pull/41

2022-03-30 v1.3.0 Dropped support for `dist` and `browser` directories.

2022-03-15 v1.2.2 Bumped minor version for TS typings and some package dependency updates.

2020-11-02 v1.2.1 Added main: "index.js" reference in package.json.

2020-06-18 v1.2.0 Enhanced multi-arg handling so that arg lengths must match precisely (thanks @amazingmarvin), unless `maxArgs` is passed as an option.
Also added `callTimeout` to go ahead and call underlying function to ensure callbacks are invoked if necessary.

2020-05-26 v1.1.11 [Fixed Issue 17]Fixed https://github.com/anywhichway/nano-memoize/issues/17. It is not known when this bug made its way into the code.

2020-02-30 v1.1.10 Moved growl to dev dependency.

2020-01-30 v1.1.9 Code style improvements.

2019-11-29 v1.1.8 Corrected typos in documentation.

2019-09-25 v1.1.7 Manually created an IE 11 compatible version by removing arrow functions and replacing Object.assign
with a custom function. Minor size increase from 660 to 780 Brotli bytes. Also eliminated complex `bind` approach in
favor of closures. The latest v8 engine handles closures as fast as bound arguments for our case and we are not as
concerned with older browser performace (particularly given how fast the code is anyway). Converted for loops to run in
reverse, which for our case is faster (but is not always guranteed to be faster).

2019-09-17 v1.1.6 Added a manually transpiled es5_ie11.html file with an Object.assign polyfill to the test directory to verify
compatibility with IE11. Modified unit tests so they are ES5 compatible. All tests pass. Added `sideEffects=false` to package.json.

2019-06-28 v1.1.5 Improved documentation. Updated version of `micro-memoize` used for benchmark testing. No code changes.

2019-05-31 v1.1.4 [Fixed Issue 7](https://github.com/anywhichway/nano-memoize/issues/7).

2019-04-09 v1.1.3 [Fixed Issue 6](https://github.com/anywhichway/nano-memoize/issues/6). Minor speed and size improvements.

2019-04-02 v1.1.2 Speed improvements for multiple arguments. Now consistently faster than `fast-memoize` and `nano-memoize` across multiple test runs. Benchmarks run in a new test environment. The benchmarks for v1.1.1 although correct from a relative perspective, grossly understated actual performance due to a corrupt testing environment.

2019-03-25 v1.1.1 Pushed incorrect version with v1.1.0. This corrects the version push.

2019-03-25 v1.1.0 Added use of `WeakMap` for high-speed caching of single argument functions when passed objects. The `serializer` option no longer defaults to `(value) => JSON.stringify(value)` so if you want to treat objects that have the same string representation as the same, you will have to provide a `serializer`.

2019-03-24 v1.0.8 Updated/corrected documentation.

2019-03-24 v1.0.7 Made smaller and faster. Renamed `sngl` to `sng` and `mltpl` to `mlt`. Converted all functions to arrow functions except `sng` and `mlt`. Simplified and optimized `mlt`. Removed `()` around args to single argument arrow function definitions, e.g. `(a) => ...` became `a => ...`. Replaced the arg signature `()` in arrow functions with `_`, which is shorter. Eliminated multiple character variables except for those used in options to request memoization. Collapsed `setTimeout` into a single location. Defined `const I = Infinity`. Eliminated `()` around `? :` condition expressions.  Changed `{}` to `Object.create(null)`. Documented all variables. Moved some variables around for clarity. Moved `options` into a destructing argument.

2019-03-20 v1.0.6 Updated documentation.

2019-03-11 v1.0.5 Now supports setting `maxAge` to Infinity and no timers will be created to expire caches.

2019-02-26 v1.0.4 Further optimized cache expiration. See [Issue 4](https://github.com/anywhichway/nano-memoize/issues/4)

2019-02-16 v1.0.3 Fixed README formatting

2019-02-16 v1.0.2 Further optimizations to deal with [Issue 4](https://github.com/anywhichway/nano-memoize/issues/4). `expireInterval` introduced in v1.0.1 removed since it is no longer needed. Also, 25% reduction in size. Code no longer thrashes when memoizing a large number of functions.

2019-02-16 v1.0.1 Memo expiration optimization. Special appreciation to @titoBouzout and @popbee who spent a good bit of time reviewing code for optimization and making recommendations. See [Issue 4](https://github.com/anywhichway/nano-memoize/issues/4) for the conversation.

2018-04-13 v1.0.0 Code style improvements.

2018-02-07 v0.1.2 Documentation updates

2018-02-07 v0.1.1 Documentationand benchmark updates

2018-02-01 v0.1.0 Documentation updates. 50 byte decrease.

2018-01-27 v0.0.7b BETA Documentation updates.

2018-01-27 v0.0.6b BETA Minor size and speed improvements.

2018-01-27 v0.0.5b BETA Fixed edge case where multi-arg key may be shorter than current args.

2018-01-27 v0.0.4b BETA Fixed benchmarks. Removed maxSize. More unit tests. Fixed maxAge.

2018-01-27 v0.0.3b BETA More unit tests. Documentation. Benchmark code in repository not yet running.

2018-01-24 v0.0.2a ALPHA Minor speed enhancements. Benchmark code in repository not yet running.

2018=01-24 v0.0.1a ALPHA First public release. Benchmark code in repository not yet running.
