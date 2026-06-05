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
| **Input	T** | REAL (outdoor temperature in ° C) |
| **V** | REAL (Wind speed in km/h) |
| **Output** | REAL (wind chill temperature) |
| | WCT calculates the wind chill temperature depending on the wind speed in km/h and the outside temperature °C. The wind chill temperature is defined only for wind speeds greater than 5 km/h and temperatures below 10 °C. For values outside the defined range, the input temperature is output. |

![wct](wct.gif)
