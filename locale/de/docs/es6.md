---
title: ECMAScript 2015 (ES6)
layout: docs.hbs
---
# ECMAScript 2015 (ES6) in Node.js

Node.js wird gegen moderne Versionen von [V8](https://developers.google.com/v8/) kompiliert. Indem wir up-to-date bleiben mit den letzten Ver&ouml;ffentlichungen dieser Engine, stellen wir sicher dass neue Features der [JavaScript ECMA-262 specification](http://www.ecma-international.org/publications/standards/Ecma-262.htm) Node.js Entwicklern zeitnah zur Verf&uuml;gung stehen, genau wie fortlaufende Leistungs- und Stabilit&auml;tsverbesserungen.

Die ECMAScript 2015 (ES6) Features werden in 3 Gruppen aufgeteilt:

* Alle **shipping** Features, die V8 als stabil erachtet, sind **in Node.js von Haus aus an** und erfordern **KEINE** runtime flag.
* **Staged** Features, welche fast fertige Features sind die vom V8 team nicht als stabil erachtet werden, erfordern eine runtime flag: `--es_staging` (oder das Synonym, `--harmony`).
* **In progress** Features k&ouml;nnen einzeln durch ihre entsprechende harmony flag aktiviert werden (e.g. `--harmony_destructuring`), obwohl davon bis auf zu Testzwecken stark abgeraten wird.

## Welche Features kommen standardm&auml;ssig mit Node.js (keine runtime flag erforderlich)?

* Block scoping
    * [let](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/let) (nur strict mode)
    * [const](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/const)
    * `function`-in-blocks (nur strict mode [[1]](#ref-1)<span id="backref-1"></span>)
* [Klassen](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes) (nur strict mode)
* Collections
    * [Map](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Map)
    * [WeakMap](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/WeakMap)
    * [Set](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Set)
    * [WeakSet](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/WeakSet)
* [Typed arrays](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Typed_arrays)
* [Generators](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/function*)
* [Binary und Octal Literale](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Lexical_grammar#Numeric_literals)
* [Object literal extensions](https://github.com/lukehoban/es6features#enhanced-object-literals) (shorthand properties and methods)
* [Promises](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise)
* [Neue String Methoden](https://developer.mozilla.org/en-US/docs/Web/JavaScript/New_in_JavaScript/ECMAScript_6_support_in_Mozilla#Additions_to_the_String_object)
* [Symbole](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Symbol)
* [Template strings](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/template_strings)
* [Arrow Functions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions)
* [new.target](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/new.target) [[2]](#ref-2)<span id="backref-2"></span>
* [Object.assign](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/assign)
* [Spread Operator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_operator) [[2]](#ref-2)<span id="backref-2"></span>

Eine detailliertere Liste, inklusive eines Vergleiches mit anderen Engines, kann auf der [compat-table](https://kangax.github.io/compat-table/es6/) eingesehen werden.

<small id="ref-1">[[1](#backref-1)]: Seit v8 3.31.74.1 sind block-scoped Deklarationen [absichtlich mit einer nicht-standard strict-mode Limitation implementiert](https://groups.google.com/forum/#!topic/v8-users/3UXNCkAU8Es). Entwickler sollten sich dar&uuml;ber im klaren sein dass sich das &auml;ndern wird sowei v8 sich weiter der ES6 Spezifikation ann&auml;hert.</small><br>
<small id="ref-2">[[2](#backref-2)]: Nur in Node.js >= 5.x.x

## Welches Features stecken hinter des --es_staging Flag?

* [`Symbol.toStringTag`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Symbol) (benutzerdefinierbare Werte f&uuml;r `Object.prototype.toString`, hinter der Flagge `--harmony_tostring`)
* [`Array.prototype.includes`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/includes) (bestimmt ob
ein Array ein bestimmtes Element enth&auml;lt, hinter der Flagge `--harmony_array_includes`) [[2]](#ref-2)<span id="backref-2"></span>
* [Rest Parameters](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/rest_parameters) (Representieren eine unbestimmte Anzahl
an Argumenten als ein Array, hinter der Flagge `--harmony_rest_parameters`) [[2]](#ref-2)<span id="backref-2"></span>

## Welche Features sind in progress?

Es kommen st&auml;ndig neue Features zur V8 Engine hinzu. Generell k&ouml;nnen sie in einer zuk&uuml;nftigen Node.js Version erwartet werden, auch wenn das genaue Datum unbekannt bleibt.

Man kann sich alle *in progress* Features in jedem Node.js Release auflisten lassen in dem man das `--v8-options` Argument durchsieht. Jedoch Vorsicht, diese Features sind nicht komplett und m&ouml;glicherweise fehlerhaft, also auf eigene Verantwortung zu verwenden:

```bash
node --v8-options | grep "in progress"
```

## Meine Infrastruktur ist auf die --harmony Flagge konfiguriert. Sollte ich sie entfernen?

Momentan aktiviert die `--harmony` Flagged nur **staged** Features, schliesslich ist sie nun ein Synonym f&uuml;r `--es-staging`. Wie bereits oben erw&auml;hnt sind diese abgeschlossene Features die noch nicht als stabil genug erachtet werden. Wer auf nur mal sicher gehen will, besonders in Production, sollte erw&auml;hnen diese Flagge zu entfernen. Wer diese Flagge aktiviert l&auml;sst sollte darauf vorbereitet sein dass zuk&uuml;nftige Node.js upgrade Probleme bereiten, wenn V8 ihre Semantik ver&auml;ndert um n&auml;her dem Standard zu folgen.

## Wie finde ich heraus welche Version von V8 mit einer bestimmten Node.js Version kommt?

Node.js stellt durch das `process` Object die Versionen aller Abh&auml;ngigkeiten zur Verf&uuml;gung. Im Falle der V8 engine, die Version kann durch folgendes Kommando im Terminal ausgelesen werden:

```bash
node -p process.versions.v8
```
