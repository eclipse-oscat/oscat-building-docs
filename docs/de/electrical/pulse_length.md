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
| **Input	IN** | BOOL (Eingangspuls) |
| **Output	SHORT** | BOOL (Puls wenn IN < T_SHORT) |
| **MIDDLE** | BOOL (Puls wenn IN =< T_LONG und IN >= T_SHORT) |
| **LONG** | BOOL (TRUE wenn IN > T_SHORT) |
| **Setup	T_SHORT** | TIME (Maximale Länge für kurzen Puls) |
| **T_LONG** | TIME (Minimale Länge für Langen Puls) |
| | PULSE_LENGTH setzt bei einem Eingangspuls an IN einen der 3 Ausgänge. Der Ausgang SHORT wird für einen Zyklus TRUE, wenn der Eingangspuls kleiner als T_SHORT ist. Der Ausgang MIDDLE wird für einen Zyklus TRUE, wenn der Eingangspuls zwischen T_SHORT und T_LONG lang ist. Der Ausgang LONG wird gesetzt, sobald der Eingangsimpuls T_LONG überschritten hat und bleibt solange auf TRUE, wie der Eingangsimpuls auf TRUE bleibt. |

![pulse_length](pulse_length.gif)
