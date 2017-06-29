# Sentences<a name="sentences"></a>

In the ATML3.0 training, sentences are defined. In the JSON tree, the structure is inside the sentences aray.

```atml3
 sentences: [
	{
		name: "satz_001",
		trigger: [ "Auto" ],
		obligatory: true,
		variants: [ "Property is true and shows value|[true_property.value()]|2NEWLINE", ]
	},
	...]
 ```

The sentence has the following fields:

* `name` - used to reference the sentence in the sentence order list inside the product_types and sentence groups.
* `trigger` - List of property names. One of the properties must be true for the sentence to be available. If the sentence is to be always
* `available`, the trigger "Auto" has to be added.
* `obligatory` - true/false; If true, the sentence may not be discarded on text shortening.
* `command` - Used to activate the story mode.
* `variants` - Variants of the sentences as string.
* `role` - Role of the sentences like heading1 or heading2.
* `style` - The way the sentence is to be displayed.
 * `heading` - heading h1
 * `subheading` - heading h2
 * `subsubheading` - heading h3

For every chosen sentence a variant should be chosen and made to a RenderedSentence in the engine. The ATML3 containers in the variant are parsed. A sentence mostly consists of ATML3 containers and free text. The free text implicitly is converted to Text containers. Assume a training that is rendered with the following data set

```json
 { "tiername": "hund", "tierfarbe": "braun", "anzahl_beine": "4" }
```

and fills propertys with the same names as the dataset keys. The following sentences result:

```atml3
   Der [tiername] hat [anzahl_beine.value()] Beine.
   - Der Hund hat 4 Beine.

   [Text:Der ][tiername][Text: hat ][anzahl_beine.value()][Text: Beine.]
   - Der Hund hat 4 Beine.

   [tiername,det=definite] hat [anzahl_beine.value()] Beine.
   - Der Hund hat 4 Beine.
```

Die Container die derzeit in der ATML3.0 Sprache existieren sind (anlehnung bei Namen an ATML2.5)

* `Textcontainer` - render static text
* `ValueContainer` - render the raw value of aproperty
* `PhraseContainer` - render the value given by a property's vocabulary
* `GroupContainer` - renders multiple properties
* `Failure` - raises an expected engine error including an error message

The containers are described in ther respective chapters. The general format is as follows:

### Kinds of tags

ATML3 tags can be classified into the following:

#### Named Tags

```atml3
   [Text:The text that is to be rendered]
   [Fail:The error message that is to be displayed]
```

#### Normal Tags

```atml3
   [propertyName]
   [propertyName.value()]
   [propertyName,case=dat,adj=yes,det=definite]
```

All ATML-Tags can have parameters. To learn more about those options, go to the section containers.

### Sentence Groups
Sentence groups can be used to apply selective operations on defined groups of sentences. A sentence group contains up to five different entries:

* `name` (string) - Each sentence group needs a unique identifier. This is also used for identification in "same"-mode.
* `mode` (string) - The following modes are available:
 * `best` - The first n active sentences are rendered.
 * `last` - The last n active sentences are rendered.
 * `random` - n random sentences are rendered
 * `same` - Same selects the exact same sentences as are selected in another sentence group. That requires the "reference"-entry, see below.
* `number` (int) - Determines the number of senteces to be rendered (-> n). It is not needed with the "same"-mode, as it will be inherited from the referenced group.
* `reference` (string) - Only needed in "same"-mode. Needs the name of another group as argument.
* `sentenceNames` (list of strings) - List of sentence names that belong to this sentence group.

```atml3
"sentenceGroups": [
  {
    "name": "sg1",
    "mode": "random",
    "number": 2,
    "sentenceNames": [
      "H1",
      "H1_2",
      "H1_3"
    ]
  },
  {
    "name": "sg2",
    "mode": "same",
    "reference": sg1",
    "sentenceNames": [
      "passende_Produkte",
      "passende_Produkte_2"
      "passende_Produkte_3"
    ]
  }
]
```

### Story Mode
ATML3 is capable of rendering a sequence of events in a so called "story mode". This mode behaves somewhat like a for loop does in programming. You will need this if you are looking to render a stream of events (goals in a soccer match or any other sorted event list).

##### prerequisites

a list of objects in your data
```json
goal: [
{
"player": "Harnik",
"minute": 5,
"type": "own_goal"
}, {
"player": "Werner",
"minute": 66,
"type": "goal"
}
]
```

a meta sentence that is included in your "default" sentence group

```atml3
{
 "name": "goals",
 "triggers": [ "Auto" ],
 "obligatory": true,
 "command": "[Meta:execute=Tor,items=event_list,iterator=CURRENT_EVENT,counter=CURRENT_INDEX]"
}

```

the meta command contains 4 different parameters (see below)
* `execute` - used to point to a sentence group
* `items` - ATML3 list property which contains the data
* `iterator` - object to access the inner data from the itemlist
* `counter` - internal counter for the story mode
* an event story type

```atml3
{
 "name": "Tor",
 "triggers": ["CURRENT_INDEX"],
 "sentenceOrder": [
 "goal_reg",
 "goal_own" ]
}
```

actual sentences that are rendered in this sentence group (goal_reg, goal_own)

```atml3
{
 "name": "goal_reg",
 "triggers": [ "LOG_Tor_not_1_0" ],
 "obligatory": true,
 "variants": { "de-DE" : [
 { "text": "NEWLINE★ [VOC_MinuteTor;trailing:.] Minute: [VOC_Score_Tor] durch [VOC_SpielerTor]!" } ]
}
```
ATML3 properties (these are a bit different since we are iterating over objects)

a list property that contains the list of objects from above

```atml3
"goal": {
 "mappingExpression": "list($spieldaten.goal)",
 "truthExpression": "int(count(list($spieldaten.goal))) >= 0",
 "voc": { "*" : [ { "noun": "[goal.value()]" } ] }
 }
2 meta properties for the story loop
"CURRENT_INDEX": {
 "mappingExpression" : "-1",
 "truthExpression" : "false"
 },
"CURRENT_EVENT" : {
 "mappingExpression" : "{}",
 "truthExpression" : "false"
 }

```

properties that point to the object in order to extract information from it

```atml3
"TRIGGER_current_event_is_goal" : {
 "mappingExpression" : "",
 "truthExpression" : "$CURRENT_EVENT.event_type == \"goal\""
 },
"VOC_SpielerTor": {
 "mappingExpression": "$CURRENT_EVENT.player",
 "truthExpression": "true",
 "voc": { "de-DE" : [ { "noun": "[VOC_SpielerTor.value()]" } ] }
 },
"VOC_MinuteTor": {
 "mappingExpression": "$CURRENT_EVENT.minute",
 "truthExpression": "true",
 "voc": { "de-DE" : [ { "noun": "[VOC_MinuteTor.value()]" } ] }
 },
"VOC_TeamTor": {
 "mappingExpression": "$CURRENT_EVENT.team",
 "truthExpression": "true",
 "voc": { "de-DE" : [ { "noun": "[VOC_TeamTor.value()]" } ] }
 },
"VOC_ScoreTor": {
 "mappingExpression": "$CURRENT_EVENT.score",
 "truthExpression": "true",
 "voc": { "de-DE" : [ { "noun": "[VOC_ScoreTor.value()]" } ] }
 }
```