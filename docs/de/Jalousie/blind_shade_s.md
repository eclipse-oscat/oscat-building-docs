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
| **Input 	UP** | BOOL (Eingang AUF) |
| **DN** | BOOL (Eingang AB) |
| **S_IN** | BYTE (ESR kompatibler Status Eingang) |
| **PI** | BYTE (Vorgabe der Position) |
| **ENABLE** | BOOL (Beschattung aktiviert) |
| **SUN** | BOOL (Eingangssignal vom Sonnensensor) |
| **HORZ1** | REAL (Horizontaler Sonnenwinkel |
| | Beschattungsbeginn) [100.0] |
| **HORZ2** | REAL (Horizontaler Sonnenwinkel |
| | Beschattungsende) [260.0] |
| **VERT** | REAL (Vertikaler Beschattungswinkel) [90.0] |
| **ALERT** | BOOL (Zwangsöffnung des Rollos) [FALSE] |
| **I/O	CX** | CALENDAR (aktuelle Zeit und Kalenderdaten) |
| **Output	QU** | BOOL (Motor Auf Signal) |
| **QD** | BOOL (Motor Ab Signal) |
| **STATUS** | BYTE (ESR kompatibler Status Ausgang) |
| **PO** | BYTE (Jalousiestellung im Automatikbetrieb) |
| | BLIND_SHADE_S ist eine wesentlich vereinfachte Funktion von BLIND_SHADE speziell für die Verwendung mit Rollos. Bei diesen muss kein Lamellenwinkel für die Beschattung berechnet werden, sondern lediglich sichergestellt, dass bei Sonnenschein das Rollo weit genug geschlossen ist. |
| | Im inaktiven Zustand reicht der Baustein die Eingänge UP, DN, PI und S_IN unverändert an die Ausgänge QU, QD, PO und STATUS durch. |
| | Der Baustein wird scharfgeschaltet, wenn UP = TRUE, DN = TRUE, ENABLE = TRUE und SUN (für mindestens SHADE_DELAY) = TRUE. Sind diese Bedingungen erfüllt, prüft der Baustein, ob aktuell der horizontale Sonnenwinkel im Bereich zwischen HORZ1 und HORZ2 liegt und der vertikale Sonnenwinkel niedriger als VERT ist. Liegt nun auch noch die aktuelle Uhrzeit zwischen Sonnenaufgang + SUNRISE_OFFSET und Sonnenuntergang – SUNSET_PRESET, dann wechselt der Baustein in den STATUS 151 (Beschattung) und stellt sicher, dass am Ausgang PO kein größerer Wert als SHADE_POS ausgegeben wird (PO ist dann das Minimum aus PI und SHADE_POS). |
| **Für die Winkel HORZ1 und HORZ2 gilt** | 90° = Osten, 180° = Süden, 270° = Westen. |
| | SHADE_DELAY verhindert, dass bei Teilbewölkung die Jalousie dauernd auf und ab fährt. |
| | Über den Eingang ALERT, kann auf einfache Weise erreicht werden, dass das Rollo z.B. bei geöffneter Tür ganz nach oben fährt. Der ALERT Eingang hat im Baustein höchste Priorität, erzwingt STATUS = 152 unabhängig von den Eingängen und setzt QU = TRUE, QD = FALSE, führt also einen manual UP durch. |
| **Innerhalb einer Rollosteuerung kann BLIND_SHADE z.B. wie folgt eingesetzt werden** |  |
| **Setup	SUNRISE_OFFSET** | TIME (Delay bei Sonnenaufgang) [T#1h] |
| **SUNSET_PRESET** | TIME (Delay bei Sonnenuntergang) [T#1h] |
| **SHADE_DELAY** | TIME (Delay der Beschattung) [T#60s] |
| **SHADE_POS** | BYTE (Maximalposition bei Beschattung) |

![blind_shade_s](blind_shade_s.gif)
![blind_shade_s_schema](blind_shade_s_schema.gif)
