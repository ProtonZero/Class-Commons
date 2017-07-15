Libraries implementing Class Commons
====================================

Any library implementing this interface MUST comply to the following:

It MUST listen to the global variable `common_class`:

It MUST provide the interface if that variable is true. It MUST NOT provide the interface if that variable is false. It MAY provide the interface if the variable is nil.

It <span style="font-variant:small-caps">must</span> populate `package.loaded["class.commons"]` with a table which <span style="font-variant:small-caps">must</span> provide the two functions `class` and `instance` as defined below.

	class = function (name, class, superclass)

This <span style="font-variant:small-caps">must</span> return a class, it <span style="font-variant:small-caps">should not</span> set it as a global. It <span style="font-variant:small-caps">should not</span> set any special functions such as metamethods.

A class <span style="font-variant:small-caps">should</span> be considered read-only after having been passed to `class`. Implementations <span style="font-variant:small-caps">may</span> ignore any changes after the class has been created.

Explanation of arguments:

 * `name` The name of the class; this value <span style="font-variant:small-caps">may</span> be used by an implementation.
 * `class` The class table.
 * `superclass` Optional superclass.


	instance = function (class, ...)

This <span style="font-variant:small-caps">must</span> return an instance of the given class, initialized with `instance:init(...)` if defined.

Libraries using Class Commons
=============================

Any library using Class Commons <span style="font-variant:small-caps">must</span> probe for its existence using `pcall(require, "class.commons")`.

In case it is absent it <span style="font-variant:small-caps">may</span> error, or it <span style="font-variant:small-caps">may</span> use its own class implementation. In either case, it <span style="font-variant:small-caps">must not</span> do anything else.

If it ships its own implementation, the `common` table MUST be reset to its
initial value (which MAY be assumed to be `nil`) when the library finishes
loading.
Furthermore, this implementation MAY implement all of the specification, but it
does not have to, but it MUST be enough to use the library itself.
