### Selecting Nodes

| Expression | Description |
| --- | --- |
| nodename | Selects all nodes with the name "nodename" |
| / | Selects from the root node |
| // | Selects nodes in the document from the current node that match the selection no matter where they are |
| . | Selects the current node |
| .. | Selects the parent of the current node |
| @ | Selects attributes |
  
**Eg:**
```xml
<?xml version="1.0" encoding="UTF-8"?>

<bookstore>

<book>
  <title lang="en">Harry Potter</title>
  <price>29.99</price>
</book>

<book>
  <title lang="en">Learning XML</title>
  <price>39.95</price>
</book>

</bookstore>
```
| Path Expression | Result |
| --- | --- |
| bookstore | Selects all nodes with the name "bookstore" |
| /bookstore | Selects the root element bookstoreNote: If the path starts with a slash ( / ) it always represents an absolute path to an element! |
| bookstore/book | Selects all book elements that are children of bookstore |
| //book | Selects all book elements no matter where they are in the document |
| bookstore//book | Selects all book elements that are descendant of the bookstore element, no matter where they are under the bookstore element |
| //@lang | Selects all attributes that are named lang |


### Predicates
Predicates are used to find a specific node or a node that contains a specific value. \
Predicates are always embedded in square brackets. \
In the table below we have listed some path expressions with predicates and the result of the expressions:

| Path Expression | Result |
| --- | --- |
| /bookstore/book[1] | Selects the first book element that is the child of the bookstore element.Note: In IE 5,6,7,8,9 first node is[0], but according to W3C, it is [1]. To solve this problem in IE, set the SelectionLanguage to XPath:In JavaScript: xml.setProperty("SelectionLanguage","XPath"); |
| /bookstore/book[last()] | Selects the last book element that is the child of the bookstore element |
| /bookstore/book[last()-1] | Selects the last but one book element that is the child of the bookstore element |
| /bookstore/book[position()<3] | Selects the first two book elements that are children of the bookstore element |
| //title[@lang] | Selects all the title elements that have an attribute named lang |
| //title[@lang='en'] | Selects all the title elements that have a "lang" attribute with a value of "en" |
| /bookstore/book[price>35.00] | Selects all the book elements of the bookstore element that have a price element with a value greater than 35.00 |
| /bookstore/book[price>35.00]/title | Selects all the title elements of the book elements of the bookstore element that have a price element with a value greater than 35.00 |

### Selecting Unknown Nodes
wildcards can be used to select unknown XML nodes.

| Wildcard | Description |
| --- | --- |
| * | Matches any element node |
| @* | Matches any attribute node |
| node() | Matches any node of any kind |

**Eg:**
| Path Expression | Result |
| --- | --- |
| /bookstore/* | Selects all the child element nodes of the bookstore element |
| //* | Selects all elements in the document |
| //title[@*] | Selects all title elements which have at least one attribute of any kind |

### Selecting Several Paths
| Path Expression | Result |
| --- | --- |
| /bookstore/* | Selects all the child element nodes of the bookstore element |
| //* | Selects all elements in the document |
| //title[@*] | Selects all title elements which have at least one attribute of any kind |


### XPath Axes
An axis represents a relationship to the context (current) node, and is used to locate nodes relative to that node on the tree.
| AxisName | Result |
| --- | --- |
| ancestor | Selects all ancestors (parent, grandparent, etc.) of the current node |
| ancestor-or-self | Selects all ancestors (parent, grandparent, etc.) of the current node and the current node itself |
| attribute | Selects all attributes of the current node |
| child | Selects all children of the current node |
| descendant | Selects all descendants (children, grandchildren, etc.) of the current node |
| descendant-or-self | Selects all descendants (children, grandchildren, etc.) of the current node and the current node itself |
| following | Selects everything in the document after the closing tag of the current node |
| following-sibling | Selects all siblings after the current node |
| namespace | Selects all namespace nodes of the current node |
| parent | Selects the parent of the current node |
| preceding | Selects all nodes that appear before the current node in the document, except ancestors, attribute nodes and namespace nodes |
| preceding-sibling | Selects all siblings before the current node |
| self | Selects the current node |


**Eg:**
| Example | Result |
| --- | --- |
| child::book | Selects all book nodes that are children of the current node |
| attribute::lang | Selects the lang attribute of the current node |
| child::* | Selects all element children of the current node |
| attribute::* | Selects all attributes of the current node |
| child::text() | Selects all text node children of the current node |
| child::node() | Selects all children of the current node |
| descendant::book | Selects all book descendants of the current node |
| ancestor::book | Selects all book ancestors of the current node |
| ancestor-or-self::book | Selects all book ancestors of the current node - and the current as well if it is a book node |
| child::*/child::price | Selects all price grandchildren of the current node |


### Descendant selectors
| h1 | //h1 |
| --- | --- |
| div p | //div//p |
| ul > li | //ul/li |
| ul > li > a | //ul/li/a |
| div > * | //div/* |
| :root | / |
| :root > body | /body |

### Attribute selectors
| #id | //*[@id="id"] |
| --- | --- |
| .class | //*[@class="class"] …kinda |
| input[type="submit"] | //input[@type="submit"] |
| a#abc[for="xyz"] | //a[@id="abc"][@for="xyz"] |
| a[rel] | //a[@rel] |
| a[href^='/'] | //a[starts-with(@href, '/')] |
| a[href$='pdf'] | //a[ends-with(@href, '.pdf')] |
| a[href*='://'] | //a[contains(@href, '://')] |
| a[rel~='help'] | //a[contains(@rel, 'help')] …kinda |

### Order selectors
| ul > li:first-of-type | //ul/li[1] |
| --- | --- |
| ul > li:nth-of-type(2) | //ul/li[2] |
| ul > li:last-of-type | //ul/li[last()] |
| li#id:first-of-type | //li[1][@id="id"] |
| a:first-child | //*[1][name()="a"] |
| a:last-child | //*[last()][name()="a"] |

### Siblings
| h1 ~ ul | //h1/following-sibling::ul |
| --- | --- |
| h1 + ul | //h1/following-sibling::ul[1] |
| h1 ~ #id | //h1/following-sibling::[@id="id"] |

### Operators
**Comparison** \
//a[@id = "xyz"] \
//a[@id != "xyz"] \
//a[@price > 25]

**Logic (and/or)** \
//div[@id="head" and position()=2] \
//div[(x and y) or not(z)]

### Indexing
//a[1]                  # first <a> \
//a[last()]             # last <a>  \
//ol/li[2]              # second <li> \
//ol/li[position()=2]   # same as above \
//ol/li[position()>1]   # :not(:first-of-type)


