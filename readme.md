# Foobar for PHP 8

Serves package testing purposes only... obviously.

>
> 💿 `composer require foobar/foobar8`
>

## Usage

When migrating from a package to another, it may be useful to know that composer schema (i.e. `composer.json`) may contain `replace` property.

The schema of this package is (abridged):
```json
{
  "name": "foobar/foobar8",
  "require": {
    "php": "^8"
  },
  "replace": {
    "foobar/foobar7": "*"
  }
}
```
Where `replace` indicates that `foobar/foobar8` completely replaces `foobar/foobar7`,
allowing Composer to consider `foobar/foobar8` as a drop-in replacement for `foobar/foobar7`.

Prop `replace` creates an implicit `conflict` rule, and is also more useful than `provide`, which serves different purpose (to implement virtual interfaces).

Read the Composer schema docs here: [Composer `replace`](https://getcomposer.org/doc/04-schema.md#replace).


## Migration

Prerequisites (or current state):
- project running on PHP 7
- `foobar/foobar7` installed (i.e. required by the project)

Migration:
1. switch to PHP 8
2. `composer require foobar/foobar8`
3. (optional) remove `foobar/foobar7` requirement

This will satisfy all the other libraries that depend on `foobar/foobar7`, too, not just the project itself.

One should end up with something like this:
```json
{
  "type": "project",
  "require": {
    "php": "^8",
    "foobar/foobar7": "^1",
    "foobar/foobar8": "^1"
  }
}
```

Useful when reimplementing older libraries or providing backport versions for older architectures.

It may be useful in other scenarios too, when reimplementing third party libraries.  
An example would be a library that is slow to be maintained, but a serious flaw is found.
One may source and distribute the patch himself and only replace a certain version.
Once the third party package is updated, it will be used again, without need for changes to the consuming project.

> Note that the replacing works not only across PHP versions. One may replace any package, or even selected versions of a package.
