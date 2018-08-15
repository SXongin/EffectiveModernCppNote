# Moving to modern C++

## item 7 Distinguish between () and {} when creating objects

- Braced initialization is the most widely initialization syntax, it prevents narrowing conversions, and it's immune to C++'s most vexing parse.
- During constructor overload resolution, braced initializers are matched to std::initializer_list parameters if at all possible, even it other constructors offer seemingly better matches.
- An example of where the choice between parentheses and braces can make a significant difference is creating a std::vector<*numeric type*> with two arguments.
- Choosing between parentheses and braces for object creation inside templates can be challenging.

## item 8 Prefer nullptr to 0 and NULL

- Prefer nullptr to 0 and NULL;
- Avoid overloading on integral and pointer types.

## item 9 Prefer alias declarations to typedefs.

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
- in Maximally generic code, prefer non-member versions of begin, end, rbegin, etc., over their member functions counterparts.

## item 14 Declare functions noexcept if they won't emit exceptions
