# grunt-plovr-extended

> Grunt plugin wrapper for google closure tool plovr - includes all Features without the need of an external config File for Plovr

## Getting Started
This plugin requires Grunt `~0.4`

If you haven't used [Grunt](http://gruntjs.com/) before, be sure to check out the [Getting Started](http://gruntjs.com/getting-started) guide, as it explains how to create a [Gruntfile](http://gruntjs.com/sample-gruntfile) as well as install and use Grunt plugins. Once you're familiar with that process, you may install this plugin with this command:

```shell
npm install grunt-plovr-extended --save-dev
```

Once the plugin has been installed, it may be enabled inside your Gruntfile with this line of JavaScript:

```js
grunt.loadNpmTasks('grunt-plovr-extended');
```

## The "plovr_extended" task

### Overview
In your project's Gruntfile, add a section named `plovr_extended` to the data object passed into `grunt.initConfig()`.

```js
grunt.initConfig({
  plovr_extended: {
    options: {
      // Task-specific options go here.
    },
    your_target: {
      // Target-specific file lists and/or options go here.
    },
  },
});
```

### Options

Generally, you can use every option plovr supports.

#### source-map-base-url
Type: `String`

#### module-source-map-name
Type: `String`

#### create_source_map
Type: `String`

#### location-mapping
Type: `Object`

```js
{'0.0.0.1/': '/0.0.0.1/app/'}
```
Rename each 0.0.0.1 to /0.0.0.1/app/ in every sourcemap.


### Usage Examples

#### Default Options
In this example, the default options are used to do something with whatever. So if the `testing` file has the content `Testing` and the `123` file had the content `1 2 3`, the generated result would be `Testing, 1 2 3.`

```js
grunt.initConfig({
  plovr_extended: {
    options: {},
    src: ['src/testing', 'src/123'],
    dest: ['dest/output.js']
  },
});
```

#### Custom Options
In this example, custom options are used to do something else with whatever else. So if the `testing` file has the content `Testing` and the `123` file had the content `1 2 3`, the generated result in this case would be `Testing: 1 2 3 !!!`

```js
grunt.initConfig({
  plovr_extended: {
    options: {
        id: 'yourid',
        paths: '["ownextensionpath"]',
        mode: 'ADVANCED',
        debug: true,
        "output-wrapper": '"// Copyright \n(function(){%output%})();"',
        define: { "goog.DEBUG": false },
        checks: { "checkTypes": "OFF",
                  "fileoverviewTags": "OFF",
                  "nonStandardJsDocs": "OFF",
                  "ambiguousFunctionDecl": "OFF",
                  "globalThis": "ERROR",
                  "externsValidation": "OFF"
                }
    },
    src: ['src/testing', 'src/123'],
    dest: ['dest/output.js']
  },
});
```


#### Example Angular Application
```js
grunt.initConfig({
    plovr_extended: {
    cwd: path.join('inputs'),
    options: {
        id: 'app',
        paths: path.join('paths'),
        externs: [
            path.join('node_modules', 'closure-compiler', 'node_modules',
              'google-closure-compiler', 'contrib', 'externs', 'angular-1.4.js'),
            path.join('node_modules', 'closure-compiler', 'node_modules',
              'google-closure-compiler', 'contrib', 'externs', 'angular-1.4-http-promise_templated.js'),
            path.join('node_modules', 'closure-compiler', 'node_modules',
              'google-closure-compiler', 'contrib', 'externs', 'angular-1.4-mocks.js'),
            path.join('node_modules', 'closure-compiler', 'node_modules',
              'google-closure-compiler', 'contrib', 'externs', 'angular-1.4-q_templated.js')
        ],
        mode: 'ADVANCED',
        debug: false,
        define: {
            'goog.DEBUG': false
        },
        checks: {
            checkDebuggerStatement: 'ERROR',
            checkRegExp: 'OFF',
            checkTypes: 'ERROR',
            checkVars: 'ERROR',
            closureDepMethodUsageChecks: 'ERROR',
            conformanceViolations: 'ERROR',
            const: 'ERROR',
            constantProperty: 'ERROR',
            deprecated: 'ERROR',
            deprecatedAnnotations: 'ERROR',
            duplicate: 'ERROR',
            es3: 'ERROR',
            extraRequire: 'ERROR',
            fileoverviewTags: 'ERROR',
            globalThis: 'ERROR',
            internetExplorerChecks: 'ERROR',
            invalidCasts: 'ERROR',
            misplacedTypeAnnotation: 'ERROR',
            missingProperties: 'OFF',
            missingProvide: 'ERROR',
            missingRequire: 'ERROR',
            missingReturn: 'ERROR',
            newCheckTypes: 'ERROR',
            nonStandardJsDocs: 'ERROR',
            reportUnknownTypes: 'OFF',
            strictModuleDepCheck: 'ERROR',
            suspiciousCode: 'ERROR',
            undefinedNames: 'ERROR',
            undefinedVars: 'ERROR',
            unknownDefines: 'ERROR',
            uselessCode: 'ERROR',
            violatedModuleDep: 'ERROR',
            visibility: 'ERROR'
        },
        'experimental-compiler-options': {
            languageIn: 'ECMASCRIPT5_STRICT',
            angularPass: true,
            colorizeErrorOutput: true,
            generateExports: true,
            removeUnusedPrototypePropertiesInExterns: false,
            externExports: true,
            removeUnusedPrototypeProperties: false
        },
        'source-map-base-url': path.join('urlPath'),
        'module-source-map-name': '/%s.advanced.min.js.map',
        'module-output-path': path.join('urlPath') + '/%s.advanced.min.js',
        'module-production-uri': path.join('urlPath') + '/%s.advanced.min.js',
        create_source_map: path.join('systemPath'),
        'location-mapping': {'0.0.0.1/': '/0.0.0.1/app/'},
        modules: {
            app: {
                inputs: path.join('app.js'),
                deps: []
            }
        }
    }
});
```

## Contributing
In lieu of a formal styleguide, take care to maintain the existing coding style. Add unit tests for any new or changed functionality. Lint and test your code using [Grunt](http://gruntjs.com/).

## Release History
1.0.0 -> Update plovr.jar and add options to gernerate source_maps for each module or standalone app.
