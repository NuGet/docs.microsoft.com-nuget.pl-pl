---
title: "Zmienne środowiskowe interfejsu wiersza polecenia NuGet | Dokumentacja firmy Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Informacje dotyczące zmiennych środowiskowych nuget.exe"
keywords: "zmienne środowiskowe nuget"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 516a66103d6159a3d68b5383090e8e3b519a5588
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-cli-environment-variables"></a>Zmienne środowiskowe NuGet interfejsu wiersza polecenia

Zachowanie nuget.exe interfejsu wiersza polecenia można skonfigurować za pośrednictwem kilku zmiennych środowiskowych, które mają wpływ na nuget.exe komputera, użytkownika lub przetwarzania poziomów.

Ogólnie rzecz biorąc, opcje określone bezpośrednio w wierszu polecenia lub w plikach konfiguracji NuGet mają pierwszeństwo przed, ale istnieją takie jak kilka wyjątków *FORCE_NUGET_EXE_INTERACTIVE*. Jeśli okaże się, że ten nuget.exe zachowuje się inaczej między komputerami, zmiennej środowiskowej może być przyczyną. Na przykład Kudu aplikacji sieci Web platformy Azure (używane podczas wdrażania) ma *NUGET_XMLDOC_MODE* ustawioną *pominąć* przyspieszenia wydajności przywracania pakietu i zaoszczędzić miejsce na dysku.

| Zmienna | Opis | Uwagi |
| --- | --- | --- |
| http_proxy | Serwer proxy HTTP używany do wykonywania operacji NuGet HTTP. | Może to być określone jako `http://<username>:<password>@proxy.com`. |
| no_proxy | Konfiguruje domen do pominięcia z przy użyciu serwera proxy. | Określony jako domen rozdzielonych przecinkami (,). |
| EnableNuGetPackageRestore | Flaga dla, jeśli NuGet niejawnie należy udzielić zgody, jeśli jest to wymagane pakietu podczas przywracania. | Określona flaga jest określona. | jako *true* lub *1*, inne wartość traktowane jako flagi nie została określona. |
| NUGET_EXE_NO_PROMPT | Zapobiega exe dla monit o podanie poświadczeń.| Żadnej wartości, z wyjątkiem null lub pusty ciąg będzie traktowany jako flagi zestawu/wartość true. |
FORCE_NUGET_EXE_INTERACTIVE | Zmienna środowiskowa globalne wymuszenie tryb interaktywny. | Żadnej wartości, z wyjątkiem null lub pusty ciąg będzie traktowany jako flagi zestawu/wartość true. |
| NUGET_PACKAGES | Ścieżka do gdy pakiety są przechowywane / w pamięci podręcznej. | Określony jako ścieżka bezwzględna. |
| NUGET_FALLBACK_PACKAGES | Foldery globalne pakietów rezerwowego. | Ścieżki bezwzględne folderu rozdzielonych średnikami (;). |
| NUGET_HTTP_CACHE_PATH | Folder pamięci podręcznej HTTP. | Określony jako ścieżka bezwzględna. |
| NUGET_PERSIST_DG | Flaga wskazująca, czy powinny zostać utrwalony dg plików (dane zbierane z MSBuild). | Określony jako *true* lub *false* (ustawienie domyślne), jeśli NUGET_PERSIST_DG_PATH nie będą przechowywane w katalogu tymczasowego (NuGetScratch folder w bieżącym katalogu tymczasowego środowiska). |
| NUGET_PERSIST_DG_PATH | Ścieżka do utrwalenia pliki grupy dystrybucyjnej. | Określony jako ścieżka bezwzględna, ta opcja jest tylko do użycia podczas *NUGET_PERSIST_DG* jest ustawiona na true. |
| NUGET_RESTORE_MSBUILD_ARGS | Ustawia dodatkowe argumenty programu MSBuild. |
| NUGET_RESTORE_MSBUILD_| Szczegółowość |Ustawia poziom szczegółowości dziennika programu MSBuild. | Domyślnie jest *quiet* ("/ v: q"). Możliwe wartości *q [uiet]*, *m [najmniej]*, *n [ormal]*, *d [egółowy]*, i *diag [nostic]*. |
| NUGET_SHOW_STACK | Określa, czy pełny wyjątek (w tym ślad stosu) powinna być wyświetlana użytkownikowi. | Określony jako *true* lub *false* (ustawienie domyślne). |
| NUGET_XMLDOC_MODE | Określa sposób obsługi wyodrębniania pliku dokumentacji XML zestawów. | Obsługiwane tryby to *pominąć* (nie wyodrębnić pliki dokumentacji XML), *Kompresuj* (przechowywać pliki dokumentu XML jako archiwum zip) lub *Brak* (domyślna, Traktuj pliki dokumentu XML jako zwykły pliki). |
