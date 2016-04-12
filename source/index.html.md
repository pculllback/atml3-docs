---
title: API Reference


toc_footers:
  - <a href='http://cloud.ax-semantics.com'>Sign Up for a Developer Key</a>
  - <a href='https://www.ax-semantics.com'>Powered by AX</a>


search: true
---

# ATML3 Syntax Documentation

### Welcome to the realms of ATML3
This site describes the basic functions and commands of the ATML3 programming language. With this handy expression language, you can train an artificial intelligence to write your stuff. All of it.
Just feed it structured data and the ATML engine will promptly churn it into a meaningful text in almost no time.
But first off, you will need to tell the ATML Engine how to text for you. And that is what you do in an ATML3 training.

### Sounds cool, but what can I actually do with it?
Your training contains reasoning: It will tell the ATML Engine how to analyze and map your data. Once trained, the engine can draw conclusions from your data and build a text about them. You can define rules to influence wording, word construction and the appearance of many other aspects in the text. (Vertigo Expression Language)
You can also tell the ATML engine in what way to mention the information it has concluded from your data. (Sentences) (Containers)
Don't forget microplanning and textplanning. That is also an aspect of ATML3. (Product Types)
Once you have your information planned and pinned down, you can do the fine-tuning and have grammar and apply to it. (Containers)

### What else do I need to work with ATML3?
First, you need an account at ax-semantics.com to work with ATML3. Don't worry, it comes for free. Once you have an account, log into my.ax-semantics.com, go to your profile page and retrieve your API token there.
You will also need your account unlocked for editing ATML3 and using our wizards. At the moment, you will have to contact us via slack. Just click the speech bubble icon on my.ax-semantics.com and leave us a message.
Second, you will need one of our editors for ATML3. Choose one among the options at atml3.rocks. 
Further, you will need structured data about your topic. If you want to know how to integrate your data into AX, use the API documentation at apidocs.ax-semantics.com.

# Container parameters
Container parameters can be attached to a container to add instructions or information to the container.

The following parameters are supported:

## Alternative

```atml3
    [Text:;Alt:Nix gerendert]
     - renders "Nix gerendert"
     
   [no_vocabulary_property;Alt,text=Nix gerendert]
     - renders "Nix gerendert" if no_vocabulary_property has no vocabulary or is false. (Use syntax of example 1)
```

The container parameter Alternative is used to render an alternative text, if the container would not render anything otherwise. 


## Capitalize

```atml3
   [Text:ich bin kleingeschrieben;Capitalize]
     - renders "Ich bin kleingeschrieben"
     
   [hund_wort,prep=mit,case=Dat;Capitalize]
     - renders "Mit dem Hund", if the property hund_wort renders the vocabulary "Hund"
```
 
Capitalize is a container parameter that forces the first letter of the rendered string to be upper case. 


## Kill

```atml3
   [Text:hallo] [Text:;Kill] [Text:welt]
     - prevents rendering, because the second container does not render anything and carries the Kill parameter
``` 

Kill is a parameter that prevents a sentence from being rendered if the container does not render to a text. 


## Lower

```
    [Text:ICH BIN GROSSGESCHRIEBEN;Lower]
     - renders "ich bin grossgeschrieben"
     
   [hund_wort,prep=mit,case=Dat;Lower]
     - renders "mit dem hund", if the property hund_wort renders "Hund"
```
Lower is a parameter that forces the rendered string of a container to be all lower case. 


## On

```atml3
   [Text:test;On,true=bool_property]
     - only renders "test", if the property bool_property is true.
    
   [Text:test;On,false=bool_property]
     - only renders "test", if the property bool_property is false.
```
 
On is a container parameter that activates or deactivates according to a condition. 



## Off

```atml3
   [Text:test;Off,true=bool_property]
     - only renders "test", if the property bool_property is false.
    
   [Text:test;Off,false=bool_property]
     - only renders "test", if the property bool_property is true.
```

Off is a container parameter that activates or deactivates according to a condition. 



## Preceeding

```atml3
   [Text:welt;Preceeding:hallo ]
     - renders "hallo welt"
     
   [drei.value();Preceeding:,text=Stückzahl: ]
     - renders "Stückzahl: 3", if the property drei renders to 3.
``` 

Preceeding is a container parameter that is used to insert text in front of a rendered string in a container. 



## Trailing

```atml3
   [Text:hallo;Trailing: welt]
     - renders "hallo welt"
     
   [drei.value();Trailing,text= Stück]
     - renders "3 Stück", if the property drei renders to 3
```

Trailing is a container parameter that is used to insert text behind a rendered string in a container. 



