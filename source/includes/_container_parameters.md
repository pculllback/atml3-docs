# Container parameters<a name="container_parameters"></a>
Container parameters can be attached to a container to add instructions or information to the container.


## Alternative

```atml3
    [text:;alt:Nix gerendert]
     - renders "Nix gerendert"

   [no_vocabulary_property;alt,text=Nix gerendert]
     - renders "Nix gerendert" if no_vocabulary_property has no vocabulary or is false. (Use syntax of example 1)
```

The container parameter `alt` (for alternative) is used to render an alternative text, if the container would not render anything otherwise.

## List

```atml3
    [Gruppe.all();list]
         - Generates a markdown list like this:
             * Element_1
             * Element_2
             * Element_3
			 
	[Gruppe.all();list,type=ordered]
         - Generates a markdown list like this:
             1. Element_1
             2. Element_2
             3. Element_3

	[Gruppe.all();list,format=HTML]
         - Generates a HTML list like this:
             <ul>
                 <li>Element_1</li>
                 <li>Element_2</li>
                 <li>Element_3</li>
             </ul>
			 
	[Gruppe.all();list,format=HTML,type=ordered]
         - Generates a HTML list like this:
             <ol>
                 <li>Element_1</li>
                 <li>Element_2</li>
                 <li>Element_3</li>
             </ol>

	[Gruppe.all();list,format=HTML,id=Test]
         - Generates a HTML list with an id:
             <ul id="Test">
                 <li>Element_1</li>
                 <li>Element_2</li>
                 <li>Element_3</li>
             </ul>
			 
	[Gruppe.all();list,format=HTML,id=Test,type=ordered]
         - Generates a HTML list with an id:
             <ol id="Test">
                 <li>Element_1</li>
                 <li>Element_2</li>
                 <li>Element_3</li>
             </ol>

	[Gruppe.all();list,format=BB]
         - Generates an BBCode list like this:
             [list]
                 [*]Element_1
                 [*]Element_2
                 [*]Element_3
             [/list]
			 
	[Gruppe.all();list,format=BB,type=ordered]
         - Generates an BBCode list like this:
             [list=1]
                 [*]Element_1
                 [*]Element_2
                 [*]Element_3
             [/list]
```

The `list` parameter makes a group into a list of elements. By default, a markdown list will be generated, with the optional style-parameter the format can be switched to HTML or BBCode. This is however discouraged because we try to render everything through markdown and process it into other output types later.

Additionally an ID can be set to the element.


## Capitalize

```atml3
   [text:ich bin kleingeschrieben;capitalize]
     - renders "Ich bin kleingeschrieben"

   [hund_wort,prep=mit,case=dat;capitalize]
     - renders "Mit dem Hund", if the property hund_wort renders the vocabulary "Hund"
```

`capitalize` is a container parameter that forces the first letter of the rendered string to be upper case.

## IMG

```
	[text:https://www.google.de/images/branding/googlelogo/1x/googlelogo_color_272x92dp.png;img]
	  - Generates a markdown image like this:
	      ![](https://www.google.de/images/branding/googlelogo/1x/googlelogo_color_272x92dp.png)

	[text:https://www.google.de/images/branding/googlelogo/1x/googlelogo_color_272x92dp.png;img,text=alt text]
	  - Generates a markdown image like this:
	      ![alt text](https://www.google.de/images/branding/googlelogo/1x/googlelogo_color_272x92dp.png)

	[text:https://www.google.de/images/branding/googlelogo/1x/googlelogo_color_272x92dp.png;img,title=This is the google logo]
	  - Generates a markdown image like this:
	      ![](https://www.google.de/images/branding/googlelogo/1x/googlelogo_color_272x92dp.png "This is the google logo")

	[text:https://www.google.de/images/branding/googlelogo/1x/googlelogo_color_272x92dp.png;img,text=alt text,title=This is the google logo]
	  - Generates a markdown image like this:
	      [alt text](https://www.google.de/images/branding/googlelogo/1x/googlelogo_color_272x92dp.png "This is the google logo")
```

The `img` parameter generates an image.

Possible sub-parameters are:

* `text` - alternative text of the image
* `title` - title of the image
* `format` - format of the image
 * markdown (default)
 * html
 * bb


## Keyword

