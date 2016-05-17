# Properties<a name="properties"></a>

```
1.
{
	"animal": "DOG",
	"color": "brown",
	"legs": 4,
	"breed": ""
}

2.
{
	"DATA_animal": {
		"truthExpression": "str(#animal) != \"\"",
		"mappingExpression": "str(#animal)"
	},
	"DATA_color": {
		"truthExpression": "str(#color) != \"\"",
		"mappingExpression": "str(#color)"
	},
	"DATA_legs": {
		"truthExpression": "numeric(#legs) != 0",
		"mappingExpression": "numeric(#legs)"
	},
	"DATA_breed": {
		"truthExpression": "str(#breed) != \"\"",
		"mappingExpression": "str(#breed)"
	}
}

2.
{
	"DATA_animal": {
		"truthExpression": "str(#animal) != \"\"",
		"mappingExpression": "str(#animal)"
	},
	"DATA_color": {
		"truthExpression": "str(#color) != \"\"",
		"mappingExpression": "str(#color)"
	},
	"DATA_legs": {
		"truthExpression": "numeric(#legs) != 0",
		"mappingExpression": "numeric(#legs)"
	},
	"DATA_breed": {
		"truthExpression": "str(#breed) != \"\"",
		"mappingExpression": "str(#breed)"
	}
}

3.
{
	"DATA_animal": {
		"truthExpression": "str(#animal) != \"\"",
		"mappingExpression": "str(#animal)",
		"voc": {
			"en-US": [{
				"noun": "[DATA_animal.value()]",
				"adjective": "",
				"headnoun": ""
			}]
		}
	},
	"DATA_color": {
		"truthExpression": "str(#color) != \"\"",
		"mappingExpression": "str(#color)",
		"voc": {
			"en-US": [{
				"noun": "[DATA_color.value()]",
				"adjective": "",
				"headnoun": ""
			}]
		}
	},
	"DATA_legs": {
		"truthExpression": "numeric(#legs) != 0",
		"mappingExpression": "numeric(#legs)",
		"voc": {
			"en-US": [{
				"noun": "[DATA_legs.value()]",
				"adjective": "",
				"headnoun": ""
			}]
		}
	},
	"DATA_breed": {
		"truthExpression": "str(#breed) != \"\"",
		"mappingExpression": "str(#breed)",
		"voc": {
			"en-US": [{
				"noun": "[DATA_breed.value()]",
				"adjective": "",
				"headnoun": ""
			}]
		}
	}
}
```

With properties, you can define truth and mapping conditions and vocabularies which refer to your data.

Thus a single property consists of three parts:

* `Truth Expression` - is the property active? Can it be used?
* `Mapping Expression` - data field storage and its modification
* `Vocabulary` - consists of three parts and contains the content to be rendered if the property is called in a container
 * bli
 * bla
 * blub

Let's take an example, assume a JSON data set is given (see item 1).

Now we create four properties which..

* check if the given fields are actually filled (truthExpression in item 2) and
* contain its values (mappingExpression in item 2).

After that, we add a vocabulary to each property to display the content if a container is called. If you want to use the content of the property itself, just paste [property_name.value()] in the noun field of the vocabulary (see item 3). 