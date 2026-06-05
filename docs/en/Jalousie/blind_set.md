<!--
  Copyright (c) 2026 Hans Mühlbauer, Franz Höpfinger and others.

  This program and the accompanying materials are made available under the
  terms of the Eclipse Public License 2.0 which is available at
  https://www.eclipse.org/legal/epl-2.0

  SPDX-License-Identifier: EPL-2.0
-->

## Type	Function module

| | | |
|:---|:---|:---|
| **Input	UP** | BOOL (Input UP) | |
| **DN** | BOOL (input DOWN) | |
| **S_IN** | BYTE (ESR compliant status input) | |
| **PI** | BYTE (blind position in automatic mode) | |
| **AI** | BYTE (slat angle in automatic mode) | |
| **IN** | BOOL (input for fire alarm) | |
| **PX** | BYTE (input for wind alarm) | |
| **AX** | BYTE (input for intrusion detection) | |
| **Output	QU** | BOOL (motor up signal) | |
| **QD** | BOOL (motor down signal) | |
| **STATUS** | BYTE (ESR compliant status output) | |
| **PO** | BYTE (start value of the blind) | |
| **AO** | BYTE (start value of the slat angle) | |
| | BLIND_SET can be used anywhere in a BLIND application to accelerate a defined position (PX, AX). Using the setup variable OVERRIDE_MANUAL defines if the module  may override a manual operation. If the variable RESTORE_POSITION is set to TRUE, the module remembers the last position and drive to this position automatically after a forced operation. The variable RESTORE_TIME determines how long the module remains active to restore the last   Position again. If not set RESTORE_POSITION the forced state remains when switch back in the automatic mode. | |
| **State table of BLIND_SET** |  | |
| **Setup	OVERRIDE_MANUAL** | BOOL (allows manual Override if | TRUE) |
| **RESTORE_POSITION** | BOOL (IF TRUE restore old position) | |
| **RESTORE_TIME** | TIME (duration for the restore of last position) | Default = T#60s) |

![blind_set](blind_set.gif)

| UP | DN | PIAI | IN | AXAX | QU | QD | STATUS | POAO | MANUAL_OVERRIDE |  |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 1 | 1 | X | 0 | - | 1 | 1 | S_IN | X | - | Standby |
| 1 | 1 | - | 1 | Y | 1 | 1 | 178 | Y | - | Forced position |
| - | - | - | 1 | Y | 1 | 1 | 178 | Y | 1 | Forced position |
| - | - | - | - | - | 1 | 1 | 179 | Z | - | Restoreoldposition |
| 0 | 1 | X | - | - | 0 | 1 | S_IN | X | - | Manual operation |
| 1 | 0 | X | - | - | 1 | 0 | S_IN | X | - | Manual operation |
| 0 | 0 | X | - | - | 0 | 0 | S_IN | X | - | Manual operation |
