Sass-versioning
===============

> Version your sass modules and test them at compile time


### Content

* [Usage](#usage)
* [Test](#test)
* [Release History](#release-history-remote)
* [License](#license)


----------------------------------------------------------------------------------------------------------------------------------------------------------------


### Usage

If you have multiple versioned Sass modules and need to defined dependencies amongst them, this is for you.

Imagine you have three modules:

- core `v2.0.0`
- grid `v1.1.0`
- accordion `v1.0.0`

Each of these come with interdependencies and we need to check for conflicts. Like if accordion was dependent on core `v1.0.0` or on an entirely different
module that we don't even have in our Sass.

To make sure this works we need to *register each module* and at the end *check for conflicts* and throw errors on compile time.

### Register

To register a module you need three parameter and call the `versioning-add` mixin.

```scss
$name: "accordion";   //the name of this module
$version: "1.0.0";    //the version of this module
                      //all dependencies of that module
                      //this module depends on a module named "core" at version "2.0.0"
                      //this module depends on a module named "grid" at version "1.0.0"
$dependencies: (
	("core", "2.0.0"),
	("grid", "1.0.0"),
);

@include versioning-add( $name, $version, $dependencies ); //call the mixin
```

If your module has no dependencies you can simply leave the `$dependencies` empty. That would look like this:

```scss
$name: "core";
$version: "2.0.0";
$dependencies: ();  //no dependencies

@include versioning-add( $name, $version, $dependencies );
```

### Check for conflicts

At the very bottom of your Sass file you must include the `versioning-check()` mixin so Sass-versioning can check for you for conflicts.

```scss
@include versioning-check();
```

This mixin will throw an descriptive `@error` if it finds a conflicts.


**[⬆ back to top](#content)**


----------------------------------------------------------------------------------------------------------------------------------------------------------------


### Test

To test run `npm test` in the project folder. The test script will run over each `*.scss` file inside the `./test/` folder. Each of those files has a comment
at the very first line of the file that looks like this:

```scss
// expected: [expected error message]

.some-css {} //etc
```

The test script will compare the error message found here `[expected error message]` against what [node-sass](https://github.com/sass/node-sass) outputs.


**[⬆ back to top](#content)**


----------------------------------------------------------------------------------------------------------------------------------------------------------------


### Release History remote

* v0.1.0 - Initial starting point

**[⬆ back to top](#content)**


----------------------------------------------------------------------------------------------------------------------------------------------------------------


### License

Copyright (c) Dominik Wilkowski. Licensed under the [GNU GPLv3](https://raw.githubusercontent.com/dominikwilkowski/sass-versioning/master/LICENSE).

**[⬆ back to top](#content)**

# };