## Void

```
   [dog_phrase,id=test123;Void]
     - renders nothin but can be referenced by grammar-from=test123 and will deliver it's grammatical properties
```

Void is a container parameter that prevents a container from rendering an actual string but preserves its grammatical properties. It is mostly used as a reference for grammar containers. 
 
Alias: `NoOut`


## Source

```
[hund_wort,prep=mit,case=Dat;Source:mit dem Hund]
```

Source is a container parameter that can be filled with an intended output.



## Keyword

```
   [Text:der goodyear 500;Keyword,id=1,alt=der Reifen]
     - here the engine will either display "der goodyear 500" or the alternative text "der Reifen"
       depending on the random selection.
```

To create a keyword, you need to set the keyword parameter with an ID and an alternative text within a container. The ID is needed for defining multiple keywords. The engine will choose randomly a selection of defined keywords in consideration of the density and deviation. Both can be adjusted in the advanced content project configuration.


# Containers

In this section the different containers and their parameters are described. Preliminary: A property generally consists of three parts:

* `truth value` - is the property active? Can it be used?
* `value` - data stored for that property
* `vocabulary` - stuff to be rendered if the property is called in a container.

Some of the containers, for example PhraseContainer and ValueContainer are supposed to render vocabulary (or value, respectively). Containers can react to the truth value of properties.

## Appeal container

```atml3
        [Appeal:reader,id=reader]
            renders to "Du", "Ihr" or "Sie", depending what formality is set. Formality is a parameter set in the myAX.
         
        [Appeal:reader,pronoun=reflexive,case=dat]
            renders to "dir", "ihnen" or "euch", depending what formality is set.
```

The appeal container can be used to adress the reader.

Parameter:

* `pronoun`: default: personal, pronomensart personal, reflexive or possessive
* `case`: default: Nom, the grammatical case

## Fail Container
If this container is rendered in a sentence, the rendering of the text itself is finished with an error message to the myAX. The error message is then displayed to the user. 

```atml3
    [Fail:Der Wert load_index ist nicht im gültigen Wertebereich;On:fehlerbedingung=true]
    The error message appears in the myAX if the container is rendered. The rendering can controlled by On and Off container parameters. 
```
    
The container does not lead to output in the text itself.

## Grammar Container
This container can be used to render words with their grammatical function and preset grammatical information.

 ```atml3
    [G:verb=gehen,num=s,person=1st;preceeding:ich ]
        - renders "ich gehe"
        
    [G:noun=Charakter,num=p]
        - renders "Charaktere" because nominative is the default case and plural was set as numerus.
        
    [G:adjective=niedlich,case=gen,num=s,gender=f,det=def]
        - renders "niedlichen", as in "der niedlichen Katze"
 ```        
        
The grammar container is intended to be used to render words, from which other words can inherit grammatical information. This can be useful if the case of something changes when a word giving grammatical information is replaced by a synonym or adjective groups which change the numerus of their noun shall be rendered.

Some defaults are set, all other fields must be filled:

* nouns:
 * case = nominative

* verbs:
 * person = 3rd
 * tense = present (default), past, etc ... depends on the target language

* adjectives:
 * case = nominative
 * determiner = kein
 * conjunctions: eg. und_sowie_KOMMA_oder for "rotes und blaues sowie grünes Haus":

The first two are for adjectives in the default position (here "und" and "sowie").
The default position is controlled by the language of the text. For german, the default position is in front of the noun, in spanish it is behind.

The other two conjunctions are for the non default position (here "KOMMA" and "oder"). They are necessary for spanish and french, for example.

The grammar container can be used to render verbs, if a "Du/Sie" switch was to be implemented.

```atml3
    Den Duft [G:verb=riechen,grammar-from=reader] [appeal:reader,id=reader] direkt nach der Anwendung.
      - This sentence renders to "Den Duft riechen Sie direkt nach der Anwendung"  if the engine renders in SIE mode
      - This sentence renders to "Den Duft riechst du direkt nach der Anwendung"  if the engine renders in DU mode
      - This sentence renders to "Den Duft riecht Ihr direkt nach der Anwendung"  if the engine renders in IHR mode
      
    Robben [G:verb=treffen,person=3rd,tense=past] mit dem Ball.
      - Robben traf mit dem Ball
      
    Robben [G:verb=treffen,person=3rd] mit dem Ball.
    Robben [G:verb=treffen,person=3rd,tense=present] mit dem Ball.
      - Robben trifft mit dem Ball
```

With grammar-from you can inherit stuff from other containers. Directly defining a parameter overrides the inheritance (for example person=3rd will override the inherited person). 

