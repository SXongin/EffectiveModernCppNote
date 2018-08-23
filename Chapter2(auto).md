# auto

## item 5 prefer auto to explicit type declarations

- auto variables must be initialized, are generally immune to type mismatches that can lead to portability or efficiency problems, can ease the process of refactoring, and typically require less typing than variables with explicitly specified types.
- auto-typed variables are subject to the pitfalls described in Item 2 and 6.

## item 6 Use the explicitly typed initializer idiom when auto deduces undesired types

- "Invisible" proxy types can cause auto to deduce the "wrong" type for a initializing expression.
- The explicitly typed initializer idiom forces auto to deduce the type you want it to have.(ps: usually use static_cast<>)
