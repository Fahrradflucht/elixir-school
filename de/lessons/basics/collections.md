---
layout: page
title: Datenstrukturen
category: basics
order: 2
lang: de
---

List, tuples, keywords, maps and functional combinators.

## Table of Contents

- [Listen](#Listen)
	- [Konkatenation von Listen](#konkatenation-von-listen)
	- [Listendifferenz](#listendifferenz)
	- [Kopf / Rest](#kopf--rest)
- [Tupel](#tupel)
- [Schlüsselwortlisten](#schlsselwortlisten)
- [Maps](#maps)

## Listen

Listen fassen Daten zusammen. Eine Liste kann verschiedene Datentypen enthalten und die einzelnen Elemente dürfen auch doppelt vorkommen: 

```elixir
iex> [3.41, :pie, "Apple"]
[3.41, :pie, "Apple"]
```
Elixir verwendet einfach verkettete listen, Der Zugriff auf die Länge oder das Ende der Liste ist eine `O(n)` Operation.
Daher ist es grundsätzlich schneller ein Element an den Kopf der Liste anzufügen.

```elixir
iex> list = [3.41, :pie, "Apple"]
[3.41, :pie, "Apple"]
iex> ["π"] ++ list
["π", 3.41, :pie, "Apple"]
iex> list ++ ["Cherry"]
[3.41, :pie, "Apple", "Cherry"]
```


### Konkatenation von Listen

List werden mit dem`++/2` Operator aneinander gefügt:

```elixir
iex> [1, 2] ++ [3, 4, 1]
[1, 2, 3, 4, 1]
```

### Listendifferenz

Der `--/2` Operator bildet die Differenz zweier Listen. Dabei dürfen in der subtrahierten Liste auch Elemente auftauchen die in der linken Liste nicht auftauchen:

```elixir
iex> ["foo", :bar, 42] -- [42, "bar"]
["foo", :bar]
```

**Info:** Es werden [strikte Vergleiche](../basics.md#vergleiche) verwendet.

### Kopf / Rest

Wenn man Listen verwendet unterscheidet teilt man die Liste oft in Kopf (das erste Element - engl. head) und den Rest (die Liste ohne das erste Element - engl. tail)
auf.  Elixir kommt mit zwei Funktionen, `hd` und `tl`, um die beiden Teile der Liste zu erhalten:

```elixir
iex> hd [3.41, :pie, "Apple"]
3.41
iex> tl [3.41, :pie, "Apple"]
[:pie, "Apple"]
```
Zusätzlich gibt es den "pipe" Operator `|` den wir uns in späteren Lektionen genauer ansehen werden.

```elixir
iex> [h|t] = [3.41, :pie, "Apple"]
[3.41, :pie, "Apple"]
iex> h
3.41
iex> t
[:pie, "Apple"]
```

## Tupel

Tupel sind Felder für Daten, diese Datenstruktur wird in einem zusammenhängenden Speicherbereich abgelegt. Hierdurch ist der Zugriff auf die Länge und der wahlfreie Zugriff Elemente schneller. Für Modifikationen an einem Tupel wird jedoch eine Kopie angelegt.
Tupel werden mit geschwungenen Klammern definiert:

```elixir
iex> {3.41, :pie, "Apple"}
{3.41, :pie, "Apple"}
```
Tupel werden sehr oft verwendet um zusätzliche Informationen aus einer Funktion zurückzugeben. Wie nützlich das ist werden wir sehen wenn wir Pattern-Matching betrachten:

```elixir
iex> File.read("path/to/existing/file")
{:ok, "... contents ..."}
iex> File.read("path/to/unknown/file")
{:error, :enoent}
```

## Schlüsselwortlisten

Keyword- oder Schlüsselwortlisten sind Listen von Tupeln mit einem Atom als erstem Element und einem wert als zweitem Element. Sie werden verwenden um Schlüsselworte zu Werten zuzuordnen.
Keywordlisten haben die gleichen Eigenschaften sonstige Listen, aber eine vereinfachte Schreibweise:

```elixir
iex> [foo: "bar", hello: "world"]
[foo: "bar", hello: "world"]
iex> [{:foo, "bar"}, {:hello, "world"}]
[foo: "bar", hello: "world"]
```
Eine Schlüsselwortliste hat drei charakteristische Eigenschaften:

+ Schlüsselwörter sind Atome.
+ Schlüsselwörter haben eine Reihenfolge.
+ Schlüsselwörter können mehrfach vorkommen.

Schlüsselwortlisten werden oft verwendet um Optionen an Funktionen zu übergeben.

## Maps

Maps sind Elixirs beliebteste assoziative Datenstruktur. Im Gegensatz zu Schlüsselwortlisten kann als "Schlüssel" jeder Datentyp verwendet werden.
Die Schlüssel-Wert-Paare in einer Map haben keine definierbare Reihenfolge.
Maps können mit der `%{}` Syntax erzeugt werden:

```elixir
iex> map = %{:foo => "bar", "hello" => :world}
%{:foo => "bar", "hello" => :world}
iex> map[:foo]
"bar"
iex> map["hello"]
:world
```

Seit Elixir Version 1.2 sind auch variablen als Schlüssel erlaubt:

```elixir
iex> key = "hello"
"hello"
iex> %{key => "world"}
%{"hello" => "world"}
```

Wird ein Duplikat zu einer Map hinzugefügt, wird der zuvor gespeicherte Wert erzetzt:

```elixir
iex> %{:foo => "bar", :foo => "hello world"}
%{foo: "hello world"}
```

Wie man an der obigen Ausgabe sehen kann, gibt es eine spezielle Syntax für Maps die nur Atome als Schlüssel haben:

```elixir
iex> %{foo: "bar", hello: "world"}
%{foo: "bar", hello: "world"}

iex> %{foo: "bar", hello: "world"} == %{:foo => "bar", :hello => "world"}
true
```
