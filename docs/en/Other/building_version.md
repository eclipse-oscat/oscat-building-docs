<!--
  Copyright (c) 2026 Hans Mühlbauer, Franz Höpfinger and others.

  This program and the accompanying materials are made available under the
  terms of the Eclipse Public License 2.0 which is available at
  https://www.eclipse.org/legal/epl-2.0

  SPDX-License-Identifier: EPL-2.0
-->

## BUILDING_VERSION

| | |
|:---|:---|
| **Type	Function** | DWORD |
| **Input	IN** | BOOL (if TRUE the module provides the   release date) |
| **Output** | (Version of the library) |
| | BUILDING_VERSION provides if IN = FALSE the current version number as DWORD. If IN is set to TRUE then the  release  date of the current version as a DWORD is returned. |

![building_version](building_version.gif)

**Example:**

Example:	BUILDING_VERSION(FALSE) = 100 for Version 1.00

DWORD_TO_DATE(OSCAT_VERSION(TRUE)) = 2011-1-30
