<!--
  Copyright (c) 2026 Hans Mühlbauer, Franz Höpfinger and others.

  This program and the accompanying materials are made available under the
  terms of the Eclipse Public License 2.0 which is available at
  https://www.eclipse.org/legal/epl-2.0

  SPDX-License-Identifier: EPL-2.0
-->

## BLIND_CONTROL_S

| | |
|:---|:---|
| **Type** | Funktionsbaustein |
| **Input	UP** | BOOL (Eingang AUF) |
| **DN** | BOOL (Eingang AB) |
| **S_IN** | BYTE (ESR kompatibler Status Eingang) |
| **PI** | BYTE (Vorgabe der Position) |
| **T_UP** | TIME (Laufzeit des Rollos nach oben) |
| **T_DN** | TIME (Laufzeit des Rollos nach unten) |
| **RU** | BOOL (Freigabe für Öffnung unten) |
| **RD** | BOOL (Freigabe für Öffnung oben) |
| **Output	POS** | BYTE (Simulierte Position) |
| **MU** | BOOL (Motor Auf Signal) |
| **MD** | BOOL (Motor Ab Signal) |
| **STATUS** | BYTE (ESR kompatibler Status Ausgang) |
| | BLIND_CONTROL_S steuert und Regelt die Stellung von Rollos. Die Ausgänge MU und MD steuern die Auf und Ab Richtung der Motoren. Die Zeit T_LOCKOUT ist die Wartezeit für eine Richtungsumkehr zwischen MU und MD und die Zeiten T_UP und T_DN legen fest wie lange der Motor für eine volle Bewegung nach unten beziehungsweise nach oben benötigt. Da die Laufzeit der Motoren variieren kann wird bei erreichen einer Endposition (oben oder unten) der entsprechende Motor zusätzlich um die Zeit T_EXT angesteuert um sicherzustellen das die Endposition sicher erreicht wird, was für eine fortlaufende Kalibrierung der Anlage sorgt. Bei der ersten Inbetriebnahme und nach einem Stromausfall wird automatisch eine Kalibrierungsfahrt nach oben durchgeführt. Die Variable EXT_TRIG gibt an ab welcher Distanz vom Endwert die Fahrzeit verlängert wird. Im Automatik Modus limitiert die Einstellung R_POS_TOP wenn RD = TRUE die maximale Stellung des Rollos. So bleibt zum Beispiel der Rollo bei 240 stehen wenn RD = TRUE und R_POS_TOP = 240 sind, was im Winter ein Einfrieren in der oberen Stellung verhindern kann. Analog ist R_POS_BOT und RU = TRUE für die unterste mögliche Stellung zuständig, was im Sommer für eine Zwangslüftung sorgen kann. Der Ausgang POS ist die simulierte Stellung des Rollos, 0 = unten und 255 = oben. S_IN und STATUS sind die ESR kompatiblem Status Ein beziehungsweise Ausgänge. |
| **Der Baustein wird mit anderen Bausteinen der Jalousiesteuerung verschaltet** |  |
| | BLIND_CONTROL_S ist speziell für die Ansteuerung von Rollos und hat im Gegensatz zu Jalousien keine Winkelstellung, weshalb der Baustein auch keinen Eingang AI und keinen Ausgang ANG besitzt. BLIND_CONTROL_S kann selbstverständlich auch mit den anderen BLIND Bausteinen der Bibliothek verschaltet werden. |
| | Der Baustein unterstützt eine automatische Kalibrierung, welche dazu führen kann das nach einem Stromausfall alle Rollos nach oben Fahren, was unter Umständen bei Abwesenheit unerwünscht ist. Deshalb ist bei Abwesenheit die gewünscht Stellung der Rollos auf den Eingang PI zu legen. Die Rollos Fahren dann zum Kalibrieren nach oben, und anschließend automatisch wieder in die gewünschte Stellung. Die automatische Kalibrierung  kann jedoch wenn beide Eingänge UP und DN auf FALSE liegen verhindert werden. |
| **Setup	T_LOCKOUT** | TIME (Totzeit bei Richtungswechsel der Motoren) |
| **T_EXT** | TIME (Verlängerungszeit bei Endanschlag) |
| **EXT_TRIG** | BYTE (Trigger für Verlängerungszeit) |
| **R_POS_TOP** | BYTE (Maximale Position wenn RD = TRUE) |
| **R_POS_BOT** | BYTE (Minimale Position wenn RU = TRUE) |

![blind_control_s](blind_control_s.gif)
![blind_control_s_sample](blind_control_s_sample.gif)

| UP | DN | STATUS |  | MU | MD |
| --- | --- | --- | --- | --- | --- |
| H | H | 103 | POS wird auf PI geregelt | Auto | Auto |
| L | H | 102 | Handbetrieb Ab | L | H |
| H | L | 101 | Handbetrieb Auf | H | L |
| L | L | - | Manual Timeout | L | L |
| - | - | 107 | LockoutTime | L | L |
| - | - | 108 | Auto Kalibrierung | H | L |
| - | - | 109 | Zeit Verlängerung | X | X |