```atml3
   [text:der goodyear 500;keyword,id=1,alt=der Reifen]
         - renders [Key,1,der goodyear 500,der Reifen]
         Depending on the defined keyword density the string `der goodyear 500` will be replaced with `der Reifen`.
```

With the `keyword` parameter you can define multiple keywords within your generated texts. Every defined id is depending on the given keyword density.


## Kill

```atml3
   [text:hallo] [text:;kill] [text:welt]
     - prevents rendering, because the second container does not render anything and carries the Kill parameter
```

`kill` is a parameter that prevents a sentence from being rendered if the container does not render to a text.


## Lower

```atml3
    [text:ICH BIN GROSSGESCHRIEBEN;lower]
     - renders "ich bin grossgeschrieben"

   [hund_wort,prep=mit,case=dat;lower]
     - renders "mit dem hund", if the property hund_wort renders "Hund"
```

`lower` is a parameter that forces the rendered string of a container to be all lower case.


## On

```atml3
   [text:test;on,true=bool_property]
     - only renders "test", if the property bool_property is true.

   [text:test;on,false=bool_property]
     - only renders "test", if the property bool_property is false.
```

`on` is a container parameter that activates or deactivates according to a condition.


## On_random

```atml3
   [text:i'm here;on_random,percentage=25]
         - will output "i'm here" with a probability of 25 percent

       [text:i'm here;on_random,percentage=LOGIC_percentage]
         - will output "i'm here" with a probability of $LOGIC_percentage percent and interpretes LOGIC_percentage as a numeric
```

`on_random` is a container param that will throw away a container param randomly.


## Preceding

```atml3
   [text:welt;preceding:hallo ]
     - renders "hallo welt"

   [drei.value();preceding:,text=StückzahlDOPPELPUNKT ]
     - renders "Stückzahl: 3", if the property drei renders to 3.
```

`preceding` is a container parameter that is used to insert text in front of a rendered string in a container.


## Raw

```atml3
  [text:https://www.google.de;raw]
	- renders "https://www.google.de" instead of "https://www.Google.De"
```

`raw` is a container parameter that forces ignoring the text modulation part.


## Trailing

```atml3
   [text:hallo;trailing: welt]
     - renders "hallo welt"

   [drei.value();trailing,text= Stück]
     - renders "3 Stück", if the property drei renders to 3
```

`trailing` is a container parameter that is used to insert text behind a rendered string in a container.


## URL

The `url` parameter generates an hyperlink.

Possible sub-parameters are:

* `text` - clickable text in a link
* `title` - title of the link
* `target` - specifies where to open the linked document
* `rel` - specifies the relationship between the current document and the linked document
* `format` - format of the link
 * markdown (default)
 * html
 * bb

```atml3
	[text:https://www.google.de;url]
		- Generates a markdown link like this:
			[https://www.google.de](https://www.google.de)

	[text:https://www.google.de;url,text=click here]
		- Generates a markdown link like this:
		[click here](https://www.google.de)

	[text:https://www.google.de;url,title=This is a link to google]
		- Generates a markdown link like this:
			[https://www.google.de](https://www.google.de "This is a link to google")
		
	[text:https://www.google.de;url,target=_blank,rel=nofollow]
		- Generates a markdown link like this:
			[https://www.google.de](https://www.google.de){:target="_blank" rel="nofollow"}

	[text:https://www.google.de;url,text=click here,title=This is a link to google]
		- Generates a markdown link like this:
			[click here](https://www.google.de "This is a link to google")
```


## Void

```atml3
   [dog_phrase,id=test123;void]
     - renders nothin but can be referenced by grammar-from=test123 and will deliver it's grammatical properties
```

`void` is a container parameter that prevents a container from rendering an actual string but preserves its grammatical properties. It is mostly used as a reference for grammar containers.


## Source

```atml3
[hund_wort,prep=mit,case=dat;source:mit dem Hund]
```

`source` is a container parameter that can be filled with an intended output.


## Keyword

```atml3
   [text:der goodyear 500;keyword,id=1,alt=der Reifen]
     - here the engine will either display "der goodyear 500" or the alternative text "der Reifen"
       depending on the random selection.
```

To create a keyword, you need to set the `keyword` parameter with an ID and an alternative text within a container. The ID is needed for defining multiple keywords. The engine will choose randomly a selection of defined keywords in consideration of the density and deviation. Both can be adjusted in the advanced content project configuration.
