# Moving to modern C++

## item 7 Distinguish between () and {} when creating objects

- Braced initialization is the most widely initialization syntax, it prevents narrowing conversions, and it's immune to C++'s most vexing parse.
- During constructor overload resolution, braced initializers are matched to std::initializer_list parameters if at all possible, even it other constructors offer seemingly better matches.
- An example of where the choice between parentheses and braces can make a significant difference is creating a std::vector<*numeric type*> with two arguments.
- Choosing between parentheses and braces for object creation inside templates can be challenging.

## item 8 Prefer nullptr to 0 and NULL

- Prefer nullptr to 0 and NULL;
- Avoid overloading on integral and pointer types.

## item 9 Prefer alias declarations to typedefs

- typedefs don't support templatization, but alias declarations do.
- Alias templates avoid the "::type" suffix and, in templates, the "typename" prefix often required to refer to typedefs.
- C++14 offers alias templates for all the C++11 type traits transformations.

## item 10 Prefer scoped enums to unscoped enums

- C++98-style enums are now known as unscoped enums.
- Enumerators of scoped enums are visible only within the enum. They convert to other types only with a cast.
- Both scoped and unscoped enums support specification of the underlying type. The default underlying type for scoped enums is int. Unscoped enums have no default underlying type.
- Scoped enums may alway be forward-declared only if their declaration specifies an underlying type.

## item 11 Prefer deleted functions to private undefined ones

- Prefer deleted functions to private undefined ones.
- Any function may be deleted, including non-member functions and template instantiations.

## item 12 Declare overriding functions override

- Declare overriding functions override.
- Member function reference qualifiers make it possible to treat lvalue and rvalue objects(*this) differently.

## item 13 Prefer const_iterators to iterators

- Prefer const_iterator to iterators
- In maximally generic code, prefer non-member versions of begin, end, rbegin, etc., over their member functions counterparts.

## item 14 Declare functions noexcept if they won't emit exceptions

- noexcept is part of a function's interface, and that means that callers may depend on it.
- noexcept functions are more optimizable than non-noexcept functions.
- noexcept is particularly valuable for the move operations, swap, memory deallocation functions, and destructors.
- Most functions are exception-neutral rather than noexcept.

## item 15 use constexpr whenever possible

- constexpr objects are const and are initialized with values known during compilation.
- constexpr functions can produce compile-time result when called with arguments whose values are known during compilation.
- constexpr objects and functions may be used in a wider range of contexts than non-constexpr objects and functions.
- constexpr is part of an object's or function's interface.

## item 16 Make const member functions thread safe

- Make const member functions thread safe unless you're certain they'll never be used in a concurrent context.
- Use of std::atomic variables may offer better performance than a mutex, but they're suited for manipulation of only a single variable or memory location.

## item 17 Understand special member function generation

- The special member functions are those compilers may generate on their own: default constructor, destructor, copy operations, and move operations.
- Move operations are generated only for classes lacking explicitly declared move operations, copy operations, and a destructor.
- The copy constructor is generated only for classes lacking an explicitly declared copy constructor, and it's deleted if a move operations is declared. The copy assignment operator is generated only for classes lacking an explicitly declared copy assignment operator, and it's deleted if a move operation is declared. Generation of the copy operations in classes with an explicitly declared destructor is deprecated.
- Member function templates never suppress generation of special member functions.
