---
title: XPath Exapmles
date: 2020-09-20 19:00:20
tags:
---

前一段时间在写 [MountBank](http://www.mbtest.org/) 相关的 Predicates 的时候，用到了`XPath`的语法，有些语法模仿已有的 case 可以很好的完成，但有些特殊一点的 case 就需要自己思考如何实现。在网上搜索的时候看到了 [Freeformatter](https://www.freeformatter.com/xpath-tester.html#ad-output) 这个站点，可以用来 `XPath Tester`/ `Evaluator` ，也有一些`XPath`的语法参考。

1. Select the document node
```XPath
/
```

2. Select the 'root' element
```XPath
/root
```

3. Select all 'actor' elements that are direct children of the 'actors' element.
```XPath
/root/actors/actor
```

4. Select all 'singer' elements regardless of their positions in the document.
```XPath
//foo:singer
```

5. Select the 'id' attributes of the 'singer' elements regardless of their positions in the document.
```XPath
//foo:singer/@id
```

6. Select the textual value of first 'actor' element.
```XPath
//actor[1]/text()
```

7. Select the last 'actor' element.
```XPath
//actor[last()]
```

8. Select the first and second 'actor' elements using their position.
```XPath
//actor[position() < 3]
```

9. Select all 'actor' elements that have an 'id' attribute.
```XPath
//actor[@id]
```

10. Select the 'actor' element with the 'id' attribute value of '3'.
```XPath
//actor[@id='3']
```

11. Select all 'actor' nodes with the 'id' attribute value lower or equal to '3'.
```XPath
//actor[@id<=3]
```

12. Select all the children of the 'singers' node.
```XPath
/root/foo:singers/*
```

13. Select all the elements in the document.
```XPath
//*
```

14. Select all the 'actor' elements AND the 'singer' elements.
```XPath
//actor|//foo:singer
```

15. Select the name of the first element in the document.
```XPath
name(//*[1])
```

16. Select the numeric value of the 'id' attribute of the first 'actor' element.
```XPath
number(//actor[1]/@id)
```

17. Select the string representation value of the 'id' attribute of the first 'actor' element.
```XPath
string(//actor[1]/@id)
```

18. Select the length of the first 'actor' element's textual value.
```XPath
string-length(//actor[1]/text())
```

19. Select the local name of the first 'singer' element, i.e. without the namespace.
```XPath
local-name(//foo:singer[1])
```

20. Select the number of 'singer' elements.
```XPath
count(//foo:singer)
```

21. Select the sum of the 'id' attributes of the 'singer' elements.
```XPath
sum(//foo:singer/@id)
```