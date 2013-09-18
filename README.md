lua-compat-5.2
==============

Compatibility module providing Lua-5.2-style APIs for Lua 5.1.

What is it
----------

This is a small module that aims to make it easier to write Lua code
in a Lua-5.2-style that runs on both Lua 5.1 and Lua 5.2. This does *not*
make Lua 5.1 entirely compatible with Lua 5.2, but it brings the API
closer to that of Lua 5.2.

How to use it
-------------

```lua
require("compat52")
```

You have to launch it like this (instead of the usual idiom of storing
the return of `require` in a local variable) because compat52 needs to
make changes to your global environment.

When run under Lua 5.2, this module does nothing.

When run under Lua 5.1, it replaces some of your standard functions and
adds new ones to bring your environment closer to that of Lua 5.2.

You may also use the "strict mode" which removes from Lua 5.1 functions
that were deprecated in 5.2; that is the equivalent of running Lua 5.2
with the LUA_COMPAT_ALL flag disabled:

```lua
require("compat52.strict")
```

What's implemented
------------------

* `load` and `loadfile`
* `table.pack` and `table.unpack`
* `string` patterns may contain embedded zeros
* `string.rep` accepts sep argument
* `string.format` calls `tostring` on arguments for `%s`
* `math.log` accepts base argument
* `xpcall` takes additional arguments
* metamethods for `pairs` and `ipairs`
* `rawlen` (but `#` still doesn't respect `__len` for tables)
* `package.searchers`
* `package.searchpath`
* `coroutine` functions dealing with the main coroutine 
* return code of `os.execute`
* `io.write` and `file:write` return file handle
* `io.lines` and `file:lines` accept format arguments (like `io.read`)
* `bit32` (actually uses bit32 available from LuaRocks as a dependency)
* optional strict mode which removes functions removed or deprecated in
  Lua 5.2, such as `setfenv` and `getfenv`

What's not implemented
----------------------

* C APIs
* _ENV
* obviously, this does not turn Lua 5.1 into Lua 5.2: syntactic changes
  to the core language, such as the `goto`   statement, and semantic
  changes such as ephemeron support for weak tables, remain unavailable.
* anything else missing in the Lua libraries?

See also
--------

* For more information about compatibility between Lua versions, see
[Compatibility With Lua
Five](http://lua-users.org/wiki/CompatibilityWithLuaFive) at the Lua-Users
wiki
* For Lua-5.1-style APIs under Lua 5.0, see
[Compat-5.1](http://keplerproject.org/compat/)
* for C support in the opposite direction (ie, loading C code using
Lua-5.1-style APIs under Lua 5.2), see
[Twoface](http://corsix.github.io/twoface/)