If you want to explicitly inherit single properties you can use the following parameters:

* grammar-from-case
* grammar-from-num
* grammar-from-gender
* grammar-from-det
* grammar-from-person
* grammar-from-tense


## Group Container
A group container outputs a part of a list. There are several selectors available, namely:
* `Best(n)` - the first n valid elements of the list
* `All()` - all valid elements
* `AllRandom()` - like All(), but in random order.
* `Last(n)` - the last n valid elements of the list
* `Random(n)` - n elements of the list chosen at random

Assume the property "group" has the mappingValue ["rot", "gelb", "grün", "blau"]. The container looks as follows:

```atml3
  [group.All()]
    - renders all members of the group, namely "rot, gelb, grün, blau"
    
  [group.Best(3)]
    - renders the first 3 elements of the group, namely "rot, gelb, grün"
    
  [group.Last(3)]
    - renders the last 3 elements of the group, namely "gelb, grün, blau"
    
  [group.All(),conj=oder]
    - renders all elements of the list but inserts a conjunction before the last element: "rot, gelb, grün oder blau" . The conjunction is free text.
    
  [group.Range(1, 2)]
    - renders the second and third element of the group (index is 0-based): "gelb, grün"
    ///
  [group.AllRandom(),conj=oder]
    - like .All() but randomizes the order of the elements.
```

The group container also knows grammatical properties:
* `adj` - are adjectives to be rendered if present? (yes/no; default: no)
* `adjconj` - conjunctions for adjectives in the form und_oder_KOMMA_MODIFIER.
* `case` - grammatical case for the elements to be rendered in. (language dependent; default: Nom)
* `det` - determiner to preceed every element (default: kein)
* `prep` - preposition to be placed in front of the whole string once ("auf dem Haus und dem Dach"; default: none)
* `conj` - conjunction before the last list element (eg rot, gelb und grün; default: ,)
* `pronoun` - renders only a pronoun of the list. (personal: "er, sie, es" or demonstrative: "dieser, diese, dieses")

## Phrase Container
A phrase container renders the vocabulary of a property. The property can itself contain containers. The vocabulary is rendered with grammatic properties.

Defaults:
`adj - adjective: Nein`
`case - Nom`
`det - determiner; default: keiner`
`prep - preposition; default: keine`
`pronoun - pronoun: Nein`

Examples for rendering (assume there is a property named "Hund" with an adjective "braun" and a noun "Hund")
```atml3
  [wort]
    - renders "Hund"
    
  [wort,case=Gen]
    - renders "Hundes"
  
  [wort,case=Gen,det=indefinite]
    - renders "eines Hundes"
    
  [wort,case=Gen,det=definite,prep=mit]
    - renders "mit des Hundes"
    
  [wort,case=Dat,adj=yes,det=definite,prep=mit]
    - renders "mit dem braunen Hund"
    
  [wort,pronoun=demonstrative,case=Dat,prep=mit]
    - renders "mit diesem" 
    
  [wort,pronoun=ihrsein,case=Dat,prep=mit,reference=subject]
    - renders "mit seinem" or "mit ihrem", depending on the gender of the container "subject"
```    
    
    
Permitted values for the parameters:

* `adj` - yes/no
* `adjconj` - und_sowie_KOMMA_oder
* `case` - language dependent; in german: Nom/Gen/Dat/Akk
* `prep` - free text
* `pronoun` - demonstrative(dieser, diese, dieses)/personal(er, sie, es)/demonstrative2(der, die, das)
* `det` -
 * `none` - no determiner, default
 * `def` - definite article, "der Hund"
 * `indef` - indefinite article, "ein Hund"
 * `demonstrative` - demonstrative article, "dieser Hund"
 * `your` - possessive determiner, "Ihr Hund"
 * `sein` - possessive determiner, "sein Hund"
 * `ihrsein` - possesive determiner able to print "sein" and "ihr", chosen by reference=containerID
 * `num-to` - sg (force singular), pl (force plural)


## Text Container
A text container simply renders a string.

```
  [Text:hallo, welt!]
    - renders "hallo, welt!"
```

Rendering of simple text by a container is useful if container parameters need to be applied to that text.

```
  [Text:dies ist ein test;Capitalize;On,merkmal=true]
    - renders "Dies ist ein test" if the boolean value of the property "merkmal" is true.
    - renders nothing otherwise
```    
    


## Value Container

Value Containers just render the value (defined by the mappingExpression) for a property. They ignore the vocabulary. They can add grammatical informations and render with a case and determiner. Default values are case = Nom and determiner = def. In einem Container wären Beispiele

