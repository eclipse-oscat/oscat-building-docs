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
| **Input	IN** | BYTE (control input 0 - 255) |
| **TEST** | BOOL (starts autorun when TRUE) |
| **ARE** | BOOL (enable for Autorun) |
| **I / O	ARX** | BOOL (autorun signal bus) |
| **Output	OUT** | BOOL (switching signal for valve) |
| **ARO** | BOOL (TRUE if autorun is active) |
| **Setup	CYCLE_TIME** | TIME (clock speed of the valve) |
| **SENS** | BYTE (Minimum and maximum input values) |
| **SELF_ACT_TIME** | TIME (self act time) |
| **SELF_ACT_PULSE** | TIME (switching time with autorun) |
| **SELF_ACT_CYCLES** | INT (number of cycles with autorun) |
| | ACTUATOR_2P is an interface for 2-point actuators such as solenoid valves. The 2-point actuator can only be on / off switching and therefore, the input value IN is canged in a pulse / pause signal at the output OUT. The cycle time (CYCLE_TIME) determines the switching times of the output. The sticking of the valve because of a long rest period is prevented by using the self act time (SELF_ACT_TIME) and the count of self act cycles (SELF_ACT_CYCLES) and the pulse duration (SELF_ACT_PULSE). The cycles runs automatically and a stick of  the valve can be avoided. After the interval, the module checks whether SELF_ACT_TIME ARE = TRUE and = ARX is FALSE, then switches ARO for the duration of self-activation to TRUE. At the same time ARX set to TRUE to prevent that other modules which are connected to the same ARX go to the Autorun. The input IN value can be varied from 0..255 If the input signal IN < SENS, the valve remains permanently closed (OUT = FALSE) and IN > 255 - SENS means the valve is permanently open (OUT = TRUE). |

![actuator_2p](actuator_2p.gif)
