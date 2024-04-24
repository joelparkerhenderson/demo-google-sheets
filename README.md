# Demo Google Sheets

Demonstration of Google Sheets.


## Demo

We want to calculate the sum of transaction amounts.

We have:

* Sheet1 is a typical sheet. 
  
* The first row is header names. 

* One of the header names is "Amount".

We want:

* Look up the column name by using the sheet name and the column header name.

Example of what we want to write:

```
=SHIFT(query(Sheet1!A:Z, "
select SUM("&COLN("sheet1","amount")&")
"))
```

## Remove auto-generated headers

To remove the automatically generated header row from a result when using a data manipulation function with QUERY, set an empty LABEL for each of the data manipulation functions.

Example:

```
=query(Sheet1!A:Z, "
select SUM("&COLN("sheet1","amount")&") 
 label SUM("&COLN("sheet1","amount")&") ''
")

Set an empty LABEL to each instance of data manipulation, i.e. AVG(C). When all headers are empty, Google Sheets prints out a range with no headers.

Real-world example:

```
=query(Transactions!A:Z, "
select 
  YEAR("&COLN("transactions", "date")&"), 
  SUM("&COLN("transactions", "amount")&") 
group by 
  YEAR("&COLN("transactions", "date")&")
label 
  SUM("&COLN("transactions", "amount")&") '',
  YEAR("&COLN("transactions", "date")&") ''
")
```

## Named functions


### COLN

Menu → Data → Named Functions

Name: COLN

Arguments:

* sheetname
  * Description: Sheet name
  * Example: Sheet1.
* colname 
  * Description: Column name
  * Example: Id

Formula definition:

```
="Col"&XMATCH(colname, INDIRECT("'"&sheetname&"'!1:1"))
```

Example:

```
=COLN("Sheet1","Id") => 1
```

### SHIFT

Menu → Data → Named Functions

Name: SHIFT

Arguments: 

* list
  * Description: list of items
  * Example: [a, b, c]

Formula definition:

```
=index(list, 2, 1)
```

Example:

```
=SHIFT([a, b, c]) => [b, c]
```
