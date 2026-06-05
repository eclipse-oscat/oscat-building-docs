<!--
  Copyright (c) 2026 Hans Mühlbauer, Franz Höpfinger and others.

  This program and the accompanying materials are made available under the
  terms of the Eclipse Public License 2.0 which is available at
  https://www.eclipse.org/legal/epl-2.0

  SPDX-License-Identifier: EPL-2.0
-->

## Type	Funktionsbaustein

| | |
|:---|:---|
| **Input	I1** | BYTE (Steuersignal 1) |
| **IS** | BOOL (Eingangs Auswahl) |
| **I2** | BYTE (Steuersignal 2) |
| **RV** | BOOL (Richtungsumkehr für Ausgang Y) |
| **DX** | BOOL (Selbstaktivierung) |
| **Output	Y** | WORD (Steuersignal für den Stellmotor) |
| | ACTUATOR_A dient zur Ansteuerung von Stellmotoren mit analog Eingang. Der Baustein hat zwei Eingänge (I1 und I2) die im Bereich 0..255 den gesamten Ausgangsbereich an Y abdecken. Der Ausgang Y ist vom Typ WORD, und sein Schaltbereich wird durch die Setup Werte OUT_MIN und OUT_MAX vorgegeben. Ein Eingangswert von 0 erzeugt den Ausgangswert OUT_MIN und ein Eingangswert von 255 erzeugt den Ausgangswert OUT_MAX, andere Eingangswerte erzeugen entsprechende Ausgangswerte  zwischen OUT_MIN und OUT_MAX. Der Baustein kann direkt zur Ansteuerung von DA Wandlern mit 16Bit Eingang verwendet werden. Der Eingang IS selektiert zwischen zwei Eingängen I1 und I2, somit kann z.B. zwischen Hand und Automatikbetrieb umgeschaltet werden. Ein weiterer Eingang DX schaltet bei steigender Flanke unmittelbar eine Selbstaktivierung ein. wenn SELF_ACT_TIME > t#0s dann wird die Selbstaktivierung nach Ablauf der Zeit SELF_ACT_TIME automatisch wiederholt, dabei schaltet der Ausgang Y für die Zeit RUNTIME auf OUT_MIN, anschließend für die gleiche Zeit auf OUT_MAX und kehrt danach wieder zum normalen Stellwert zurück. Der Eingang RV kann den Ausgang Invertieren, Y = OUT_MAX wenn I = 0 und Y = OUT_MIN wenn I = 255. Auf diese Weise kann ganz einfach die Laufrichtung des Stellmotors umgekehrt werden. |
| **Setup	RUNTIME** | TIME (Laufzeit des Stellmotors) |
| **SELF_ACT_TIME** | TIME (Zeit für automatische Bewegung) |
| **OUT_MIN** | DWORD (Ausgangswert bei I = 0) |
| **OUT_MAX** | DWORD (Ausgangswert bei I = 255) |

![actuator_a](actuator_a.gif)

| IS | RV | DX | Y |
| --- | --- | --- | --- |
| 0 | 0 | 0 | Y = (OUT_MAX-OUT_MIN) * I1 /255 +OUT_MIN |
| 1 | 0 | 0 | Y = (OUT_MAX-OUT_MIN) * I2 /255 +OUT_MIN |
| 0 | 1 | 0 | Y = OUT_MAX - (OUT_MAX-OUT_MIN) * I1 /255 |
| 1 | 1 | 0 | Y = OUT_MAX - (OUT_MAX-OUT_MIN) * I2 /255 |
| - | - |  | startet einen Selbstaktivierungszyklus |
