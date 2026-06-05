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
| **Input	IN** | BOOL (Steuersignal für Pumpe) |
| **MANUAL** | BOOL (Manuelles Steuersignal) |
| **RST** | BOOL (Reset Signal) |
| **Output	PUMP** | BOOL (Steuersignal für die Pumpe) |
| **RUNTIME** | REAL (Betriebsstunden des Motors in Stunden) |
| **CYCLES** | REAL (Anzahl der Ein / Aus Zyklen der Pumpe) |
| **Setup	MIN_ONTIME** | TIME (Minimale Laufzeit für Motor) |
| **MIN_OFFTIME** | TIME (Minimale Totzeit für Motor) |
| **RUN_EVERY** | TIME (Zeit nach der die Pumpe selbsttätig läuft) |
| | ACTUATOR_PUMP ist ein Pumpeninterface mit Betriebsstundenzähler. Die Pumpe kann sowohl mit IN oder Manual eingeschaltet werden. Die Setup-Variablen MIN_ONTIME und MIN_OFFTIME legen eine minimale Einschaltdauer und eine minimale Laufzeit fest. Wird der Eingang IN kürzer als MIN_ONTIME auf TRUE gesetzt, so läuft die Pumpe weiter bis die minimale Laufzeit erreicht ist. Wird der Eingang IN länger als MIN_ONTIME auf TRUE gesetzt, läuft die Pumpe bis IN wieder FALSE ist. |
| | Wird die Pumpe kurz hintereinander eingeschaltet, so wartet die Pumpe bis die Zeit MIN_OFFTIME verstrichen ist, bis sie die Pumpe wieder einschaltet. Mit der Setup-Variablen RUN_EVERY wird die Zeit definiert, nach der die Pumpe selbsttätig läuft, wenn sie länger als RUN_EVERY stillsteht um ein festsitzen der Pumpe zu vermeiden. Die Pumpe schaltet in diesem Fall selbsttätig ein und läuft für MIN_ONTIME. Durch RUN_EVERY = T#0s kann die automatische Aktivierung abgeschaltet werden. |
| | Ein interner Betriebsstundenzähler zählt die Laufzeit der Pumpe in Stunden und auch die Anzahl der Schaltzyklen. Beide Werte können mit TRUE am Eingang RST auf Null zurückgesetzt werden. Der Betriebsstundenzähler ist permanent und geht weder bei Stromausfall oder Reset verloren. RUNTIME und CYCLES sind beides REAL-Werte, damit nicht der übliche Overflow wie bei TIME Werten nach 50 Tagen passiert. |

![actuator_pump](actuator_pump.gif)
