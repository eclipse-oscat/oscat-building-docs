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
| **Input	IN** | BOOL (input signal from the switch or push button) |
| **TD** | TIME (debounce) |
| **PM** | BOOL (operation mode TRUE = pulse mode operation) |
| **Output	Q** | BOOL (output) |
| | DEBOUNCE can debounce the signal from a switch or button and pass it debounced to the output Q . If PM = FALSE, the output Q follows the input signal IN debounced, if PM = TRUE at the input IN a leading edge is detected and the output Q remains only for one cycle to TRUE. The debounce time for the input IN is set by the time TD. |

![debounce](debounce.gif)
