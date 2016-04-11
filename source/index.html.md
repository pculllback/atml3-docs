---
title: API Reference

language_tabs:
  - atml3

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

The container parameter Alternative is used to render an alternative text, if the container would not render anything otherwise. 

```atml3
    [Text:;Alt:Nix gerendert]
     - renders "Nix gerendert"
     
   [no_vocabulary_property;Alt,text=Nix gerendert]
     - renders "Nix gerendert" if no_vocabulary_property has no vocabulary or is false. (Use syntax of example 1)
 ```

## Capitalize

Captalize is a container parameter that forces the first letter of the rendered string to be upper case. 

```atml3
   [Text:ich bin kleingeschrieben;Capitalize]
     - renders "Ich bin kleingeschrieben"
     
   [hund_wort,prep=mit,case=Dat;Capitalize]
     - renders "Mit dem Hund", if the property hund_wort renders the vocabulary "Hund"
 ```

## Kill

Kill is a parameter that prevents a sentence from being rendered if the container does not render to a text. 

```atml3
   [Text:hallo] [Text:;Kill] [Text:welt]
     - prevents rendering, because the second container does not render anything and carries the Kill parameter
```atml3 

## Lower

Lower is a parameter that forces the rendered string of a container to be all lower case. 

```
    [Text:ICH BIN GROSSGESCHRIEBEN;Lower]
     - renders "ich bin grossgeschrieben"
     
   [hund_wort,prep=mit,case=Dat;Lower]
     - renders "mit dem hund", if the property hund_wort renders "Hund"
```

## On

On is a container parameter that activates or deactivates according to a condition. 

```
   [Text:test;On,true=bool_property]
     - only renders "test", if the property bool_property is true.
    
   [Text:test;On,false=bool_property]
     - only renders "test", if the property bool_property is false.
 

Off

Off is a container parameter that activates or deactivates according to a condition. 

Examples:
   [Text:test;Off,true=bool_property]
     - only renders "test", if the property bool_property is false.
    
   [Text:test;Off,false=bool_property]
     - only renders "test", if the property bool_property is true.
```

## Preceeding

Preceeding is a container parameter that is used to insert text in front of a rendered string in a container. 

```
   [Text:welt;Preceeding:hallo ]
     - renders "hallo welt"
     
   [drei.value();Preceeding:,text=Stückzahl: ]
     - renders "Stückzahl: 3", if the property drei renders to 3.
``` 

Trailing

Trailing is a container parameter that is used to insert text behind a rendered string in a container. 

```
   [Text:hallo;Trailing: welt]
     - renders "hallo welt"
     
   [drei.value();Trailing,text= Stück]
     - renders "3 Stück", if the property drei renders to 3
```

## Void

Void is a container parameter that prevents a container from rendering an actual string but preserves its grammatical properties. It is mostly used as a reference for grammar containers. 

```
   [dog_phrase,id=test123;Void]
     - renders nothin but can be referenced by grammar-from=test123 and will deliver it's grammatical properties
```
 
Alias: `NoOut`


## Source

Source is a container parameter that can be filled with an intended output.

```
[hund_wort,prep=mit,case=Dat;Source:mit dem Hund]
```


## Keyword

To create a keyword, you need to set the keyword parameter with an ID and an alternative text within a container. The ID is needed for defining multiple keywords. The engine will choose randomly a selection of defined keywords in consideration of the density and deviation. Both can be adjusted in the advanced content project configuration.

```
   [Text:der goodyear 500;Keyword,id=1,alt=der Reifen]
     - here the engine will either display "der goodyear 500" or the alternative text "der Reifen"
       depending on the random selection.
```

# Product Types
The product_types enable creating one training for different kinds of things. The sentence selector is the component chosing the sentences that are to be rendered. It works as follows:

<aside class="notice">
In the GUI, these are called "Story Types".
<aside>


1. Choose a product type2
2. Choose all sentences that are listed in that product type
3. Filter those sentences, whose sentence triggers are not true

Deciding on a product type, ATML3 first tries to select an element of product_types that is not named "default" and whose triggers are true. (BEWARE: sentences need only one true trigger, for product types all triggers must be true) If none fits, the product type named "default" will be chosen.

It looks like this in the training:
```
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

```
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
* name - used to reference the sentence in the sentence order list inside the product_types and sentence groups.
* trigger - List of property names. One of the properties must be true for the sentence to be available. If the sentence is to be always * available, the trigger "Auto" has to be added.
* obligatory - true/false; If true, the sentence may not be discarded on text shortening.
* command - Used to activate the story mode.
* variants - Variants of the sentences as string.
* role - Role of the sentences like heading1 or heading2.
* style - The way the sentence is to be displayed.
 * heading - heading h1
 * subheading - heading h2
 * subsubheading - heading h3

For every chosen sentence a variant should be chosen and made to a RenderedSentence in the engine. The ATML3 containers in the variant are parsed. A sentence mostly consists of ATML3 containers and free text. The free text implicitly is converted to Text containers. Assume a training that is rendered with the following data set
```json
 { "tiername": "hund", "tierfarbe": "braun", "anzahl_beine": "4" } 
``` 
and fills propertys with the same names as the dataset keys. The following sentences result:
```
   Der [tiername] hat [anzahl_beine.value()] Beine.
   - Der Hund hat 4 Beine.
   
   [Text:Der ][tiername][Text: hat ][anzahl_beine.value()][Text: Beine.]
   - Der Hund hat 4 Beine.
   
   [tiername,det=definite] hat [anzahl_beine.value()] Beine.
   - Der Hund hat 4 Beine.
```
 
Die Container die derzeit in der ATML3.0 Sprache existieren sind (anlehnung bei Namen an ATML2.5)

* Textcontainer - render static text
* ValueContainer - render the raw value of aproperty
* PhraseContainer - render the value given by a property's vocabulary
* GroupContainer - renders multiple properties
* Failure - raises an expected engine error including an error message
* TODO: BulletGroupContainer - renders multiple properties to a bulletpoint list in markdown syntax
* The containers are described in ther respective chapters. The general format is as follows:

### Kinds of tags

ATML3 tags can be classified into the following:

#### Named Tags

```
   [Text:The text that is to be rendered]
   [Fail:The error message that is to be displayed]
```

#### Normal Tags

```
   [propertyName]
   [propertyName.value()]
   [propertyName,case=Dat,adj=yes,det=definite]
``` 
 
All ATML-Tags can have parameters. To learn more about those options, go to the section containers.




