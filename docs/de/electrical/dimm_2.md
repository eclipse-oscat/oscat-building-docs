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
| **Input	SET** | BOOL (Eingang zum Einschalten des Ausgangs auf VAL) |
| **VAL** | BYTE (Wert für die SET Operation) |
| **I1** | BOOL (Steuereingang für Taster1, Auf) |
| **I2** | BOOL (Steuereingang für Taster2, Ab) |
| **RST** | BOOL (Eingang zum Ausschalten des Ausgangs) |
| **Output	Q** | BOOL (Schaltausgang) |
| **D1** | BOOL (Ausgang für Doppelklick an I1) |
| **D2** | BOOL (Ausgang für Doppelklick an I2) |
| **I/O	OUT** | Byte (Dimmer Ausgang) |
| **Setup	T_DEBOUNCE** | TIME (Entprellzeit für Taster) |
| **T_ON_MAX** | TIME (Einschaltbegrenzung) |
| **T_DIMM_START** | TIME (Reaktionszeit zum Dimmen) |
| **T_DIMM** | TIME (Zeit für eine Dimm Rampe) |
| **MIN_ON** | BYTE (Minimalwert von OUT beim Einschalten) |
| **MAX_ON** | BYTE (Maximalwert von OUT beim Einschalten) |
| **RST_OUT** | BOOL (Reset setzt OUT auf 0 gesetzt wenn TRUE) |
| **SOFT_DIMM** | BOOL (Soft Start beim Einschalten) |
| **DBL1_TOG** | BOOL (Enable Toggle für D1) |
| **DBL2_TOG** | BOOL (Enable Toggle für D2) |
| **DBL1_SET** | BOOL (Enable Wert für Doppelklick I1) |
| **DBL2_SET** | BOOL (Enable Wert für Doppelklick I2) |
| **DBL1_POS** | BYTE (Stellwert bei Doppelklick an I1) |
| **DBL2_POS** | BYTE (Stellwert bei Doppelklick an I2) |
| | DIMM_2 ist ein intelligenter Dimmer für 2-Taster Bedienung. Der Dimmer kann über Setup-Variablen eingestellt werden. Die Zeit T_DEBOUNCE dient zur Entprellung des Tasters und ist standardmäßig auf 10ms eingestellt. Eine Einschaltbegrenzung T_ON_MAX schaltet den Ausgang automatisch ab, wenn sie überschritten wird. Die Zeiten T_DIMM_Start und T_DIMM legen das Zeitverhalten des Dimmers fest. |
| | Mit den Eingängen SET und RST kann der Ausgang Q jederzeit Ein- beziehungsweise Aus-geschaltet werden. SET setzt dabei den Ausgang OUT auf den durch VAL Vorgegebenen Wert, RST setzt OUT auf 0 wenn die Setup Variable RST_OUT auf TRUE steht. RST schaltet zusätzlich D1 und D2 auf FALSE. SET und RST können unter anderem zum Anschluss von Brandmeldeanlagen oder Alarmanlagen benutzt werden. Mit SET können im Brandfall oder bei Einbruch alle Leuchten auf Ein oder mit RST beim verlassen des Gebäudes Zentral auf Aus geschaltet werden. |
| **Beim Ein- und Aus- schalten bleibt der letzte Ausgangswert des Dimmers am Ausgang OUT erhalten, lediglich ein FALSE am Ausgang Q schaltet das Leuchtmittel ab, und TRUE am Ausgang Q schaltet das Leuchtmittel wieder ein. Beim Einschalten durch einen kurzen Tastendruck limitiert der Baustein den Ausgang OUT auf mindestens MIN_ON und maximal MAX_ON. Steht z.B. der Dimmer auf 0 so setzt der Baustein den Ausgang OUT automatisch auf 50 und umgekehrt wird der Ausgang OUT falls er höher als MAX_ON steht auf MAX_ON begrenzt. Diese Parameter sollen verhindern das nach dem Einschalten ein sehr kleiner Wert am Ausgang OUT anliegt und trotz aktiven Q kein Licht angeht. Es wird durch den Parameter MIN_ON ein minimaler Leuchtwert beim Einschalten vorgegeben. Umgekehrt kann z.B** | bei Schlafzimmern verhindert werden das beim Einschalten sofort volle Leuchtstärke anliegt. Wird der Parameter SOFT_DIMM auf TRUE gesetzt, so beginnt das DIMMEN beim Einschalten mit langem Tastendruck immer bei 0. zusätzlich zur Funktion des Dimmers wird an den Eingängen I1 und I2 ein Doppelklick dekodiert der die Ausgänge D1 beziehungsweise D2 für einen Zyklus auf TRUE setzt. Wird die Setup Variable D?_TOGGLE auf TRUE gesetzt so wird der Ausgang D? bei jedem Doppelklick invertiert. Die Ausgänge D1 und D2 können benutzt werden um zusätzliche Verbraucher oder Ereignisse mit einem Doppelklick zu schalten. Ein Ausgang D? kann auch auf den Eingang SET gelegt werden und der Dimmer mittels eines Doppelklicks auf einen durch VAL vordefinierten Wert gesetzt werden. Wird die Setup Variable DBL?_SET auf TRUE gesetzt, so wird bei einem entsprechenden Doppelklick nicht der zugehöriger Ausgang D? verändert, sondern es wird der Wert der Variable DBL?_POS auf den Ausgang OUT geschrieben und der Ausgang Q falls nötig eingeschaltet. OUT ist der Wert des Dimmers und wird als I/O Variable extern definiert. dies hat den Vorteil das der Wert des Dimmers jederzeit extern beeinflusst werden kann und auch nach einem Stromausfall wieder rekonstruiert werden kann. OUT kann auf Wunsch Remanent und Persistent definiert werden. |
| **Die folgende Tabelle zeigt die Betriebszustände des Dimmers** |  |

![dimm_2](dimm_2.gif)

| I1 | I2 | SET | RST | Q | D1 | D2 | OUT |
| --- | --- | --- | --- | --- | --- | --- | --- |
| single | - | 0 | 0 | 1 | - | - | LIMIT(MIN_ON,OUT,MAX_ON) |
| - | single |  |  | 0 | - | - |  |
| double | - | 0 | 0 |  | TOGPULSE |  |  |
| - | double | 0 | 0 |  |  | TOGPULSE |  |
| long | - | 0 | 0 | 1 | - |  | dimm upstart from 1 if SOFT_DIMM = TRUE |
| - | long |  |  | 1 |  |  | dimm downandturnoffat 0 |
| - | - | 1 | 0 | ON | - |  | VAL |
| - | - | 0 | 1 | OFF | OFF |  | 0 wenn RST_OUT = TRUE |
