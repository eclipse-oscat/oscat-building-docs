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
| **Input	UD** | BOOL (direction input in Auto Mode UP = TRUE) |
| **ON** | BOOL (TRUE, when in Auto Mode) |
| **MANUAL** | BOOL (TRUE, if Manual Mode) |
| **UP** | BOOL (UP enable in Manual Mode) |
| **DN** | BOOL (DN enable in Manual Mode) |
| **OFF** | BOOL (safety switch TRUE = outputs FALSE) |
| **YUP_IN** | BOOL (return input UP relay) |
| **YDN_IN** | BOOL (return input DN relay) |
| **Output	YUP** | BOOL (output for direction UP) |
| **YDN** | BOOL (output direction for DN) |
| **STATUS** | Byte (ESR compliant status and error output) |
| **Config	SOUND** | TIME (minimum on-time) |
| **TOFF** | TIME (minimum off time) |
| **OUT_RETURN** | BOOL (switches and the return input YUP_In and YDN_in) |
| **ACTUATOR_UD is a reversing contactor interface with locking and configurable timing. With additional return inputs a activation was prevented as long as a relais stuck. The module has an automatic and a manual mode. In automatic mode (ON = TRUE and Manual = FALSE), the input of the UD decides about the direction and ON/OFF. As soon as the manual input is TRUE starts the Manual mode and outputs will follow only the inputs UP and DN. UP and DN may never be both TRUE, if happens both outputs gets FALSE. With a safety-switch-off input OFF the outputs are switched off in  both the manual and in automatic mode at any time.  Two return inputs YUP_IN and YDN_IN serve as separate inputs for the state of the relays due to the avoid activating the output of a other relais in case of a failure of one relay module. This error is reported through error messages at the output STATUS. The feedback function is only available if the config variable OUT_RETURN is set to TRUE. Status reports all activities of the module in order to provide them for a data record. The status output is  ESR compatible and combinable with other ESR modules from our library. The output status reports two errors** |  |
| **1** | YUP can not be set because YDN_IN TRUE. |
| **2** | YDN can not be set because YUP_IN TRUE. |
| | The Config variables TON and TOFF define a minimum ontime and a dead time between two output impulses and therefore large motors or transmissions can be switched, even if they needs a start and stop time. |

![actuator_ud](actuator_ud.png)

| Manual | UP | DN | ON | UD | OFF | YUP | YDN | Status |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 1 | 0 | 0 | - | - | 0 | 0 | 0 | 102 |
| 1 | 1 | 0 | - | - | 0 | 1 | 0 | 103 |
| 1 | 0 | 1 | - | - | 0 | 0 | 1 | 104 |
| 1 | 1 | 1 | - | - | 0 | 0 | 0 | 102 |
| 0 | - | - | 1 | 1 | 0 | 1 | 0 | 111 |
| 0 | - | - | 1 | 0 | 0 | 0 | 1 | 112 |
| - | - | - | - | - | 1 | 0 | 0 | 101 |
| 1 | 0 | 0 | 0 | - | 0 | 0 | 0 | 110 |
| 0 | - | - | 0 | - | - | 0 | 0 | 110 |
