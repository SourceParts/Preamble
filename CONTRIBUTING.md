# Contributing to Preamble

Thank you for taking the time to contribute! All PRs and feedback are welcome.

## Issues

1. **Include enough context to reproduce.**  
   A clear description, hardware, and what you observed vs. what you expected goes a long way.

2. **Use the issue templates when they fit.**  
   Bug reports and feature requests have templates. Use them if relevant.

## Code style guidelines

1. **Bracket style**  
   1TBS ("javascript" style):

```c++
if (foo) {
  bar();
} else {
  baz();
}
```

2. **Tabs**  
   Use 2 space characters for indentation.

3. **Single-line comments**  
   Start on a new line, one space after `//`, lower-case first letter.

```c++
// this function does something
foo("bar");
```

4. **Split code into blocks**  
   Group related lines with a comment, separated by blank lines.

```c++
// build a temporary buffer
uint8_t* data = new uint8_t[len + 1];
if(!data) {
  return(RADIOLIB_ERR_MEMORY_ALLOCATION_FAILED);
}

// read the received data
state = readData(data, len);
```

5. **Doxygen**  
   New public methods need Doxygen comments so the API reference stays complete.

6. **Keywords**  
   Add new keywords to `keywords.txt` using true tabs (not spaces).

7. **Dynamic memory**  
   Every dynamically allocated array needs a static counterpart for `RADIOLIB_STATIC_ONLY` builds. Free everything you allocate.

```c++
#if defined(RADIOLIB_STATIC_ONLY)
  uint8_t data[RADIOLIB_STATIC_ARRAY_SIZE + 1];
#else
  uint8_t* data = new uint8_t[length + 1];
  if(!data) {
    return(RADIOLIB_ERR_MEMORY_ALLOCATION_FAILED);
  }
#endif

readData(data, length);

#if !defined(RADIOLIB_STATIC_ONLY)
  delete[] data;
#endif
```

8. **God Mode**  
   New classes with private members must include the `RADIOLIB_GODMODE` macro guard:

```c++
class Module {
  void publicMethod();

#if defined(RADIOLIB_GODMODE)
  private:
#endif

  void privateMethod();
};
```

9. **No Arduino Strings**  
   `String` is only allowed in public API methods at the top-most layer. Never use it internally.
