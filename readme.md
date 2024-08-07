# Foobar for PHP 8

Serves package testing purposes only... obviously.

>
> 💿 `composer require foobar/foobar8`
>

## Usage

When migrating from a package to another, it may be useful to know that composer schema (i.e. `composer.json`) may contain `replace` and `conflict` properties.

The schema of this package is (abridged):
```json
{
  "name": "foobar/foobar8",
  "require": {
    "php": "^8"
  },
  "conflict": {
    "foobar/foobar7": "*"
  },
  "replace": {
    "foobar/foobar7": "*"
  }
}
```
Where
- `conflict`:
  - Ensures that the `foobar/foobar8` package conflicts with any version of `foobar/foobar7`, preventing both from being installed together.
- `replace`:
  - Indicates that `foobar/foobar8` completely replaces `foobar/foobar7`, allowing Composer to consider `foobar/foobar8` as a drop-in replacement for `foobar/foobar7`.

So, after having installed `foobar/foobar7` on a project with PHP 7,  
then switching to PHP 8 and running `composer update`,  
one should see the package switched to `foobar/foobar8`.

Useful when reimplementing older libraries or providing backport versions for older architectures.

It may be useful in other scenarios too, when reimplementing third party libraries.  
An example would be a library that is slow to be maintained, but a serious flaw is found.
One may source and distribute the patch himself and only replace a certain version.
Once the third party package is updated, it will be used again, without need for changes to the consuming project.
