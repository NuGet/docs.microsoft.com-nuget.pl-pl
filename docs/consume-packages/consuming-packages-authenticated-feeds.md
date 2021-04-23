---
title: Korzystanie z pakietów z uwierzytelnionych źródeł danych
description: Korzystanie z pakietów z uwierzytelnionych źródeł danych we wszystkich scenariuszach klienta NuGet
author: nkolev92
ms.author: nikolev
ms.date: 02/28/2020
ms.topic: conceptual
ms.openlocfilehash: e76fefaf4d3c86aa15cf279090c0adb8ed779aab
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901515"
---
# <a name="consuming-packages-from-authenticated-feeds"></a>Korzystanie z pakietów z uwierzytelnionych źródeł danych

Oprócz publicznego źródła [nuget.org,](https://api.nuget.org/v3/index.json)klienci NuGet mogą wchodzić w interakcje z kanałami informacyjnymi plików i prywatnymi kanałami informacyjnymi HTTP.


Do uwierzytelniania za pomocą prywatnych kanałów informacyjnych HTTP są dostępne 2 podejścia:

* Dodawanie poświadczeń w [NuGet.config](../reference/nuget-config-file.md#packagesourcecredentials)
* Uwierzytelnianie przy użyciu jednego z wielu modeli rozszerzalności w zależności od używanego klienta.

## <a name="nuget-clients-authentication-extensibility"></a>Rozszerzalność uwierzytelniania klientów NuGet

W przypadku różnych klientów NuGet za uwierzytelnianie odpowiada sam prywatny dostawca kanału informacyjnego.
Wszyscy klienci NuGet mają metody rozszerzalności, które to obsługują. Są to rozszerzenie Visual Studio lub wtyczka, która może komunikować się z nuGet w celu pobrania poświadczeń.

### <a name="visual-studio"></a>Visual Studio

W Visual Studio NuGet uwidacznia interfejs, który dostawcy kanału informacyjnego mogą implementować i dostarczać swoim klientom. Aby uzyskać więcej informacji, zapoznaj się z dokumentacją dotyczącą tworzenia dostawcy [Visual Studio poświadczeń.](../reference/extensibility/NuGet-Credential-Providers-for-Visual-Studio.md)

#### <a name="available-nuget-credential-providers-for-visual-studio"></a>Dostępni dostawcy poświadczeń NuGet dla Visual Studio

Dostawca poświadczeń jest wbudowany w Visual Studio do obsługi Azure DevOps.


Do dostępnych dostawców poświadczeń wtyczki należą:

* [MyGet Dostawca poświadczeń for Visual Studio](http://docs.myget.org/docs/reference/credential-provider-for-visual-studio)

### <a name="nugetexe"></a>nuget.exe

Gdy `nuget.exe` potrzebuje poświadczeń do uwierzytelnienia za pomocą kanału informacyjnego, szuka ich w następujący sposób:

1. Poszukaj poświadczeń w `NuGet.config` plikach.
1. Korzystanie z dostawców poświadczeń wtyczki w wersji 2
1. Korzystanie z dostawców poświadczeń wtyczki w wersji 1
1. Następnie program NuGet monituje użytkownika o poświadczenia w wierszu polecenia.

#### <a name="nugetexe-and-v2-credential-providers"></a>nuget.exe i dostawcy poświadczeń w wersji 2

W wersji NuGet zdefiniowano nowy mechanizm wtyczki uwierzytelniania, nazywany dostawcami `4.8` poświadczeń w wersji 2.
Aby uzyskać informacje na temat instalacji i odnajdywania tych dostawców, zapoznaj się z [tematem NuGet cross platform plugins (Wtyczki NuGet dla wielu platform).](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery)

#### <a name="nugetexe-and-v1-credential-providers"></a>nuget.exe i dostawcy poświadczeń w wersji 1

W wersji `3.3` NuGet wprowadzono pierwszą wersję wtyczek uwierzytelniania.
Aby uzyskać informacje na temat instalacji i odnajdywania tych dostawców, [ zobacznuget.exe dostawcy poświadczeń](../reference/extensibility/nuget-exe-Credential-Providers.md#nugetexe-credential-provider-discovery)

#### <a name="available-credential-providers-for-nugetexe"></a>Dostępni dostawcy poświadczeń dla nuget.exe

* [Azure DevOps dostawcy poświadczeń w wersji 2](/azure/devops/artifacts/nuget/nuget-exe#add-a-feed-to-nuget-482-or-later) [lub Azure Artifacts Dostawca poświadczeń](https://github.com/microsoft/artifacts-credprovider)

W Visual Studio 2017 r. w wersji 15.9 lub nowszej dostawca poświadczeń Azure DevOps jest dołączony do Visual Studio.
Jeśli `nuget.exe` program korzysta z programu MSBuild z Visual Studio zestawu narzędzi, wtyczka zostanie wykryta automatycznie.

### <a name="dotnetexe"></a>dotnet.exe

Gdy `dotnet.exe` wymaga poświadczeń do uwierzytelnienia za pomocą kanału informacyjnego, szuka ich w następujący sposób:

1. Poszukaj poświadczeń w `NuGet.config` plikach.
1. Korzystanie z dostawców poświadczeń wtyczki w wersji 2

Domyślnie nie jest interakcyjna, więc może być konieczne podanie flagi w celu zablokowania narzędzia `dotnet.exe` `--interactive` na potrzeby uwierzytelniania.

#### <a name="dotnetexe-and-v2-credential-providers"></a>dotnet.exe i dostawcy poświadczeń w wersji 2

W wersji `2.2.100` zestawu SDK program NuGet zdefiniuje mechanizm wtyczki uwierzytelniania, który działa we wszystkich klientach.
Aby uzyskać informacje na temat instalacji i odnajdywania tych dostawców, zapoznaj się z [tematem NuGet cross platform plugins (Wtyczki NuGet dla wielu platform).](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery)

#### <a name="available-credential-providers-for-dotnetexe"></a>Dostępni dostawcy poświadczeń dla dotnet.exe

* [Azure Artifacts Dostawca poświadczeń](https://github.com/microsoft/artifacts-credprovider)

### <a name="msbuildexe"></a>MSBuild.exe

Gdy `MSBuild.exe` potrzebuje poświadczeń do uwierzytelnienia za pomocą kanału informacyjnego, szuka ich w następujący sposób:

1. Poszukaj poświadczeń w `NuGet.config` plikach
1. Korzystanie z dostawców poświadczeń wtyczki w wersji 2

Domyślnie nie jest interakcyjna, więc może być konieczne ustawienie właściwości w celu zablokowania `MSBuild.exe` `/p:NuGetInteractive=true` narzędzia na potrzeby uwierzytelniania.

#### <a name="msbuildexe-and-v2-credential-providers"></a>MSBuild.exe i dostawcy poświadczeń w wersji 2

W Visual Studio 2019 Update 9 nuGet zdefiniuje mechanizm wtyczki uwierzytelniania, który działa na wszystkich klientach.
Aby uzyskać informacje na temat instalacji i odnajdywania tych dostawców, zapoznaj się z [tematem NuGet cross platform plugins (Wtyczki NuGet dla wielu platform).](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery)

#### <a name="available-credential-providers-for-msbuildexe"></a>Dostępni dostawcy poświadczeń dla MSBuild.exe

* [Azure Artifacts Dostawca poświadczeń](https://github.com/microsoft/artifacts-credprovider)

W Visual Studio 2017 Update 9 i nowszych dostawca poświadczeń Azure DevOps jest dołączony do Visual Studio. Nie są wymagane żadne dodatkowe kroki.
