---
layout: default
title: Elysium Full Text Search
nav_order: 50
has_children: false
redirect_from: /documentation/search/
has_toc: false
---

# Elysium Full Text Search
search engine
{: .label .label-yellow :}

## Introduction

Elysium Search is a search tool designed to help users quickly find and filter data within a database. It allows users to search for specific values or patterns within a dataset, and offers a range of options for customizing the search process.

## How to Guides

### Add Index To add an index to Elysium Search, follow these steps:
1.	Open the Elysium Search.
2.	Click on the three horizontal bars to open side menu.
3.	 Click on the “Stack Management“ button.<br>
![Policy]({{site.baseurl}}/images/s1.png)
4.	Click on the "Index Patterns" button.
5.	Click on the "Create Index Pattern" button.
6.	Search for the table name 
7.	Click on the “Next Step“ button and wait until the load completes (at the right top corner).<br>
![Policy]({{site.baseurl}}/images/s2.png)
8.	Once loaded use “Time field“ dropdown to select the timestamp.
9.	Selecting timestamp is mandatory to preform search. Do not create index without selecting the timestamp.<br>
![Policy]({{site.baseurl}}/images/s3.png)
10.	Click on the "Create Index pattern" button.

### Set Result Limit for a search in Elysium Search, follow these steps:
1.	Open the Elysium Search.
2.	Click on the three horizontal bars to open side menu.
3.	 Click on the “Stack Management“ button.<br>
![Policy]({{site.baseurl}}/images/s4.png)
4.	Click on the "Advanced Settings" button.
5.	Find “Number of rows” and change to desired number.<br>
![Policy]({{site.baseurl}}/images/s6.png)
6.	Click on the “Save changes” to save the setting.<br>
![Policy]({{site.baseurl}}/images/s7.png)

### Elysium Search allows users to specify the time zone for their searches. To set the time zone, follow these steps:
1.	Open the Elysium SaaS.
2.	Click on the “user icon” at the top right corner and then click “My account“.<br>
![Policy]({{site.baseurl}}/images/s8.png)
3.	Click “Timezone” for the dropdown and select to the desired time zone.
4.  Once selected then Click on the button “Save“ which requires password.<br>
![Policy]({{site.baseurl}}/images/s9.png)
5.	Enter the password and click on the button “YES“.<br>
![Policy]({{site.baseurl}}/images/s10.png)

### How to search:
1.	Open the Elysium Search.
2.	Click on the three horizontal bars to open side menu.
3.	Click on the “Discover“ button.<br>
![Policy]({{site.baseurl}}/images/s11.png)
4.	Click on the “index“ dropdown to select the index on which search needs to performed.<br>
![Policy]({{site.baseurl}}/images/s12.png)
5.	Select the time range from right top corner.<br>
![Policy]({{site.baseurl}}/images/s13.png)
6. Use search bar for entering different types of searches.<br>
![Policy]({{site.baseurl}}/images/s14.png)
7. Click on the “Refresh“/”Update” button for results.<br>
![Policy]({{site.baseurl}}/images/s15.png)

## Different types of searches you can use to filter data.

### Unquoted Search:

Use unquoted search to filter data that partially matches with the value. For example, to filter data where the username field values are like "john white", “john whitehead”,"sara white", etc., use the following syntax:

`username: white`

The field parameter is optional. If not provided, all fields will be searched for the given value. For example, to search all fields for "white", use the following:

`white`

### Quoted Search:
Use quoted search to filter data that exactly matches with the value. For example, to filter data where the username field value is "john white", use the following syntax:

`username: "john white"`

The field parameter is optional. If not provided, Smart Search will be enabled and it will identify fields that might be a possible match and search those fields for the given value. For more information on Smart Search, refer Smart Search. To use Exact Match, use the following:

`"john white"`

### Wildcard Search:
Even though unquoted search is used for partial matches, there are cases where wildcard search can be useful. To filter data that starts with "tom", use the following syntax:

`username: tom*`

To filter data that ends with "sam", use the following syntax:

`username: *sam`

Wildcard search can only be used with unquoted searches. If the wildcard (*) is used in a quoted search, it will be considered as a literal. For example, "sam*" will search for "sam*".

Ulike unquoted search which comes with default wildcards at the start and end of the input value. For example, sam will be queried as *sam*. Meaning any characters can be before and after “sam“. So, when using wildcards explicitly, it removes the default wildcards and treats the input (*) as a wildcard.

Wildcards can also be used to find fields where a value exists. Use the following syntax to get all values without nulls:

`username: *`

Note: Wildcard Searches doesn’t query on flatten columns like raw.src.ip 
while column is not mentioned.

### Matching Multiple Fields:
Wildcards can also be used to query multiple fields. For example, to search for documents where any sub-field of "http.response" equals "error", use the following:

`http.response.*: "error"`

