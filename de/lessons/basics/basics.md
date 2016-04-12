---
layout: page
title: Basics
category: basics
order: 1
lang: de
---

Installation, Basistypen und Basisoperationen.

## Inhalt

- [Installation](#installation)
	- [Elixir installieren](#elixir-installieren)
	- [Interaktiver Interpreter](#interaktive-eingabe)
- [Basistypen](#basistypen)
	- [Ganzzahlen](#ganzzahlen)
	- [Gleitkommazahlen](#gleitkommazahlen)
	- [Wahrheitswerte](#wahrheitswerte)
	- [Atome](#atome)
	- [Zeichenketten](#zeichenketten)
- [Basisoperationen](#basisoperationen)
	- [Arithmetik](#arithmetisch)
	- [Logik](#logik)
	- [Vergleiche](#vergleiche)
	- [Zeichenketteninterpolation](#zeichenketteninterpolation)
	- [Konkatenation](#konkatenation)

## Installation

### Elixir installieren

Installationsanleitungen für die meisten Betriebssysteme gibt es auf der Elixir Homepage unter "[Installing Elixir](http://elixir-lang.org/install.html)".

### Interaktiver Interpreter

Elixir kommit mit einem interaktiver Interpreter, des es uns erlaubt Elixir Ausdrücke auszuwerten. Diesen interpreter, `iex` , werden wir im laufe dieses Tutorials verwenden.

Los geht'ss, wir starten `iex`:

	Erlang/OTP 17 [erts-6.4] [source] [64-bit] [smp:8:8] [async-threads:10] [hipe] [kernel-poll:false] [dtrace]

	Interactive Elixir (1.0.4) - press Ctrl+C to exit (type h() ENTER for help)
	iex>

## Basistypen

### Ganzzahlen

```elixir
iex> 255
255
iex> 0xFF
255
```
Zahlen werden in binärer, oktaler und hexadezimaler Notation unterstützt:

```elixir
iex> 0b0110
6
iex> 0o644
420
iex> 0x1F
31
```

### Gleitkommazahlen

In Elixir werden Gleitkommazahlen mit einem Dezimalpunkt geschrieben, dem mindestens eine Ziffer vorangehen muss. Gleitkommazahlen in Elixir haben 64 bit Genauigkeit (double) und verwenden die e-Notation für Exponenten.

```elixir
iex> 3.41
3.41
iex> .41
** (SyntaxError) iex:2: syntax error before: '.'
iex> 1.0e-10
1.0e-10
```


### Wahrheitswerte

Elixir kennt `true` und `false` als boolsche Konstanten.
`false` und `nil` werden als "falsch" ausgewertet, alle anderen Terme werden als wahr ausgewertet.

```elixir
iex> true
true
iex> false
false
```

### Atome

Atome sind Konstanten die für ihren eigenen Namen stehen. Atome entsprechen Rubys Symbolen, solltest du dich mit Ruby auskennen.

```elixir
iex> :foo
:foo
iex> :foo == :bar
false
```
INFO: Die beiden Konstanten `true` und `false` sind eigentlich die beiden Atome `:true` and `:false`.

```elixir
iex> true |> is_atom
true
iex> :true |> is_boolean
true
iex> :true === true
true
```

### Zeichenketten

Zeichenketten sind in Elixir UTF-8 kodiert. Sie werde in doppelten Anführungszeichen eingefasst:

```elixir
iex> "Hello"
"Hello"
iex> "dziękuję"
"dziękuję"
```
Es werden Zeilenumbrüche und Escape-Sequenzen unterstützt:

```elixir
iex> "foo
...> bar"
"foo\nbar"
iex> "foo\nbar"
"foo\nbar"
```

## Basisoperationen

### Arithmetik

Wie zu erwarten unterstützt Elixir die grundlegenden Operatoren `+`, `-`, `*`, und `/`.   Es ist jedoch wichtig anzumerken, dass `/` immer Gleitkommawerte zurückgibt:

```elixir
iex> 2 + 2
4
iex> 2 - 1
1
iex> 2 * 5
10
iex> 10 / 5
2.0
```

Für Ganzzahl-Division oder die Division mit Rest hat Elixir zwei hilfreiche Funktionen:

```elixir
iex> div(10, 5)
2
iex> rem(10, 3)
1
```

### Logik

Elixir hat  `||`, `&&`, und `!` als Operationen für Boolsche Ausdrücke. 
Diese Operatoren definieren Wahrheitswerte für alle Elixir Datentypen:

```elixir
iex> -20 || true
-20
iex> false || 42
42

iex> 42 && true
true
iex> 42 && nil
nil

iex> !42
false
iex> !false
true
```

Drei weitere Operatoren erfordern `true` oder `false` als erstes Argument.

```elixir
iex> true and 42
42
iex> false or true
true
iex> not false
true
iex> 42 and true
** (ArgumentError) argument error: 42
iex> not 42
** (ArgumentError) argument error
```

### Vergleiche

Elixir kennt die gängigen Vergleichsoperatoren: `==`, `!=`, `===`, `!==`, `<=`, `>=`, `<` und `>`.

```elixir
iex> 1 > 2
false
iex> 1 != 2
true
iex> 2 == 2
true
iex> 2 <= 3
true
```
Für eines strikten Vergleich von verschiedene Zahlen typen benutzt man `===`:

```elixir
iex> 2 == 2.0
true
iex> 2 === 2.0
false
```

Eine wichtige Eigenart von Elixir ist es, das alle Datentypen verglichen werden können. Daher gibt es eine stabile Ordnung beim Sortieren von Daten verschiedener Typen. Die genaue Sortierreihenfolge muss man sich nicht merken, aber es ist gut sich daran zu erinnern dass es eine Ordnung gibt.

```elixir
number < atom < reference < functions < port < pid < tuple < maps < list < bitstring
```

Hierdurch kommt es zu interessanten, und absolut gültigen, Vergleichen, die man in anderen Programmiersprachen eher nicht sieht:

```elixir
iex> :hello > 999
true
iex> {:hello, :world} > [1, 2, 3]
false
```

### Zeichenketteninterpolation

Wer zuvor Ruby benutzt hat, dem sollte die Zeichenketteninterpolation in Elixir bekannt vorkommen.

```elixir
iex> name = "Sean"
iex> "Hello #{name}"
"Hello Sean"
```

### Konkatenation

Die Aneinanderreihung von Zeichenketten erfolgt mit dem `<>` Operator:

```elixir
iex> name = "Sean"
iex> "Hello " <> name
"Hello Sean"
```
