<!--
  Copyright (c) 2026 Hans Mühlbauer, Franz Höpfinger and others.

  This program and the accompanying materials are made available under the
  terms of the Eclipse Public License 2.0 which is available at
  https://www.eclipse.org/legal/epl-2.0

  SPDX-License-Identifier: EPL-2.0
-->

## Type	Funktionsbaustein

| | |
|:---|:---|
| **Input	TS** | INT (Außentemperatur Sensor) |
| **DTI** | DT (Datum und Tageszeit) |
| **RST** | BOOL (Reset) |
| **Output	TA** | REAL (Momentane Außentemperatur) |
| **TP** | BOOL (TRUE wenn T24 erneuert wird |
| **I/O	T24** | REAL (Tagesmitteltemperatur) |
| **T24_MAX** | REAL (Maximaltemp. in den letzten 24 Stunden) |
| **T24_MIN** | REAL (Minimaltemperatur in den letzten 24 Stunden) |
| | T_AVG24 ermittelt die Tagesmitteltemperatur T24. Der Sensor Eingang TS ist vom Typ INT und stellt die Temperatur * 10 dar (ein Wert von 234 bedeutet 23,4 °C). Die Daten von Filter laufen zur Unterdrückung von Störungen über ein Tiefpassfilter mit der Zeit T_FILTER. Mittels SCALE und OFS können Nullpunktfehler und Skalierung des Sensors angepasst werden. Der Ausgang TA gibt die aktuelle Außentemperatur, welche jede halbe und volle Stunde gemessen wird, an. Der Baustein schreibt alle 30 Minuten den über die letzten 48 Werte ermittelten Tagesmittelwert in die I/O Variable T24, die extern definiert werden muss und dadurch auch REMANENT oder PERSISTENT definiert werden kann. Wird beim ersten Start ein Wert von -1000 in T24 vorgefunden, so initialisiert sich der Baustein beim ersten Aufruf mit dem aktuellen Sensorwert, so dass danach alle 30 Minuten ein gültiger Mittelwert ausgegeben werden kann. Hat T24 einen beliebigen anderen Wert als -1000, so initialisiert sich der Baustein mit diesem Wert und Rechnet den Mittelwert basierend aus diesem Wert weiter. Dies ermöglicht bei Stromausfall und remanenter Speicherung von T24 ein sofortiges Weiterarbeiten nach dem wieder Einschalten. Ein Reset Eingang kann jederzeit einen Neustart des Bausteins erzwingen, wobei abhängig vom Wert in T24 der Baustein entweder mit TS oder dem alten Wert von T24 initialisiert wird. Möchte man den Baustein auf einen bestimmten Mittelwert setzen, so wird der gewünschte Wert in T24 geschrieben und dann ein Reset erzeugt. |
| | T24_MAX und T24_MIN geben den Maximal- und Minimal-Wert der letzten 24 Stunden aus. Zur Ermittlung des Maximal und Minimal Wertes werden die Temperaturen zur jeweils halben Stunde berücksichtigt. Eine Temperaturwert der zwischen 2 Messungen auftritt wird hierbei nicht berücksichtigt. |
| **Setup	T_FILTER** | TIME (T des Eingangsfilters) |
| **SCALE** | REAL := 1.0 (Skalierungsfaktor) |
| **OFS** | REAL (Nullpunktabgleich) |

![T_avg24](T_avg24.gif)
