<!--
  Copyright (c) 2026 Hans Mühlbauer, Franz Höpfinger and others.

  This program and the accompanying materials are made available under the
  terms of the Eclipse Public License 2.0 which is available at
  https://www.eclipse.org/legal/epl-2.0

  SPDX-License-Identifier: EPL-2.0
-->

## Type	Function module

| | |
|:---|:---|
| **Input	UP** | BOOL (Input UP) |
| **DN** | BOOL (input DOWN) |
| **S_IN** | BYTE (ESR compliant status input) |
| **T_UD** | TIME (run time up / down) |
| **T_ANGLE** | TIME (duration of the slat adjustment) |
| **Output	POS** | BYTE (position of the shutter, 0 = bottom, 255 = top) |
| **ANG** | BYTE (angle of the fin, 0 = vertical, 255 = horiz.) |
| **QU** | BOOL (motor up signal) |
| **QD** | BOOL (motor down signal) |
| **STATUS** | BYTE (ESR compliant status output) |
| **BLIND_ACTUATOR is a blind / shutter actuator to simulate the position and the angle of the slats. The inputs UP and DN are mutually interlocked, so that QU and QD can never be active at the same time. With time T_LOCKOUT the minimum pause is set between a change of direction. Additionally BLIND_ACTUATOR provides two outputs with the type Byte which simulate the position of fin and the position of the shutter. For accurate simulation, adjust the setup times and T_UD T_ANGLE accordingly. T_UD sets the time to drive from "closed" needed to "open" (up position). T_ANGLE specifies the time for adjusting the  fin  from "vertical" to horizontal. The actuator ensures that first the fin be placed horizontally and then starting the "open" action of the shutter. Conversely, when "close" the shutter the fin set vertically before the down movement begins. POS = 0 means blinds shut down, and POS means = 255 blind is up. Intermediate positions are in accordance with intermediate values 0 ..255   The angle of the blades is issued by the output ANG, with mean ANG = 0 is invertical position and ANG = 255 is the horizontal position, values 0-255 indicate the appropriate angle. By outputs POS and ANG the information on the position of the shutter control is provided. ANG and POS may only provide useful results if the times T_UD and T_ANGLE are precisely adapted to the corresponding blind. The actuator may, if T_ANGLE is set to T#0s, be used for all types of roller shutters. The inputs T_UD, T_ANGLE T_LOCKOUT and have the following default values** |  |
| | T_UD = T#10S |
| | T_ANGLE = T#3S |
| | T_LOCKOUT = T#100MS |
| | The input and output S_IN STATUS are ESR compliant outputs and inputs. In Input S_IN  the upstream functions report their status to the module, this status will be forwarded to the output of STATUS, and own status messages also issued on STATUS. If a status message is present at the input it will overwrite the own status messages, an error will be put out with highest priority. |
| **The following graphic shows the internal structure and function of the module** |  |
| **Setup	T_LOCKOUT** | TIME (delay time between change of direction) |

![blind_actuator](blind_actuator.gif)
![blind_actuator_circuitry](blind_actuator_circuitry.gif)

| STATUS | Meaning |
| --- | --- |
| 0 | no message |
| 1 | Error, UP and DN active simultaneously |
| 101 | Manual UP |
| 102 | Manual DN |
| NNN | forwarded message |
