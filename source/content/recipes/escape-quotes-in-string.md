---
layout: recipe
title: Escape quotes in a string
category: strings
date: "2013-11-15"
published: true
---
## Problem

You need to build a data file that makes special use of quote marks, such as
comma separated value (CSV) files, and the strings that are part of the data
might contain quote marks.

## Solution

Before placing the data in the file, escape quote marks in a way that is
appropriate for the file format. For example, in typical comma separated value
(CSV) files, quote marks are escaped by doubling them.

### CoffeeScript

```coffeescript
escapeQuotes = (text) -> text.replace(/"/g, '""')
```

### JavaScript

```javascript
function escapeQuotes(text) {
  return text.replace(/"/g, '""');
}
```

### Perl 5

```perl
sub escapeQuotes {
  my($text) = @_;

  $text =~ s/"/""/g;
  $text;
}
```

### Python

```python
def escapeQuotes(text):
  text.replace('"', '""')
```

### Scala

```scala
def escapeQuotes(text: String) = '"'.r.replaceAllIn(text, '""')
```

### XSLT 1.0

Something that is fairly easy in other languages requires a different approach
in XSLT since there are no regular expressions in the language. In this
solution, we escape the first occurance of the quote mark and then call the
function again for the remainder of the string.

```xml
<xsl:variable name="quoteReplacement"><xsl:text>""</xsl:text></xsl:variable>
<xsl:variable name="quoteText"><xsl:text>"</xsl:text></xsl:variable>

<xsl:template name="escapeQuote">
  <xsl:param name="text" select="."/>
  <xsl:if test="string-length($text) > 0">
    <xsl:value-of select="substring-before(concat($text, $quoteText), $quoteText)"/>
    <xsl:if test="contains($text, $quoteText)">
      <xsl:value-of select="$quoteReplacement" />
      <xsl:call-template name="escapeQuote">
        <xsl:with-param name="text" select="substring-after($text, $quoteText)"/>
      </xsl:call-template>
    </xsl:if>
  </xsl:if>
</xsl:template>

<!-- call the escapeQuote template with the following pattern -->
<xsl:call-template name="escapeQuote">
  <xsl:with-param name="text" select="..." />
</xsl:call-template>
```

### XSLT 2.0

```xml
<xsl:template name="escapeQuotes">
  <xsl:param name="text" select="."/>
  <xsl:value-of select="replace(text, /&quot;/, '&quot;&quot;')" />
</xsl:template>

<!-- call the escapeQuote template with the following pattern -->
<xsl:call-template name="escapeQuote">
  <xsl:with-param name="text" select="..." />
</xsl:call-template>
```

## Discussion

Most modern languages have regular expression facilities that allow escaping
selected characters with a single line of code. The only solution above which
doesn't fit this is for XSLT 1.0. In such languages, we have to go through the
string and find each occurance of the quote mark and then manipulate the
string to make the replacement.

It's easy to change both the text that is being searched for (the quote mark)
and the text used as its replacement.
