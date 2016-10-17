# Containers<a name="containers"></a> 

In this section the different containers and their parameters are described.

Some of the containers, for example PhraseContainer and ValueContainer are supposed to render vocabulary (or value, respectively). Containers can react to the truth value of properties.

## Container basics

```atml3
        [main_expression;trailing:);preceding:(]
        [main_expression,case=dat,prep=mit,det=definite;on,true=other_expression]

        [LIST_of_expressions.all()]
        [LIST_of_expressions.random(2)]
```

Containers go into sentences and their purpose is to "summon" atml rules, values and vocabulary into the sentences. They point at a property to be summoned into the text, but also define how the grammar module will inflect and construct the output of the property, so it will fit into the syntax of the sentence.

Containers are separated from the rest of the sentence by brackets [ and ]. They consist of a main expression and parameters. Parameter. The main expression can either be a property, a grouped property, a grammar container or text. All  types except text come with a set of grammar subparameters.

Remember:

* If a parameter accepts any string (free text), you delimit by ":"
* If a parameter expects only certain strings (choice), you delimit by "="
* Parameters are separated by ";"
* Subparameters are separated by ","
* If you refer to a certain aspect of a container, you delimit by "."
* If that aspect is a method (draw the best out of a group, retrieve the value, etc.), you will need to add "([the method's argument])"


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

```atml3
    [Fail:Der Wert load_index ist nicht im gültigen Wertebereich;On:fehlerbedingung=true]
    The error message appears in the myAX if the container is rendered. The rendering can be controlled by On and Off container parameters.
```

If this container is rendered in a sentence, the rendering of the text itself is aborted with an error message to the myAX. The error message is then displayed to the user.

The container does not lead to output in the text itself.

## Grammar Container
This container can be used to render words with their grammatical function and preset grammatical information.

 ```atml3
    [G:verb=gehen,num=s,person=1st;preceding:ich ]
        - renders "ich gehe"

    [G:noun=Charakter,num=p]
        - renders "Charaktere" because nominative is the default case and plural was set as numerus.

    [G:adjective=niedlich,case=gen,num=s,gender=f,det=def]
        - renders "niedlichen", as in "der niedlichen Katze"

    [G:determiner=def,num=s,gender=f]
        - renders "die"
 ```        

The grammar container is intended to be used to render words, from which other words can inherit grammatical information. This can be useful if the case of something changes when a word giving grammatical information is replaced by a synonym or adjective groups which change the numerus of their noun shall be rendered.

Some defaults are set, all other fields must be filled:

* nouns
 * case = nominative

* verbs
 * person = 3rd
 * tense = present (default), past, etc ... depends on the target language

* adjectives
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

> Assume the property "group" has the mappingValue ["rot", "gelb", "grün", "blau"]. The container looks as follows:

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

  [group.AllRandom(),conj=oder]
    - like .All() but randomizes the order of the elements.
```

A group container outputs a part of a list. There are several selectors available, namely:

* `Best(n)` - the first n valid elements of the list
* `All()` - all valid elements
* `AllRandom()` - like All(), but in random order.
* `Last(n)` - the last n valid elements of the list
* `Random(n)` - n elements of the list chosen at random
* `Range(m, n)` - all elements in the inclusive range of m and n will be chosen

The group container also knows grammatical properties:

* `adj` - are adjectives to be rendered if present? (true/false/first; default: false)
* `adjconj` - conjunctions for adjectives in the form und_oder_KOMMA_MODIFIER.
* `case` - grammatical case for the elements to be rendered in. (language dependent; default: Nom)
* `det` - determiner to preceed every element (default: kein)
* `prep` - preposition to be placed in front of the whole string once ("auf dem Haus und dem Dach"; default: none)
* `conj` - conjunction before the last list element (eg rot, gelb und grün; default: ,)
* `pronoun` - renders only a pronoun of the list. (personal: "er, sie, es" or demonstrative: "dieser, diese, dieses")

## Phrase Container

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

A phrase container renders the vocabulary of a property. The property can itself contain containers. The vocabulary is rendered with grammatic properties.

Defaults:

* `adj - adjective: false`
* `case - nom`
* `det - determiner; default: none`
* `prep - preposition; default: none`


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

```
  [Text:hallo, welt!]
    - renders "hallo, welt!"
```

A text container simply renders a string.

```
  [Text:dies ist ein test;Capitalize;On,merkmal=true]
    - renders "Dies ist ein test" if the boolean value of the property "merkmal" is true.
    - renders nothing otherwise
```

Rendering of simple text by a container is useful if container parameters need to be applied to that text.


## Value Container

> Some examples:

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

Value Containers just render the value (defined by the mappingExpression) for a property. They ignore the vocabulary. They can add grammatical informations and render with a case and determiner. Default values are case = Nom and determiner = def.

The cases that exist are language dependent, eg Nom, Gen, Dat, Akk in German. Determiners might be

* `none` - default, no determiner
* `def` - definite determiner, zB der Hund
* `indef` - indefinite determiner, zB. ein Hund
* `demonstrative` - demonstrative determiner, zB. dieser Hund
* `your` - possesive determiner, zB. Ihr Hund
* `sein` - possessive determiner, zB. sein Hund

If a numeric property is rendered, use_numerals=true can be used to render number words in the current language. This is not implemented for all supported languages. If a numeric property is rendered, singular and plural can be inherited from the container using grammar-from or grammar-from-num.
