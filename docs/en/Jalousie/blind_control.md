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
| **PI** | BYTE (default of position) |
| **AI** | BYTE (default of fin angle) |
| **T_UD** | TIME (time to move up 0 ..255) |
| **T_ANGLE** | TIME (time to move flap from von 0 ..255) 255 |
| **Output	POS** | BYTE (simulated shutter position) |
| **ANG** | BYTE (simulated fin angle) |
| **MU** | BOOL (motor up signal) |
| **MD** | BOOL (Motor down Signal) |
| **STATUS** | BYTE (ESR compliant status output) |
| | BLIND_CONTROL controls the shutter and the fin angle according to settings in PI and AI if UP and DN is both TRUE (automatik modue). POS und ANG are herein the values of the shutter. At this outputs  the simulated position and angle of the shutter are bypassed. BLIND_CONTROL switch the outputs MU or MD to TRUE in a corresponding order until the values in POS and ANG correspond to default of PI and AI. A internal sequencer controls that while shutter moves up and down the fin angle is adjusted before the up and down movement happens. So when the shutter moves up or down, the fin angle is adjusted and after the movement it restores it's angle. The input SNES defines at which difference the control module is active and adjusts the output in a way to correspond to the inputs PI and AI.  IF SENS = 0 every difference is controlled, if SENS = 5 (default) after a difference of 5 between the setup values and the actual values controlling is done. If UP and DN is not TRUE, BLIND_CONTROL leaves the automatic mode and the outputs QU and QD are controled by manual mode of UP and DN. BLIND_CONTROL does not need BLIND_ACTUATOR to control a shutter because BLIND_ACTUATOR is integrated in BLIND_CONTROL already. If no automatic mode for a shutter is needed, BLIND_ACTUATOR only is recommended. Use of BLIND_CONTROL must be carefully and must set the cycle time for the module smaller than T_ANGLE / 512 * SENS. With a doubleclick to the SENS symbol the setup values can be adjusted (default 5). If the cycle time is to long, the shutter moves up and down in a not periodically manner. If a smaller cycle time is not possible, the SENS value can be increased. |
| | The graph shows the shutter geometry. |
| | The table shows the working states of the module. |
| | The input and output S_IN STATUS are ESR compliant outputs and inputs. In Input S_IN  the upstream functions report their status to the module, this status will be forwarded to the output of STATUS, and own status messages also issued on STATUS. |
| **Setup	SENS** | BYTE (resolution of controll module) |
| **T_LOCKOUT** | TIME (lockout time at direction reverse of motors) |

![blind_control](blind_control.gif)
![blind_control_sample1](blind_control_sample1.gif)

| UP | DN | PI | AI | MU | MD |  |
| --- | --- | --- | --- | --- | --- | --- |
| L | L | - | - | L | L | no action |
| H | L | - | - | H | L | shutter moves up |
| L | H | - | - | L | H | shutter moves down |
| H | H | P | A | X | X | Position P and angle A are driven automatically. |

| STATUS | Meaning |
| --- | --- |
| 0 | no message |
| 101 | manually up |
| 102 | manually down |
| 121 | position up |
| 122 | position down |
| 123 | fin setting horizontally |
| 124 | fin setting vertically |
| NNN | forwarded messages |
