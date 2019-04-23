---
title: Zmienne środowiskowe interfejsu wiersza polecenia NuGet
description: Odwołania do zmiennych środowiskowych nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: ac1bf2b65ab6ec4e8cf864810181fc661236262a
ms.sourcegitcommit: 6b71926f062ecddb8729ef8567baf67fd269642a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/22/2019
ms.locfileid: "59931985"
---
# <a name="nuget-cli-environment-variables"></a>Zmienne środowiskowe interfejsu wiersza polecenia NuGet

Zachowanie nuget.exe interfejsu wiersza polecenia można skonfigurować pewne zmienne środowiskowe, które mają wpływ na nuget.exe całego komputera, użytkownika lub przetworzyć poziomów. Zmienne środowiskowe zawsze zastępuje wszelkie ustawienia w `NuGet.Config` plików, dzięki czemu serwer kompilacji z usługą Zmień odpowiednie ustawienia bez modyfikowania żadnych plików.

Ogólnie rzecz biorąc, opcje określone bezpośrednio w wierszu polecenia lub w plikach konfiguracyjnych NuGet ma pierwszeństwo, ale istnieje kilka wyjątków takich jak *FORCE_NUGET_EXE_INTERACTIVE*. Okaże się, że ten nuget.exe zachowuje się inaczej między komputerami, przyczyną może być zmienną środowiskową. Na przykład Azure Web Apps Kudu, (używane podczas wdrażania) ma *NUGET_XMLDOC_MODE* równa *pominąć* wydajność przywracania pakietów i zaoszczędzić miejsce na dysku.

Interfejs wiersza polecenia NuGet używa programu MSBuild, aby odczytywać pliki projektu. Wszystkie zmienne środowiskowe są dostępne jako [właściwości](/visualstudio/msbuild/msbuild-command-line-reference) podczas oceny MSBuild.
Lista właściwości, które opisano w [NuGet pakowanie i przywrócić jako elementów docelowych MSBuild](../reference/msbuild-targets.md#restore-properties) może być także ustawiona jako zmienne środowiskowe.

| Zmienna | Opis | Uwagi |
| --- | --- | --- |
| http_proxy | Serwer proxy HTTP jest używany do wykonywania operacji HTTP w programie NuGet. | To może być określony jako `http://<username>:<password>@proxy.com`. |
| no_proxy | Służy do konfigurowania domen w celu obejścia z przy użyciu serwera proxy. | Określony jako domen rozdzielonych przecinkami (,). |
| EnableNuGetPackageRestore | Flaga Jeśli NuGet niejawnie należy udzielić zgody, jeśli jest to wymagane pakietu podczas przywracania. | Określona flaga jest traktowany jako *true* lub *1*, wszelkie inne wartości traktowane jako flaga nie jest ustawiona. |
| NUGET_EXE_NO_PROMPT | Zapobiega exe dla monit o podanie poświadczeń. | Dowolna wartość, z wyjątkiem null lub pusty ciąg, będzie traktowane jako flaga zestawu/wartość true. |
| FORCE_NUGET_EXE_INTERACTIVE | Zmienna środowiskowa globalnego wymusić tryb interakcyjny. | Dowolna wartość, z wyjątkiem null lub pusty ciąg, będzie traktowane jako flaga zestawu/wartość true. |
| NUGET_PACKAGES | Ścieżkę do użycia dla *globalnymi pakietami* folderu zgodnie z opisem na [Zarządzanie globalnymi pakietami i folderami pamięci podręcznej](../consume-packages/managing-the-global-packages-and-cache-folders.md). | Określony jako ścieżka bezwzględna. |
| NUGET_FALLBACK_PACKAGES | Foldery globalnymi pakietami rezerwowego. | Ścieżki bezwzględne folderów, oddzielone średnikami (;). |
| NUGET_HTTP_CACHE_PATH | Ścieżkę do użycia dla *pamięci podręcznej http* folderu zgodnie z opisem na [Zarządzanie globalnymi pakietami i folderami pamięci podręcznej](../consume-packages/managing-the-global-packages-and-cache-folders.md). | Określony jako ścieżka bezwzględna. |
| NUGET_PERSIST_DG | Flaga wskazująca, czy powinny zostać utrwalone dg pliki (dane zbierane z programu MSBuild). | Określony jako *true* lub *false* (ustawienie domyślne), jeśli NUGET_PERSIST_DG_PATH nie będą przechowywane do katalogu tymczasowego (NuGetScratch folder w bieżącym katalogu temp środowiska). |
| NUGET_PERSIST_DG_PATH | Ścieżka do utrwalania plików członkowstwa. | Określony jako ścieżka bezwzględna, ta opcja jest tylko do użycia podczas *NUGET_PERSIST_DG* jest ustawiona na wartość true. |
| NUGET_RESTORE_MSBUILD_ARGS | Ustawia dodatkowe argumenty programu MSBuild. | |
| NUGET_RESTORE_MSBUILD_VERBOSITY | Ustawia poziom szczegółowości dziennika MSBuild. | Wartość domyślna to *cichy* ("/ v: q"). Możliwe wartości *q [uiet]*, *m [najmniej]*, *n [ormal]*, *d [egółowy]*, i *diag [Diagnostyka]*. |
| NUGET_SHOW_STACK | Określa, czy pełny wyjątek (w tym ślad stosu) powinna być wyświetlana użytkownikowi. | Określony jako *true* lub *false* (ustawienie domyślne). |
| NUGET_XMLDOC_MODE | Określa sposób obsługi wyodrębniania pliku dokumentacji XML zestawów. | Tryby obsługiwane są *pominąć* (nie wyodrębnić pliki dokumentacji XML), *skompresować* (przechowywać pliki dokumentacji XML jako archiwum zip) lub *Brak* (domyślnie, Traktuj pliki dokumentacji XML jako zwykłych pliki). |
| NUGET_CERT_REVOCATION_MODE | Określa, jak sprawdzanie stanu odwołania certyfikatu używanego do podpisania pakietu, odbywa się po zainstalowaniu lub przywrócić podpisanych pakietów. Gdy nie są ustawione, wartość domyślna to `online`.| Możliwe wartości *online* (ustawienie domyślne), *offline*.  Powiązane z [NU3028](../reference/errors-and-warnings/NU3028.md) |

