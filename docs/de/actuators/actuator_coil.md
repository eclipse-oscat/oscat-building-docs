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
| **Input	IN** | BOOL (Steuersignal) |
| **Output	OUT** | BOOL (Steuersignal für die Pumpe) |
| **STATUS** | BYTE (ESR kompatibler Statusausgang) |
| **ACTUATOR_COIL dient zur Ansteuerung von einfachen Ventilen. Der Ausgang OUT folgt dabei dem Eingangssignal IN. Wird die Setup Variable SELF_ACT_CYCLE auf einen Wert größer 0 gesetzt, wird das Ventil Automatisch für die Dauer von SELF_ACT_TIME aktiviert falls es für die Zeit SELF_ACT_CYCLE ausgeschaltet war. Ein ESR kompatibler Statusausgang meldet Zustandsänderungen des Ventils zur Weiterverarbeitung oder zum Data Logging. Die Statusmeldungen sind wie folgt definiert** |  |
| | STATUS = 100, Standby. |
| | STATUS = 101, Ventil wurde durch TRUE am Eingang IN aktiviert. |
| | STATUS = 102, Ventil wurde Automatisch aktiviert. |
| **Setup	SELF_ACT_CYCLE** | TIME (Automatische Aktivierungszeit) |
| **SELF_ACT_TIME** | TIME (Einschaltzeit bei Autoaktivierung) |

![actuator_coil](actuator_coil.gif)
