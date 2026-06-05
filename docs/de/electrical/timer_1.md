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
| **Input	E** | BOOL (Enable Eingang) |
| **DTI** | DATE_TIME (Datum Zeit Eingang) |
| **START** | TOD (Startzeit) |
| **DURATION** | TIME (Zeitdauer des Ausgangssignals) |
| **DAY** | BYTE (Auswahl der Wochentage) |
| **Output	Q** | BOOL (Schaltausgang) |
| | TIMER_1 erzeugt an selektierbaren Tagen der Woche ein Ausgangsereignis Q mit einer programmierbaren Dauer (DURATION) und festgelegter Anfangszeit START. DTI liefert dem Baustein die Lokalzeit. START und DURATION legt die Tageszeit und die Dauer des Ereignisses fest. Der Eingang DAY legt fest, an welchen Wochentagen das Ereignis erzeugt wird. Wird DAY auf 0 gesetzt, so kein Ereignis erzeugt. Eine DURATION = 0 legt fest, dass das Ausgangssignal nur für einen Zyklus gesetzt wird. Das erzeugte Ausgangssignal kann auch über Mitternacht verlaufen, oder es kann auch länger als einen Tag sein. Die maximale Impulsdauer liegt jedoch bei 49 tagen (T#49d). Der Eingang DAY ist vom Typ BYTE und die Bits 0..7 legen die Tage des Ereignisses Fest. Bit 0 entspricht Sonntag, Bit 1 Samstag .. Bit 6 entspricht Montag. Werden die Bits 0..6 in DAY gesetzt so wird jeden Tag ein Ereignis erzeugt, ansonsten nur für diejenigen Tage, für die das entsprechende Bit gesetzt ist. Der Eingang Default ist wenn er nicht beschaltet wird auf 2#0111_1111 gesetzt und somit ist der Baustein für jeden Tag aktiv. Ein zusätzlicher Enable Eingang E kann den Baustein Freischalten Dieser Eingang ist TRUE wenn er nicht beschaltet wird. |

![timer_1](timer_1.gif)
