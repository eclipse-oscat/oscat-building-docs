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
| **PI** | BYTE (blind position in automatic mode) |
| **AI** | BYTE (slat angle in automatic mode) |
| **FIRE** | BOOL (input for fire alarm) |
| **WIND** | BOOL (input for wind alarm) |
| **ALARM** | BOOL (input for intrusion detection) |
| **DOOR** | BOOL (input for door contact) |
| **RAIN** | BOOL (input for rain sensor) |
| **Output	QU** | BOOL (motor up signal) |
| **QD** | BOOL (motor down signal) |
| **STATUS** | BYTE (ESR compliant status output) |
| **PO** | BYTE (output value of the blind in automatic mode) |
| **AO** | BYTE (output value of the blade angle in automatic mode) |
| | BLIND_SECURITY makes sure the blinds drive either up or down when certain events occur. The inputs UP and DN control a downstream module BLIND_ACTUATOR over the outputs of QU and QD. With the inputs FIRE, WIND, RAIN ALARM the inputs UP and DN are overwritten and the blinds drive either completely up or completely down. This FIRE has the highest priority followed by WIND, Alarm and with the lowest priority RAIN. Rain can be overridden as the only one by manual inputs UP and DN. Therefore, if the user should decide to remain open the blind despite the rain, he must interrupt the rain mode only by a short press of the UP or DN. FIRE drives the shutter to the top while RAIN, Wind and Alarm are configurable for up or down. ALARM is configured using the setup variables ALARM_UP for both high and down drive, the setup variable WIND_UP specifies whether to run in Wind up or down. The variable RAIN_UP determine what position will be approached at Rain. The default values are UPfor Alarm, UP for Wind and DNfor Rain. The setup variables can be changed by double-clicking the icon at any time. |
| | The input and output S_IN STATUS are ESR compliant outputs and inputs. In Input S_IN  the upstream functions report their status to the module, this status will be forwarded to the output of STATUS, and own status messages also issued on STATUS. |
| **The following graphic shows the application of BLIND_SECURITY with BLIND_ACTUATOR for controlling a blind** |  |
| | BLIND_SECURITY must necessarily used directly on BLIND_CONTROL.  If other modules are installed between BLIND_SECURITY and BLIND_CONTROL the security functions can not be guaranteed. |
| **Setup	ALARM_UP** | BOOL (default direction at ALARM Default = Up) |
| **WIND_UP** | BOOL (default direction at wind, Default = Up) |
| **RAIN_UP** | BOOL (default direction at rain, Default = Down) |

![blind_security](blind_security.gif)
![blind_security_sample](blind_security_sample.gif)

| STATUS | Meaning |
| --- | --- |
| 0 | no message |
| 111 | Fire |
| 112 | Wind |
| 113 | Burglar alarm |
| 114 | Door alarm |
| 115 | Rain |
| NNN | forwarded messages |
