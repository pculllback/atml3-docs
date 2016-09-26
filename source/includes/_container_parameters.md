# Container parameters<a name="container_parameters"></a>
Container parameters can be attached to a container to add instructions or information to the container.


## Alternative

```atml3
    [Text:;Alt:Nix gerendert]
     - renders "Nix gerendert"

   [no_vocabulary_property;Alt,text=Nix gerendert]
     - renders "Nix gerendert" if no_vocabulary_property has no vocabulary or is false. (Use syntax of example 1)
```

The container parameter `Alternative` is used to render an alternative text, if the container would not render anything otherwise.

## Bullet

```atml3
    [Gruppe.All();Bullet]
         - Generates a markdown bullet list like this:
             * Element_1
             * Element_2
             * Element_3

       [Gruppe.All();Bullet,format=HTML]
         - Generates a HTML Bullet list like this:
             <ul>
                 <li>Element_1</li>
                 <li>Element_2</li>
                 <li>Element_3</li>
             </ul>

       [Gruppe.All();Bullet,format=HTML,id=Test]
         - Generates a HTML Bullet list with an id:
             <ul id="Test">
                 <li>Element_1</li>
                 <li>Element_2</li>
                 <li>Element_3</li>
             </ul>

       [Gruppe.All();Bullet,format=BB]
         - Generates an BBCode Bullet list.
             [list]
                 [*]Element_1
                 [*]Element_2
                 [*]Element_3
             [/list]  
```

The `Bullet` parameter makes a group into a list of elements. By default, a markdown list will be generated, with the optional style-parameter the format can be switched to HTML or BBCode. This is however discouraged because we try to render everything through markdown and process it into other output types later.

Additionally an ID can be set to the element.


## Capitalize

```atml3
   [Text:ich bin kleingeschrieben;Capitalize]
     - renders "Ich bin kleingeschrieben"

   [hund_wort,prep=mit,case=Dat;Capitalize]
     - renders "Mit dem Hund", if the property hund_wort renders the vocabulary "Hund"
```

`Capitalize` is a container parameter that forces the first letter of the rendered string to be upper case.

## IMG

The IMG parameter generates an image.

Possible sub-parameters:

* text - alternative text of the image
* title - title of the image
* format - format of the image
 * markdown (default)
 * html
 * bb

```
	[Text:https://www.google.de/images/branding/googlelogo/1x/googlelogo_color_272x92dp.png;img]
	  - Generates a markdown image like this:
	      ![](https://www.google.de/images/branding/googlelogo/1x/googlelogo_color_272x92dp.png)
	      
	[Text:https://www.google.de/images/branding/googlelogo/1x/googlelogo_color_272x92dp.png;img,text=alt text]
	  - Generates a markdown image like this:
	      ![alt text](https://www.google.de/images/branding/googlelogo/1x/googlelogo_color_272x92dp.png)
	      
	[Text:https://www.google.de/images/branding/googlelogo/1x/googlelogo_color_272x92dp.png;img,title=This is the google logo]
	  - Generates a markdown image like this:
	      ![](https://www.google.de/images/branding/googlelogo/1x/googlelogo_color_272x92dp.png "This is the google logo")
	      
	[Text:https://www.google.de/images/branding/googlelogo/1x/googlelogo_color_272x92dp.png;img,text=alt text,title=This is the google logo]
	  - Generates a markdown image like this:
	      [alt text](https://www.google.de/images/branding/googlelogo/1x/googlelogo_color_272x92dp.png "This is the google logo")
```

## Keyword

```atml3
   [Text:der goodyear 500;Keyword,id=1,alt=der Reifen]
         - renders [Key,1,der goodyear 500,der Reifen]
         Depending on the defined keyword density the string `der goodyear 500` will be replaced with `der Reifen`.
```

With the `Keyword` parameter you can define multiple keywords within your generated texts. Every defined id is depending on the given keyword density.


## Kill

```python
   [Text:hallo] [Text:;Kill] [Text:welt]
     - prevents rendering, because the second container does not render anything and carries the Kill parameter
```

`Kill` is a parameter that prevents a sentence from being rendered if the container does not render to a text.


## Lower

```shell
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



## OnRandom

```atml3
   [Text:i'm here;OnRandom,percentage=25]
         - will output "i'm here" with a probability of 25 percent

       [Text:i'm here;OnRandom,percentage=LOGIC_percentage]
         - will output "i'm here" with a probability of $LOGIC_percentage percent and interpretes LOGIC_percentage as a numeric
```

OnRandom is a container param that will throw away a container param randomly.



## Preceding

```atml3
   [Text:welt;Preceding:hallo ]
     - renders "hallo welt"

   [drei.value();Preceding:,text=StückzahlDOPPELPUNKT ]
     - renders "Stückzahl: 3", if the property drei renders to 3.
```

Preceding is a container parameter that is used to insert text in front of a rendered string in a container.

## Raw

Raw is a container parameter that forces ignoring the text modulation part.

```
  [Text:https://www.google.de;raw]
    - renders "https://www.google.de" instead of "https://www.Google.De"

```



## Trailing

```atml3
   [Text:hallo;Trailing: welt]
     - renders "hallo welt"

   [drei.value();Trailing,text= Stück]
     - renders "3 Stück", if the property drei renders to 3
```

Trailing is a container parameter that is used to insert text behind a rendered string in a container.

## URL

The URL parameter generates an hyperlink.

Possible sub-parameters:

* text - clickable text in a link
* title - title of the link
* format - format of the link
 * markdown (default)
 * html
 * bb

```
  [Text:https://www.google.de;url]
	- Generates a markdown link like this:
		[https://www.google.de](https://www.google.de)

  [Text:https://www.google.de;url,text=click here]
	- Generates a markdown link like this:
		[click here](https://www.google.de)

  [Text:https://www.google.de;url,title=This is a link to google]
	- Generates a markdown link like this:
		[https://www.google.de](https://www.google.de "This is a link to google")

[Text:https://www.google.de;url,text=click here,title=This is a link to google]
	- Generates a markdown link like this:
		[click here](https://www.google.de "This is a link to google")
```

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
