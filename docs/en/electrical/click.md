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
| **Input	IN** | BOOL (control input for buttons) |
| **Output	Q** | BOOL (output) |
| **SINGLE** | BOOL (output for simple key press) |
| **DOUBLE** | BOOL (output for double key press) |
| **TRIPLE** | BOOL (output for tripple key press) |
| **STATUS** | BYTE (ESR compliant status output) |
| **Setup	T_DEBOUNCE** | TIME (debounce time for buttons) |
| **T_SHORT** | TIME (Maximum time for short pulse) |
| **T_PAUSE** | TIME (maximum interval between two pulses) |
| **T_RESetup** | TIME (reconfiguration time) |
| | CLICK is a button interface which automatically adjusts to the connected switch. If a switch is connected, CLICK recognize themselves whether it is an opener or closer, and then evaluates each case only the first flank. With the setup variable T_DEBOUNCE the debounce of the buttons is set. It is set by default to 10 ms. The time T_RESetup is used to decide whether a make or break is connected to the input IN. If the input is for more than this time in a state, it is assumed as rest mode. The default value is 1 minute for T_RESetup. With short successive pulses a single, double or triple pulse evaluated and switches according to the output SINGLE, DOUBLE or TRIPLE. If the pulse is longer than the setup time T_SHORT or a pause between two pulses is longer than T_PAUSE, then the pulse sequence is interrupted and the corresponding output is set, until the contrary input pulse is inactive. The output Q corresponds to the input pulse. However, it is always  High- active. An ESR compliant status output indicates state changes to subsequent ESR compliant evaluation modules. With short pulses, the output  SINGLE (one pulse), DOUBLE (2 pulses) or  TRIPLE (3 pulses) is selected. The corresponding output remains at least one cycle active and as a maximum of as long as the input IN remains active. |

![click](click.gif)
![click_sample_1](click_sample_1.gif)
![click_sample_2](click_sample_2.gif)

**Example:**

Example 1 shows an application of CLICK with three subsequent dimming modules. Analog can also be used up to 3 switch or a mixture of dimmers   or switches.

Example 2 shows CLICK with a dimmer, and behaves like a dimmer without CLICK, however, a short double-click sets the output of the dimmer at 100% and a triple-click is as an additional switching output available.

| Status |  |
| --- | --- |
| 110 | Inactive input |
| 111 | Output SINGLE activated |
| 112 | Output DOUBLE activated |
| 113 | TRIPLE output enabled |