```atml3
              [merkmalsname.value()]
                - renders the value of a property, case=Nom and det=none
                
              [merkmalsname.value(),case=Dat]
                - renders the value of a property, overrides case with Dativ and does not use a determiner
                
              [merkmalsname.value(),case=Dat,det=definite]
                - renders the value of the property with a definitite determiner and in Dativ.
                
              [merkmalsname.value(),use_numerals=true]
                - renders the value and if it's a numerical value (eg 4) it will perform a lookup to find out if it's a number with a special word if 
                  special words are used in the current language by convention (eg in German: 0 = null, 1 = ein, 2 = zwei, ... till 12 = zwölf, theese may
                  differ in other languages).
            
              [merkmalsname.value(),use_numerals=true,numeral_type=cardinal]
                - use cardinal or ordinal to switch what kind of number to render.
```
            
The cases that exist are language dependent, eg Nom, Gen, Dat, Akk in German. Determiners might be
* `none` - default, no determiner
* `def` - definite determiner, zB der Hund
* `indef` - indefinite determiner, zB. ein Hund
* `demonstrative` - demonstrative determiner, zB. dieser Hund
* `your` - possesive determiner, zB. Ihr Hund
* `sein` - possessive determiner, zB. sein Hund

If a numeric property is rendered, use_numerals=true can be used to render number words in the current language. This is not implemented for all supported languages. If a numeric property is rendered, singular and plural can be inherited from the container using grammar-from or grammar-from-num . 



# Product Types
The product_types enable creating one training for different kinds of things. The sentence selector is the component chosing the sentences that are to be rendered. It works as follows:

<aside class="notice">
In the GUI, these are called "Story Types".
</aside>


1. Choose a product type
2. Choose all sentences that are listed in that product type
3. Filter those sentences, whose sentence triggers are not true

Deciding on a product type, ATML3 first tries to select an element of product_types that is not named "default" and whose triggers are true. (BEWARE: sentences need only one true trigger, for product types all triggers must be true) If none fits, the product type named "default" will be chosen.

It looks like this in the training:

```atml3
	product_types: [
        {
            "name": "produkt_1",
            "triggers": ["my_property"],
            "sentenceOrder": [ "Satz_02" ]
        },
        { 
            "name": "default", 
            "sentenceOrder":  [ "satz_01" ]
        }
    ],
```

In this example, product type "produkt_1" would be chosen if and only if the truthExpression of the property "my_property" evalues to true. Otherwise, the "default" product type would be chosen.

# Sentences

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
*  TODO `BulletGroupContainer` - renders multiple properties to a bulletpoint list in markdown syntax

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
   [propertyName,case=Dat,adj=yes,det=definite]
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
* an event Product Type

```atml3
{
 "name": "Tor",
 "truggers": ["CURRENT_INDEX"],
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

# Vertigo Expression Language
The vertigo expression language is a collection of operations and functions which calculate logic and linguistic properties in an ATML3 training.

Vertigo expressions are used in the mappingExpression and the truthExpression of a property and have values of certain data types.

## Expression Languages

### contains()

This function can be used to check if an element is inside a list. 
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

### convert_comma(input, divisor, lowerUnit, upperUnit)

This function takes a numeric value and converts it to a distance or time value.
```atml3
  convert_comma(5300, 1000, "m", "km")
    renders string "5,3 km"
    
  convert_comma(900, 1000, "m", "km")
    renders string "900 m"
    
  convert_comma(120, 60, "Minuten", "Stunden")
    renders string "2 Minuten"
```

### convert_count(input, divisor, lowerUnit, upperUnit[, conjunction])

This function takes a numeric value and converts it to a currency or date value.
Optionally, a conjunction can be given. 
```atml3
  convert_count(145, 60, "Minuten", "Stunden")
    returns string "2 Stunden 25 Minuten"
    
  convert_count(45, 60, "Minuten", "Stunden")
    returns string "45 Minuten"
    
  convert_count(350, 100, "Cent", "Euro")
    returns string "3 Euro 50 Cent"
    
  convert_count(350, 100, "Cent", "Euro", "und")
    returns string "3 Euro und 50 Cent"
```

### cur_lang()

This function returns the current language in the current text generation process as an ISO 2-letter code. 
```atml3
  cur_lang()
    returns "de", "es" or "en" or whatever language is currently used.
```

### date_add(date, number, type)

This function adds a time value to a given date and returns that new date.
These types of times can be added: years, months, weeks, days, hours, minutes, seconds.
```atml3
  date_add("16.05.1983", 3, "years")
    returns string "16.05.1986"
