<!--
  Copyright (c) 2026 Hans Mühlbauer, Franz Höpfinger and others.

  This program and the accompanying materials are made available under the
  terms of the Eclipse Public License 2.0 which is available at
  https://www.eclipse.org/legal/epl-2.0

  SPDX-License-Identifier: EPL-2.0
-->

## Type	 Function  : REAL

| | |
|:---|:---|
| **Input	T** | REAL (temperature in °C) |
| **RH** | REAL (Relative Humidity) |
| **Output** | REAL (  Heat  Temperature Index) |
| | HEAT_INDEX calculates at high temperatures and high humidity wind chill. The function is defined for temperatures above 20 ° C and relative humidity > 10%. For values outside the defined range, the input temperature is passed out. |

![heat_index](heat_index.gif)
