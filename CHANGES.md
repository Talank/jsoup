# jsoup Changelog

## 1.18.1 (Pending)

### Improvements

* Added `Path` accepting parse methods: `Jsoup.parse(Path)`, `Jsoup.parse(path, charsetName, baseUri, parser)`,
  etc. [2055](https://github.com/jhy/jsoup/pull/2055)
* Updated the `button` tag configuration to include a space between multiple button elements in the `Element.text()` 
  method. [2105](https://github.com/jhy/jsoup/issues/2105)

### Changes

* Removed previously deprecated internal classes and methods. [2094](https://github.com/jhy/jsoup/pull/2094)

### Bug Fixes

* When tracking source positions, if the first node was a TextNode, its position was incorrectly set
  to `-1.` [2106](https://github.com/jhy/jsoup/issues/2106)
* When connecting (or redirecting) to URLs with characters such as `{`, `}` in the path, a Malformed URL exception would
  be thrown (if in development), or the URL might otherwise not be escaped correctly (if in
  production). The URL encoding process has been improved to handle these characters
  correctly. [2142](https://github.com/jhy/jsoup/issues/2142)
* When using `W3CDom` with a custom output Document, a Null Pointer Exception would be
  thrown. [2114](https://github.com/jhy/jsoup/pull/2114)

---

## 1.17.2 (2023-Dec-29)

### Improvements

* **Attribute object accessors**: Added `Element.attribute(String)` and `Attributes.attribute(String)` to more simply
  obtain an `Attribute` object. [2069](https://github.com/jhy/jsoup/issues/2069)
* **Attribute source tracking**: If source tracking is on, and an Attribute's key is changed (
  via `Attribute.setKey(String)`), the source range is now still tracked
  in `Attribute.sourceRange()`. [2070](https://github.com/jhy/jsoup/issues/2070)
* **Wildcard attribute selector**: Added support for the `[*]` element with any attribute selector. And also restored
  support for selecting by an empty attribute name prefix (`[^]`). [2079](https://github.com/jhy/jsoup/issues/2079)

### Bug Fixes

* **Mixed-cased source position**: When tracking the source position of attributes, if the source attribute name was
  mix-cased but the parser was lower-case normalizing attribute names, the source position for that attribute was not
  tracked correctly. [2067](https://github.com/jhy/jsoup/issues/2067)
* **Source position NPE**: When tracking the source position of a body fragment parse, a null pointer
  exception was thrown. [2068](https://github.com/jhy/jsoup/issues/2068)
* **Multi-point emoji entity**: A multi-point encoded emoji entity may be incorrectly decoded to the replacement
  character. [2074](https://github.com/jhy/jsoup/issues/2074)
* **Selector sub-expressions**: (Regression) in a selector like `parent [attr=va], other`, the `, OR` was binding
  to `[attr=va]` instead of `parent [attr=va]`, causing incorrect selections. The fix includes a EvaluatorDebug class
  that generates a sexpr to represent the query, allowing simpler and more thorough query parse
  tests. [2073](https://github.com/jhy/jsoup/issues/2073)
* **XML CData output**: When generating XML-syntax output from parsed HTML, script nodes containing (pseudo) CData
  sections would have an extraneous CData section added, causing script execution errors. Now, the data content is
  emitted in a HTML/XML/XHTML polyglot format, if the data is not already within a CData
  section. [2078](https://github.com/jhy/jsoup/issues/2078)
* **Thread safety**: The `:has` evaluator held a non-thread-safe Iterator, and so if an Evaluator object was
  shared across multiple concurrent threads, a NoSuchElement exception may be thrown, and the selected results may be
  incorrect. Now, the iterator object is a thread-local. [2088](https://github.com/jhy/jsoup/issues/2088)

---
Older changes for versions 0.1.1 (2010-Jan-31) through 1.17.1 (2023-Nov-27) may be found in
[change-archive.txt](./change-archive.txt).