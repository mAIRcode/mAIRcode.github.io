---
title: Testfälle
author: Manuel
layout: post
permalink: /155a21bb93/  # sha256(Testfälle EPR)[:10]
categories:
  - 'EPR'
tags:
  - 'Analyse'
  - 'Doku'
  - 'Python'
  - 'Einführung in die Programmierung'

accordion: 
  - title: Funktion, welche zwei Zahlen bekommt und die Summe davon zurückgibt (returnd)
    content: Lorem ipsum dolor sit amet, consectetur adipiscing elit. 
  - title: this is item 2
    content: Lorem ipsum dolor sit amet, consectetur adipiscing elit.
---

Wie man Testfälle in EPR Abgaben angibt (gültig für Gruppen 11 und 21 im WiSe 21/22).

{% include important.html content="Keine Ahnung was die nächsten Übungblätter alles für Anforderungen haben werden. Folgendes galt für alle *bisherigen* Übungsblätter." %}

## Im einfachsten Fall...

...durfte man Testfälle in eine .pdf/.txt Datei angeben.
Eine Idee hierfür wäre folgendes Template zu benutzen:

1. **Aufgabe/Funktion**: Testfall bezieht sich auf Anforderung in Aufgabe 3.a., die ich als Funktion `lower_or_equal(num1, num2)` implementiert habe.
2. **Was wird geprüft**: Ob return-Wert richtig ist.
3. **Wie reproduzieren**: In `main.py` in einer neuen Zeile: `print(create_sum(5, 5))`
4. **Kurze Erklärung**: Überprüfung mit zwei gleich großen Zahlen.
5. **Ist-Ergebnis**: `True`
6. **Soll-Ergebnis**: `True`
7. **Bestanden**: Ja

Gerne mit Screenshots ergänzen. Tabellarische Darstellung erwünscht, das macht es noch übersichtlicher.

## Automatisiert mit dem `doctest` Modul

Angenommen wir haben ein modul mit folgendem Inhalt:


{% highlight python %}
def sum_nums(a, b):
    """ This functions returns the sum of two numbers (i.e. both arguments).
    :param a: a number
    :param b: another number
    :return: sum of a and b
    """
    result = a + b
    return result
    
if __name__ == "__main__":
    x = sum_nums(1, 2)
    print(x)  #
{% endhighlight %}

Unser Ziel ist es jetzt die Funktion `sum_nums` mit bestimmten Argumenten aufzurufen (z.B. `sum_nums(1, 2)`), den zurückgegebenen Wert mit einem erwarteten Wert (z.B. `3`) zu vergleichen (Soll/Ist-Vergleich), und falls die zwei Werte nicht übereinstimmen, einen Fehler ausgeben.

Eine Möglichkeit dieses Ziel zu erreichen ist über das `doctest` modul:

{% highlight python %}
import doctest
{% endhighlight %}

Die Soll-Ist Vergleiche werden jetzt einfach in den Docstrings geschrieben, das sieht dann so aus (Erklärung zu den einzelnen Zeilen weiter unten):

{% highlight python %}
def sum_nums(a, b):
    """ This functions returns the sum of two numbers (i.e. both arguments).
    
    >>> sum_nums(1, 2)
    3
    >>> sum_nums(-5, 5)
    0
    >>> sum_nums(-5, 5)
    1
    
    :param a: a number
    :param b: another number
    :return: sum of a and b
    """
    result = a + b
    return result
{% endhighlight %}


Zeilen 4 bis 9 sollten an die Python Console erinnern: Den Eingabezeilen wird `>>>` vorangesetzt. Der erwartete zurückgegebene Wert wird einfach in eine neue Zeile geschrieben. z.B.:
{% highlight python %}
>>> sum_nums(1, 2)
3
{% endhighlight %}

Jetzt müssen wir nur noch das doctest modul auffordern sich das Docstring "anzuschauen" und die darin enthalteten tests auszuführen: `doctest.testmod()`.

*"Wie erkennt doctest welche Funktionen ich testen will?"* Gute Frage, tatsächlich werden hiermit die Doctests *aller* Funktionen im Modul ausgeführt. Funktionen ohne Doctests in den Docstrings werden natürlich nicht getestet...

Das ganze zusammen sieht dann so aus:

{% highlight python %}
import doctest

def sum_nums(a, b):
    """ This functions returns the sum of two numbers (i.e. both arguments).

    >>> sum_nums(1, 2)
    3
    >>> sum_nums(-5, 5)
    0
    >>> sum_nums(-5, 5)
    1

    :param a: a number
    :param b: another number
    :return: sum of a and b
    """

    result = a + b
    return result


if __name__ == "__main__":
    doctest.testmod()
{% endhighlight %}

Wie sieht das Ergebnis aus wenn ich das modul ausführe? Schließlich sollte der dritte Test ja fehlschlagen...


```
**********************************************************************
File "C:/path/to/example.py", line 10, in __main__.sum_nums
Failed example:
    sum_nums(-5, 5)
Expected:
    1
Got:
    0
**********************************************************************
1 items had failures:
   1 of   3 in __main__.sum_nums
***Test Failed*** 1 failures.

Process finished with exit code 0
```

### Doctests mit zufälligen Werten

Angenommen eine Funktion soll einen zufälligen Wert ausgebe: Wie können wir diesen Wert testen?

Hierfür kann man im `random` modul einen sogenannten seed setzen. Das geht ganz einfach mit `random.seed(5)`, wobei es egal ist welche Zahl man einsetzt. Seed hat folgende Auswirkung:

**Skript**:
{% highlight %}

import random

random.seed(10)

print(random.randint(1, 100))
print(random.randint(1, 100))

{% endhighlight %}

**Output**: 
```
74
5
```

jetzt rufen wir das Modul nochmal auf:

**Output**: 
```
74
5
```

Output hat sich also beim zweiten Durchlauf nicht geändert!

Nutze jetzt diese Eigenschaft um randomisierte Ausgaben zu testen :)



