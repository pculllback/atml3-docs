# Methods<a name="methods"></a> 

With methods you can modify and format your own data to implement perfectly good stories.

Methods are used in mapping or truth expressions of properties and return following data types:

* `Strings`
* `Numerics`
* `Booleans`
* `Lists`
* `JSON objects`

## String methods

### convert_comma(input, divisor, lowerUnit, upperUnit)
```
	convert_comma(5300, 1000, "m", "km")
		returns "5,3 km"

	convert_comma(900, 1000, "m", "km")
		returns "900 m"

	convert_comma(120, 60, "Minuten", "Stunden")
		returns "2 Minuten"
```
This method takes a numeric value and converts it to a distance or time value.

### convert_count(input, divisor, lowerUnit, upperUnit[, conjunction])
```
	convert_count(145, 60, "Minuten", "Stunden")
		returns "2 Stunden 25 Minuten"

	convert_count(45, 60, "Minuten", "Stunden")
		returns "45 Minuten"

	convert_count(350, 100, "Cent", "Euro")
		returns "3 Euro 50 Cent"

	convert_count(350, 100, "Cent", "Euro", "und")
		returns "3 Euro und 50 Cent"
```
This method takes a numeric value and converts it to a currency or date value.
Optionally, a conjunction can be given.

### cur_lang()
```
	cur_lang()
		returns "de", "es" or "en" or whatever language is currently used.
```
This method returns the current language in the current text generation process as an ISO 2-letter code.

### date_add(date, number, type)
```
	date_add("16.05.1983", 3, "years")
		returns "16.05.1986"
```
This method adds a time value to a given date and returns that new date.
These types of times can be added:

* `years`
* `months`
* `weeks`
* `days`
* `hours`
* `minutes`
* `seconds`

### date_convert(date, format)
```
	date_convert("16.05.1983", "yyyy-MM-dd")
		returns string "1983-05-16"
```
This method converts a date value to a specific format.

### date_format(date)
```
	date_format("16.05.1983")
		returns string "dd.MM.yyyy"
```
Returns a format of a date value.

### date_now()
```
	date_now()
		returns "13.06.2015"
```
This method returns the date in the following format: dd.MM.yyyy.

### formatNumber(number, decimal_place)
```
	format_number(2, 2)
		returns for example "2.00" (english) or "2,00" (german)
```
This method formats a number to enforce a certain number of decimal digits and converts it to the correct locale.

### join(list[, delimiter])
```
	join([1, 2, 3, 4, 5])
		returns "12345"

	join([1, 2, 3, 4, 5], ", ")
		returns "1, 2, 3, 4, 5"
```
This method joins all elements of a list into a string.

Optionally, it is possible to set a delimiter.

### lookup(entry, lookup table_name)
```
	lookup("summer", "reifen_art")
		looks up the entry "summer" in the lookup table (of the current language) "reifen_art" and
		returns its value as a string. If nothing is found, an empty string is returned.
 ```
Performs a lookup for fitting entries in a known lookup table.

Note: This method only return the noun as a string. For getting a whole vocabulary, use split_lookup() (see list methods).

### lower(string)
```
	lower("STRING")
		returns "string"
```
This method converts a string to its lowercase form.

### render($property)
```
	render($property)
		returns the string "kleine Katze" if the property's adjective field contains "klein" and
		its noun field contains "Katze".
```
This method takes a property and returns the content of its vocabulary.

### replace(string, old, new[, max])
```
	replace("old old old old", "old", "new")
		returns "new new new new"
		
	replace("old old old old", "old", "new", 2)
		returns "new new old old"
```
This method replaces all occurrences of a substring with a new stated substring.

Optionally, it is possible to set the number of times of replacements.

### replace_last(string, old, new)
```
	replace("1, 2, 3, 4", ",", "and")
		returns "1, 2, 3 and 4"
```
This method replaces the last occurrence of a substring with a new stated substring.

### re_get(list, pattern, direction, position)
```
	re_get([1, 2, 3], ".*", "l", 0)
		returns "1"

	re_get([1, 2, 3], ".*", "r", 0)
		returns "3"

	re_get([1, 2, 3], "4", "l", 0)
		returns an empty string

	re_get([1, 2, 3], ".*", "l", 1)
		returns "2"
```
This method searches for a regex pattern in a list of string elements and returns the string if there is a match.

