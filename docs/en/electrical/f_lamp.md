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
| **Input	SWITCH** | BOOL (dimmer switch input) |
| **DIMM** | BYTE (input from the dimmer) |
| **RST** | BOOL (input for resetting the counter) |
| **Output	LAMP** | BYTE (dimmer output) |
| **STATUS** | BYTE (ESR compliant status output) |
| **I / O	ONTIME** | UDINT (operating time in seconds) |
| **ONTIME** | UDINT (operating time in seconds) |
| **Setup	T_NO_DIMM** | UINT (cut off time dimmer in hours) |
| **T_Maintenance** | UINT (reporting time for lamp replacement in |
| | Hours) |
| | F_LAMP is an interface for fluorescent lamp. The output LAMP follows the input DIMM and SWITCH. If DIMM is not connected, the default is off 255 is used and the output LAMP passes 0-255 depending on SWITCH. The outputs ONTIME and  CYCLES count the operating time of the light bulb in seconds and the switching cycles. Both values  are externally  stored and can be saved   permanent  or persistent , more info, see the module ONTIME. A TRUE at the input RST resets both values to 0. The setup variables T_NO_DIMM determines after which length of time a new lamp the dimming may be done. This value, when not otherwise set by the user, defaults to 100 hours. Fluorescent lamps may not use reduced levels of brightness, during the first 100 hours , otherwise your life is shortened dramatically. By a RST at replace of the lamp module it prevents the dimming in the initial phase. The output state is ESR compatible, and can report operating conditions, but also pass a message to change the bulb. The   default time T_MAINTENANCE is, if not modified by the  user, 15000 hours. If T_Maintenance  set to 0 so no message is generated for lamp replacement. |
| **The following example shows the use of the module F_LAMP in conjunction with  DIMM_I** |  |

![f_lamp](f_lamp.gif)
![f_lamp_sample](f_lamp_sample.gif)

| Status |  |
| --- | --- |
| 110 | Lamp off |
| 111 | Lamp on, no dimming allowed |
| 112 | Lamp on, dim allowed |
| 120 | Call for lamp replacement |
