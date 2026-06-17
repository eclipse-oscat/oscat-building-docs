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

- [📄 PDF Deutsch (oscat-building-docs-de.pdf)](https://eclipse-oscat.github.io/oscat-building-docs/de/pdf/oscat-building-docs-de.pdf)
- [📄 PDF English (oscat-building-docs-en.pdf)](https://eclipse-oscat.github.io/oscat-building-docs/en/pdf/oscat-building-docs-en.pdf)
- [GitHub Repository](https://github.com/eclipse-oscat/oscat-building-docs)


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
