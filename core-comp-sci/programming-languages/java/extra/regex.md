# Regular Expressions (Regex)

Regular expressions (regex or regexp) are powerful patterns used for searching, matching, and manipulating text.

## Basic Characters

- `.` (dot): Matches any character except a newline.
- `\d`: Matches any digit (0-9).
- `\D`: Matches any character that is not a digit.
- `\w`: Matches any word character (alphanumeric and underscore).
- `\W`: Matches any non-word character.
- `\s`: Matches any whitespace character (space, tab, newline).
- `\S`: Matches any non-whitespace character.

## Quantifiers

- `*`: Matches 0 or more occurrences of the preceding element.
- `+`: Matches 1 or more occurrences of the preceding element.
- `?`: Matches 0 or 1 occurrence of the preceding element.
- `{n}`: Matches exactly n occurrences of the preceding element.
- `{n,}`: Matches n or more occurrences of the preceding element.
- `{n,m}`: Matches between n and m occurrences of the preceding element.

## Anchors

- `^`: Matches the start of a line.
- `$`: Matches the end of a line.

## Character Classes

- `[abc]`: Matches any single character 'a', 'b', or 'c'.
- `[a-z]`: Matches any lowercase letter from 'a' to 'z'.
- `[A-Z]`: Matches any uppercase letter from 'A' to 'Z'.
- `[0-9]`: Matches any digit from 0 to 9.

## Predefined Character Classes

- `\d` is equivalent to `[0-9]`.
- `\w` is equivalent to `[a-zA-Z0-9_]`.
- `\s` includes various whitespace characters (space, tab, newline, etc.).

## Negation

- `[^abc]`: Matches any character that is not 'a', 'b', or 'c'.

## Grouping and Alternation

- `(abc)`: Groups characters together.
- `a|b`: Matches 'a' or 'b'.

## Escaping

- Some characters have special meanings in regex (e.g., `.`). To match them literally, escape with a backslash (e.g., `\.`).

## Modifiers

- `i`: Case-insensitive matching.
- `m`: Multi-line matching.
- `s` (dotall): Allows `.` to match newlines.

## Quantifier Greediness

- By default, quantifiers are greedy (match as much as possible). Use `*?`, `+?`, and `??` for non-greedy matching.

```html
Greedy will consume as much as possible. Suppose you have the following:

<em>Hello World</em>

Use <.+> will get <em>Hello World</em>

But if you only want <em> or </em> , use <.+?> , the regex will match
non-greedily.
```

## Anchors

- `^` matches the start of a line.
- `$` matches the end of a line.
- `\b` matches a word boundary.

```
\bword\b  # Matches "word" as a whole word
```

## Lookahead and Lookbehind

- `(?=...)`: Positive lookahead assertion

  - Only find strings that have `...` behind , eg:

    regex = apple(?=pie)

    `apple`pie ✅

    apple ❌

- `(?!...)`: Negative lookahead assertion

  - Only find strings that don't have `...` behind

- `(?<=...)`: Positive lookbehind assertion

  - Only find strings that have `...` in front

- `(?<!...)`: Negative lookbehind assertion

  - Only find strings that don't have `...` in front

## Comments

- `(?#...)`: Add comments within your regular expression.
