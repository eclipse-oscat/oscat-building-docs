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
| **Input	IN1..6** | BOOL (push button inputs) |
| **Output	Qx** | BOOL (switch outputs) |
| **Setup	T_DEBOUNCE** | TIME (debounce time for buttons) |
| | SWITCH_X is an interface for up to 6 push-buttons. The individual buttons are debounced with  T_DEBOUNCE and switch the respective outputs Q1 to Q6. IN3 to IN6 are directly connected to the outputs when they be operated alone. IN1 and IN2 generate a pulse for one cycle after they are pressed. If one of the inputs IN3 up to N6 is pressed during input IN1 or IN2 is operated , then no output pulse passed to Q1 to Q6, but the corresponding output Q31 to Q62 is activated. Q42, for example, is activated if IN4 is operated while IN2 is operated. Q2 and Q4 are then inactive. |
| | SWITCH_X thus allows the inputs IN3 to IN6  to realize a triple occupancy and select it by pressing IN1 or IN2 and a further input. |

![switch_x](switch_x.gif)
