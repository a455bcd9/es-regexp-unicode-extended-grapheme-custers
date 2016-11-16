# ECMAScript proposal: Unicode word boundary assertions

Proposal to add the word boundary assertions `\b{w}` to regular expressions in ECMAScript with the `u` flag, to match Unicode extended grapheme cluster boundaries, as described in [Unicode Technical Standard #18](http://unicode.org/reports/tr18/#Tailored_Graphemes_Clusters).

## Status



## Motivation

Characters that are matched by the short-hand character class `\w` are the characters that are treated as word characters by word boundaries. So `/na\b/u.test('naïve')` returns `true`. And yet nobody would normally consider in Unicode-aware contexts that there are two word boundaries in the middle of `naïve` or `fiancée`.

There currently is no way to access these Unicode character properties natively in ECMAScript regular expressions. This makes it painful for developers to support full Unicode in their regular expressions.

## Proposed solution

We propose the addition of _Unicode word boundaries_ of the form `\b{w}` and `\B{W}` available in regular expressions that have the `u` flag set. With this feature, the above regular expression could be written as:

```js
/na\b{w}/u.test('naïve')
// → false
```
