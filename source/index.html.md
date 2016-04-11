---
title: API Reference

language_tabs:
  - atml3

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://www.axsemantics.com'>Powered by AX</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to the Kittn API! You can use our API to access Kittn API endpoints, which can get information on various cats, kittens, and breeds in our database.

# ATML3 Documentation
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

```
    [Text:;Alt:Nix gerendert]
     - renders "Nix gerendert"
     
   [no_vocabulary_property;Alt,text=Nix gerendert]
     - renders "Nix gerendert" if no_vocabulary_property has no vocabulary or is false. (Use syntax of example 1)
 ```

## Capitalize

Captalize is a container parameter that forces the first letter of the rendered string to be upper case. 

```
   [Text:ich bin kleingeschrieben;Capitalize]
     - renders "Ich bin kleingeschrieben"
     
   [hund_wort,prep=mit,case=Dat;Capitalize]
     - renders "Mit dem Hund", if the property hund_wort renders the vocabulary "Hund"
 ```

## Kill

Kill is a parameter that prevents a sentence from being rendered if the container does not render to a text. 

```
   [Text:hallo] [Text:;Kill] [Text:welt]
     - prevents rendering, because the second container does not render anything and carries the Kill parameter
``` 

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

Examples:
   [dog_phrase,id=test123;Void]
     - renders nothin but can be referenced by grammar-from=test123 and will deliver it's grammatical properties
 
Alias: NoOut

## Source

Source is a container parameter that can be filled with an intended output.

```
[hund_wort,prep=mit,case=Dat;Source:mit dem Hund]
```


Keyword

To create a keyword, you need to set the keyword parameter with an ID and an alternative text within a container. The ID is needed for defining multiple keywords. The engine will choose randomly a selection of defined keywords in consideration of the density and deviation. Both can be adjusted in the advanced content project configuration.

```
   [Text:der goodyear 500;Keyword,id=1,alt=der Reifen]
     - here the engine will either display "der goodyear 500" or the alternative text "der Reifen"
       depending on the random selection.
```
