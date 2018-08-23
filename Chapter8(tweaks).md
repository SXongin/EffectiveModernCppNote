# Tweaks

## item 41 Consider pass by value for copyable parameters that are cheap to move and always copied

- For copyable, cheap-to-move parameters that are always copied, pass by value may be nearly as efficient as pass by reference, it's easier to implement, and it can generate less object code.
- Copying parameters via construction may be significantly more expensive than copying them via assignment.(ps:? maybe construction must alloc memory?)
- Pass by value is subject to slicing problem, so it's typically inappropriate for base class parameter types.

## item 42 Consider emplacement instead of insertion

- In principle, emplacement functions should sometimes be more efficient than their insertion counterparts, and they should never be less efficient.
- In practice, they're most likely to be faster when (1) the value being added is constructed into the container, not assigned; (2) the argument type(s) passed differ from the type held by the container; and (3) the container won't reject the value being added due to it being a duplicate.
- Emplacement functions may perform type conversions than would be rejected by insertion functions.(ps:? explicit doesn't reject implicit conversion in direct initialization?)
