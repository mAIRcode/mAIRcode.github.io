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

...durfte man Testfällen in eine .pdf/.txt Datei angeben.
Hierfür könnt ihr folgendes Template benutzen:

1. **Aufgabe/Funktion**: Testfall bezieht sich auf Anforderung in Aufgabe 3.a. was ich über die Funktion `lower_or_equal(num1, num2)` implementiert habe.
2. **Was wird geprüft**: Ob return-Wert richtig ist.
3. **Wie reproduzieren**: In `main.py` in einer neuen Zeile: `print(create_sum(5, 5))`
4. **Kurze Erklärung**: Überprüfung mit zwei gleich großen Zahlen.
5. **Ist-Ergebnis**: `True`
6. **6. Soll-Ergebnis**: `True`
7. **Bestanden**: Ja

Gerne mit Screenshots ergänzen. Tabellarische Darstellung erwünscht, das macht es noch übersichtlicher.
