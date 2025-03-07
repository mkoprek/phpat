# Changelog
All notable changes to this project will be documented in this file.

## v0.7.7
* Do not analyze excluded files ([+info](https://github.com/carlosas/phpat/pull/157#issuecomment-967341532))

## v0.7.6
* Move CI to GitHub Actions
* Optimize FullClassName usage

## 0.7.5
* Fix random silent failures while creating internal php classmap
* Fix test file valid names
* Set default verbosity on invalid configuration

## 0.7.4
* Fix exclusions when they are not part of the src
* Allow to include test files with more valid names

## 0.7.3
* Change composer package name to `phpat/phpat`
* Refactor AST build to a better-reflection/php-parse hybrid
* Add support to generic types in docs
* Add support to callable types in docs
* Add support to union types in docs
* Fix src path configuration sometimes giving issues
* Drop Symfony 2 compatibility
* Move Fatal Error exceptions out of event listener
* Fix issue with FQCNs starting with backslash
* Add psalm and phpstan to CI checks

## 0.7.2
* Move composer parsing to ReferenceMap creation stage
* Include unknown FQCNs (out of src) in ClassNameSelector

## 0.7.1
* Fix composer dependencies with empty namespace selected as `*`

## 0.7.0
* Package name changed to `phpat/phpat`
* Add support for tests in YAML and XML files
* Ignore only core and extension classes (instead of all classes without namespace)
* Add `ignore_php_extensions` option
* Change `ignore_docblocks` option name
* Change the configuration needed for composer selectors:
```yaml
# phpat.yaml
composer:
  your-package-name:
    json: path-to-composer.json
    lock: path-to-composer.lock
```
* Modify `ComposerSourceSelector` and `ComposerDependencySelector` so:
  * `areAutoloadableFromComposer` selects _non-dev_ composer autoload classes
  * `areDevAutoloadableFromComposer` selects _dev_ composer autoload classes
  * `areDependenciesFromComposer` selects _non-dev_ composer dependencies
  * `areDevDependenciesFromComposer` selects _dev_ composer dependencies

## 0.6.1
* Fix exclusions ignored in non-ast classes
* Add `ComposerSourceSelector` and `ComposerDependencySelector`
```
$this->newRule
    ->classesThat(Selector::areAutoloadableFromComposer('file-composer-json', false))
    ->mustNotDependOn()
    ->classesThat(Selector::areDependenciesFromComposer('file-composer-json', 'file-composer-lock', true))
```

## 0.6.0
* Add selection out of the src scope using full or partial class names
```
$this->newRule
    ->classesThat(Selector::haveClassName('App\*'))
    ->mustNotDependOn()
    ->classesThat(Selector::haveClassName('Symfony\*'))
```
* Add warnings when using regex class names with affirmative `must` assertions
* Fix some docblock types not resolved
* Fix error while using anonymous classes

## 0.5.8
* Add warnings when selectors do not find any class
* Fix group use declarations
* Fix some functions and primitive types resolved as classes
* Ignore dependencies without namespace (predefined PHP classes)

## 0.5.7
* Added support for `*` on _include_ and _exclude_ options
* Fixed ignored _include_ option when using other than PathSelector
* Modified command now looks for default `phpat.yaml` or `phpat.yml` files
* Modified success report character from `·` to `.`

## 0.5.6
* Fixed false exception message shown on violated rules report

## 0.5.4
* Added dry-run to internal errors
* Modified fatal error handler
* Modified executable to match php version requirement
* Fixed _include_ option

## 0.5.3
* Added `CanOnlyImplement` and `MustOnlyImplement` rule types
* Added `CanOnlyInclude` and `MustOnlyInclude` rule type
* Added `CanOnlyDepend` and `MustOnlyDepend` rule types
* Added `CanOnlyExtend` rule type
* Modified statements now check all the defined relations of a class
* Fixed native PHP classes not correctly found

## 0.5.2
* Added `Selector::implementInterface` to select classes that implement a certain interface
* Added `Selector::extendClass` to select classes that extend a certain class
* Added `Selector::includeTrait` to select classes that include a certain trait
* Added some PHP configurations (error_reporting, display_errors, gc_disable)
* Added verbosity as a cli command option
* Fixed options being ignored in configuration files

## 0.5.1
* Added `Selector::haveClassName` to select classes by fully qualified names
* Performance boost by building an AST map instead of parsing each time

## 0.5.0
* Added a changelog :smile:
* Changed Minimum PHP version from `7.1` to `7.2`.
* Changed dependency `symfony/event-dispatcher` to `carlosas/simple-event-dispatcher`.
