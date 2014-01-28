---
layout: recipe
title: Encode a string for use in a URL
category: strings
date: "2013-11-16"
published: true
---
## Problem

You want to add a string to a URL, but it might have characters in it that are
special in URLs, such as a forward slash, ampersand, or a non-ASCII printable
character.

## Solution

Escape the special characters in the string as URL escape sequences before
adding the string to the URL.

### CoffeeScript

Some text about the CoffeeScript solution.

```coffeescript
# coffeescript code here
```

### Perl 5

Some text about the Perl solution.

```perl
# perl code here
```

### Python

```python

```

### Scala

```scala

```

### XSLT

```xml
<xsl:variable name="textForEscaping" value="..." />
<xsl:value-of select="uri:encode($textForEscaping)" />
```

## Discussion

In this section, provide enough information for readers to understand why the
general approach taken in the above code works. What are the pitfalls to watch
out for? When might the solution not work? What are some other ways to
approach the problem?

Include references to other resources that might be useful in understanding
the nuances of the problem. Provide links to resources from which you drew
your code examples.

## See Also

List links to additional resources or materials from which example code might
have been drawn.
