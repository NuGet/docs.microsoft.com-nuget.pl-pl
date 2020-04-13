---
title: Korzystanie z pakietów z uwierzytelnionych kanałów informacyjnych
description: Korzystanie z pakietów z uwierzytelnionych kanałów informacyjnych we wszystkich scenariuszach klienta NuGet
author: nkolev92
ms.author: nikolev
ms.date: 02/28/2020
ms.topic: conceptual
ms.openlocfilehash: bb624ec6987dd5c6ee38d5bb7e01200487dd4bed
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "78231792"
---
# <a name="consuming-packages-from-authenticated-feeds"></a>Korzystanie z pakietów z uwierzytelnionych kanałów informacyjnych

Oprócz nuget.org [publicznych kanałów informacyjnych,](https://api.nuget.org/v3/index.json)klienci NuGet mają możliwość interakcji z plikami danych i prywatnymi źródłami http.


Aby uwierzytelnić się za pomocą prywatnych kanałów http, 2 podejścia są:

* Dodawanie poświadczeń w pliku [NuGet.config](../reference/nuget-config-file.md#packagesourcecredentials)
* Uwierzytelnij się przy użyciu jednego z wielu modeli rozszerzalności w zależności od używanego klienta.

## <a name="nuget-clients-authentication-extensibility"></a>Rozszerzalność uwierzytelniania klientów NuGet

Dla różnych klientów NuGet sam dostawca prywatnego źródła danych jest odpowiedzialny za uwierzytelnianie.
Wszystkie klienci NuGet mają metody rozszerzalności do obsługi tego. Są to rozszerzenie programu Visual Studio lub wtyczki, które mogą komunikować się z NuGet do pobierania poświadczeń.

### <a name="visual-studio"></a>Visual Studio

W programie Visual Studio NuGet udostępnia interfejs, który dostawcy kanałów informacyjnych można zaimplementować i dostarczyć do swoich klientów. Aby uzyskać więcej informacji, zapoznaj się z [dokumentacją dotyczącą tworzenia dostawcy poświadczeń programu Visual Studio.](../reference/extensibility/NuGet-Credential-Providers-for-Visual-Studio.md)

#### <a name="available-nuget-credential-providers-for-visual-studio"></a>Dostępne dostawców poświadczeń NuGet dla programu Visual Studio

Istnieje dostawca poświadczeń wbudowany w programie Visual Studio do obsługi usługi Azure DevOps.


Wśród dostawców poświadczeń dostępnych dodatków dodatku plug-in są:

* [Dostawca poświadczeń MyGet dla programu Visual Studio](http://docs.myget.org/docs/reference/credential-provider-for-visual-studio)

### <a name="nugetexe"></a>nuget.exe

Gdy `nuget.exe` potrzebne poświadczenia do uwierzytelniania za pomocą pliku danych, wyszukuje je w następujący sposób:

1. Poszukaj `NuGet.config` poświadczeń w plikach.
1. Korzystanie z dostawców poświadczeń dodatku plug-in w wersji 2
1. Korzystanie z dostawców poświadczeń dodatku plug 1
1. Następnie NuGet monituje użytkownika o poświadczenia w wierszu polecenia.

#### <a name="nugetexe-and-v2-credential-providers"></a>dostawcy poświadczeń nuget.exe i V2

W `4.8` wersji NuGet zdefiniowano nowy mechanizm wtyczki uwierzytelniania, dalej określane jako dostawców poświadczeń V2.
Aby uzyskać informacje na temat instalacji i wykrywania tych dostawców, zobacz [wtyczki platformy wieloplatformowej NuGet](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).

#### <a name="nugetexe-and-v1-credential-providers"></a>dostawcy poświadczeń nuget.exe i V1

W `3.3` wersji NuGet wprowadzono pierwszą wersję wtyczek uwierzytelniania.
W przypadku instalacji i odnajdywania tych dostawców można znaleźć w [u dostawców poświadczeń nuget.exe](../reference/extensibility/nuget-exe-Credential-Providers.md#nugetexe-credential-provider-discovery)

#### <a name="available-credential-providers-for-nugetexe"></a>Dostawcy poświadczeń dostępnych dla pliku nuget.exe

* [Dostawcy poświadczeń usługi Azure DevOps w wersji V2](/azure/devops/artifacts/nuget/nuget-exe?view=azure-devops#add-a-feed-to-nuget-482-or-later) lub [dostawca poświadczeń artefaktów platformy Azure](https://github.com/microsoft/artifacts-credprovider)

W programie Visual Studio 2017 w wersji 15.9 lub nowszej dostawca poświadczeń usługi Azure DevOps jest dołączany do programu Visual Studio.
Jeśli `nuget.exe` używa MSBuild z tego konkretnego zestawu narzędzi programu Visual Studio, wtyczka zostanie wykryta automatycznie.

### <a name="dotnetexe"></a>plik dotnet.exe

Gdy `dotnet.exe` potrzebne poświadczenia do uwierzytelniania za pomocą pliku danych, wyszukuje je w następujący sposób:

1. Poszukaj `NuGet.config` poświadczeń w plikach.
1. Korzystanie z dostawców poświadczeń dodatku plug-in w wersji 2

Domyślnie `dotnet.exe` nie jest interaktywna, więc `--interactive` może być konieczne przekazanie flagi, aby narzędzie do blokowania do uwierzytelniania.

#### <a name="dotnetexe-and-v2-credential-providers"></a>Dostawcy poświadczeń dotnet.exe i V2

W `2.2.100` wersji SDK NuGet zdefiniowane mechanizm wtyczki uwierzytelniania, który działa we wszystkich klientach.
Aby uzyskać informacje na temat instalacji i wykrywania tych dostawców, zobacz [wtyczki platformy wieloplatformowej NuGet](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).

#### <a name="available-credential-providers-for-dotnetexe"></a>Dostawcy poświadczeń dostępnych dla programu dotnet.exe

* [Dostawca poświadczeń artefaktów platformy Azure](https://github.com/microsoft/artifacts-credprovider)

### <a name="msbuildexe"></a>Msbuild.exe

Gdy `MSBuild.exe` potrzebne poświadczenia do uwierzytelniania za pomocą pliku danych, wyszukuje je w następujący sposób:

1. Szukaj poświadczeń w `NuGet.config` plikach
1. Korzystanie z dostawców poświadczeń dodatku plug-in w wersji 2

Domyślnie `MSBuild.exe` nie jest interaktywna, więc `/p:NuGetInteractive=true` może być konieczne ustawienie właściwości, aby narzędzie do blokowania uwierzytelniania.

#### <a name="msbuildexe-and-v2-credential-providers"></a>Dostawcy poświadczeń MSBuild.exe i V2

W programie Visual Studio 2019 Update 9 NuGet zdefiniował mechanizm wtyczki uwierzytelniania, który działa na wszystkich klientach.
Aby uzyskać informacje na temat instalacji i wykrywania tych dostawców, zobacz [wtyczki platformy wieloplatformowej NuGet](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).

#### <a name="available-credential-providers-for-msbuildexe"></a>Dostawcy poświadczeń dla programu MSBuild.exe

* [Dostawca poświadczeń artefaktów platformy Azure](https://github.com/microsoft/artifacts-credprovider)

Z visual studio 2017 Update 9 i nowsze, dostawca poświadczeń usługi Azure DevOps jest w pakiecie w programie Visual Studio. Nie są wymagane żadne dodatkowe kroki.
