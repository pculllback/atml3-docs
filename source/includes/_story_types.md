# Story types<a name="story_types"></a> 

Story types determine the order of the sentences you want to set.

ATML3 first tries to select a story type that is not named "default" and whose triggers are true (BEWARE: sentences need only one true trigger, for story types all triggers must be true). If none fits, the story type named "default" will be chosen.

```
name: "default",
"triggers": ["my_property_01"],
"sentenceOrder": [ "sentence_01", "sentence_02", "sentence_03" ]

name: "story_type_01",
"triggers": ["my_property_02"],
"sentenceOrder": [ "sentence_03", "sentence_02", "sentence_01" ]

In this example, story type "story_type_01" would be chosen if and only if the truth value of the property "my_property_02" is true. Otherwise, the "default" story type would be chosen.
```