<!--
  Copyright (c) 2026 Hans Mühlbauer, Franz Höpfinger and others.

  This program and the accompanying materials are made available under the
  terms of the Eclipse Public License 2.0 which is available at
  https://www.eclipse.org/legal/epl-2.0

  SPDX-License-Identifier: EPL-2.0
-->

## SDD

| | |
|:---|:---|
| **Type	Funktion** | REAL |
| **Input	T** | REAL (Temperatur der Luft in °C) |
| **ICE** | BOOL (TRUE für Luft über Eis und FALSE für Luft über |
| | Wasser) |
| **Output** | REAL (Sättigungsdampfdruck in Pa) |
| | SDD berechnet den Sättigungsdampfdruck für Wasserdampf in Luft. Die Temperatur T wird in °C angegeben. Das Ergebnis kann sowohl für Luft über Eis (ICE = TRUE) und für Luft über Wasser (ICE = FALSE) berechnet werden. Der Gültigkeitsbereich der Funktion liegt bei -30°C bis 70°C über Wasser und bei -60°C bis 0°C über Eis. Die Berechnung wird nach der Magnusformel ausgeführt. |

![sdd](sdd.gif)
