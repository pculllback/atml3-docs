# Methods<a name="methods"></a> 

With methods you can modify and format your own data to implement perfectly good stories.

Methods are used in mapping or truth expressions of properties and return following data types:

* Strings
* Numerics
* Booleans
* Lists

## String methods

### convert_comma(input, divisor, lowerUnit, upperUnit)
```atml3
  convert_comma(5300, 1000, "m", "km")
    returns "5,3 km"

  convert_comma(900, 1000, "m", "km")
    returns "900 m"

  convert_comma(120, 60, "Minuten", "Stunden")
    returns "2 Minuten"
```
This method takes a numeric value and converts it to a distance or time value.

### convert_count(input, divisor, lowerUnit, upperUnit[, conjunction])
```atml3
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
```atml3
  cur_lang()
    returns "de", "es" or "en" or whatever language is currently used.
```
This method returns the current language in the current text generation process as an ISO 2-letter code.

### date_add(date, number, type)
```atml3
  date_add("16.05.1983", 3, "years")
    returns "16.05.1986"
```
This method adds a time value to a given date and returns that new date.
These types of times can be added:

* years
* months
* weeks
* days
* hours
* minutes
* seconds

### date_convert(date, format)
```atml3
  date_convert("16.05.1983", "yyyy-MM-dd")
    returns string "1983-05-16"
```
This method converts a date value to a specific format

### date_format(date)
```atml3
  date_format("16.05.1983")
    returns string "dd.MM.yyyy"
```
Returns a date value's format.

### date_now()
```atml3
    date_now()
        - returns 13.06.2015
```
This method returns the date in the following format: dd.MM.yyyy

### formatNumber()
```atml3
  format_number(2, 2)
    returns 2.00 as string (english) or 2,00 (german)
```
This method formats a number to enforce a certain number of decimal digits and converts it to the correct locale

### join(list[, delimiter])

This method joins all elements of a list into a string.

Optionally, it is possible to set a delimiter.

```
             Input:
             join([1, 2, 3, 4, 5])

             Output:
             "12345"

             Input:
             join([1, 2, 3, 4, 5], ", ")

             Output:
             "1, 2, 3, 4, 5"
```

### lookup()

Performs a lookup for fitting properties in a known lookup table. This is defined in the ATML3 training but is planned to come from Nummer5 later.

```atml3
   lookup("summer", "reifen_art")
     - looks up the entry "summer" in the lookup table (of the current language) "reifen_art" and returns its value.
       If nothing is found, an empty string is returned.
 ```
Beware: This version can not return adjectives. Use a group and split_lookup() for that purpose.

### lower(string)

This method converts a string to it's lowercase form.

```
                lower("STRING")
                   - returns the string "string"
```

### render($property)
```atml3
  render($property)
    - returns the string "kleine Katze" if property's adjective field contains "klein" and its noun field contains "Katze"
```
This method takes a property and returns the content of its vocabulary.

### replace(string, old, new[, max])

This method replaces all occurrences of a substring with a new stated substring.

Optionally, it is possible to set the number of times of replacements.

```
             Input:
             replace("old old old old", "old", "new")

             Output:
             "new new new new"

             Input:
             replace("old old old old", "old", "new", 2)

             Output:
             "new new old old"
```

### replace_last(string, old, new)

This method replaces the last occurrence of a substring with a new stated substring.

```
             Input:
             replace("1, 2, 3, 4", ",", "and")

             Output:
             "1, 2, 3 and 4"
```

### re_get(list, pattern, direction, position)
```atml3
  re_get([1, 2, 3], ".*", "l", 0)
    - returns the string "1"

  re_get([1, 2, 3], ".*", "r", 0)
    - returns the string "3"

  re_get([1, 2, 3], "4", "l", 0)
    - returns an empty string

  re_get([1, 2, 3], ".*", "l", 1)
    - returns the string "2"
```

This method searches for a regex pattern in a list of string elements and returns the string if there is a match.

* `list` - The list to search in``
* `pattern` - RegEx Pattern
* `direction` - Direction to search in ("r" or "l")
* `position` - The position of the list element

### re_group(pattern, string[, i])

This method returns an existing group match within a string.

Optionally, it is also possible to set an ignoreCase flag ("i").

```
             Input:
             re_group("String1(.*)String3", "String1String2String3")

             Output:
             "String2"

             Input:
             re_group("^.*(String2).*$", "STRING1STRING2STRING3", "i")

             Output:
             "STRING2"

