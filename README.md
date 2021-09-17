# Drupal Code Quality Checker
---

## Overview

Provides set of libraries to easily setup code quality checks based on [GrumPHP](https://github.com/phpro/grumphp) for Drupal module/theme/profile. Check out this [Lullabot article](https://www.lullabot.com/articles/how-enforce-drupal-coding-standards-git) for more details.

>*Note:* This library aim to help contributed/custom Drupal module/theme/profile hosted in individual git repository.


## Install

1. Add repo to `composer.json` as 

```
"repositories": [{
     "type": "vcs",
     "url": "git@github.com:OAPI-Commercial-IT/all-in-one-code-checker.git"
 }]
```
 
1. Run `composer require oapi-commercial-it/all-in-one-code-checker`
 
1. Copy `grumphp.yml` in project's root directory (not Drupal root directory) with `grumphp.yml.dist`

1. Adjust config in `grumphp.yml`

1. Run `npm init` (optional)

1. Run `npm install dallask-all-in-one-code-checker`

1. If you do not see needed scripts in your package.json file, just copy them from file: ./node_modules/dallask-all-in-one-code-checker/package.json

```
"scripts": {
     "stylelint": "stylelint '**/*.scss'",
     "stylelint:fix": "stylelint '**/*.scss' --fix",
     "prettier": "prettier '**/*' --check",
     "prettier:fix": "prettier '**/*' --write",
     "eslint": "eslint '**/*.js'",
     "eslint:fix": "eslint '**/*.js' --fix"
   }
```

That's it. Now, all tasks (listed below) run on every `git commit`.

>*Note:* As part of install, GrumPHP adds `pre-commit` hook to repository. Existing `pre-commit` might get [destroyed](https://github.com/phpro/grumphp/issues/416) when install/uninstall.

## Features

1. [PHPCS](https://github.com/squizlabs/PHP_CodeSniffer) with Drupal standard.
1. [PHP Lint](http://www.icosaedro.it/phplint/)
1. [YAML Lint](http://www.yamllint.com/)
1. [Composer](https://github.com/composer/composer)
1. [Composer Normalize](https://github.com/ergebnis/composer-normalize)
1. [JSONLint](https://jsonlint.com/)
1. [PHP Copy/Paste Detector (CPD)](https://github.com/sebastianbergmann/phpcpd)

Long list of additional checks/validators available [here](https://github.com/phpro/grumphp/blob/master/doc/tasks.md#tasks-1).

## NPM Scripts

You can use next scripts to check and fix your files:

    sasslint
    sasslint:fix
    prettier
    prettier:fix
    eslint
    eslint:fix 
   
    Just run `npm run script_name` in root directory.

## Usage

To start from CLI use `./vendor/bin/grumphp run`. It will check only files added by `git add`.
