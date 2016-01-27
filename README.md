# grunt-qunit-istanbul

> Run QUnit unit tests in a headless PhantomJS instance with code coverage
> analysis provided by istanbul.

## IMPORTANT

This is a fork of the grunt-contrib-qunit repo, adding the ability to generate
[istanbul](http://gotwarlost.github.com/istanbul/) test coverage reports.
Unfortunately this cannot be handled as a seperate plugin, because it needs to
hook into the grunt-contrib-qunit and grunt-lib-phantomjs structure.

This plugin should work as a drop-in replacement for your current `qunit`
task. For any further configuration, please check out the
[original plugin's repo](https://github.com/gruntjs/grunt-contrib-qunit).

## Getting Started

This plugin requires Grunt `~0.4.0`.

If you haven't used [Grunt](http://gruntjs.com/) before, be sure to check out
the [Getting Started](http://gruntjs.com/getting-started) guide, as it explains
how to create a [Gruntfile](http://gruntjs.com/sample-gruntfile), as well as
how to install and use Grunt plugins. Once you're familiar with that process,
you can install this plugin with this command:

```shell
npm install grunt-qunit-istanbul --save-dev
```

Once the plugin has been installed, it can be enabled inside your Gruntfile
with this line of JavaScript:

```js
grunt.loadNpmTasks('grunt-qunit-istanbul');
```

## QUnit task

_Run this task with the `grunt qunit` command._

Task targets, files and options may be specified according to the grunt
[Configuring tasks](http://gruntjs.com/configuring-tasks) guide.

When installed by npm, this plugin will automatically download and install
[PhantomJS][] locally via the [grunt-lib-phantomjs-istanbul][] library.

[PhantomJS]: http://www.phantomjs.org/
[grunt-lib-phantomjs-istanbul]: https://github.com/asciidisco/grunt-lib-phantomjs-istanbul

Also note that running grunt with the `--debug` flag will output a lot of
PhantomJS-specific debugging information. This can be very helpful in seeing
what actual URIs are being requested and received by PhantomJS.

#### OS Dependencies

This plugin uses PhantomJS to run tests. PhantomJS requires the following
dependencies:

**On Ubuntu/Debian**

`apt-get install libfontconfig1 fontconfig libfontconfig1-dev libfreetype6-dev`

**On CentOS**

`yum install fontconfig freetype`

### Options (Coverage object)

#### src

* Type: `array`
* Default: `[]`

The js files you would like to end up in the coverage report.

#### instrumentedFiles

* Type: `string`

A temporary folder (that will be automatically generated and deleted after the
test suite finishes) containing the instrumented source code.

#### tempDir

* Type: `string` [optional]

A folder where the temporary coverage data files should be stored.

#### reportOnFail

* Type: `boolean` [optional]
* Default: `false`

Whether to generate coverage report, when a test fails. 
By default, on test failure, the coverage report is not generated.

#### htmlReport

* Type: `string` [optional]

A folder where the HTML reports should be stored.

#### jsonReport

* Type: `string` [optional]

A folder where the JSON reports should be stored.

#### jsonSummaryReport

* Type: `string` [optional]

A folder where the JSON summary reports should be stored.

#### coberturaReport

* Type: `string` [optional]

A folder where the Cobertura reports should be stored.

#### lcovReport

* Type: `string` [optional]

A folder where the LCOV reports should be stored.

#### cloverReport

* Type: `string` [optional]

A folder where the Clover reports should be stored.

#### prefixUrl

* Type: `string` [optional]
* Default: ``

If you're running your qunit tests with the help of a webserver, and there is
a path that precedes the file system path of the assets.

Example:
```js
// File system: './javascripts/index.js'
// Webserver url: 'localhost:8080/assets/my-project/javascripts/index.js'

{
  baseUrl: '../', // Go up one level to `my-project`
  prefixUrl: 'assets/' // Prefix used before the file path on the web url
}
```


#### baseUrl

* Type: `string` [optional]
* Default: `.`

If you're running your qunit tests with the help of a webserver, you have to
point the coverage inspector to the physical path that is the base url of the
qunit page you're running.

#### linesThresholdPct

* Type: `number` [optional]

Lines coverage percentage threshold to evaluate when running the build. If the
actual coverage percentage is less than this value, the build will fail.

#### statementsThresholdPct

* Type: `number` [optional]

Statements coverage percentage threshold to evaluate when running the build. If
the actual coverage percentage is less than this value, the build will fail.

#### functionsThresholdPct

* Type: `number` [optional]

Functions coverage percentage threshold to evaluate when running the build. If
the actual coverage percentage is less than this value, the build will fail.

#### branchesThresholdPct

* Type: `number` [optional]

Branches coverage percentage threshold to evaluate when running the build. If
the actual coverage percentage is less than this value, the build will fail.

#### disposeCollector

* Type: `boolean` [optional]
* Default: `false`

Whether or not to dispose the previous collector and create a new instance of
it, discarding the info of previously instrumented files. This is useful if
using `grunt-qunit-istanbul` as a
[multi task](http://gruntjs.com/api/inside-tasks#inside-multi-tasks) with
separate targets generating separate coverage reports. If set to `true` for a
particular target, the plugin will generate a coverage report only for the
files specified in the `coverage.src` property, even when files used by the
current target were also instrumented by a previous target. See the related
[bug report](https://github.com/asciidisco/grunt-qunit-istanbul/issues/10).

### Usage

```js
qunit: {
  options: {
    '--web-security': 'no',
    coverage: {
      disposeCollector: true,
      src: ['src/js/**/*.js'],
      instrumentedFiles: 'temp/',
      htmlReport: 'report/coverage',
      coberturaReport: 'report/',
      linesThresholdPct: 85
    }
  },
  all: ['test/**/*.html']
}
```

---

Original Task by ["Cowboy" Ben Alman](http://benalman.com/)

Modified by [asciidisco](http://twitter.com/asciidisco)
