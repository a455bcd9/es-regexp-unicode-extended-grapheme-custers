# ECMAScript proposal: Unicode word boundary assertions

Proposal to add the word boundary assertions `\b{w}` to regular expressions in ECMAScript with the `u` flag, to match Unicode extended grapheme cluster boundaries, as described in [Unicode Technical Standard #18](http://unicode.org/reports/tr18/#Tailored_Graphemes_Clusters).

## Status



## Motivation

Currently, `/na\b/u.test('naïve')` return `false`, and yet nobody would normally consider that there is two word boundaries in the middle of `fiancée`, and it is not a useful semantics, especially in Unicode-aware contexts (that is, in situations where you should use the u flag).

There currently is no way to access these Unicode character properties natively in ECMAScript regular expressions. This makes it painful for developers to support full Unicode in their regular expressions.

## Proposed solution

We propose the addition of _Unicode word boundaries_ of the form `\b{w}` and `\B{W}` available in regular expressions that have the `u` flag set. With this feature, the above regular expression could be written as:

```js
/na\b{w}/u.test('naïve')
// → true
```