### re_group(pattern, string[, i])
```
	re_group("String1(.*)String3", "String1String2String3")
		returns "String2"
		
	re_group("^.*(String2).*$", "STRING1STRING2STRING3", "i")
		returns "STRING2"
```
This method returns an existing group match within a string.

Optionally, it is also possible to set an ignoreCase flag ("i").

Note: With this method, you can only extract _one_ group.

### re_replace(string, old, new)
```
	re_replace("old Old old Old", "(o|O)ld", "new")
		returns "new new new new"
```
This method searches for a regex pattern and replaces it with a new substring.

### substring(string, index, length)
```
	substring("Hello world", 0, 1)
		returns the substring "H" from the string "Hello world",
		which is the substring from index 0 with length 1.

	substring("Hello world", 5, 3)
		returns the substring "wor" from the string "Hello world",
		which is the substring from index 5 (the w) with a length of 3 chars.

	substring("Hello world", 5)
		returns the substring "world" from the string "Hello world",
		which is from position 5 to the end of the string.
```
This method extracts a substring from a string with a given index and length.

### trim(string)
```
	trim("hallo welt")
		returns "hallo welt" (unchanged)

	trim("  hallo welt")
		returns "hallo welt" (stripped whitespace from the beginning)

	trim("hallo welt   ")
		returns "hallo welt" (stripped whitespace from the end)

	trim("  hallo welt   ")
		returns "hallo welt" (stripped whitespace from the beginning and the end)
```
this method cuts away trailing and preceding whitespaces from a string.

### upper(string)
```
	upper("string")
		returns "STRING"
```
Converts a string to uppercase.

## Numeric methods

### count(list)
```
	count([1, 2, 10, 12, 14])
		returns 5
```
This method can be used to count the elements in a list.

### date_difference(date, date)
```
	date_difference("16.05.1983", "19.05.1983")
		returns 3

	date_difference("19.05.1983", "16.05.1983")
		returns -3
```
This method returns the difference between two dates as an integer number of days. The expected time format is dd.MM.yyyy.

### len(type)
```
	len("string")
		returns 6

	len(1234567890)
		returns 10
```
Calculates the length of the string representation of a value.

### list_pos(list, search_string)
```
	list_pos([$property1, $property2, $property3], "$property3")
		if truth($property3) is true:
			returns 2, because property3 is the third element in the list
		if truth($property3) is false:
			returns -1

	list_pos([$property1, $property2, $property3], "$property4")
		returns -1

	list_pos(["hallo", "welt"], "hallo")
		returns 0, because "hallo" is in the first position of the list

	list_pos(["hallo", "welt"], "ciaosen")
		returns -1, because the searched string "ciaosen" was not found in the list
```
This method finds the position of a property in a list.
This one needs context. A list of properties (also called a group) may contain properties that evaluate to false while rendering, thus making the list shorter. To find out, at what position our property of interest is in the list, we can use this method.

### max(list)
```
	max([1,2,3,6,4,5])
		returns 6
```
Extracts the maximum number from a list of numerics.

### min(list)
```
	min([1,2,3,4,5,6])
		returns 1
```
This method returns the lowest number of a list of numerics.

### month_no(month)
```
	month_no("Januar")
		returns 0, because january is the first month in a year

	month_no("February")
		returns 1, because february is the second month of a year
```
This method can be used to convert a month into a numerical representation

Note: This method only supports the german and english notation of months.

### rnd_int(left_bound, right_bound)
```
	rnd_int(0, 10)
		returns a numeric between 0 and 10
```
This method returns a random integer number.

It requires a left bound as well as a right bound statement.

### round(double[, decimals])
```
	round(0.6)
		returns - 1

	round(0.144743575, 2)
		returns - 0.14
```
This method rounds a numeric value.
There's an optional parameter to set the decimals to round to.

Note: The behavior of round() for doubles can be surprising:
For example, round(2.675, 2) gives 2.67 instead of the expected 2.68.
This is not a bug: It’s a result of the fact that most decimal fractions can’t be represented exactly as a doubles.

### weekday_int(days)
```
	weekday_int(1)
		returns the integer 2 (Tuesday), if today is a monday

  weekday_int(5)
    - returns the integer 6 (Saturday), if today is a monday
```
This method takes a numeric n between 1 and 7. It returns a numeric representation of the weekday of today + n days.
The returned numeric is to be interpreted as follows:

