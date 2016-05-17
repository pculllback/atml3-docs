# Properties<a name="properties"></a>

With properties, you can define truth and mapping conditions and vocabularies which refer to your data.

Thus a single property consists of three parts:

* `Truth Expression` - is the property active? Can it be used?
* `Mapping Expression` - data field storage and its modification.
* `Vocabulary` - contains the content to be rendered if the property is called in a container. It consists of a language node which again consists of three parts: 
 * `noun` - enter here the noun of the property.
 * `adjective` - enter here the adjective of the property.
 * `headnoun` - enter here a word that should be used as representation for inflections instead of the original noun.
 
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

> After that, we add a vocabulary to each property to set the content if a container is called.
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

> Maybe you have noticed it already, the data set contains a field which can be used as an adjective (color)! So now, we can just paste the DATA_color property as an adjective of the DATA_animal property.

```
{
	"DATA_animal": {
		"truthExpression": "str(#animal) != \"\"",
		"mappingExpression": "str(#animal)",
		"voc": {
			"en-US": [{
				"noun": "[DATA_animal.value()]",
				"adjective": "[DATA_color.value()]",
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

> That's it for now, we have already created four valid properties with truth/mapping expressions and vocabularies! However, these properties are still pretty basic. If you want to see the true power of properties, just take a look at the next section "Methods".