```

### re_replace(string, old, new[, max])

This method replaces a substring with a regex pattern.

```
            Input:
            re_replace("old Old old Old", "(o|O)ld", "new")

            Output:
            "new new new new"

```

### substring()
```atml3
  substring("Hello world", 0, 1)
    extracts the substring "H" from the string "Hello world", which is the substring from index 0 with length 1

  substring("Hello world", 5, 3)
    extracts the substring wor from the string "Hello world", which is the substring from index 5 (the w) with a length of 3 chars.

  substring("Hello world", 5)
    extracts the substring "world" from the string "Hello world", which is from position 5 to the end (leaving the optional parameter length unset)
```
This vertigo method will extract a substring from a string.

### trim()
```atml3
    trim("hallo welt")
        - returns the string "hallo welt" (unchanged)

    trim("  hallo welt")
        - returns the string "hallo welt" (stripped whitespace from the beginning)

    trim("hallo welt   ")
        - returns the string "hallo welt" (stripped whitespace from the end)

    trim("  hallo welt   ")
        - returns the string "hallo welt" (stripped whitespace from the beginning and the end)
```

this method cuts away trailing and preceding whitespaces from a string

### upper(string)

Converts a string to uppercase.

```
                 upper("string")
                    - returns the string value "STRING"
```

## Numeric methods

### len(type)

Calculates the length of a string / the length of the string representation of a value.

```
                len("string")
                   - returns the numeric value 6

                len(1234567890)
                   - returns the value 10

```

### rnd_int([bndLeft, bndRight])

This method returns a random integer number.

It requires a left bound as well as a right bound statement.

```
            Input:
            rnd_int(0, 10)

            Output:
            4
```

### re_match(pattern, string[, i])

This method returns true, if a string starts with a defined pattern.

Optionally, it is also possible to set an ignoreCase flag ("i").

```
             Input:
             re_match("String\d", "String1String2")

             Output:
             true

             Input:
             re_match("String\d", "STRING1STRING2", "i")

             Output:
             true

             Input:
             re_match("String2", "String1String2")

             Output:
             false

```

### re_search(pattern, string[, i])

This method returns true, if a string contains a defined pattern.

Optionally, it is also possible to set an ignoreCase flag ("i").

```
             Input:
             re_search("String\d", "String1String2")

             Output:
             true

             Input:
             re_search("String\d", "STRING1STRING2", "i")

             Output:
             true

             Input:
             re_search("String2", "String1String2")

             Output:
             true

```

### round(double[, decimals])

This method rounds a numeric value.
There's an optional parameter to set the decimals to round to.


Note: The behavior of round() for doubles can be surprising:
For example, round(2.675, 2) gives 2.67 instead of the expected 2.68.
This is not a bug: it’s a result of the fact that most decimal fractions can’t be represented exactly as a doubles.

```
                    round(0.6)
                       - 1

                    round(0.144743575, 2)
                       - 0.14


```

### split(string[, delimiter])

This method returns a splitted string as a list.

Optionally, it is possible to set a delimiter.
The default delimiter is " ".

```
             Input:
             split("string1 string2 string3")

             Output:
             ["string1", "string2", "string3"]

             Input:
             split("string1, string2, string3", ", ")

             Output:
             ["string1", "string2", "string3"]

```

### contains()

This method can be used to check if an element is inside a list.

```atml3
  contains(2, [1, 2, 3, 4, 5])
    returns true since 2 is an element of the list containing the numbers from 1 to 5

  contains("welt", ["hallo", "welt", "!"])
    would also return true

  contains("5555", ["hallo", "welt", "!"])
    returns false

  contains("hellblau", ["rot", "grün", "Blau"], "substring")
    returns true since "blau" is contained in the word "hellblau"

  contains("hellblau", ["rot", "grün", "blau"])
    returns false because substring search is not active.
```

### date_difference(date, date)

```atml3
  date_difference("16.05.1983", "19.05.1983")
    returns numeric 3

  date_difference("19.05.1983", "16.05.1983")
    returns numeric -3