```

### date_difference(date, date)
```atml3
  date_difference("16.05.1983", "19.05.1983")
    returns numeric 3

  date_difference("19.05.1983", "16.05.1983")
    returns numeric -3
```
This function returns the difference between two dates as an integer number of days.
Expected time format is dd.MM.yyyy.



### date_convert(date, format)
```atml3
  date_convert("16.05.1983", "yyyy-MM-dd")
    returns string "1983-05-16"
```
This function converts a date value to a specific format


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
This function returns the date in the following format: dd.MM.yyyy



### formatNumber()
```atml3
  format_number(2, 2)
    returns 2.00 as string (english) or 2,00 (german)
```
This function formats a number to enforce a certain number of decimal digits and converts it to the correct locale



### has_entry(type, entry)
```atml3
  has_entry("noun", "tire")
    returns true
    
  has_entry("noun", "thisIsNotAWord")
    returns false
```
This function checks if an entry contains as lemma in the lexicon. 


### in_range()
```atml3
  in_range(#value, 5, 10)
    - returns the truth value "true" if the value lies between 5 and 10.
      It implements the function 5 ≤ #value ≤ 10
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
This function checks if a string value is in a correct date format.


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

This function finds the position of a property in a list.
This one needs context. A list of properties (also called a group) may contain properties that evaluate to false while rendering, thus making the list shorter. To find out, at what position our property of interest is in the list, we can use this function.


### month_no()
```atml3
  month_no("Januar")
    returns number 0 because january is the first month in a year
    
  month_no("February")
    returns number 1 because february is the second month of a year. 
    NB that german and english month names can be used as parameters
```
This function can be used to convert a month into a numerical representation 


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

This function searches for a regex pattern in a list of string elements and returns the string if there is a match.

* `list` - The list to search in``
* `pattern` - RegEx Pattern
* `direction` - Direction to search in ("r" or "l")
* `position` - The position of the list element

### re_keep(list, pattern, direction[, position])
```atml3
  re_keep(["xyz1", "abc", "xyz2"], "xyz.")
    - returns the list ["xyz1", "xyz2"]
    
  re_keep(["xyz1", "abc", "xyz2"], "xyz.", "l", 1)
    - returns the list ["xyz2"]
    
  re_keep(["xyz1", "abc", "xyz2"], "xyz.", "r", 1)
    - returns the list ["xyz1"]
```

This function searches for a regex pattern in a list and returns a list of all matched elements.
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
This function searches for a regex pattern in a list and returns a list of all elements that do not contain matched elements.
Optionally a starting postition and a search direction can be given
* `list` - The list to search in
* `pattern` - regex pattern
* `direction` - The direction to search in ("r" or "l")
* `position` - starting position


### render($property)
```atml3
  render($property)
    - returns the string "kleine Katze" if property's adjective field contains "klein" and its noun field contains "Katze"
```
This function takes a property and returns the content of its vocabulary.


### substring()
```atml3
  substring("Hello world", 0, 1)
    extracts the substring "H" from the string "Hello world", which is the substring from index 0 with length 1
    
  substring("Hello world", 5, 3)
    extracts the substring wor from the string "Hello world", which is the substring from index 5 (the w) with a length of 3 chars.
    
  substring("Hello world", 5)
    extracts the substring "world" from the string "Hello world", which is from position 5 to the end (leaving the optional parameter length unset)
```
This vertigo function will extract a substring from a string.




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

this function cuts away trailing and preceeding whitespaces from a string 



### unique(list)
```atml3
  unique([1, 2, 3, 1, 2])
    returns the [1, 2, 3]
```
Returns a list with unique elements. 


### weekday_int(days)
```atml3 
  weekday_int(1)
    - returns the integer 2 (Tuesday), if today is a monday.
    
  weekday_int(5)
    - returns the integer 6 (Saturday), if today is a monday.
```

This function takes an integer n. It returns a numeric representation of the weekday of today+n days.
The returned integer is to be interpreted as follows:

|Weekday|	Integer|
|Monday|	1|
|Tuesday|	2|
|Wednesday|	3|
|Thursday|	4|
|Friday|	5|
|Saturday|	6|
|Sunday|	7| 



### weekday_no()
```atml3
  month_no("Dienstag")
    returns number 2 because tuesday is the second day in a week (monday = 1)
    
  month_no("monday")
    returns number 1 because monday is the first day of the week (sunday = 7) 
    NB that german and english weekday names can be used as parameters
```
This function can be used to convert a weekday into a numerical representation






