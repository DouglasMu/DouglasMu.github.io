---
layout: post
title:  leetcode-有效的括号
categories: leetcode
tags:  Python leetcode
author: Keyon
---

* content
{:toc}

## 有效的括号
给定一个只包括 '('，')'，'{'，'}'，'['，']' 的字符串，判断字符串是否有效。

有效字符串需满足：

左括号必须用相同类型的右括号闭合。
左括号必须以正确的顺序闭合。
注意空字符串可被认为是有效字符串。







示例 1:

> 输入: "()"

> 输出: true

示例 2:

> 输入: "()[]{}"

> 输出: true

示例 3:

> 输入: "(]"

> 输出: false

示例 4:

> 输入: "([)]"

> 输出: false

示例 5:

> 输入: "{[]}"

> 输出: true

## 解题思路
## 解法1
使用栈，左括号代表入栈，右括号代表出栈
如果要出栈，出栈的元素要与当前元素匹配
最终栈要为空
```python
class Solution:
    def isValid(self,s):
      stack = []
      map = {
        "{":"}",
        "[":"]",
        "(":")"
      }
      for x in s:
        if x in map:
          stack.append(map[x])
        else:
          if len(stack)!=0:
            top_element = stack.pop()
            if x != top_element:
              return False
            else:
              continue
          else:
            return False
      return len(stack) == 0
```
## 解法2
不断通过消除 '[]' ， '()', '{}' ，最后判断剩下的是否是空串即可，就像开心消消乐一样。
```python
class Solution:
   def isValid(self, s):
       while '[]' in s or '()' in s or '{}' in s:
           s = s.replace('[]','').replace('()','').replace('{}','')
           return not len(s)
```


