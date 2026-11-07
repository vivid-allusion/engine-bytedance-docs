---
title: "Character Functions"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/character-functions"
---

<span id="splitbychar（separator，s"></span>
## splitByChar（**separator**，s)
Splits the string into multiple substrings using 'separator'. 'separator' must be a string constant containing only one character. Returns an array of the substrings after splitting. If the delimiter appears at the beginning or end of the string, or if there are consecutive delimiters, empty substrings will be filled in the corresponding positions.
<span id="splitbystring-separator，s"></span>
## splitByString(**separator**，s)
Similar to the above, but it uses a string with multiple characters as the delimiter. The string must be non-empty.
<span id="arraystringconcat-arr-separator"></span>
## arrayStringConcat(arr[,**separator**])
Concatenate the strings listed in the array using the separator. The 'separator' is an optional parameter: a constant string, which by default is set to an empty string. Return the concatenated string.
<span id="alphatokens-s"></span>
## alphaTokens(s)
Select consecutive byte substrings from the range a-z and A-Z. Return an array of substrings.
Example:
```plaintext
SELECT alphaTokens('abca1abc')

┌─alphaTokens('abca1abc')─┐
│ ['abca','abc']          │
└─────────────────────────┘
```

<span id="empty"></span>
## empty
Returns 1 for an empty string and 0 for a non-empty string. The result type is UInt8. If a string contains at least one byte, it is considered a non-empty string, even if it's just a space or a null character. This function is also applicable to arrays.
<span id="notempty"></span>
## notEmpty
Returns 0 for an empty string and 1 for a non-empty string. The result type is UInt8. This function is also applicable to arrays.
<span id="length"></span>
## length
Returns the byte length of the string. The result type is UInt64. This function is also applicable to arrays.
<span id="lengthutf8"></span>
## lengthUTF8
Assuming the string is composed of UTF-8 encoded text, it returns the Unicode character length of this string. If the input string is not encoded in UTF-8, the function may return an unexpected value (without throwing an exception). The result type is UInt64.
<span id="char-length-char-length"></span>
## char_length,CHAR_LENGTH
Assuming the string is composed of UTF-8 encoded text, it returns the Unicode character length of this string. If the input string is not encoded in UTF-8, the function may return an unexpected value (without throwing an exception). The result type is UInt64.
<span id="character-length-character-length"></span>
## character_length,CHARACTER_LENGTH
Assuming the string is composed of UTF-8 encoded text, it returns the Unicode character length of this string. If the input string is not in UTF-8 encoding, the function might return an unexpected value (it won't throw an exception). The result type is UInt64.
<span id="lower-lcase"></span>
## lower, lcase
Converts ASCII characters in the string to lowercase.
<span id="upper-ucase"></span>
## upper, ucase
Converts ASCII characters in the string to uppercase.
<span id="lowerutf8"></span>
## lowerUTF8
Converts the string to lowercase, assuming the string is encoded in UTF-8. The function does not check the language. Therefore, the result may not be completely correct for Turkish speakers. If the length of the UTF-8 byte sequence differs for uppercase and lowercase of a code point, the result may be incorrect. If the string contains a sequence of non-UTF-8 bytes, undefined behavior will occur.
<span id="upperutf8"></span>
## upperUTF8
Converts the string to uppercase, assuming the string is in the UTF-8 encoded character set. The function does not detect language. Therefore, for Turkish people, the results may not be completely correct. If the length of the UTF-8 byte sequence differs for uppercase and lowercase of a code point, the result may be incorrect. If the string contains a sequence of non-UTF-8 bytes, undefined behavior will occur.
<span id="isvalidutf8"></span>
## isValidUTF8
Checks if a string is valid UTF-8 encoding; returns 1 if true, otherwise returns 0.
<span id="tovalidutf8"></span>
## toValidUTF8
Replace invalid UTF-8 characters with `�` (U+FFFD) character. All consecutive invalid characters are replaced with a replacement character.
```plaintext
toValidUTF8( input_string )
```

Parameters:

* input_string — Any object of string type.

Return value: A valid UTF-8 string.
<span id="示例"></span>
### Example
SELECT toValidUTF8('\x61\xF0\x80\x80\x80b')
```SQL
┌─toValidUTF8('a����b')─┐
│ a�b                   │
└───────────────────────┘
```

<span id="reverse"></span>
## reverse
Reverse the string.
<span id="reverseutf8"></span>
## reverseUTF8
Reverse a UTF-8 encoded string by Unicode characters. If the string is not UTF-8 encoded, an unexpected result may be obtained (no exception is thrown).
<span id="format-pattern-s0-s1-…"></span>
## format(pattern, s0, s1, …)
Format other parameters using the constant string `pattern`. The `pattern` string contains "replacement fields" surrounded by curly braces `{}`. Any content not included in curly braces is considered as text content, which is preserved as is in the return value. If you need to include a curly brace character in the text content, it can be escaped by doubling: `{{ '{' }}` and `{{ '{' }} '}' }}`. Field names can be numeric (starting from zero) or empty (then considered as sequential numbers).
```SQL
SELECT format('{1} {0} {1}', 'World', 'Hello')

┌─format('{1} {0} {1}', 'World', 'Hello')─┐
│ Hello World Hello                       │
└─────────────────────────────────────────┘

SELECT format('{} {}', 'Hello', 'World')

┌─format('{} {}', 'Hello', 'World')─┐
│ Hello World                       │
└───────────────────────────────────┘
```

<span id="concat-s1-s2-…"></span>
## concat(s1, s2, …)
Concatenate multiple strings in the parameter without a delimiter.
<span id="concatassumeinjective-s1-s2-…"></span>
## concatAssumeInjective(s1, s2, …)
Similar to concat, the difference is that you need to ensure concat(s1, s2, s3) -> s4 is injective, which will be used for optimization in GROUP BY.
<span id="substring-s-offset-length-mid-s-offset-length-substr-s-offset-length-substrings-offset-length-mids-offset-length-substrs-offset-length"></span>
## substring(s,offset,length),mid(s,offset,length),substr(s,offset,length) {#substrings-offset-length-mids-offset-length-substrs-offset-length}
Extract a substring starting at the 'offset' position, with a byte as the unit, returning a substring of 'length'. 'offset' starts from 1 (same as standard SQL). The 'offset' and 'length' parameters must be constants.
<span id="substringutf8-s-offset-length"></span>
## substringUTF8(s,offset,length)
Same as 'substring', but operates in Unicode characters, assuming the string is encoded in UTF-8 text. If not, it might return an unexpected result (without throwing an exception).
<span id="appendtrailingcharifabsent-s-c"></span>
## appendTrailingCharIfAbsent(s,c)
If the string 's' is not empty and does not end with the character 'c', append 'c' to the end.
<span id="convertcharset-s-from-to"></span>
## convertCharset(s,from,to)
Return the string 's' converted from the encoding 'from' to 'to'.
<span id="base64encode-s"></span>
## base64Encode(s)
Encode the string 's' into base64.
<span id="base64decode-s"></span>
## base64Decode(s)
Decode the string using base64 into the original string. If it fails, throw an exception.
<span id="trybase64decode-s"></span>
## tryBase64Decode(s)
Decode strings into original strings using base64. But if an error occurs, an empty string will be returned.
<span id="endswith-s-suffix"></span>
## endsWith(s, suffix)
Returns whether it ends with the specified suffix. If the string ends with the specified suffix, return 1; otherwise, return 0.
<span id="startswith（s，prefix"></span>
## startsWith（s，prefix)
Returns whether it starts with the specified prefix. If the string starts with the specified prefix, return 1; otherwise, return 0.
<span id="trimleft-s"></span>
## trimLeft(s)
Returns a string that removes white space characters from the left.
<span id="trimright-s"></span>
## trimRight(s)
Returns a string used to delete whitespace characters on the right side.
<span id="trimboth-s"></span>
## trimBoth(s)
Returns a string used to delete whitespace characters on either side.
<span id="replaceone-haystack-pattern-replacement"></span>
## replaceOne(haystack, pattern, replacement)
Replaces the first occurrence of 'pattern' substring in 'haystack' with 'replacement' substring (if it exists). 'pattern' and 'replacement' must be constants.
<span id="replaceall-haystack-pattern-replacement-replace-haystack-pattern-replacement"></span>
## replaceAll(haystack, pattern, replacement), replace(haystack, pattern, replacement)
Replaces all occurrences of 'pattern' substring in 'haystack' with 'replacement' substring.
<span id="replaceregexpone-haystack-pattern-replacement"></span>
## replaceRegexpOne(haystack, pattern, replacement)
Replacement using 'pattern' regular expression. 'Pattern' can be any valid re2 regular expression. If there is a match with 'pattern' regular expression, replace only the first match. Mode pattern can be specified as ‘replacement’. This mode can include substitutions `\\0-\\9`. Substitution `\\0` contains the entire regular expression. Substitutions `\\1-\\9` correspond to subpattern numbers. To use backslash `\\` in the template, please use `\\` to escape it. Additionally, remember that string literals need extra escaping.
Example 1. Convert Date to American Format:
```SQL
SELECT DISTINCT EventDate, replaceRegexpOne(toString(EventDate), '(\\d{4})-(\\d{2})-(\\d{2})', '\\2/\\3/\\1') AS res FROM test.hitsLIMIT 7 FORMAT TabSeparated
```

```plaintext
2014-03-17      03/17/2014
2014-03-18      03/18/2014
2014-03-19      03/19/2014
2014-03-20      03/20/2014
2014-03-21      03/21/2014
2014-03-22      03/22/2014
2014-03-23      03/23/2014
```

Example 2: Copy the string ten times:
```SQL
SELECT replaceRegexpOne('Hello, World!', '.*', '\\0\\0\\0\\0\\0\\0\\0\\0\\0\\0') AS res
```

```plaintext
┌─res────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────┐
│ Hello, World!Hello, World!Hello, World!Hello, World!Hello, World!Hello, World!Hello, World!Hello, World!Hello, World!Hello, World! │
└────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────┘
```

<span id="replaceregexpall-haystack-pattern-replacement"></span>
## replaceRegexpAll(haystack, pattern, replacement)
The same as replaceRegexpOne, but replaces all occurrences of the match. Example:
```SQL
SELECT replaceRegexpAll('Hello, World!', '.', '\\0\\0') AS res
```

```plaintext
┌─res────────────────────────┐
│ HHeelllloo,,  WWoorrlldd!! │
└────────────────────────────┘
```

As an exception, for an empty substring, the regular expression is replaced only once. Example:
```SQL
SELECT replaceRegexpAll('Hello, World!', '^', 'here: ') AS res
```

```plaintext
┌─res─────────────────┐
│ here: Hello, World! │
└─────────────────────┘
```

<span id="regexpquotemeta-s"></span>
## regexpQuoteMeta(s)
This function is used to add a backslash before certain predefined characters in a string. Predefined characters: `\\0`, `\\\\`, `|`, `(`, `)`, `^`, `$`, `.`, `[`, `]`, `?`, `*`, `+`, `{`, `:`, `-`. This implementation differs slightly from re2::RE2::QuoteMeta. It escapes the zero byte with `\\0` instead of `\\x00`, and only escapes the necessary characters. For more details, refer to [RE2](https://github.com/google/re2/blob/master/re2/re2.cc#L473).
All the following functions are case-sensitive by default. For case-insensitive search, separate variants exist.
<span id="position-haystack-needle-locate-haystack-needle"></span>
## **position(haystack, needle), locate(haystack, needle)**
Search for the substring needle in the string haystack. R`needle in the string haystack`. Returns the position of the substring (in bytes), starting at 1; if the substring isn't found, returns 0.
For case-insensitive search, use the function `positionCaseInsensitive`.
<span id="positionutf8-haystack-needle"></span>
## positionUTF8(haystack, needle)
Similar to `position`, but returns the position in Unicode characters. This function operates within UTF-8 encoded text character sets. If using a character set other than this encoding, it returns some unexpected results (it will not throw an exception).
For case-insensitive searches, use the function `positionCaseInsensitiveUTF8`.
<span id="multisearchallpositions-haystack，-needle1-needle2-needlen"></span>
## multiSearchAllPositions(haystack，[needle1, needle2, ..., needlen])
Same as `position`, but the function returns an array containing all the positions that match the needle (I).
For case-insensitive searches and/or UTF-8 format, use the function `multiSearchAllPositionsCaseInsensitive, multiSearchAllPositionsUTF8, multiSearchAllPositionsCaseInsensitiveUTF8`.
<span id="multisearchfirstposition-haystack，-needle1-needle2-needlen"></span>
## multiSearchFirstPosition(haystack，[needle1, needle2, ..., needlen])
The same as `location`, but returns the leftmost offset of a match in `haystack` with the string needles.
For case-insensitive or/and UTF-8 searches, use functions `multiSearchFirstPositionCaseInsensitive, multiSearchFirstPositionUTF8, multiSearchFirstPositionCaseInsensitiveUTF8`.
<span id="multisearchfirstindex-haystack，-needle1-needle2-needlen"></span>
## multiSearchFirstIndex(haystack，[needle1, needle2, ..., needlen])
Returns the index i of the first found needle in string haystack (s`i of the first found needle in string haystack` (starting from 1), or returns 0 if no match is found.
For case-insensitive or/and UTF-8 searches, use functions `multiSearchFirstIndexCaseInsensitive, multiSearchFirstIndexUTF8, multiSearchFirstIndexCaseInsensitiveUTF8`.
<span id="multisearchany-haystack，-needle1-needle2-needlen"></span>
## multiSearchAny(haystack，[needle1, needle2, ..., needlen])
If there is at least one needle match in `haystack`, returns 1, otherwise returns 0.
For case-insensitive or/and UTF-8 searches, use functions `multiSearchAnyCaseInsensitive, multiSearchAnyUTF8, multiSearchAnyCaseInsensitiveUTF8`.
:::warning
In all `multiSearch*` functions, due to implementation standards, the quantity of needles should be smaller than 2(8).
:::
<span id="match-haystack-pattern"></span>
## match(haystack, pattern)
Check if the String Matches the `regular expression` pattern. The `pattern` can be any `re2` regular expression. The `re2` regular expression's [syntax](https://github.com/google/re2/wiki/Syntax) has more restrictions compared with Perl regular expression's syntax.
If there is no Match, return 0, Otherwise return 1.
Please note that the backslash symbol (`\\`) is used to escape in regular expressions. Since the same symbol is used to escape in Strings. Therefore, to escape a symbol in a regular expression, two backslashes (\\) must be written in the string literal.
Regular expressions are used with Strings as if they were a set of bytes. Regular expressions cannot contain empty bytes. For patterns searching for substrings in a string, it is better to use LIKE or «position», as they are more efficient.
<span id="multimatchany-haystack-pattern-1-pattern-2-…-pattern-n"></span>
## multiMatchAny(haystack, [pattern(1), pattern(2), …, pattern(n)])
Similar to `match`, but returns 0 if all regular expressions do not match; returns 1 if any pattern matches. It uses the [hyperscan](https://github.com/intel/hyperscan) library. For patterns searching for substrings in a string, it is better to use «multisearchany» because it is more efficient.
:::warning
The length of any `haystack` string must be smaller than 2(32 bytes, otherwise throws an exception. This restriction arises due to the hyperscan API.
:::
<span id="multimatchanyindex-haystack-pattern-1-pattern-2-…-pattern-n"></span>
## multiMatchAnyIndex(haystack, [pattern(1), pattern(2), …, pattern(n)])
Similar to `multiMatchAny`, but returns the index position of anything that matches with haystack.
<span id="multifuzzymatchany-haystack-pattern-1-pattern-2-…-pattern-n"></span>
## multiFuzzyMatchAny(haystack, [pattern(1), pattern(2), …, pattern(n)])
Similar to `multiMatchAny`, but returns 1 if any pattern match can be found within a specified [edit distance](https://en.wikipedia.org/wiki/Edit_distance) in the haystack. This function is also in Experiment Mode and may be very slow. For more details, see [hyperscan document](https://intel.github.io/hyperscan/dev-reference/compilation.html#approximate-matching).
<span id="multifuzzymatchanyindex-haystack-pattern-1-pattern-2-…-pattern-n"></span>
## multiFuzzyMatchAnyIndex(haystack, [pattern(1), pattern(2), …, pattern(n)])
Similar to `multiFuzzyMatchAny`, but returns the location index of the match in the haystack.
:::warning
* The `multiFuzzyMatch*` functions do not support UTF-8 regular expressions and are parsed by bytes due to hyperscan limitations.
* To terminate the use of all hyperscan functions, set `SET allow_hyperscan = 0;`.
:::
<span id="extract-haystack-pattern"></span>
## extract(haystack, pattern)
Use regular expressions to extract strings. If 'haystack' does not match 'pattern', an empty string is returned. If the regular expression does not contain a subpattern, it extracts the substring that matches the entire regular expression. Otherwise, it extracts the substring that matches the first subpattern.
<span id="extractallt-haystack-pattern"></span>
## extractAllt(haystack, pattern)
Use regular expressions to extract all fragments of the string. If 'haystack' does not match the 'pattern' regular expression, an empty string array is returned. Otherwise, it returns an array of strings that match the regular expression. Typically, the behavior is the same as the 'extract' function (it adopts the first subpattern, if there is no subpattern, it adopts the whole expression).
<span id="like-haystack-pattern-haystack-like-pattern-operator"></span>
## like(haystack, pattern), haystack LIKE pattern operator
Check if the string matches a simple regular expression. Regular expressions can contain metacharacters such as `%` and `_`.
`%` represents any number of bytes (including zero characters).
`_` represents any single byte.
Metacharacters can be escaped using a backslash (`\\`). Please refer to the description about escaping in the «match» function description.
For regular expressions like `%needle%`, this function is as fast as the `position` function. For other regular expressions, the function is the same as the 'match' function.
<span id="notlike-haystack-pattern-haystack-not-like-pattern-operator"></span>
## notLike(haystack, pattern), haystack NOT LIKE pattern operator
Yields the opposite result of the 'not like' function.
<span id="ngramdistance-haystack-needle"></span>
## ngramDistance(haystack, needle)
Computes the distance between `haystack` and `needle` based on 4-gram: calculate the symmetric difference between two 4-gram sets, and normalize it with their cardinality. Returns any floating-point number between 0 and 1 - the closer to 0, the more similar the strings are to each other. If the constants `needle` or `haystack` exceed 32KB, the function will throw an exception. If the non-constant strings `haystack` or `needle` exceed 32Kb, the distance is always 1.
For case-insensitive search or/and UTF-8 format, use the function `ngramDistanceCaseInsensitive, ngramDistanceUTF8, ngramDistanceCaseInsensitiveUTF8`.