Weekday	|	Numeric
------	|	--------
Monday	|	1
Tuesday	|	2
Wednesday	|	3
Thursday	|	4
Friday	|	5
Saturday	|	6
Sunday	|	7

### weekday_no(day)
```
	month_no("Dienstag")
		returns number 2, because tuesday is the second day in a week

	month_no("monday")
		returns number 1, because monday is the first day of the week
```
This method can be used to convert a weekday into a numerical representation.

Note: This method only supports the german and english notation of weekdays.

## Boolean methods

### contains(type, list)
```
	contains(2, [1, 2, 3, 4, 5])
		returns true

	contains("welt", ["hallo", "welt", "!"])
		returns true

	contains("5555", ["hallo", "welt", "!"])
		returns false

	contains("hellblau", ["rot", "grün", "Blau"], "substring")
		returns true

	contains("hellblau", ["rot", "grün", "blau"])
		returns false because substring search is not active.
```
This method can be used to check if an element is inside a list.

### has_entry(type, entry)
```
	has_entry("noun", "tire")
		returns true

	has_entry("noun", "thisIsNotAWord")
		returns false
```
This method checks if an entry contains as lemma in the lexicon in the given language.

### in_range(number, left_bound, right_bound)
```
	in_range(6, 5, 10)
		returns true
		
	in_range(12, 5, 10)
		returns false
```
Checks if a numeric value lies between two other values.

### is_date(string)
```
	is_date("16.05.1983")
		returns true

	is_date("string")
		returns false
```
This method checks if a string value is in a correct date format.

### re_match(pattern, string[, i])
```
	re_match("String\d", "String1String2")
		returns true

	re_match("String\d", "STRING1STRING2", "i")
		returns true

	re_match("String2", "String1String2")
		returns false
```
This method returns true, if a string starts with a defined pattern.

Optionally, it is also possible to set an ignoreCase flag ("i").

### re_search(pattern, string[, i])
```
	re_search("String\d", "String1String2")
		returns true

	re_search("String\d", "STRING1STRING2", "i")
		returns true

	re_search("String2", "String1String2")
		returns true
```
This method returns true, if a string contains a defined pattern.

Optionally, it is also possible to set an ignoreCase flag ("i").

## List methods

### collect(list, fieldname)
```
	collect([{ name: "gerät 1" }, { name: "gerät 3" }, { name: "gerät 2" }], "name")
		returns ["gerät 1", "gerät 2", "gerät 3"]
```
Takes a field from all objects in a list and returns those field values as a list.

### filter(list, object/lambda_expression)
> Example list:

```
    [
        { "type": "goal", "team": "host", "score": "1-0" },
        { "type": "yellowcard", "team": "guest" },
        { "type": "goal", "team": "guest", "score": "1-1" },
        { "type": "redcard", "team": "host" },
        { "type": "goal", "team": "host", "score": "2-1" }
    ]
```

> Example method calls:

```
	filter(list($list), { "type": "goal", "team": "host" })
		returns a list that includes the objects from the given input list that contain entries having type=goal and team=host,
		in our case entries with number one and five of the original list.

	filter(list($list), { "type": "yellowcard" })
		returns a list with entries that have type=yellowcard,
		in our example entry two of the original list.

	filter(list($list), [entry -> #entry.type == "yellowcard" ])
		returns the same thing as the last example but uses a lambda expression to match the object.
		In this example the entry variable of the lambda expression contains the complete object to be matched.
```
Filters a list of objects for the elements that match a given filter or lambda expression.

### first(list, number)
```
	first([ 1, 2, 3, 4, 5 ], 3)
		returns [1, 2, 3]

	first([ 1, 2, 3, 4, 5 ], 5)
		returns [1, 2, 3, 4, 5]
	 
	first([ 1, 2, 3, 4, 5 ], 6)
		returns also [1, 2, 3, 4, 5]
```
Gets n elements from a list, starting left.

### intersection(list, list)
```
	intersection([1, 2, 3], [1, 2, 4])
		returns [1, 2]
```
Returns elements of two lists that are present in both lists.

### split(string[, delimiter])
```
	split("string1 string2 string3")
		returns ["string1", "string2", "string3"]

	split("string1, string2, string3", ", ")
		returns ["string1", "string2", "string3"]
```
This method returns a splitted string as a list.

Optionally, it is possible to set a delimiter. The default delimiter is " ".

