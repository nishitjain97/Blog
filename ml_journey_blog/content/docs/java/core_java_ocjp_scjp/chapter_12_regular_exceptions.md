---
title: 12. Regular Expressions
description: Java language fundamentals
toc: true
authors:
tags:
categories:
series:
date: '2020-10-13'
lastmod: '2020-10-13'
---

## Introduction

- Applications

    - Form validation

    - Pattern matching

    - Translators

- java.util.regex.*

- Pattern object is a compiled version of regular expression. We can create Pattern object by using complie() method of Pattern class

    ```public static Pattern compile(String re)```

- Matcher object is used to check if given pattern is in the target string. It can be created using matcher object of Pattern class

    ```public Matcher matcher(String target)```

- Methods of Matcher class

    - ```boolean find()```: Attempts to find next match and returns true if available

    - ```int start()```: Start index of match

    - ```int end()```: Returns end + 1 index of match

    - ```String group()```

- Symbols

    - Character classes

        - \[abc\] => either a or b or c

        - \[^abc\] => except a and b and c

        - \[a-z\] => lower case letters

        - \[A-Z\] => upper case letters

        - \[a-zA-Z\] => any alphabet

        - \[0-9\] => any digit

        - \[0-9a-zA-Z\] => alphanumeric characters

        - \[^0-9a-zA-Z\] => speecial characters

    - Predefined character classes

        - \s => space character

        - \S => except space character

        - \d => any digit, \[0-9\]

        - \D => except digit, \[^0-9\]

        - \w => word character, \[a-zA-Z0-9\]

        - \W => special characters, \[^a-zA-Z0-9\]

        - . => any character

    - Quantifiers

        - a => exactly one 'a'

        - a+ => one or more 'a'

        - a* => zero or more 'a'

        - a? => zero or one 'a'

    - Pattern class split()

        - To split target string according to a particular pattern

        - String class also contains split method to split according to pattern

### StringTokenizer

- Present in java.util

- Used for tokenizing

```
StringTokenizer st = new StringTokenizer("Nishit Jain");

while(st.hasMoreTokens()) {
    System.out.println(st.nextToken());
}
```

- Default regular expression for this is space

```
StringTokenizer st = new StringTokenizer("Nishit_Jain", "_");
```