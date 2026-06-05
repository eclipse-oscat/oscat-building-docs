<!--
  Copyright (c) 2026 Hans Mühlbauer, Franz Höpfinger and others.

  This program and the accompanying materials are made available under the
  terms of the Eclipse Public License 2.0 which is available at
  https://www.eclipse.org/legal/epl-2.0

  SPDX-License-Identifier: EPL-2.0
-->
# OSCAT Building Documentation

Dieses Repository enthält die Dokumentation für die **OSCAT Building Library**.

Die Dokumentation ist verfügbar unter: [https://oscat-building.readthedocs.io](https://oscat-building.readthedocs.io)

## Kategorien

- **HLK** - Heizung, Lüftung, Klimatechnik
- **Jalousie** - Jalousie- und Rollladensteuerung
- **actuators** - Aktoren und Stellglieder
- **electrical** - Elektroinstallation und Schaltungen
- **Other** - Sonstige Funktionen

## Lokale Entwicklung

```bash
pip install -r docs/requirements.txt
mkdocs serve -f docs/en/mkdocs.yml  # or: mkdocs serve -f docs/de/mkdocs.yml
```

## Lizenz

Eclipse Public License 2.0