### random_el(list, number)
```
	random_el([1, 2, 3, 4, 5], 2)
		returns for example [3, 5, 2]

	random_el(list($list), 5)
		returns for example [5, 3, 1, 2, 4]
```  
This method gets random elements from a list.  

### re_keep(list, pattern, direction[, position])
```
	re_keep(["xyz1", "abc", "xyz2"], "xyz.")
		returns ["xyz1", "xyz2"]

	re_keep(["xyz1", "abc", "xyz2"], "xyz.", "l", 1)
		returns ["xyz2"]

	re_keep(["xyz1", "abc", "xyz2"], "xyz.", "r", 1)
		returns ["xyz1"]
```
This method searches for a regex pattern in a list and returns a list of all matched elements.
Optionally, a starting postition and a search direction can be given.

* `list` - the list to search in
* `pattern` - regex pattern
* `direction` - the search direction ("r" or "l")
* `position` - starting position

### re_remove(list, pattern, direction[, position])
```
	re_remove(["xyz1", "abc", "xyz2"], "abc")
		returns ["xyz1", "xyz2"]

	re_remove(["xyz1", "abc", "xyz2"], "abc", "l", 1)
		returns ["xyz1", "xyz2"]

	re_remove(["xyz1", "abc", "xyz2"], "xyz.", "r", 1)
		returns ["xyz1", "abc"]
```
This method searches for a regex pattern in a list and returns a list of all elements that do not contain matched elements.
Optionally, a starting postition and a search direction can be given.

* `list` - the list to search in
* `pattern` - regex pattern
* `direction` - the search direction ("r" or "l")
* `position` - starting position

### map(list, lambda_expression[, context])
```
	map([1, 2, 3], [entry -> numeric(#entry) * 2])
		returns [2, 4, 6]

	map([{"score": "1-0", "player": "Dennis"}, {"score": "1-1", "player": "Baris"}, {"score": "2-1", "player": "Niki"}], [entry -> #entry.player])
		returns ["Dennis", "Baris", "Niki"]

	map([{"score": "1-0", "player": "Dennis"}, {"score": "1-1", "player": "Baris"}, {"score": "2-1", "player": "Niki"}], [entry, index, context -> #entry.player + " (" + #index + ") [" + #context + "]"], "context" )
		returns ["Dennis (0) [context]", "Baris (1) [context]", "Niki (2) [context]"]
	 
	map(["Niki", "Sandro"], [entry, index, context -> #entry + \" (\" + #context[#index] + \".)\"], [5, 90])
		returns ["Niki (5.)", "Sandro (90.)"]
```
Applies a method to all elements of a list and returns a list of objects with the result of applying the lambda.

### sort(list[, fieldname/lambda_expression])
```
	sort([5, 4, 3, 2, 1])
		returns [1, 2, 3, 4, 5]

	sort([ {"type": "tor3", "minute": 80}, {"type": "tor1", "minute": 60}, {"type": "gelb", "minute": 10} ], "minute")
		returns a sorted list with original elements sorted by the minute key in them, thus ["gelb", "tor1", "tor3"]

	sort([ "type": "tor3", "minute": 80}, {"type": "tor1", "minute": 60}, {"type": "gelb", "minute": 10} ], [a, b -> int(#a.minute) - int(#b.minute)])
		returns the same output but now by a lambda expression
```
Sorts a list numerically, a list of objects by a given field or by a lambda expression that compares the objects contained in the list.

### unique(list)
```
	unique([1, 2, 3, 1, 2])
		returns [1, 2, 3]
```
Returns a list with unique elements.

### split_lookup()
```
	split_lookup(#duftnoten, ", ", "headnotes")
		- splits the contents of the data set duftnoten at the string ", " and looks up all resulting elements in a lookup table called headnotes.
		- If duftnoten contains "heiliges holz, fisch, knoblauch" for example and the headnotes lookup table looks like this:

		"heiliges holz" => "Holz, heiliges"
		"fisch" => "Fisch"
		"knoblauch is missing and the result of the whole lookup will be a list consisting of "Holz, heiliges" and "Fisch".

	split_lookup( ["heiliges holz", "grün", "fisch"], "headnotes")
		- does not split a string but looks up each list element, everything else is as in ex. 1.
		There are only two argument this time, as no split marker is necessary.
```
Performs a lookup for fitting properties in a known lookup table. This is defined in the ATML3 training but is planned to come from Nummer5 later.

