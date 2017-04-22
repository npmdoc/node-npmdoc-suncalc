# npmdoc-suncalc

#### api documentation for  [suncalc (v1.8.0)](https://github.com/mourner/suncalc)  [![npm package](https://img.shields.io/npm/v/npmdoc-suncalc.svg?style=flat-square)](https://www.npmjs.org/package/npmdoc-suncalc) [![travis-ci.org build-status](https://api.travis-ci.org/npmdoc/node-npmdoc-suncalc.svg)](https://travis-ci.org/npmdoc/node-npmdoc-suncalc)

#### A tiny JavaScript library for calculating sun/moon positions and phases.

[![NPM](https://nodei.co/npm/suncalc.png?downloads=true&downloadRank=true&stars=true)](https://www.npmjs.com/package/suncalc)

- [https://npmdoc.github.io/node-npmdoc-suncalc/build/apidoc.html](https://npmdoc.github.io/node-npmdoc-suncalc/build/apidoc.html)

[![apidoc](https://npmdoc.github.io/node-npmdoc-suncalc/build/screenCapture.buildCi.browser.%252Ftmp%252Fbuild%252Fapidoc.html.png)](https://npmdoc.github.io/node-npmdoc-suncalc/build/apidoc.html)

![npmPackageListing](https://npmdoc.github.io/node-npmdoc-suncalc/build/screenCapture.npmPackageListing.svg)

![npmPackageDependencyTree](https://npmdoc.github.io/node-npmdoc-suncalc/build/screenCapture.npmPackageDependencyTree.svg)



# package.json

```json

{
    "author": {
        "name": "Vladimir Agafonkin"
    },
    "bugs": {
        "url": "https://github.com/mourner/suncalc/issues"
    },
    "dependencies": {},
    "description": "A tiny JavaScript library for calculating sun/moon positions and phases.",
    "devDependencies": {
        "eslint": "^3.12.2",
        "eslint-config-mourner": "^2.0.1",
        "tap": "^8.0.1"
    },
    "directories": {},
    "dist": {
        "shasum": "1d9898109563078750f4994a959e654d876acbf5",
        "tarball": "https://registry.npmjs.org/suncalc/-/suncalc-1.8.0.tgz"
    },
    "eslintConfig": {
        "extends": "mourner",
        "rules": {
            "indent": 0,
            "array-bracket-spacing": 0,
            "strict": 0,
            "brace-style": 0
        },
        "env": {
            "amd": true
        }
    },
    "gitHead": "b08d1f6f8e56a3c0d85469d6cf0ff8675cba40a5",
    "homepage": "https://github.com/mourner/suncalc",
    "jshintConfig": {
        "quotmark": "single",
        "trailing": true,
        "unused": true
    },
    "keywords": [
        "sun",
        "astronomy",
        "math",
        "calculation",
        "sunrise",
        "sunset",
        "twilight",
        "moon",
        "illumination"
    ],
    "main": "suncalc.js",
    "maintainers": [
        {
            "name": "mourner"
        }
    ],
    "name": "suncalc",
    "optionalDependencies": {},
    "repository": {
        "type": "git",
        "url": "git://github.com/mourner/suncalc.git"
    },
    "scripts": {
        "cov": "tap test.js --cov",
        "pretest": "eslint suncalc.js test.js",
        "test": "tap test.js"
    },
    "version": "1.8.0",
    "bin": {}
}
```



# misc
- this document was created with [utility2](https://github.com/kaizhu256/node-utility2)
