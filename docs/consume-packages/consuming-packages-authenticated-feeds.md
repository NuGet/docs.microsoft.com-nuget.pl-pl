---
title: Używanie pakietów z uwierzytelnionych kanałów informacyjnych
description: Zużywanie pakietów ze źródeł uwierzytelnionych we wszystkich scenariuszach klienta NuGet
author: nkolev92
ms.author: nikolev
ms.date: 02/28/2020
ms.topic: conceptual
ms.openlocfilehash: bb624ec6987dd5c6ee38d5bb7e01200487dd4bed
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/02/2020
ms.locfileid: "78231792"
---
# <a name="consuming-packages-from-authenticated-feeds"></a>Używanie pakietów z uwierzytelnionych kanałów informacyjnych

Oprócz [publicznego kanału informacyjnego](https://api.nuget.org/v3/index.json)NuGet.org klienci programu NuGet mogą korzystać ze źródeł danych i prywatnych źródeł http.


Aby uwierzytelnić się za pomocą prywatnych źródeł http, dwa podejścia są następujące:

* Dodaj poświadczenia w [pliku NuGet. config](../reference/nuget-config-file.md#packagesourcecredentials)
* Uwierzytelnianie przy użyciu jednego z wielu modeli rozszerzalności w zależności od używanego klienta programu.

## <a name="nuget-clients-authentication-extensibility"></a>Rozszerzalność uwierzytelniania klientów NuGet

W przypadku różnych klientów programu NuGet sam dostawca kanału informacyjnego jest odpowiedzialny za uwierzytelnianie.
Wszyscy klienci NuGet mają metody rozszerzalności obsługujące ten program. Są to rozszerzenia programu Visual Studio lub wtyczka, która może komunikować się z pakietem NuGet w celu pobierania poświadczeń.

### <a name="visual-studio"></a>Visual Studio

W programie Visual Studio pakiet NuGet udostępnia interfejs, który dostawcy kanału informacyjnego mogą zaimplementować i udostępnić klientom. Aby uzyskać więcej informacji, zapoznaj się z dokumentacją dotyczącą [tworzenia dostawcy poświadczeń programu Visual Studio](../reference/extensibility/NuGet-Credential-Providers-for-Visual-Studio.md).

#### <a name="available-nuget-credential-providers-for-visual-studio"></a>Dostępni dostawcy poświadczeń NuGet dla programu Visual Studio

Istnieje Dostawca poświadczeń wbudowany w program Visual Studio w celu obsługi usługi Azure DevOps.


Dostępne są następujące dostawcy poświadczeń wtyczek:

* [Dostawca poświadczeń MyGet dla programu Visual Studio](http://docs.myget.org/docs/reference/credential-provider-for-visual-studio)

### <a name="nugetexe"></a>nuget.exe

Gdy `nuget.exe` wymaga poświadczeń do uwierzytelnienia ze źródłem danych, wygląda w następujący sposób:

1. Wyszukaj poświadczenia w plikach `NuGet.config`.
1. Użyj dostawców poświadczeń wtyczek v2
1. Użyj dostawców poświadczeń wtyczki w wersji 1
1. Następnie pakiet NuGet monituje użytkownika o poświadczenia w wierszu polecenia.

#### <a name="nugetexe-and-v2-credential-providers"></a>dostawcy poświadczeń NuGet. exe i v2

W wersji `4.8` NuGet zdefiniowano nowy mechanizm wtyczek uwierzytelniania, zwany dalej dostawcą poświadczeń w wersji 2.
Aby przeprowadzić instalację i odnajdywanie tych dostawców, zapoznaj się z [dodatkami międzyplatformowymi NuGet](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).

#### <a name="nugetexe-and-v1-credential-providers"></a>dostawcy poświadczeń NuGet. exe i v1

W wersji `3.3` NuGet wprowadził pierwszą wersję wtyczek uwierzytelniania.
Na potrzeby instalacji i odnajdywania tych dostawców odwołują się do [dostawców poświadczeń NuGet. exe](../reference/extensibility/nuget-exe-Credential-Providers.md#nugetexe-credential-provider-discovery)

#### <a name="available-credential-providers-for-nugetexe"></a>Dostępni dostawcy poświadczeń dla programu NuGet. exe

* Dostawcy [poświadczeń usługi Azure DevOps v2](/azure/devops/artifacts/nuget/nuget-exe?view=azure-devops#add-a-feed-to-nuget-482-or-later) lub [Dostawca poświadczeń Azure Artifacts](https://github.com/microsoft/artifacts-credprovider)

W programie Visual Studio 2017 w wersji 15,9 lub nowszej Dostawca poświadczeń usługi Azure DevOps jest powiązany z programem Visual Studio.
Jeśli `nuget.exe` używa programu MSBuild z tego konkretnego zestawu narzędzi programu Visual Studio, Wtyczka zostanie odnaleziona automatycznie.

### <a name="dotnetexe"></a>dotnet.exe

Gdy `dotnet.exe` wymaga poświadczeń do uwierzytelnienia ze źródłem danych, wygląda w następujący sposób:

1. Wyszukaj poświadczenia w plikach `NuGet.config`.
1. Użyj dostawców poświadczeń wtyczek v2

Domyślnie `dotnet.exe` nie jest interaktywna, więc może być konieczne przekazanie flagi `--interactive` w celu uzyskania narzędzia do zablokowania uwierzytelniania.

#### <a name="dotnetexe-and-v2-credential-providers"></a>dostawcy poświadczeń dotnet. exe i v2

W wersji `2.2.100` zestawu SDK pakiet NuGet definiuje mechanizm wtyczki uwierzytelniania, który działa na wszystkich klientach.
Aby przeprowadzić instalację i odnajdywanie tych dostawców, zapoznaj się z [dodatkami międzyplatformowymi NuGet](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).

#### <a name="available-credential-providers-for-dotnetexe"></a>Dostępni dostawcy poświadczeń dla programu dotnet. exe

* [Dostawca poświadczeń Azure Artifacts](https://github.com/microsoft/artifacts-credprovider)

### <a name="msbuildexe"></a>MSBuild. exe

Gdy `MSBuild.exe` wymaga poświadczeń do uwierzytelnienia ze źródłem danych, wygląda w następujący sposób:

1. Wyszukaj poświadczenia w plikach `NuGet.config`
1. Użyj dostawców poświadczeń wtyczek v2

Domyślnie `MSBuild.exe` nie jest interaktywna, więc może być konieczne ustawienie właściwości `/p:NuGetInteractive=true` w celu zablokowania uwierzytelniania.

#### <a name="msbuildexe-and-v2-credential-providers"></a>Dostawcy poświadczeń MSBuild. exe i v2

W programie Visual Studio 2019 Update 9 pakiet NuGet definiuje mechanizm wtyczki uwierzytelniania, który działa na wszystkich klientach.
Aby przeprowadzić instalację i odnajdywanie tych dostawców, zapoznaj się z [dodatkami międzyplatformowymi NuGet](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).

#### <a name="available-credential-providers-for-msbuildexe"></a>Dostępni dostawcy poświadczeń dla programu MSBuild. exe

* [Dostawca poświadczeń Azure Artifacts](https://github.com/microsoft/artifacts-credprovider)

W programie Visual Studio 2017 Update 9 lub nowszym Dostawca poświadczeń usługi Azure DevOps jest powiązany z programem Visual Studio. Nie są wymagane żadne dodatkowe czynności.
