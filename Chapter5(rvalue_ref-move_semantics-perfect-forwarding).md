# Rvalue References, Move Semantics, and Perfect Forwarding

## item 23 Understand std::move and std::forward

- std::move performs an unconditional cast to an rvalue. In and of itself, it doesn't move anything.
- std::forward casts its argument to an rvalue only if that argument is bound to an rvalue.
- Neither std::move nor std::forward do anything at runtime.

## item 24 Distinguish universal references from rvalue references

- If a function template parameter has type T&& for a deduced type T, of if an object is declared using auto&&, the parameter or objects is a universal reference.
- If the form of the type declaration isn't precisely type&&, or if type deduction dees not occur, type&& denotes an rvalue reference.
- Universal references correspond to rvalue references if they're initialized with rvalues. They correspond to lvalue references if they're initialized with lvalues.

## item 25 Use std::move on rvalue references, std::forward on universal references

- Apply std::move to rvalue references and std::forward to universal references the last time each is used.
- Do the same thing for rvalue references and universal references being returned from functions that return by value.
- Never apply std::move or std::forward to local objects if they would otherwise be eligible for the return value optimization.

## item 26 Avoid overloading on universal references

- Overloading on universal references almost always leads to the universal reference overload being called more frequently than expected.
- Perfect-forwarding constructors are especially problematic, because they're typically better matches than copy constructors for non-const lvalues, and they can hijack derived class calls to base class copy and move constructors.

## item 27 Familiarize yourself with alternatives to overloading on universal references

- Alternatives to the combination of universal references and overloading include the use of distinct function names, passing parameters by lvalue-reference-to-const, passing parameters by value, and using tag dispatch.
- Constraining templates via std::enable_if permits the use of universal references and overloading together, but it controls the conditions under which compilers may use the universal reference overloads.
- Universal reference parameters often have efficiency advantages, but they typically have usability disadvantages.

## item Understand reference collapsing

- Reference collapsing occurs in four contexts: template instantiation, auto type generation, creation and use of typedefs and alias declarations, and decltype.
- When compilers generate a reference to a reference in a reference collapsing context, the result becomes a single reference. If either or the original references is an lvalue reference, the result is an lvalue reference. Otherwise it's an rvalue reference.
- Universal references are rvalue references in contexts where type deduction distinguishes lvalues from rvalues and where reference collapsing occurs.

## item 29 Assume that move operations are not present, not cheap, and not used

- Assume that move operations are present, not cheap, and not used.
- In code with known types or support for semantics, there is no need for assumptions.

## item 30 Familiarize yourself with perfect forwarding failure cases

- Perfect forwarding fails when template type deduction fails or when it deduces the wrong type.
- The kinds of arguments that lead to perfect forwarding failure are braced initializers, null pointers expressed as 0 or NULL, declaration-only integral const static data members, template and overloaded function names, and bitfields.
