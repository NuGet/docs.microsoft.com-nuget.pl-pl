---
title: Zmienne środowiskowe interfejsu wiersza polecenia NuGet
description: Odwołanie do zmiennych środowiskowych NuGet. exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: b04efaecce1d5bc892dfc48ae3e872d80aad209d
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/18/2019
ms.locfileid: "68328352"
---
# <a name="nuget-cli-environment-variables"></a>Zmienne środowiskowe interfejsu wiersza polecenia NuGet

Zachowanie interfejsu wiersza polecenia NuGet. exe można skonfigurować za pomocą kilku zmiennych środowiskowych, które mają wpływ na program NuGet. exe na poziomie komputera, użytkownika lub procesu. Zmienne środowiskowe zawsze zastępują wszystkie `NuGet.Config` ustawienia w plikach, co pozwala serwerom kompilacji zmieniać odpowiednie ustawienia bez modyfikowania plików.

Ogólnie rzecz biorąc, opcje określone bezpośrednio w wierszu polecenia lub w plikach konfiguracji NuGet mają pierwszeństwo, ale istnieje kilka wyjątków, takich jak *FORCE_NUGET_EXE_INTERACTIVE*. Jeśli okaże się, że plik NuGet. exe działa inaczej między różnymi komputerami, zmienna środowiskowa może być przyczyną. Na przykład usługa Azure Web Apps kudu (używana podczas wdrażania) ma ustawioną funkcję  *NUGET_XMLDOC_MODE* , aby przyspieszyć przywracanie pakietów i zaoszczędzić miejsce na dysku.

Interfejs wiersza polecenia NuGet używa programu MSBuild do odczytywania plików projektu. Wszystkie zmienne środowiskowe są dostępne jako [Właściwości](/visualstudio/msbuild/msbuild-command-line-reference) podczas obliczania programu MSBuild.
Listę właściwości udokumentowanych w [pakiecie NuGet oraz przywracania jako obiekty docelowe programu MSBuild](../msbuild-targets.md#restore-properties) można także ustawić jako zmienne środowiskowe.

| Zmienna | Opis | Uwagi |
| --- | --- | --- |
| http_proxy | Serwer proxy HTTP używany do operacji HTTP programu NuGet. | Zostanie to określone jako `http://<username>:<password>@proxy.com`. |
| no_proxy | Konfiguruje domeny do pomijania przy użyciu serwera proxy. | Określone jako domeny oddzielone przecinkami (,). |
| EnableNuGetPackageRestore | Flaga w przypadku, gdy program NuGet powinien niejawnie udzielić zgody, jeśli jest wymagany przez pakiet podczas przywracania. | Określona flaga jest traktowana jako *true* lub *1*, każda inna wartość traktowana jako flaga nie jest ustawiona. |
| NUGET_EXE_NO_PROMPT | Uniemożliwia programowi exe monitowanie o poświadczenia. | Wszystkie wartości poza wartością null lub pusty ciąg będą traktowane jako ten zestaw flag/true. |
| FORCE_NUGET_EXE_INTERACTIVE | Globalna zmienna środowiskowa aby wymusić tryb interaktywny. | Wszystkie wartości poza wartością null lub pusty ciąg będą traktowane jako ten zestaw flag/true. |
| NUGET_PACKAGES | Ścieżka do użycia dla folderu *Global-Packages* , zgodnie z opisem w temacie [Zarządzanie pakietami globalnymi i folderami pamięci](../../consume-packages/managing-the-global-packages-and-cache-folders.md)podręcznej. | Określono jako ścieżkę bezwzględną. |
| NUGET_FALLBACK_PACKAGES | Foldery globalnych pakietów bazowych. | Bezwzględne ścieżki folderu rozdzielone średnikami (;). |
| NUGET_HTTP_CACHE_PATH | Ścieżka do użycia dla folderu *pamięci podręcznej http* zgodnie z opisem w temacie [Zarządzanie pakietami globalnymi i folderami pamięci](../../consume-packages/managing-the-global-packages-and-cache-folders.md)podręcznej. | Określono jako ścieżkę bezwzględną. |
| NUGET_PERSIST_DG | Flaga oznaczająca, czy pliki DG (dane zbierane z programu MSBuild) powinny zostać utrwalone. | Określony jako *true* lub *false* (wartość domyślna), jeśli NUGET_PERSIST_DG_PATH nie jest ustawiony w katalogu tymczasowym (NuGetScratch folder w bieżącym katalogu tymczasowym środowiska). |
| NUGET_PERSIST_DG_PATH | Ścieżka do utrwalania plików DG. | Określona jako ścieżka bezwzględna, ta opcja jest używana tylko wtedy, gdy *NUGET_PERSIST_DG* ma wartość true. |
| NUGET_RESTORE_MSBUILD_ARGS | Ustawia dodatkowe argumenty MSBuild. | Przekazuj argumenty identyczne z sposobem przekazywania ich do programu MSBuild. exe. Przykładem ustawienia właściwości projektu foo z wiersza polecenia na pasek wartości będzie/p: foo = bar |
| NUGET_RESTORE_MSBUILD_VERBOSITY | Ustawia poziom szczegółowości dziennika programu MSBuild. | Wartość domyślna  to cicha ("/v: q"). Możliwe wartości *q [uiet]* , *m [inimal]* , *n [ormal]* , *d [egółowy]* i *diag [nostic]* . |
| NUGET_SHOW_STACK | Określa, czy pełny wyjątek (w tym ślad stosu) powinien być widoczny dla użytkownika. | Określony jako *true* lub *false* (wartość domyślna). |
| NUGET_XMLDOC_MODE | Określa, jak zestawy plików XML dokumentacji mają być obsługiwane. | Obsługiwane tryby są *pomijane* (nie Wyodrębniaj plików dokumentacji XML), *Kompresuj* (Przechowuj pliki doc XML jako archiwum zip) lub *none* (domyślnie Traktuj pliki doc XML jako zwykłe pliki). |
| NUGET_CERT_REVOCATION_MODE | Określa, w jaki sposób sprawdzanie stanu odwołania certyfikatu użytego do podpisania pakietu jest wykonywane podczas instalowania lub przywracania podpisanego pakietu. Gdy wartość nie jest ustawiona, `online`wartością domyślną jest.| Możliwe wartości *online* (domyślnie), *offline*.  Powiązane z [NU3028](../errors-and-warnings/NU3028.md) |

