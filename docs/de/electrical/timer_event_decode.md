<!--
  Copyright (c) 2026 Hans Mühlbauer, Franz Höpfinger and others.

  This program and the accompanying materials are made available under the
  terms of the Eclipse Public License 2.0 which is available at
  https://www.eclipse.org/legal/epl-2.0

  SPDX-License-Identifier: EPL-2.0
-->

## Type	Funktion

| | |
|:---|:---|
| **Input	EVENT** | STRING (Event Zeichenkette) |
| **LANG** | INT (Sprachauswahl) |
| **OUTPUT** | TIMER_EVENT |
| | TIMER_EVENT_DECODE erlaubt die Programmierung von Timer Ereignissen mittels Zeichenkette anstelle des Ladens der Struktur TIMER_EVENT. |
| **Die Ereignisse werden wie folgt spezifiziert** |  |
| | <Typ;Kanal;Day;Start;Dauer;Land;Lor> |
| | Das Feld DAY hat je nach Typ des Ereignisses verschiedenen Bedeutung und kann auch mit Wochentagen als Text oder einer Liste von Wochentagen spezifiziert werden. Der Eingang LANG spezifiziert die zu verwendende Sprache, 0 = die im Setup eingestellt Default Sprache, 1 = Englisch, .... nähere Infos zu Sprachen siehe im Kapitel Datentypen. |

![timer_event_decode](timer_event_decode.gif)

| Element | Beschreibung | Formate |
| --- | --- | --- |
| < > | Start und Stopp Zeichen des Datensatzes. |  |
| Typ | Typ des Ereignisses (siehe Beschreibung in TIMER_P4) | '123', 2#0101, 8#33, 16#FF |
| Kanal | zu programmierender Kanal | '123', 2#0101, 8#33, 16#FF |
| Day | Auswahlnummer z.B. Tag | '123', 2#0101, 8#33, 16#FF, 'Mo''MO,DI,DO' |
| Start | Startzeitpunkt (Tageszeit) | 'TOD#12:00' |
| Dauer | Zeitdauer des Ereignisses | 'T#1h3m22s' |
| Land | logische Und Verknüpfung | '123', 2#0101, 8#33, 16#FF |
| Lor | logische oder Verknüpfung | '123', 2#0101, 8#33, 16#FF |
