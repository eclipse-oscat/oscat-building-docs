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
| **Input	SET** | BOOL (Eingang zum Einschalten des Ausgangs auf 100%) |
| **IN** | BOOL (Steuereingang für Taster) |
| **RST** | BOOL (Eingang zum Ausschalten des Ausgangs) |
| **Output	Q** | BOOL (Schaltausgang) |
| **Setup	T_DEBOUNCE** | TIME (Entprellzeit für Taster) |
| **T_RESetup** | TIME (Rekonfigurationszeit) |
| **T_ON_MAX** | TIME (Einschaltbegrenzung) |
| | SWITCH_I ist ein intelligenter Schalter der sich selbsttätig auf den angeschlossenen Taster oder Schalter einstellt. Wird ein Schalter angeschlossen, so folgt der Ausgang jeder Schaltflanke des Schalters. Wird jedoch ein Taster angeschlossen, so erkennt SWITCH_I selbst, ob es ein Öffner oder Schließer ist und wertet dann nur die jeweils erste Flanke aus. Die Setup-Variable T_ON_MAX legt fest, nach welcher Zeit der Ausgang automatisch wieder ausgeschaltet werden soll. Mit den Eingängen SET und RST kann der Ausgang jederzeit auf 100% ein oder ausgeschaltet werden. Anwendungsbeispiele sind die Meldung von Rauchmeldern oder Alarmanlagen. Die Zeit T_DEBOUNCE dient zum Entprellen des Tasters und ist standardmäßig auf 10ms eingestellt. Die Zeit T_RESetup wird verwendet, um zu entscheiden, ob ein Schließer oder Öffner am Eingang IN angeschlossen ist. Bleibt der Eingang länger als diese Zeit in einem Zustand, so wird dies als Ruhestellung angenommen. |

![switch_I](switch_I.gif)
