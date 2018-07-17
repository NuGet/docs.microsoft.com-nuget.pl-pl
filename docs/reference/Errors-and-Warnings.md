---
title: Skorowidz ostrzeżenia i błędy NuGet
description: Pełna dokumentacja ostrzeżenia i błędy wygenerowane z pakietu NuGet podczas różnych operacji NuGet.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 05/18/2018
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: a787d036f7682b54adb30140152655fe165ee161
ms.sourcegitcommit: a76ecc58f41c2c5b3536ff4a3f3fcbdf5258177c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/17/2018
ms.locfileid: "39069664"
---
# <a name="errors-and-warnings"></a>Błędy i ostrzeżenia

W 4.3.0+ NuGet błędy i ostrzeżenia są ponumerowane, zgodnie z opisem w tym temacie i zawierają szczegółowe informacje, aby pomóc Ci rozwiązać problemy związane z.

Błędy i ostrzeżenia, wymienione w tym miejscu są dostępne tylko w przypadku [oparte na funkcji PackageReference](../consume-packages/package-references-in-project-files.md) projektów i NuGet 4.3.0+. NuGet honoruje także właściwości programu MSBuild do pomijania ostrzeżeń albo podnoszenie ich poziomu do błędów. Aby uzyskać więcej informacji, zobacz [porady: pomijanie ostrzeżeń kompilatora](/visualstudio/ide/how-to-suppress-compiler-warnings) w dokumentacji programu Visual Studio.

**Błędy**

| Grupa | Błąd liczby |
| --- | --- |
| Nieprawidłowy błędy wejścia | [NU1001](./errors-and-warnings/NU1001.md), [NU1002](./errors-and-warnings/NU1002.md), [NU1003](./errors-and-warnings/NU1003.md) |
| Brak błędów pakietu i projekt | [NU1100](./errors-and-warnings/NU1100.md), [NU1101](./errors-and-warnings/NU1101.md), [NU1102](./errors-and-warnings/NU1102.md), [NU1103](./errors-and-warnings/NU1103.md), [NU1104](./errors-and-warnings/NU1104.md), [NU1105](./errors-and-warnings/NU1105.md), [NU1106](./errors-and-warnings/NU1106.md), [NU1107](./errors-and-warnings/NU1107.md), [NU1108](./errors-and-warnings/NU1108.md) |
| Błędy zgodności | [NU1201](./errors-and-warnings/NU1201.md), [NU1202](./errors-and-warnings/NU1202.md), [NU1203](./errors-and-warnings/NU1203.md), [NU1401](./errors-and-warnings/NU1401.md) |
| Wewnętrzne błędy NuGet | [NU1000](./errors-and-warnings/NU1000.md) |
| Błędy podpisanych pakietów (Tworzenie i weryfikacji) | [NU3000](./errors-and-warnings/NU3000.md), [NU3001](./errors-and-warnings/NU3001.md), [NU3004](./errors-and-warnings/NU3004.md), [NU3008](./errors-and-warnings/NU3008.md) |

**Ostrzeżenia**

| Grupa | Numery ostrzeżeń |
| --- | --- |
| Nieprawidłowy ostrzeżenia danych wejściowych | [NU1501](./errors-and-warnings/NU1501.md), [NU1502](./errors-and-warnings/NU1502.md), [NU1503](./errors-and-warnings/NU1503.md) |
| Nieoczekiwany pakiet wersji ostrzeżenia | [NU1601](./errors-and-warnings/NU1601.md), [NU1602](./errors-and-warnings/NU1602.md), [NU1603](./errors-and-warnings/NU1603.md), [NU1604](./errors-and-warnings/NU1604.md), [NU1605](./errors-and-warnings/NU1605.md), [NU1606](./errors-and-warnings/NU1108.md), [NU1607](./errors-and-warnings/NU1107.md) |
| Mechanizm rozpoznawania konfliktu ostrzeżenia | [NU1608](./errors-and-warnings/NU1608.md) |
| Ostrzeżenia dotyczące rezerwowego pakietu | [NU1701](./errors-and-warnings/NU1701.md) |
| Ostrzeżenia dotyczące kanału informacyjnego | [NU1801](./errors-and-warnings/NU1801.md) |
| Ostrzeżenia wewnętrznego NuGet | [NU1500](./errors-and-warnings/NU1500.md) |
| Ostrzeżenia podpisanych pakietów (Tworzenie i weryfikacji) | [NU3002](./errors-and-warnings/NU3002.md), [NU3018](./errors-and-warnings/NU3018.md), [NU3028](./errors-and-warnings/NU3028.md) |
