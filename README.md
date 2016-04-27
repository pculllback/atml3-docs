![AX Semantics](https://github.com/axsemantics/atml3-docs/blob/master/source/images/logo.png) Semantics ATML3 Docs
========

## How to Contribute to this documentation

* edit documentation in source/index.html.md
* public docs will be build automatically: [![Build Status](https://travis-ci.org/axsemantics/atml3-docs.svg?branch=master)](https://travis-ci.org/axsemantics/atml3-docs)


Dokumentation
-------------

Weitere Informationen über den [verwendeten Markdown-Stil](https://github.com/tripit/slate/wiki/Markdown-Syntax) und das [Deployment](https://github.com/tripit/slate/wiki/Deploying-Slate) befinden sich in der Slate-Dokumentation.

Fehler und Unklarheiten
-----------------------

Falls Unstimmigkeiten oder Fehler auffallen, können diese am besten über [einen Issue](https://github.com/axsemantics/atml3-docs/issues) geklärt werden.


## Local Development for large scale changes

#### Voraussetzungen
 - **Linux oder OS X** — Windows ist nicht getestet
 - **Ruby, Version 1.9.3 oder neuer**
 - **Bundler** — Falls der Befehl `bundle` nach der Ruby-Installation nicht vorhanden ist, muss `bundler` separat mit dem Befehl `gem install bundler` installiert werden.

#### Setup ohne Docker

```shell
git clone https://github.com/axsemantics/atml3-docs.git
cd atml3-docs
bundle install
bundle exec middleman server
```

Danach liegt die Dokumentation unter <http://localhost:4567>.

#### Setup mit Vagrant
```
vagrant up
```
Mit dem Befehl

```shell
bundle exec middleman build --clean
```
wird eine deploy-fertige Version des Projekts im `build`-Verzeichnis erstellt.

#### Dokumentation


Weitere Informationen über den [verwendeten Markdown-Stil](https://github.com/tripit/slate/wiki/Markdown-Syntax) und das [Deployment](https://github.com/tripit/slate/wiki/Deploying-Slate) befinden sich in der Slate-Dokumentation.

Verwendete Tools
--------------------
- [Slate](https://github.com/tripit/slate)
- [GitHub Pages](https://pages.github.com)
- [Docker](https://docker.com)

Verwendete Tools
--------------------
- [Slate](https://github.com/tripit/slate)
- [GitHub Pages](https://pages.github.com)
- [Docker](https://docker.com)
