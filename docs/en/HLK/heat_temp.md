<!--
  Copyright (c) 2026 Hans Mühlbauer, Franz Höpfinger and others.

  This program and the accompanying materials are made available under the
  terms of the Eclipse Public License 2.0 which is available at
  https://www.eclipse.org/legal/epl-2.0

  SPDX-License-Identifier: EPL-2.0
-->

## HEAT  _TEMP

| | |
|:---|:---|
| **Type** | Function module |
| **Input	T_EXT** | REAL (TAT) |
| **T_INT** | REAL (nominal room temperature) |
| **OFFSET** | REAL (lowering or raising the |
| | Room temperature) |
| **T_REQ** | REAL (temperature requirement) |
| **Output	TY** | REAL (heating circuit flow temperature) |
| **HEAT** | BOOL (heating requirement) |
| **Setup	TY_MAX** | REAL (maximum heating circuit temperature, 70°C) |
| **TY_MIN** | REAL (minimum heating circuit temperature, 25°C) |
| **TY_C** | REAL (design temperature, 70°C) |
| **T_INT_C** | REAL (room design temperature, 20°C) |
| **T_EXT_C** | REAL (T_EXT at design temperature -15°C) |
| **T_DIFF_C** | REAL (forward / reverse differential 10°C) |
| **C** | REAL (constant of the heating system, DEFAULT = 1.33) |
| **H** | REAL (threshold requirement for heating 3°C) |
| **HEAT_TEMP  calculates  the flow temperature of the outside temperature by the following formula** |  |
| | TY =  TR + T_DIFF / 2 * TX + (TY_Setup - T_DIFF / 2 - TR) * TX ^ (1 / C) |
| **with** | TR = T_INT + OFFSET |
| **TX** | = (TR - T_EXT) / (T_INT_Setup - T_EXT_Setup); |
| | The parameters of the heating curve are given by the setup variables  TY_C (design flow temperature), T_INT_C (room temperature at the design point), T_EXT_C (outside temperature at the design point) and T_DIFF_C (difference between forward / reverse at the design point). With the input offset, the heating curve of room reduction (negative offset)  or room boost (positive offset) can be adjusted. With the setup variables TY_MIN and TY_MAX the flow temperature can be kept to a minimum and maximum value. The input T_REQ is used to support requirements such as external temperature from the boiler. If T_REQ is larger than the calculated value of the heating curve for TY so TY is set to T_REQ. The limit of TY_MAX does not apply to the request by T_REQ. The setup variable H define at what outside temperature the heating curve is calculated, as long as T_EXT + H  >=  T_INT +OFFSET the TY stays at 0 and HEAT is FALSE. If T_EXT + H < T_INT + OFFSET the HEAT is TRUE and TY  outputs the calculated flow temperature. The setup variable C determines the curvature of the heating curve. The curvature is dependent on the heating system. |
| **Convectors** | C = 1.25 – 1.45 |
| **Panel radiators** | C = 1.20 – 1.30 |
| **Radiators** | C = 1.30 |
| **Pipes** | C = 1.25 |
| **Floor heating** | C = 1.1 |
| | The larger the value of C, the stronger the heating curve is curved. A value of 1.0 gives a straight line as the heating curve.   Typical heating systems are between 1.0 and 1.5. |
| **The graph shows  Heating curves  for the design temperatures of 30 - 80°C flow temperature at -20 ° C outside temperature and at a C of 1.33** |  |

![heat_temp](heat_temp.gif)
![heat_temp_kurve](heat_temp_kurve.gif)
