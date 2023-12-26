# PowerBI Mini Practice 001

## Overview

The PowerBI Mini Practice 001 focuses on leveraging DAX (Data Analysis Expressions) to identify the maximum sales value and its corresponding sales date for each month. The data model is structured with three interconnected tables: the product table, sales table (fact table), and date table (dimension tables).

## Measures

### Total Sales

The "Total Sales" measure calculates the sum of sales on a row basis using the formula:

```DAX
total sales = SUMX('销售表', '销售表'[销售]*RELATED('商品表'[售价]))
```

### Peak Sales

The "Peak Sales" measure determines the highest total sales based on the date table, allowing for filtered results by date. The formula is:

```DAX
peak sales = MAXX('日期表', [total sales])
```

### Peak Date

The "Peak Date" measure returns the relevant date of the highest sales, considering only cases where there is a single highest sales value. The formula is:

```DAX
peak date = 
VAR x=[peak sales]
VAR tb=FILTER(VALUES('日期表'[日期]), [total sales]=x)
RETURN IF(COUNTROWS(tb)=1, tb, BLANK())
```

## Attribution

This DAX implementation was credited to [source](https://space.bilibili.com/437239552).

Feel free to explore the provided DAX expressions and adapt them to suit your specific PowerBI analysis needs.

---

**Note:** Make sure to replace Chinese characters with English equivalents in your actual implementation.
