<!--
  Copyright (c) 2026 Hans Mühlbauer, Franz Höpfinger and others.

  This program and the accompanying materials are made available under the
  terms of the Eclipse Public License 2.0 which is available at
  https://www.eclipse.org/legal/epl-2.0

  SPDX-License-Identifier: EPL-2.0
-->

## DIMM_I

| | |
|:---|:---|
| **Typ** | Funktionsbaustein |
| **Eingang SET** | BOOL (Eingang zum Schalten des Ausgangs auf VAL) |
| | VAL BYTE (Wert für die SET-Operation) |
| **IN** | BOOL (Steuereingang für Taster) |
| **RST** | BOOL (Eingang zum Rücksetzen des Ausgangs) |
| **Ausgang Q** | BOOL (Ausgang) |
| **DBL** | BOOL (Doppelklick-Ausgang) |
| **I / O OUT** | Byte (Dimmer-Ausgang) |
| **Setup T_DEBOUNCE** | TIME (Entprellzeit für Taster) |
| **T_RECONFIG** | TIME (Rekonfigurationszeit) |
| **T_ON_MAX** | TIME (Einschaltdauerbegrenzung) |
| **T_DIMM_START** | TIME (Reaktionszeit bis zum Dimmen) |
| **T_DIMM** | TIME (Zeit für eine Dimmrampe) |
| **MIN_ON** | BYTE := 50 (Minimalwert von OUT beim Einschalten) |
| **MAX_ON** | BYTE := 255 (Maximalwert von OUT beim Einschalten) |
| **SOFT_DIMM** | BOOL (wenn TRUE, beginnt das Dimmen nach dem Einschalten bei 0) |
| **DBL_TOGGLE** | BOOL (wenn TRUE, wird der Ausgang DBL bei jedem Doppelklick invertiert) |
| **RST_OUT** | BOOL (wenn Reset wahr ist, wird OUT auf 0 gesetzt) |
| | DIMM_I ist ein intelligenter Dimmer, der sich automatisch an Öffner oder Schließer anpasst, ohne dass eine Rekonfiguration erforderlich ist. Der Dimmer kann über die Setup-Variablen eingestellt werden. Über die Zeit T_DEBOUNCE wird der Taster entprellt (standardmäßig 10ms). Die Zeitvariable T_RECONFIG entscheidet, ob ein Öffner oder Schließer am Eingang IN angeschlossen ist. Wenn der Eingang länger als die definierte Zeit T_RECONFIG in einem Zustand verbleibt, wird dies als Ruhestellung angenommen. Wenn die Einschaltdauerbegrenzung T_ON_MAX überschritten wird, schaltet der Ausgang automatisch ab. Die Zeiten T_DIMM_START und T_DIMM legen das Zeitverhalten des Dimmers fest. |
| | Mit den Eingängen SET und RST kann der Ausgang Q jederzeit ein- oder ausgeschaltet werden. SET setzt den Ausgang OUT auf den durch VAL vorgegebenen Wert, RST setzt OUT auf 0, wenn die Setup-Variable RST_OUT auf TRUE gesetzt ist. RST schaltet zudem DBL auf FALSE. SET und RST können verwendet werden, um Brandmeldeanlagen oder Alarmanlagen anzuschließen. Mit SET können im Notfall alle Lichter zentral eingeschaltet oder beim Verlassen des Gebäudes mit RST ausgeschaltet werden. |
| | Beim Ein- und Ausschalten bleibt der letzte Ausgangswert des Dimmers am Ausgang OUT erhalten; nur ein FALSE am Ausgang Q schaltet das Licht aus, und ein TRUE an Q schaltet die Lampe wieder ein. Bei einem kurzen Tastendruck begrenzt das Modul den Ausgang OUT auf mindestens MIN_ON und maximal MAX_ON. Wenn der Dimmer zum Beispiel auf 0 steht, setzt das Gerät den Ausgang OUT automatisch auf 50 (Vorgabe MIN_ON) und umgekehrt wird der Ausgang OUT, wenn er höher als MAX_ON ist, auf MAX_ON begrenzt. |
| **Diese Parameter sollen verhindern, dass nach dem Einschalten ein sehr kleiner Wert am Ausgang OUT anliegt und Q aktiv ist, obwohl kein Licht leuchtet. Durch den Parameter MIN_ON wird ein Mindesthelligkeitswert beim Einschalten definiert. Umgekehrt wird zum Beispiel** | im Schlafzimmer durch MAX_ON verhindert, dass das Licht sofort nach dem Einschalten mit voller Helligkeit leuchtet. Wenn der Parameter SOFT_DIMM auf TRUE gesetzt ist, startet das Dimmen beim Einschalten mit einem langen Tastendruck jedes Mal bei 0. Zusätzlich zur Dimmerfunktion wird ein Doppelklick am Eingang IN dekodiert und der Ausgang DBL für einen Zyklus auf TRUE gesetzt. Wenn die Setup-Variable DBL_TOGGLE auf TRUE gesetzt ist, wird der Ausgang DBL bei jedem Doppelklick invertiert. |
| | Der Ausgang DBL kann verwendet werden, um zusätzliche Lasten oder Ereignisse mit einem Doppelklick zu schalten. Der Ausgang DBL kann auf den Eingang SET geschaltet werden, sodass der Dimmer durch einen Doppelklick auf einen vordefinierten Wert VAL gesetzt wird. OUT ist der Wert des Dimmers und ist als externe I/O-Variable definiert. Dies hat den Vorteil, dass der Dimmwert jederzeit extern geändert werden kann und auch nach einem Stromausfall rekonstruiert werden kann. OUT kann auf Wunsch remanent (retentive) und persistent definiert werden. |
| **Die folgende Tabelle zeigt den Betriebsstatus des Dimmers** |  |

![dimm_i](dimm_i.gif)

| IN | SET | RST | Q | DIR | DBL | OUT |
| --- | --- | --- | --- | --- | --- | --- |
| einfach | 0 | 0 | NOT Q | OUT<127 | - | LIMIT(MIN_ON,OUT,MAX_ON) |
| doppelt | 0 | 0 | - | - | TOGPULSE |  |
| lang | 0 | 0 | ON | NOT DIR | - | Rampe auf oder ab abhängig von DIR; startet bei 0, wenn SOFT_DIMM = TRUE und Q = 0; Richtungsumkehr, wenn 0 oder 255 erreicht wird |
| - | 1 | 0 | ON | OUT<127 | - | VAL |
| - | 0 | 1 | OFF | UP | OFF | 0 wenn RST_OUT = TRUE |
