# Drupal Code Quality Checker
---

## Overview

Provides set of libraries to easily setup code quality checks based on [GrumPHP](https://github.com/phpro/grumphp) for Drupal module/theme/profile. Check out this [Lullabot article](https://www.lullabot.com/articles/how-enforce-drupal-coding-standards-git) for more details.

>*Note:* This library aim to help contributed/custom Drupal module/theme/profile hosted in individual git repository.


## Install

1. Add all dependencies to `composer.json`
Add repo as 

`"repositories": [{
     "type": "vcs",
     "url": "git@github.com:OAPI-Commercial-IT/all-in-one-code-checker.git"
 }]`
 
2. Copy `grumphp.yml` in project's root directory (not Drupal root directory) with `grumphp.yml.dist`

3. Adjust config in `grumphp.yml`

4. Copy all needed files and configs from root directory (`package.json`, `package-lock.json`, `.eslintrc.js`, etc.) to your root

5. Run `composer install`

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
