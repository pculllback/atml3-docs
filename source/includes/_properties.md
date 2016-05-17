# Properties<a name="properties"></a>

With properties, you can define truth and mapping conditions and vocabularies which refer to your data.

Thus a single property consists of three parts:

* `Truth Expression` - is the property active? Can it be used?
* `Mapping Expression` - data field storage and its modification
* `Vocabulary` - consists of three parts and contains the content to be rendered if the property is called in a container
 * noun - enter here the noun of the property
 * adjective - enter here the adjective of the property
 * headnoun - enter here a word that should be used as representation for inflections instead of the original noun
 
> Let's take an example, assume following JSON data set is given:

```
{
	"animal": "DOG",
	"color": "brown",
	"legs": 4,
	"breed": ""
}
```

> Now we create four properties which check if the given fields are actually filled (truthExpression) and contain its values (mappingExpression):

```
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
```

> After that, we add a vocabulary to each property to display the content if a container is called.
> If you want to use the content of the property itself, just paste [property_name.value()] in the noun field of the vocabulary:

```
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