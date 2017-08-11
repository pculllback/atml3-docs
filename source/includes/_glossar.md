# Glossar
## API
Access point for data and texts, accessible by third party software (PIMs, CMS’).

## ATML3 (Automated Text Markup Language)
A configuration language defined by AX in which rules for automated text generation can be implemented.

## Cockpit
Current, integrated entry point to the AX NLG-Cloud-Plattform. Provides access to imported data, the created rule sets and also to the generated texts.
Reachable via: cockpit.ax-semantics.com

## Container
Variable content  in a Sentence that mostly refers to a -> Property. A container is marked by [ ] in the wizard and in the cockpit.

## Group
List of more than one ->properties. Used to implement multiple-value operations or enumerations.

## Lexicon
Dictionary of the AX NLG-Cloud platform, used by the text engine to look up the number and gender of a word and also the spelling of a word in the desired grammatical case

## Lookup
They are used to look up strings in a ->Training and translate one string into another.

## mappingExpression
Part of a ->property. Pulls data from a data set value or another property and can modify it. Used to create ->Groups.

## MyAX
Deprecated entry point to the AX NLG-Cloud-Platform. Provides Access to the uploaded data and the texts created for it.
Reachable via: my.ax-semantics.com.

## Property
Smallest unit of a ->Training. Consists of a ->mappingExpression, a ->truthExpression and a ->Property Output. Used for reading data, changing data and to make logical conclusions.

## Trigger
->Property that is used to switch a sentence or ->Story Type on or off. The value of its ->truthExpression controls if the sentence or the Story Type may appear.

## Text Rule Set
Contains all sentences needed for the automated text generation, including several wording variants.

## Story Type
Sequence of sentences. Every ->Training can have several but must at least have of them.

## Training
Rule set that contains all linguistic content and logical rules necessary for the automated content production.

## truthExpression
Part of a ->Property. It makes logical decisions and switches its ->Property Output on and off. May never be empty.

## Property Output
Part of a ->Property. Contains the text that a property will output into a sentence. It itself consists of a noun, an adjective and a headnoun.

## Wizard
Deprecated Web-App to create and modify ->Trainings.
Reachable via: wizard.ax-semantics.com.