```

This method returns the difference between two dates as an integer number of days.
Expected time format is dd.MM.yyyy.

### has_entry(type, entry)
```atml3
  has_entry("noun", "tire")
    returns true

  has_entry("noun", "thisIsNotAWord")
    returns false
```
This method checks if an entry contains as lemma in the lexicon.


### in_range()
```atml3
  in_range(#value, 5, 10)
    - returns the truth value "true" if the value lies between 5 and 10.
      It implements the method 5 ≤ #value ≤ 10
```
Checks if a numeric value lies between two other values.



### intersection()
```atml3
  intersection([1, 2, 3], [1, 2, 4])
    returns list [1, 2]
```
Returns elements of two lists that are present in both lists.


### is_date(string)
```atml3
  is_date("16.05.1983")
    returns true

  is_date("value")
    returns false
```
This method checks if a string value is in a correct date format.

### month_no()
```atml3
  month_no("Januar")
    returns number 0 because january is the first month in a year

  month_no("February")
    returns number 1 because february is the second month of a year.
    NB that german and english month names can be used as parameters
```
This method can be used to convert a month into a numerical representation

### weekday_int(days)
```atml3
  weekday_int(1)
    - returns the integer 2 (Tuesday), if today is a monday.

  weekday_int(5)
    - returns the integer 6 (Saturday), if today is a monday.
```

This method takes an integer n. It returns a numeric representation of the weekday of today+n days.
The returned integer is to be interpreted as follows:

Weekday|	Integer
------ | --------
Monday|	1
Tuesday|	2
Wednesday|	3
Thursday|	4
Friday|	5
Saturday|	6
Sunday|	7

### weekday_no()
```atml3
  month_no("Dienstag")
    returns number 2 because tuesday is the second day in a week (monday = 1)

  month_no("monday")
    returns number 1 because monday is the first day of the week (sunday = 7)
    NB that german and english weekday names can be used as parameters
```
This method can be used to convert a weekday into a numerical representation

## List methods

### count(list)

This method can be used to count the elements in a list. Example:

```
               count([1, 2, 10, 12, 14])
                 - returns the number 5
```

### filter()

Filters a list of objects for the elements that match a given filter or λ-method. Given an example list:

```json
    [
        { "type": "goal", "team": "host", "score": "1-0" },
        { "type": "yellowcard", "team": "guest" },
        { "type": "goal", "team": "guest", "score": "1-1" },
        { "type": "redcard", "team": "host" },
        { "type": "goal", "team": "host", "score": "2-1" }
    ]
```

If one wants a list with all goals by the host team, they could use this method call:

```atml3
    filter( list($list), { "type": "goal", "team": "host" })
      - returns a list that includes the objects from the given input list that contain entries having type=goal and team=host, in our case
        entries with number one and five of the original list.

    filter( list($list), { "type": "yellowcard" })
      - returns a list with entries that have type=yellowcard, in our example entry 2 of the original list.

    filter( list($list), [entry -> #entry.type == "yellowcard" ])
      - does the same thing as the last example but uses a λ-method to match the object. in this example the entry variable of the λ-
        method contains the complete object to be matched.

    filter( list($list), [entry, index, context -> #entry.type == "yellowcard" ], object($context_object))
      - this is the maximum λ-method, which contains the current
```

Parameters:

* `list` - a list that should be filtered
* `filter` - a filter definition, either as a Key / Value object (equal filter only) or a λ-method (complex filters possible)
* `context` - something given to each call of the λ as a context object

### list_pos()

```atml3
  list_pos([$property1, $property2, $property3], "$property3")
    if truth($property3) == true:
      returns 2, because property3 is the third element in the list.
    if truth($property3) == false:
      returns -1

  contains([$property1, $property2, $property3], "$property4")
    returns -1

  contains(["hallo", "welt"], "hallo")
    returns 0, because "hallo" is in the first position of the list

  contains(["hallo", "welt"], "ciaosen")
    returns -1, because the searched string "ciaosen" was not found in the list
```

This method finds the position of a property in a list.
This one needs context. A list of properties (also called a group) may contain properties that evaluate to false while rendering, thus making the list shorter. To find out, at what position our property of interest is in the list, we can use this method.

### max(list)

Extracts the maximum number from a list of numerics.

```
                max([1,2,3,6,4,5])
                   - returns 6
```

### min(list)

This method returns the lowest number of a list.

```
              min([1,2,3,4,5,6])
               - returns 1
```

### random_el()


Gets random elements from a list. $list = [ 1, 2, 3, 4, 5 ]

```atml3
               random_el(list($list), 3)
                 - returns for example the elements 4 and 2 as a list, thus [4, 2]

               random_el(list($list), 5)
                 - would return all elements from the given list but in a random order, for example [5, 3, 1, 2, 4]
```    

Parameter:

* list - a list of things
* count - the number of items in the list to be returned

### re_keep(list, pattern, direction[, position])
```atml3
  re_keep(["xyz1", "abc", "xyz2"], "xyz.")
    - returns the list ["xyz1", "xyz2"]

  re_keep(["xyz1", "abc", "xyz2"], "xyz.", "l", 1)
    - returns the list ["xyz2"]

  re_keep(["xyz1", "abc", "xyz2"], "xyz.", "r", 1)
    - returns the list ["xyz1"]
```

This method searches for a regex pattern in a list and returns a list of all matched elements.
Optionally a starting postition and a search direction can be given

* `list` - The list to search in
* `pattern` - regex pattern
* `direction` - The direction to search in ("r" or "l")
* `position` - starting position


### re_remove(list, pattern, direction[, position])
```atml3
  re_remove(["xyz1", "abc", "xyz2"], "abc")
    - returns the list ["xyz1", "xyz2"]

  re_remove(["xyz1", "abc", "xyz2"], "abc", "l", 1)
    - returns the list ["xyz1", "xyz2"]

  re_remove(["xyz1", "abc", "xyz2"], "xyz.", "r", 1)
    - returns the list ["xyz1", "abc"]
```
This method searches for a regex pattern in a list and returns a list of all elements that do not contain matched elements.
Optionally a starting postition and a search direction can be given

* `list` - The list to search in
* `pattern` - regex pattern
* `direction` - The direction to search in ("r" or "l")
* `position` - starting position

### first(n)

Gets n elements from a list, starting left.

```atml3
    $list = [ 1, 2, 3, 4, 5 ]

   first(list($list), 3)
     - returns for example the elements 1, 2 and 3 as a list, thus [1, 2, 3]

   first(list($list), 5)
     - would return all elements from the given list in order, for example [1, 2, 3, 4, 5]
   first(list($list), 6)
     - would return all elements from the given list. Index overruns are caught, for example [1, 2, 3, 4, 5]
```

Parameter:
* list      ... a list of things
* count     ... the number of items in the list to be returned

### map()
```atml3
   map([1, 2, 3], [x -> numeric(#x) ** 2])
     - returns a list with the squares of the values of the input list

   map([{"score": "1-0", "player": "Dennis"}, {"score": "1-1", "player": "Baris"}, {"score": "2-1", "player": "Niki"}], [x -> #x.player])
     - returns a list with the names of the people who scored goals (in this case ["Dennis", "Baris", "Niki"])

   map([{"score": "1-0", "player": "Dennis"}, {"score": "1-1", "player": "Baris"}, {"score": "2-1", "player": "Niki"}], [x, y, z -> #x.player + " (" + y + ") [" + z + "]"], "context" )
     - uses all possible vars in the mapping: current_object, index and context object. supplies a context in form of a string
     - returns a list [ "Dennis (0) [context]", "Baris (1) [context]", "Niki (2) [context]" ]
   map([\"Niki\",\"Sandro\"], [entry,index,context -> #entry + \" (\" + #context[#index] + \".)\"], [5,90])
     - takes two lists and an lambda expression and combines them, resulting in a output list of: Niki (5.), Sandro (90.)
```

Applies a method to all elements of a list and returns a list of
objects with the result of applying the lambda: map(list, expression) - list ...
list of things that should be applied - expression ... the expression to be
applied to the elements

### next_event()

Searches in a list the next element from an index. Assume the following list:

```json
    [
        { "id":"1", "type": "goal", "team": "host", "score": "1-0" },
        { "id":"2", "type": "yellowcard", "team": "guest" },
        { "id":"3", "type": "goal", "team": "guest", "score": "1-1" },
        { "id":"4", "type": "redcard", "team": "host" },
        { "id":"5", "type": "goal", "team": "host", "score": "2-1" }
    ]
```

```atml3
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

```json
    [
        { "id":"1", "type": "goal", "team": "host", "score": "1-0" },
        { "id":"2", "type": "yellowcard", "team": "guest" },
        { "id":"3", "type": "goal", "team": "guest", "score": "1-1" },
        { "id":"4", "type": "redcard", "team": "host" },
        { "id":"5", "type": "goal", "team": "host", "score": "2-1" }
    ]
```

```atml3
   prev_event( list($list), 2, { "type": "goal" } )
     - Searches the next element with type = "goal" starting at index 2. Result would be the element with id = 1 (index 0).
```

Parameters

* list - List to be filtered
* startindex - index to start the search from
* filter - Definition of the filter as key/value pair. Applicable for equal filters only!

The method prev_event searches in the other direction. Is no event found, an empty object is returned.

### sort()

storts a list numerically, a list of objects by a given field or by a lambda method that compares the objects contained in the list:
```atml3
  sort(list)
  sort(list, fieldname)
  sort(list, expression)
```  
* list - list to be sorted
* fieldname - (optional) If the list to be sorted is a list of objects, sorts the objects using the field names.
* expression - (optional) If the list to be sorted is a list of objects, sorts the objects applying pairs of objects to a lambda expression

```atml3
   sort([5, 4, 3, 2, 1])
     - returns the list sorted by the values of the elements it contains: 1, 2, 3, 4, 5

   sort([ {"type": "tor3", "minute": 80}, {"type": "tor1", "minute": 60}, {"type": "gelb", "minute": 10} ], "minute")
     - returns a sorted list with original elements sorted by the minute key in them, thus being the types: "gelb", "tor1", "tor3"

   sort([ "type": "tor3", "minute": 80}, {"type": "tor1", "minute": 60}, {"type": "gelb", "minute": 10} ], [a, b -> int(#a.minute) - int(#b.minute)])
     - produced the same output as the previous example.
```

### unique(list)
```atml3
  unique([1, 2, 3, 1, 2])
    returns the [1, 2, 3]
```
Returns a list with unique elements.

### split_lookup()

Performs a lookup for fitting properties in a known lookup table. This is defined in the ATML3 training but is planned to come from Nummer5 later.

```atml3
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

### nr5()

With this instruction a data set of the world knowledge (Project: Nummer5) can be accessed. Definition: nr5(aggregator, search_criteria)
* aggregator - a string containing the name of the data aggregator in Nummer5
* search_criteria - an object that contains the search criteria in key/value form

```atml3
    nr5("test_aggregator", { "key1": "bob", "key2": "alice" })
      - accesses the object, that is stored in the Nummer5 type "test_aggregator" and carries the value "bob" as key1 and "alice" as key2

    nr5("test_aggregator", { "key2": "python" })
      - accesses the object, that is stored in the Nummer5 type "test_aggregator" and carries the value "python" under key2
```
 
Return value is always a complete object from which properties can be selected by the property notation.

```atml3
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

```atml3
    nr5("nummer5_doc_type", {"id":#uuid})
```

### Navigating in nr5 objects
You can look up any path inside nr5 objects if you use the proper tricks. Look at the mapping expression in the example below. Here, we try to navigate into our number5 object, go into  a child named "branch" and there go into a child named "subbranch", which holds our key.

Note that ATML assumes that children of nr5 objects come as lists. You will have to add a dummy iterator "[0]" to every tier you want to walk through.

```atml3
    "nummer5_test_2_key_2": {
	        "mappingExpression": "$nummer5_test_2.branch[0].subbranch[0].key2",
	        "truthExpression" : "true",
	        "voc": [ {noun: "[nummer5_test_2_key2.value()]" ]
	    }
```

### collect()

Takes a field from all objects in a list and returns those field values as a list.

Input:
```atml3  
     "devices": [ { name: "gerät 1" }, { name: "gerät 3" }, { name: "gerät 2" } ]
```

Operation:
```atml3
     collect( list(#devices, "name")
         - returns list: [ "gerät 1", "gerät 2", "gerät 3" ]
```

### pick_object()

This method picks an object at the end of a key path out of a data set.

```atml3
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