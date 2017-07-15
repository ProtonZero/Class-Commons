Libraries implementing Class Commons 2.0
========================================

The library MUST inspect `package.loaded["class.commons"]`, and if it is `nil` then the library MUST populate it with a table which MUST provide the two functions `class` and `instance` as defined below.

## class

	class = function (name, class, superclass)

This MUST return a class, and it SHOULD NOT set it as a global. It SHOULD NOT set any special functions, such as metamethods, based on the class's members.

A class SHOULD be considered read-only after having been passed to `class`. Implementations MAY ignore any changes after the class has been created.

Explanation of arguments:

 * `name` The name of the class; this value MAY be used by an implementation.
 * `class` The class table.
 * `superclass` Optional superclass.

## instance

	instance = function (class, ...)

This MUST return an instance of the given class, initialized with `instance:init(...)` if defined.

Libraries using Class Commons 2.0
=================================

Any library using Class Commons 2.0 <span style="font-variant:small-caps">must</span> probe for its existence using `pcall(require, "class.commons")`.

In case it is absent it MAY error, or it MAY use its own class implementation. In either case, it MUST be reset to its initial value (which MAY be assumed to be `nil`) when the library finishes loading.
