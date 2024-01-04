# PowerBI Mini Practice 001

## Overview

The PowerBI Mini Practice 001 focuses on leveraging DAX (Data Analysis Expressions) to identify the maximum sales value and its corresponding sales date for each month. The data model is structured with three interconnected tables: the product table, sales table (fact table), and date table (dimension tables).

## Measures

### Total Sales

The "Total Sales" measure calculates the sum of sales on a row basis using the formula:

```DAX
total sales = SUMX('Sales Table', 'Sales Table'[Sales]*RELATED('Product Table'[Price]))
```

### Peak Sales

The "Peak Sales" measure determines the highest total sales based on the date table, allowing for filtered results by date. The formula is:

```DAX
peak sales = MAXX('Date Table', [total sales])
```

### Peak Date

The "Peak Date" measure returns the relevant date of the highest sales, considering only cases where there is a single highest sales value. The formula is:

```DAX
peak date = 
VAR x = [peak sales]
VAR tb = FILTER(VALUES('Date Table'[Date]), [total sales] = x)
RETURN IF(COUNTROWS(tb) = 1, tb, BLANK())
```

Alternatively, the same function can be achieved by using ADDCOLUMNS and SELECTCOLUMNS functions:

```DAX
peak date = 
VAR tb1 = ADDCOLUMNS(VALUES('Date Table'[Date]), "sales amount", [sales amount])
VAR x = [peak sales]
VAR tb2 = SELECTCOLUMNS(FILTER(tb1, [sales amount] = x), "sales date", 'Date Table'[Date])
RETURN IF(COUNTROWS(tb2) = 1, tb2, BLANK())
```

## Attribution

This DAX implementation was credited to [source](https://space.bilibili.com/437239552).

Feel free to explore the provided DAX expressions and adapt them to suit your specific PowerBI analysis needs.

---

**Note:** Make sure to replace Chinese characters with English equivalents in your actual implementation.
```

Remember to replace the Chinese characters with English equivalents in your actual implementation, as mentioned in the note.
