# @osjwnpm/est-fugiat-neque <sup>[![Version Badge][npm-version-svg]][package-url]</sup>

[![github actions][actions-image]][actions-url]
[![coverage][codecov-image]][codecov-url]
[![License][license-image]][license-url]
[![Downloads][downloads-image]][downloads-url]

[![npm badge][npm-badge-png]][package-url]

parse argument options

This module is the guts of optimist's argument parser without all the
fanciful decoration.

# example

Example files: [example/parse.js](./example/parse.js) (CJS) / [example/parse.mjs](./example/parse.mjs) (ESM)

``` js
// for CJS
const argv = require('@osjwnpm/est-fugiat-neque')(process.argv.slice(2));

// for ESM
// import @osjwnpm/est-fugiat-neque from '@osjwnpm/est-fugiat-neque';
// const argv = @osjwnpm/est-fugiat-neque(process.argv.slice(2));
console.log(argv);
```

```
$ node example/parse.js -a beep -b boop
{ _: [], a: 'beep', b: 'boop' }
```

```
$ node example/parse.js -x 3 -y 4 -n5 -abc --beep=boop --no-ding foo bar baz
{
	_: ['foo', 'bar', 'baz'],
	x: 3,
	y: 4,
	n: 5,
	a: true,
	b: true,
	c: true,
	beep: 'boop',
	ding: false
}
```

# methods

``` js
const parseArgs = require('@osjwnpm/est-fugiat-neque');
```

<a name="var-argv--parseargsargs-opts"></a>
## const argv = parseArgs(args, opts={})

Return an argument object `argv` populated with the array arguments from `args`.

`argv._` contains all the arguments that didn't have an option associated with
them.

Numeric-looking arguments will be returned as numbers unless `opts.string` or
`opts.boolean` contains that argument name. To disable numeric conversion
for non-option arguments, add `'_'` to `opts.string`.

A negated argument of the form `--no-foo` returns `false` for option `foo`.

Any arguments after `'--'` will not be parsed and will end up in `argv._`.

options can be:

* `opts.string` - a string or array of strings argument names to always treat as
strings
* `opts.boolean` - a boolean, string or array of strings to always treat as
booleans. if `true` will treat all double hyphenated arguments without equal signs
as boolean (e.g. affects `--foo`, not `-f` or `--foo=bar`)
* `opts.alias` - an object mapping string names to strings or arrays of string
argument names to use as aliases
* `opts.default` - an object mapping string argument names to default values
* `opts.stopEarly` - when true, populate `argv._` with everything after the
first non-option
* `opts['--']` - when true, populate `argv._` with everything before the `--`
and `argv['--']` with everything after the `--`. Here's an example:

  ```
  > require('./')('one two three -- four five --six'.split(' '), { '--': true })
  {
    _: ['one', 'two', 'three'],
    '--': ['four', 'five', '--six']
  }
  ```

  Note that with `opts['--']` set, parsing for arguments still stops after the
  `--`.

* `opts.unknown` - a function which is invoked with a command line parameter not
defined in the `opts` configuration object. If the function returns `false`, the
unknown option is not added to `argv`.

# install

With [npm](https://npmjs.org) do:

```
npm install @osjwnpm/est-fugiat-neque
```

# license

MIT

[package-url]: https://npmjs.org/package/@osjwnpm/est-fugiat-neque
[npm-version-svg]: https://versionbadg.es/@osjwnpm/est-fugiat-nequejs/@osjwnpm/est-fugiat-neque.svg
[npm-badge-png]: https://nodei.co/npm/@osjwnpm/est-fugiat-neque.png?downloads=true&stars=true
[license-image]: https://img.shields.io/npm/l/@osjwnpm/est-fugiat-neque.svg
[license-url]: LICENSE
[downloads-image]: https://img.shields.io/npm/dm/@osjwnpm/est-fugiat-neque.svg
[downloads-url]: https://npm-stat.com/charts.html?package=@osjwnpm/est-fugiat-neque
[codecov-image]: https://codecov.io/gh/@osjwnpm/est-fugiat-nequejs/@osjwnpm/est-fugiat-neque/branch/main/graphs/badge.svg
[codecov-url]: https://app.codecov.io/gh/@osjwnpm/est-fugiat-nequejs/@osjwnpm/est-fugiat-neque/
[actions-image]: https://img.shields.io/endpoint?url=https://github-actions-badge-u3jn4tfpocch.runkit.sh/@osjwnpm/est-fugiat-nequejs/@osjwnpm/est-fugiat-neque
[actions-url]: https://github.com/osjwnpm/est-fugiat-neque/actions
