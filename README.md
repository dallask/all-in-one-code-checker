# Drupal Code Quality Checker
---

## Overview

Provides set of libraries to easily setup code quality checks based on [GrumPHP](https://github.com/phpro/grumphp) for Drupal module/theme/profile. Check out this [Lullabot article](https://www.lullabot.com/articles/how-enforce-drupal-coding-standards-git) for more details.

>*Note:* This library aim to help contributed/custom Drupal module/theme/profile hosted in individual git repository.


## Install

1. Run `composer require dallask/all-in-one-code-checker`
 
1. Copy `grumphp.yml` in project's root directory (not Drupal root directory) with `grumphp.yml.dist`

1. Adjust config in `grumphp.yml`

1. Run `npm init` (optional)

1. Run `npm install dallask-all-in-one-code-checker`

1. If you do not see needed scripts in your package.json file, just copy them from file: ./node_modules/dallask-all-in-one-code-checker/package.json

```
"scripts": {
    "grumphp": "./vendor/bin/grumphp run",
        "phpcs:total": "./vendor/bin/phpcs --standard=Drupal --extensions=php,module,inc,install,test,profile .",
        "phpcs:current": "./vendor/bin/phpcs --standard=Drupal --extensions=php,module,inc,install,test,profile $(git diff --name-status | grep -v \"^[RD]\" | awk '{ print $2 }')",
        "phpcs:total:fix": "./vendor/bin/phpcbf --standard=Drupal --extensions=php,module,inc,install,test,profile .",
        "phpcs:current:fix": "./vendor/bin/phpcbf --standard=Drupal --extensions=php,module,inc,install,test,profile $(git diff --name-status | grep -v \"^[RD]\" | awk '{ print $2 }')",
        "stylelint:total": "stylelint '**/*.scss'",
        "stylelint:current": "stylelint $(git diff --name-status | grep '\\.scss$' | grep -v \"^[RD]\" | awk '{ print $2 }')",
        "stylelint:total:fix": "stylelint '**/*.scss' --fix",
        "stylelint:current:fix": "stylelint --fix $(git diff --name-status | grep '\\.scss$' | grep -v \"^[RD]\" | awk '{ print $2 }')",
        "prettier:total": "prettier '**/*' --check",
        "prettier:current": "prettier --check $(git diff --name-status | grep '\\.scss$\\|\\.js$' | grep -v \"^[RD]\" | awk '{ print $2 }')",
        "prettier:total:fix": "prettier '**/*' --write",
        "prettier:current:fix": "prettier --write $(git diff --name-status | grep '\\.scss$\\|\\.js$' | grep -v \"^[RD]\" | awk '{ print $2 }')",
        "eslint:total": "eslint '**/*.js'",
        "eslint:current": "eslint $(git diff --name-status | grep '\\.js$' | grep -v \"^[RD]\" | awk '{ print $2 }')",
        "eslint:total:fix": "eslint '**/*.js' --fix",
        "eslint:current:fix": "eslint --fix $(git diff --name-status | grep '\\.js$' | grep -v \"^[RD]\" | awk '{ print $2 }')"
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

    grumphp - total grumphp check according to your grumphp.yml config
        
    PHPCS:
    phpcs:total - total phpcs check for all project files
    phpcs:total:fix - total phpcbf fix for all project files
    phpcs:current - phpcs check for project files that were changed
    phpcs:current:fix - phpcbf fix for project files that were changed
    
    Stylelint:
    stylelint:total - stylelint check for all project files
    stylelint:total:fix - stylelint fix for all project files
    stylelint:current - stylelint check for project files that were changed
    stylelint:current:fix - stylelint fix for project files that were changed
    
    Prettier:
    prettier:total - prettier check for all project files
    prettier:total:fix - prettier fix for all project files
    prettier:current - prettier check for project files that were changed
    prettier:current:fix - prettier fix for project files that were changed
    
    ESLint:
    eslint:total - eslint check for all project files
    eslint:total:fix - eslint fix for all project files
    eslint:current - eslint check for project files that were changed
    eslint:current:fix - prettier fix for project files that were changed
   
    Just run `npm run script_name` in root directory.

## Composer scripts

You can use next composer scripts to check and fix your files (just copy them from the composer.json file to your project composer.json and modify options if it needed):

```
"scripts": {
        "post-install-cmd": [
            "npm install"
        ],
        "post-update-cmd": [
            "npm install"
        ],
        "grumphp": "./vendor/bin/grumphp run",
        "phpcs:total": "./vendor/bin/phpcs --standard=Drupal --extensions=php,module,inc,install,test,profile .",
        "phpcs:current": "./vendor/bin/phpcs --standard=Drupal --extensions=php,module,inc,install,test,profile $(git diff --name-status | grep -v \"^[RD]\" | awk '{ print $2 }')",
        "phpcs:total:fix": "./vendor/bin/phpcbf --standard=Drupal --extensions=php,module,inc,install,test,profile .",
        "phpcs:current:fix": "./vendor/bin/phpcbf --standard=Drupal --extensions=php,module,inc,install,test,profile $(git diff --name-status | grep -v \"^[RD]\" | awk '{ print $2 }')",
        "stylelint:total": "./node_modules/.bin/stylelint '**/*.scss'",
        "stylelint:current": "./node_modules/.bin/stylelint $(git diff --name-status | grep '\\.scss$' | grep -v \"^[RD]\" | awk '{ print $2 }')",
        "stylelint:total:fix": "./node_modules/.bin/stylelint '**/*.scss' --fix",
        "stylelint:current:fix": "./node_modules/.bin/stylelint --fix $(git diff --name-status | grep '\\.scss$' | grep -v \"^[RD]\" | awk '{ print $2 }')",
        "prettier:total": "./node_modules/.bin/prettier '**/*' --check",
        "prettier:current": "./node_modules/.bin/prettier --check $(git diff --name-status | grep '\\.scss$\\|\\.js$' | grep -v \"^[RD]\" | awk '{ print $2 }')",
        "prettier:total:fix": "./node_modules/.bin/prettier '**/*' --write",
        "prettier:current:fix": "./node_modules/.bin/prettier --write $(git diff --name-status | grep '\\.scss$\\|\\.js$' | grep -v \"^[RD]\" | awk '{ print $2 }')",
        "eslint:total": "./node_modules/.bin/eslint '**/*.js'",
        "eslint:current": "./node_modules/.bin/eslint $(git diff --name-status | grep '\\.js$' | grep -v \"^[RD]\" | awk '{ print $2 }')",
        "eslint:total:fix": "./node_modules/.bin/eslint '**/*.js' --fix",
        "eslint:current:fix": "./node_modules/.bin/eslint --fix $(git diff --name-status | grep '\\.js$' | grep -v \"^[RD]\" | awk '{ print $2 }')"
    }
```


    grumphp - total grumphp check according to your grumphp.yml config
    
    PHPCS:
    phpcs:total - total phpcs check for all project files
    phpcs:total:fix - total phpcbf fix for all project files
    phpcs:current - phpcs check for project files that were changed
    phpcs:current:fix - phpcbf fix for project files that were changed
    
    Stylelint:
    stylelint:total - stylelint check for all project files
    stylelint:total:fix - stylelint fix for all project files
    stylelint:current - stylelint check for project files that were changed
    stylelint:current:fix - stylelint fix for project files that were changed
    
    Prettier:
    prettier:total - prettier check for all project files
    prettier:total:fix - prettier fix for all project files
    prettier:current - prettier check for project files that were changed
    prettier:current:fix - prettier fix for project files that were changed
    
    ESLint:
    eslint:total - eslint check for all project files
    eslint:total:fix - eslint fix for all project files
    eslint:current - eslint check for project files that were changed
    eslint:current:fix - prettier fix for project files that were changed
   
    Just run `composer run-script script_name` in root directory.

## Usage

* To start from CLI use `./vendor/bin/grumphp run`. It will check only files added by `git add`.
* Just follow [GrumPHP](https://github.com/phpro/grumphp) documentation
