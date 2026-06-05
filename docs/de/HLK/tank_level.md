<!--
  Copyright (c) 2026 Hans Mühlbauer, Franz Höpfinger and others.

  This program and the accompanying materials are made available under the
  terms of the Eclipse Public License 2.0 which is available at
  https://www.eclipse.org/legal/epl-2.0

  SPDX-License-Identifier: EPL-2.0
-->

## TANK_LEVEL

| | |
|:---|:---|
| **Type** | Funktionsbaustein |
| **Input	LEVEL** | BOOL (Eingang für Niveau Sensor) |
| **LEAK** | BOOL (Eingang für Leck Sensoren) |
| **ACLR** | BOOL (Eingang zum Rücksetzen des Alarms) |
| **Output	VALVE** | BOOL (Ausgangssignal zum Ventil) |
| **ALARM** | BOOL (Alarmausgang) |
| **STATUS** | BYTE (ESR kompatibler Status Ausgang) |
| | TANK_LEVEL dient dazu den Flüssigkeitsstand in einem Tank konstant zu halten. Am Eingang LEVEL wird der Niveausensor angeschlossen und am Ausgang VALVE das Nachspeiseventil. Um bei unruhigen Oberflächen den Niveausensor zu entprellen kann dessen Ansprechzeit mittels der Setup Variable LEVEL_DELAY_TIME entsprechend eingestellt werden. Am Eingang LEVEL wird mit TRUE angezeigt das der Flüssigkeitsstand zu niedrig ist, nachdem der Eingang durchgehend für Die Zeit LEVEL_DELAY_TIME auf TRUE war wird der Ausgang VALVE auf TRUE gesetzt um Flüssigkeit nachzuspeisen. Während des Nachspeisevorgangs wird MAX_VALVE_TIME überwacht und falls VALVE länger als diese Zeit auf TRUE bleibt wird ein ALARM generiert um bei Sensorfehlern oder Lecks ein Dauerndes Nachspeisen zu verhindern. Der Baustein überwacht zusätzlich den Eingang LEAK welcher für normalen Betrieb immer FALSE sein muss. Sobald LEAK auf TRUE geht wird sofort die Nachspeisung unterbrochen und ein Alarm generiert. LEAK dient zum Anschluß von Lecksensoren und oder zusätzlichen Niveausensoren oberhalb des normalen Niveaus. Tritt im Betrieb ein Alarm auf so stoppt de Baustein jegliche Nachspeisung bis der Fehler beseitigt wurde und der Eingang ACLR kurz auf TRUE getastet wird. Am ESR kompatiblen Statusausgang werden alle Betriebszustände mittels ESR Meldungen ausgegeben. |
| | STATUS = 1, Lecksensor (LEAK) ist aktiviert. |
| | STATUS = 2, Nachspeisezeit (MAX_VALVE_TIME) wurde überschritten. |
| | STATUS = 100, Niveau ist erreicht, Nachspeisung abgeschaltet. |
| | STATUS = 101, ACLR wurde betätigt. |
| | STATUS = 102, Niveau unterschritten, Nachspeisung läuft. |
| **Setup** | MAX_VALVE_TIME (Maximale Nachspeisezeit für Ventil) |
| **LEVEL_DELAY_TIME** | TIME (Ansprechzeit für LEVEL Eingang) |

![tank_level](tank_level.gif)
