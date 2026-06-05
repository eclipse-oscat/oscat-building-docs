<!--
  Copyright (c) 2026 Hans Mühlbauer, Franz Höpfinger and others.

  This program and the accompanying materials are made available under the
  terms of the Eclipse Public License 2.0 which is available at
  https://www.eclipse.org/legal/epl-2.0

  SPDX-License-Identifier: EPL-2.0
-->

## HEAT_METER

| | |
|:---|:---|
| **Type	Funktion** | REAL |
| **Input	TF** | REAL (Vorlauftemperatur in °C) |
| **TR** | REAL (Rücklauftemperatur in °C) |
| **LPH** | REAL (Durchflussmenge in L/h bzw. L/Impuls) |
| **E** | BOOL (Enable Signal) |
| **RST** | BOOL (asynchroner Reset Eingang) |
| **Output	C** | REAL (aktueller Verbrauch in Joule / Stunde ) |
| **I/O	Y** | REAL (Wärmemenge in Joule) |
| | HEAT_METER ist ein Wärmemengenzähler. Die Wärmemenge Y wird in Joule gemessen. Die Eingänge TF und TR sind die Vorlauf und Rücklauftemperatur des Mediums. Am Eingang LPH wird die Durchflussmenge in Liter / Stunde beziehungsweise die Durchflussmenge je Impuls an E spezifiziert. Die Eigenschaft von E wird durch die Setup Variable PULSE_MODE bestimmt. PULSE_MODE = FALSE bedeutet das  die Wärmemenge kontinuierlich aufaddiert wird solange E auf TRUE ist. PULSE_MODE = TRUE bedeutet das die Wärmemenge mit jeder steigenden Flanke von E aufaddiert wird. Der PULSE_MODE ist bei Verwendung von Wärmezählern einzuschalten, während am Eingang LPH die Flussmenge in Litern je Impuls anzugeben ist und am Eingang E wird der Wärmezähler angeschlossen. Wenn kein Flussmengenmesser Vorhanden ist, so wird am Eingang E das Pumpensignal angeschlossen und am Eingang LPH die Pumpenleistung in Litern / Stunde angegeben. Bei Verwendung eines Flussmengenmessers mit Analogem Ausgang wird der Ausgang entsprechend auf Liter / Stunde umgerechnet und auf den Eingang LPH gelegt, Der Eingang E wird hierbei auf TRUE gesetzt. Mit den Setup- Variablen CP, DENSITY und CONTENT wird die 2te Komponente des Mediums spezifiziert. Für den Betrieb mit reinem Wasser sind keinerlei Angaben von CP, DENSITY und CONTENT nötig. Wenn ein Gemisch aus Wasser und einem 2ten Medium vorhanden ist werden mit CP die Spezifische Wärmekapazität in J/KgK, mit DENSITY die DICHTE in KG/l und mit CONTENT der Anteil der 2ten Komponente spezifiziert. Ein Anteil von 0.5 bedeutet 50% und 1 wäre entsprechend 100%. Mit der Setup Variablen RETURN_METER wird angegeben ob der Durchflussmesser im Vorlauf oder Rücklauf sitzt. RETRUN_METER = TRUE steht für Rücklaufmessung und FALSE für Vorlaufmessung. Am Ausgang C stellt der Baustein den momentanen Verbrauch zur Verfügung. Der momentane Verbrauch wird in Joule / Stunde angegeben, und in den Zeitabständen von AVG_TIME ermittelt. |
| **Der Baustein hat folgende Vorgabewerte, die aktiv sind wenn die entsprechenden Werte vom Anwender nicht gesetzt werden** |  |
| | PULSE_MODE = FALSE |
| | RETURN_METER = FALSE |
| | AVG_TIME = T#5s |
| **Setup	CP** | REAL (Spezifische Wärmekapazität der  2ten Komponente) |
| **DENSITY** | REAL (Dichte der 2ten Komponente) |
| **CONTENT** | REAL (Anteil, 1 = 100%) |
| **PULSE_MODE** | BOOL (Impulszähler wenn TRUE) |
| **RETURN_METER** | BOOL (Durchflussmesser im Rücklauf |
| | wenn TRUE) |
| **AVG_TIME** | TIME (Zeitintervall für Momentanen Verbrauch) |

![heat_meter](heat_meter.gif)
