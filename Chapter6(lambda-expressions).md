# Lambda Expressions

## Avoid default capture modes

- Default by-reference capture can lead to dangling references.
- Default by-value capture is susceptible to dangling pointers(especially this), and it misleadingly suggests that lambdas are self-contained.

## item32 Use init capture to move objects into closures

- Use C++14's init capture to move objects into closures.
- In C++11, emulate init capture via hand-written classes or std::bind.

## item 33 Use decltype on auto&& parameters to std::forward them

- Use decltype on auto&& parameters to std::forward them.

## item 34 Prefer lambdas to std::bind

- Lambdas are more readable, more expressive, and may be more efficient than using std::bind.
- In C++11 only, std::bind may be useful for implementing move capture or for binding objects with templatized function call operator.