### Negating a Query:
To negate or exclude a set of data, use the "not" keyword. For example, to filter documents where the "http.request.method" is not "GET", use the following query:

`NOT http.request.method: “GET”`

Negating also contains the null value while a specific search will always negate null values.

### Combining Multiple Queries:
To combine multiple queries, use the "and" or "or" keywords. For example, to find documents where the "http.request.method" is "GET" or the "http.response.status_code" is 400, use the following query:

`http.request.method: “GET” OR http.response.status_code: “400”`

Similarly, to find documents where the "http.request.method" is "GET" and the "http.response.status_code" is 400, use this query:

`http.request.method: “GET” AND http.response.status_code: “400”`

To specify precedence when combining multiple queries, use parentheses. For example, to find documents where the "http.request.method" is "GET" and the "http.response.status_code" is 200, or the "http.request.method is POST" and "http.response.status_code" is 400, use the following:

`(http.request.method: “GET” AND http.response.status_code: “200”) OR (http.request.method: “POST” AND http.response.status_code: “400”)`

You can also use parentheses for shorthand syntax when querying multiple values for the same field. For example, to find documents where the "http.request.method" is "GET", "POST", or "DELETE", use the following:

`http.request.method: (“GET” OR “POST” OR “DELETE”)`

http.request.method:”GET” OR “POST“ This would return results that either contain “GET “in the specified field http.request.method or contain the term "POST" anywhere in the document.

Precedence: When using multiple logical operators in a search, it is important to consider the precedence of the operators. The AND operator has the highest precedence, followed by OR.

So the search term "A AND B OR C" will be evaluated as "(A AND B) OR C", while the search term "A OR B AND C" will be evaluated as "A OR (B AND C)".

### Escaping Special Characters:
There may be times when you need to search for a value that includes special characters. In these cases, you will need to escape these characters.

To search for documents where  http.request.referrer  is  https://example.com, use either of the following queries: 

`http.request.referrer: "https://example.com"`

`http.request.referrer: https\://example.com `

You must escape following characters (unless surrounded by quotes/quoted search): 
( ) : < > " * { } 

### Smart Search:
Smart Search is a feature that enables searching without specifying the field. When using Smart Search, the system will identify fields that might be a possible match and search those fields for the given value.

For example, if you search for "john white" without specifying a field, the system will search all fields that contain "john white" .
To use Smart Search, enclose the search value in quotes. For example:

`"john white".`

### Numeric Range Search:
Elysium Search supports numeric searches, but there are a few considerations to keep in mind.

Rounding: Elysium Search rounds numeric values to the nearest value that can be represented in double-precision floating-point format. This can affect the accuracy of numeric searches.

Value will be rounded after 9 digits after the decimal point and values with a leading zero.. In cases where more precision is needed , users should use Double Quotes to treat the number as a string.

`110.0 is treated as 110 and 10.00000 is treated as 10.`

`Score : 123`

`Score : “1.123456789123“`

`Score : “10.0“`

Any number more than 16 digits (for both +ve and –ve numbers). We should use double quotes in that case. Adding  a + in front treats the search value as a string.

Hex number such as 0xabcd is not supported as a number. It must be searched as string.

For example, to search for the value "01", you would enter "01" in the search bar.

You can also use the ">" and "<" operators to specify an open-ended range. For example, to search for documents where the "age" field is greater than 18, use the following:
`age > 18`

To search for documents where the "age" field is less than 25, use the following:
`age < 25`

### Case Sensitivity:

Elysium Search is case-Sensitive by default, meaning that it does distinguish between uppercase and lowercase characters in searches. However, you can enable case-Insensitivity by using the following steps.
1.	Open the Elysium Search.
2.	Click on the three horizontal bars to open side menu.
3.	 Click on the “Discover“ button to open search.
4.	On the search page find “settings icon”
 
5.	Click on the "settings icon" button.
6.	Click on the “Case Sensitivity“ toggle to turn it on or off.

### Highlights:

Unquoted search will highlight the exact value entered while matching doing a partial match.

User: Sannith → User: Sannith Reddy

Quoted search will highlight the exact value entered.

User: “Sannith Reddy”: → User: Sannith Reddy

Wildcard matches will highlight depending on the *.

User : *Reddy → User: Sannith Reddy

### Limitations

Elysium Search has a number of limitations that users should be aware of:
*	Arithmetic expressions and variables are not supported.
*	Only a limited set of character sets is supported.
*	Searches on timestamps are not available currently.

### Workarounds

Arithmetic Expressions: You will need to use an alternative approach if you need to perform calculations in your searches. One option is to you use a script to pre-process your data and add calculated fields,, which you can then search using Elysium Search or User can also use Dashboards(Looker).

Copy/Paste: users have to be careful while copy pasting the results to search as there might be chances to characters which needs to be escaped or numbers with accurate precision.

