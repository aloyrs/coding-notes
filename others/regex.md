# Regex Notes

## 1. Character Classes `[]`

- **Definition**: Matches any one character from a specified set.
- **Syntax**: `[abc]` matches `a`, `b`, or `c`.
- **Ranges**: `[0-9]` matches any digit (0 through 9).
- **Example**:
  - `[aeiou]` matches any vowel.
  - `[A-Za-z]` matches any letter (uppercase or lowercase).

## 2. Grouping `()`

- **Definition**: Groups part of a regex for applying quantifiers or capturing matched text.
- **Syntax**: `(abc)` matches the exact sequence "abc".
- **Alternation**: `(cat|dog)` matches either "cat" or "dog".
- **Example**:
  - `(abc)+` matches "abc" one or more times (e.g., `abc`, `abcabc`).

## 3. Quantifiers

- **Definition**: Specifies how many times the preceding element should be matched.
- **Common Quantifiers**:

  - `*` - Zero or more times.
  - `+` - One or more times.
  - `?` - Zero or one time.
  - `{n}` - Exactly `n` times.
  - `{n,}` - At least `n` times.
  - `{n,m}` - Between `n` and `m` times.

- **Example**:
  - `a*` matches zero or more `a`s.
  - `a+` matches one or more `a`s.
  - `\d{3}` matches exactly three digits (e.g., `123`).

## Combining Concepts

- **Example**:
  - `([A-Za-z]+)\s+([0-9]+)` matches a word followed by one or more spaces and then digits.