## JSON object methods

### next_event()

Searches in a list the next element from an index. Assume the following list:

```
    [
        { "id":"1", "type": "goal", "team": "host", "score": "1-0" },
        { "id":"2", "type": "yellowcard", "team": "guest" },
        { "id":"3", "type": "goal", "team": "guest", "score": "1-1" },
        { "id":"4", "type": "redcard", "team": "host" },
        { "id":"5", "type": "goal", "team": "host", "score": "2-1" }
    ]
```

```
   next_event( list($list), 2, { "type": "goal" } )
     - searches from index 2 (id = 3) the next event with type = "goal", which in this case is the element with id = 5 (index 4).
```

Parameters:

* list - List to be filtered
* startindex - index to start the search from
* filter - Definition of the filter as key/value pair. Applicable for equal filters only!


The method prev_event searches in the other direction. Is no event found, an empty object is returned.

### prev_event()

Searches for the last occurrence of an element in a list before a given index. Assume the list:

```
    [
        { "id":"1", "type": "goal", "team": "host", "score": "1-0" },
        { "id":"2", "type": "yellowcard", "team": "guest" },
        { "id":"3", "type": "goal", "team": "guest", "score": "1-1" },
        { "id":"4", "type": "redcard", "team": "host" },
        { "id":"5", "type": "goal", "team": "host", "score": "2-1" }
    ]
```

```
   prev_event( list($list), 2, { "type": "goal" } )
     - Searches the next element with type = "goal" starting at index 2. Result would be the element with id = 1 (index 0).
```

Parameters

* list - List to be filtered
* startindex - index to start the search from
* filter - Definition of the filter as key/value pair. Applicable for equal filters only!

The method prev_event searches in the other direction. Is no event found, an empty object is returned.

### nr5()

With this instruction a data set of the world knowledge (Project: Nummer5) can be accessed. Definition: nr5(aggregator, search_criteria)
* aggregator - a string containing the name of the data aggregator in Nummer5
* search_criteria - an object that contains the search criteria in key/value form

```
    nr5("test_aggregator", { "key1": "bob", "key2": "alice" })
      - accesses the object, that is stored in the Nummer5 type "test_aggregator" and carries the value "bob" as key1 and "alice" as key2

    nr5("test_aggregator", { "key2": "python" })
      - accesses the object, that is stored in the Nummer5 type "test_aggregator" and carries the value "python" under key2
```
 
Return value is always a complete object from which properties can be selected by the property notation.

```
 properties: {
     "nummer5_test_1": {
		    "mappingExpression": "nr5(\"test_aggregator\", {\"key1\": \"monty\" })",
		    "truthExpression": "true",
		    "voc": []
	    },
	    "nummer5_test_1_key_2": {
	        "mappingExpression": "$nummer5_test_1.key2",
	        "truthExpression" : "true",
	        "voc": [ {noun: "[nummer5_test_1_key1.value()]" ]
	    }
	}
```

In this example the property nummer5_test_1_key_2 would take the value "python" and the property nummer5_test_1 the value { key1: "monty", key2: "python", ... } because that is defined in the test_aggregator.

With the following aggregator notation, the actual data aggregator name will be automatically extracted from the requests:
nummer5_doc_type

```
    nr5("nummer5_doc_type", {"id":#uuid})
```

### Navigating in nr5 objects
You can look up any path inside nr5 objects if you use the proper tricks. Look at the mapping expression in the example below. Here, we try to navigate into our number5 object, go into  a child named "branch" and there go into a child named "subbranch", which holds our key.

Note that ATML assumes that children of nr5 objects come as lists. You will have to add a dummy iterator "[0]" to every tier you want to walk through.

```
    "nummer5_test_2_key_2": {
	        "mappingExpression": "$nummer5_test_2.branch[0].subbranch[0].key2",
	        "truthExpression" : "true",
	        "voc": [ {noun: "[nummer5_test_2_key2.value()]" ]
	    }
```

### pick_object()

This method picks an object at the end of a key path out of a data set.

```
pick_object(#object.list, "fieldName", "value 2")
     In a data structure like this:
         {
             "object:" {
                 "list": [
                     { "fieldName": "value 1", ... },
                     { "fieldName": "value 2", ... },
                     ...
                 ]
             }
         }
         the object with the fieldName "value 2" will be picked.
 ```
 This is useful to pick elements out of deeply nested data structures.