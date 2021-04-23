---
title: Omówienie witryny NuGet.org
description: Omówienie witryny NuGet.org
author: mikejo5000
ms.author: mikejo
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: 2dac6ebd6367f3ed1a5ef9e81d843867a4a22f62
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901879"
---
# <a name="overview-of-nugetorg"></a>Omówienie witryny NuGet.org

NuGet.org to publiczny host pakietów NuGet, które są codziennie stosowane przez miliony deweloperów .NET i .NET Core.

## <a name="role-of-nugetorg-in-the-nuget-ecosystem"></a>Rola NuGet.org w ekosystemie NuGet

W swojej roli jako host publiczny NuGet.org obsługuje centralne repozytorium ponad 100 000 unikatowych pakietów w nuget.org [.](https://www.nuget.org) NuGet.org nie jest jedynym możliwym hostem pakietów. Technologia NuGet umożliwia również hostować pakiety prywatnie w chmurze (na przykład w usłudze Azure DevOps), w sieci prywatnej, a nawet tylko w lokalnym systemie plików. Jeśli interesuje Cię inny host lub opcja hostingu, zobacz [Hosting your own NuGet feeds (Hostowanie własnych źródeł danych NuGet).](../hosting-packages/overview.md)

NuGet.org, tak jak każdy host pakietów NuGet, służy jako punkt połączenia między twórcami pakietów a *ich* *odbiorcami.* Twórcy skompilowali przydatne pakiety NuGet i opublikowali je. Następnie użytkownicy wyszukują przydatne i zgodne pakiety na dostępnych hostach, pobierając i uwzględniając te pakiety w swoich projektach. Po zainstalowaniu w projekcie interfejsy API pakietów są dostępne dla pozostałej części kodu projektu.

![Relacja między twórcami pakietów, hostami pakietów i konsumentami pakietów](media/nuget-roles.png)

## <a name="accounts"></a>Konta

Aby opublikować pakiety NuGet.org, należy najpierw utworzyć [indywidualne konto (użytkownika).](individual-accounts.md) Stanie się to Twoją tożsamością NuGet.org.

NuGet.org umożliwia również utworzenie konta [organizacji.](organizations-on-nuget-org.md) Konto organizacji ma co najmniej jedno indywidualne konto jako jego członków. Członkowie mogą zarządzać zestawem pakietów przy zachowaniu jednej tożsamości na własność. Za pomocą indywidualnego konta możesz być członkiem dowolnej liczby organizacji.

Pakiet może należeć do konta organizacji, tak jak może należeć do pojedynczego konta. Odbiorcy pakietów nie widzą żadnej różnicy między indywidualnym kontem a kontem organizacji: oba elementy są wyświetlane jako pakiet `owners` .

## <a name="api-keys"></a>Klucze interfejsu API

Po opublikowaniu pakietu NuGet (pliku *.nupkg)* należy opublikować go w programie NuGet.org przy użyciu interfejsu wiersza polecenia programu nuget.exe lub interfejsu wiersza polecenia programu dotnet.exe, a także klucza interfejsu [API](scoped-api-keys.md) uzyskanego z usługi NuGet.org.

Podczas [publikowania pakietu wartość](../create-packages/creating-a-package.md)klucza interfejsu API jest uwzględniana w poleceniu interfejsu wiersza polecenia.

## <a name="id-prefixes"></a>Prefiksy identyfikatorów

Podczas publikowania pakietów można zarezerwować i chronić swoją tożsamość, [rezerwując prefiksy identyfikatorów](id-prefix-reservation.md). Podczas instalowania pakietu odbiorcy pakietów są dostarczani z dodatkowymi informacjami wskazującymi, że pakiet, z których są oni oni konsumujący, nie jest złudny w jego właściwościach identyfikujących.

## <a name="api-endpoint-for-nugetorg"></a>Punkt końcowy interfejsu API dla NuGet.org

Aby używać NuGet.org jako repozytorium pakietów z klientami NuGet, należy użyć następującego punktu końcowego interfejsu API w wersji 3: 

`https://api.nuget.org/v3/index.json`

Starsi klienci mogą nadal używać protokołu V2 w celu osiągnięcia NuGet.org. Należy jednak pamiętać, że klienci NuGet w wersji 3.0 lub nowszej będą mieć wolniejsze i mniej niezawodne usługi korzystające z protokołu V2:

`https://www.nuget.org/api/v2` (Protokół **V2 jest przestarzały!**)
