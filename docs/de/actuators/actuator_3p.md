<!--
  Copyright (c) 2026 Hans Mühlbauer, Franz Höpfinger and others.

  This program and the accompanying materials are made available under the
  terms of the Eclipse Public License 2.0 which is available at
  https://www.eclipse.org/legal/epl-2.0

  SPDX-License-Identifier: EPL-2.0
-->

## ACTUATOR_3P

| | |
|:---|:---|
| **Type** | Funktionsbaustein |
| **Input	IN** | BYTE (Eingang Steuersignal 0 - 255) |
| **TEST** | BOOL (Baustein führt Diagnose aus wenn TRUE) |
| **ARE** | BOOL (Auto Diagnose ist erlaubt wenn TRUE) |
| **END_POS** | BOOL (Eingang für Endschalter) |
| **Output	OUT1** | BOOL (Steuersignal für Klappe in Richtung Auf) |
| **OUT2** | BOOL (Steuersignal für Klappe in Richtung Zu) |
| **POS** | BYTE (Simulierte Klappenstellung) |
| **ERROR** | BOOL (TRUE wenn Diagnosefehler) |
| **STATUS** | BYTE (ESR kompatibler Status Ausgang) |
| **I/O	ARX** | BOOL (Autorun Kommunikation) |
| **Setup	T_RUN** | TIME (Laufzeit für volle Bewegung 0 - 255) |
| **T_EXT** | TIME (Laufzeitverlängerung bei Diagnose) |
| **T_CAL** | TIME (Klappenlaufzeit bis zur Kalibrierung) |
| **T_DIAG** | TIME (Zeitspanne für Autodiagnose) |
| **SWITCH_AVAIL** | BOOL (TRUE, wenn Endschalter |
| | angeschlossen ist) |
| | ACTUATOR_3P ist ein 3-Punkt Aktuator Interface zum Ansteuern von Stellmotoren mit Auf / Ab Eingang. Das Signal am Eingang IN wird umgesetzt in Steuerimpulse an den Ausgängen OUT1 und OUT2 die den Motor entsprechend Steuern. Das Eingangssignal IN wird so verarbeitet und die beiden Steuerausgänge (OUT1 und OUT2) so gesteuert, dass ein Eingangswert von 0 Klappe geschlossen, 255 Klappe offen, 127 Klappe halb geöffnet usw. bewirkt. Der Baustein kann auch einen Endschalter verarbeiten. Die Endschalter müssen so angeschlossen werden, dass egal ob oberes oder unteres Ende erreicht wurden, der Eingang END_POS TRUE wird und damit anzeigt, dass die Klappe eine der beiden Endstellungen erreicht hat. Um die Endschalterfunktion in Betrieb zu setzen muss die Setup-Variable SWITCH_AVAIL auf TRUE stehen, ansonsten wird der Endschalter ignoriert. Der Diagnose Eingang TEST kann zu jederzeit eine Klappen und Motor-Diagnose starten. Der Baustein durchläuft dann einen Diagnosezyklus und meldet eventuelle Fehler am Ausgang ERROR. Ein Diagnosezyklus fährt die Klappe zurück auf 0%, vermisst dann die Laufzeit von 0% - 100% und wieder zurück auf 0%. Er prüft auch, ob Endschalter funktionieren (falls diese durch die Setup-Variable SWITCH_AVAIL aktiviert wurden). Nach dem Diagnose-Zyklus fährt die Klappe wieder in die durch den Eingang IN definierte Stellung. Die während der Diagnose gemessenen Laufzeiten werden im Betrieb verwendet um die Klappe extrem genau auf die jeweils geforderte Position zu bewegen. Mit der Setup-Variable T_DIAG wird spezifiziert, nach welcher Zeit eine Diagnose selbständig ohne durch den Eingang TEST aktiviert zu werden, durchgeführt wird. Nach dem Einschalten wird automatisch immer ein Diagnose-Zyklus durchgeführt. Ist der Wert T_DIAG = T#0s, wird keine automatische Diagnose durchgeführt. |
| | Eine Klappe wird Üblicherweise Auf und Ab bewegt um verschiedene Volumenströme einzustellen. Je mehr sich eine Klappe bewegt, desto mehr weicht sie von einer idealen absoluten Position ab, weil bei jeder Bewegung ein kleiner Positionsfehler auftritt und sich über viele Bewegungen addiert. Um diesem Fehler entgegen zu Wirken kann mit der Setup Variablen T_CAL nach einer definierten Laufzeit (aufaddierte Zeit aller Klappenbewegungen) der Klappe eine Kalibrierung automatisch durchgeführt werden. Bei dieser Kalibrierung fährt der Motor in Nullstellung und stellt die Klappe anschließend wieder auf den durch IN spezifizierten Wert. Ein Wert von T#0s für die CAL_RUNTIME bedeutet, dass keine automatische Kalibrierung durchgeführt wird. |
| | Bei Kalibrierung und Diagnose ohne Endschalter wird für eine volle Bewegung die Zeit T_EXT zur Laufzeit T_RUN addiert um sicherzustellen das die Klappe seine Endposition auch ohne Endschalter sicher erreicht. |
| | Am Ausgang POS simuliert der Baustein die aktuelle Klappenstellung mittels der eingestellten Zeit T_RUN. An diesem Ausgang kann auch festgestellt werden wann die Klapp die am Eingang angeforderte Stellung erreicht hat. Wird der Eingang TEST = TRUE gesetzt führt der Baustein einen Diagnosezyklus durch. Über die externe Variable ARX kommunizieren mehrere Bausteine miteinander und sorgen selbständig dafür das Diagnosezyklen nach dem Einschalten nacheinander und nicht Parallel ausgeführt werden. Der Anwender legt dabei fest wie viele und welche Bausteine an die gleiche Variable geschaltet werden und sich dadurch abstimmen können. Wird jeder Baustein an eine eigenen Variable ARX geschaltet erfolgt keine koordination der Diagnosezyklen. Weitere Informationen zu den Eingängen TEST, ARE und ARX ist beim Baustein Autorun nachzulesen. |
| **Statusmeldungen des Bausteins** |  |

![actuator_3p](actuator_3p.gif)

| STATUS |  | ARE | ARX |
| --- | --- | --- | --- |
| 100 | Normal operation | - | - |
| 101 | Calibration | - | - |
| 103 | Diagnostic UP | TRUE | TRUE |
| 104 | Diagnostic DN | TRUE | TRUE |
