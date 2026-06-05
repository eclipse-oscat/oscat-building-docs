<!--
  Copyright (c) 2026 Hans Mühlbauer, Franz Höpfinger and others.

  This program and the accompanying materials are made available under the
  terms of the Eclipse Public License 2.0 which is available at
  https://www.eclipse.org/legal/epl-2.0

  SPDX-License-Identifier: EPL-2.0
-->

## CLICK_MODE

| | |
|:---|:---|
| **Type** | Function module |
| **Input	IN** | BOOL (control input for buttons) |
| **Output	SINGLE** | BOOL (output for simple key press) |
| **DOUBLE** | BOOL (output for double key press) |
| **LONG** | BOOL (output for a long key press) |
| **TP_LONG** | BOOL (pulse when long key press starts) |
| **Setup	T_LONG** | TIME (decoding time for long key press) |
| | CLICK_MODE is a push button interface which decodes  both simple click, double click or long keystrokes. With short pulses a single or double-click is decoded switches the according outputs SINGLE or DOUBLE, each for a one cycle. If the pulse is longer than the T_LONG, then the output TP_OUT is set for one cycle to TRUE and the output LONG remains TRUE until the input IN goes back to FALSE. |

![click_mode](click_mode.gif)
