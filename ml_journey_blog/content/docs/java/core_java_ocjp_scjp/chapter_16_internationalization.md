---
title: 16. Internationalization (I18N)
description: Java language fundamentals
toc: true
authors:
tags:
categories:
series:
date: '2020-11-11'
lastmod: '2020-11-18'
---

## Introduction

- The process of designing web applications that provide support for various languages, currencies etc. automatically

- We can implement it by using

    - Locale

    - NumberFormat

    - DateFormat

## Locale

- It represents a geographical location or language or both

- It is present in java.util package. It is final class that is direct child of Object

- Implements Serializable and Cloneable

- Constructors

    - ```Locale l = new Locale(String language)```

    - ```Locale l = new Locale(String language, String country)```

- Locale class contains some constants we can use directly

- Methods

    - ```Locale.getDefault()```

    - ```Locale.setDefault(Locale l)```

    - ```public String getcountry()```

    - ```public String getLanguage()```

    - ```public String getDisplayCountry()```

    - ```public String getDisplayLanguage()```

    - ```public static String[] getISOLanguage()```

    - ```public static String[] getISOCountries()```

    - ```public static Locale[] getAvailableLocales()```

## NumberFormat

- Present in java.text package and is an abstract class

- Making NumberFormat object

    - ```public static NumberFormat getInstance()```

    - ```public static NumberFormat getCurrencyInstance()```

    - ```public static NumberFormat getParentInstance()```

    - ```public static NumberFormat getNumberInstance()```: These methods are for default locale. For specific locale, pass Locale l as argument

    - ```public String format(long l)```

    - ```public String format(double d)```: Convert java number to locale specific String

    - ```public Number parse(String s) throws ParseException```: Locale specific string to java number

    - ```public void setMaximumFractionDigits(int n)```

    - ```public void setMinimumFractionDigits(int n)```

    - ```public void setMaximumIntegerDigits(int n)```

    - ```public void setMinimumIntegerDigits(int n)```

## DateFormat

- Object creation

    - ```public static DateFormat getInstance()```

    - ```public static DateFormat getDateInstance()```

    - ```public static DateFormat getDateInstance(int style)```

    - ```public static DateFormat getDateInstance(int style, Locale l)```

- Methods

    - ```public String format(Date d)```

    - ```public Date parse(String s) throws ParseException```