---
title: Omówienie witryny NuGet.org
description: Omówienie witryny NuGet.org
author: mikejo5000
ms.author: mikejo
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: 9a75ecbc589afa664e5684005e077b02913e8039
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "67427522"
---
# <a name="overview-of-nugetorg"></a>Omówienie witryny NuGet.org

NuGet.org jest publicznym hostem pakietów NuGet, które są codziennie zatrudniane przez miliony deweloperów platformy .NET i .NET Core.

## <a name="role-of-nugetorg-in-the-nuget-ecosystem"></a>Rola NuGet.org w ekosystemie NuGet

W swojej roli jako gospodarza publicznego, NuGet.org sam utrzymuje centralne repozytorium ponad 100.000 unikalnych pakietów w [nuget.org](https://www.nuget.org). NuGet.org nie jest jedynym możliwym hostem dla pakietów. Technologia NuGet umożliwia również hostowania pakietów prywatnie w chmurze (na przykład w usłudze Azure DevOps), w sieci prywatnej, a nawet tylko w lokalnym systemie plików. Jeśli jesteś zainteresowany inną opcją hosta lub hostingu, zobacz [Hostowanie własnych kanałów NuGet](../hosting-packages/overview.md).

NuGet.org, podobnie jak każdy host pakietów NuGet, służy jako punkt połączenia między *twórcami pakietów* a *konsumentami pakietów.* Twórcy twórz przydatne pakiety NuGet i publikują je. Następnie konsumenci wyszukują przydatne i kompatybilne pakiety na dostępnych hostach, pobierając i włączając te pakiety do swoich projektów. Po zainstalowaniu w projekcie interfejsy API pakietów są dostępne dla pozostałej części kodu projektu.

![Relacje między twórcami pakietów, hostami pakietów i odbiorcami pakietów](media/nuget-roles.png)

## <a name="accounts"></a>Konta

Aby opublikować pakiety na NuGet.org, należy najpierw utworzyć [indywidualne konto (użytkownika).](individual-accounts.md) To staje się twoją tożsamością na NuGet.org.

NuGet.org umożliwia również utworzenie konta [organizacji](organizations-on-nuget-org.md). Konto organizacji ma co najmniej jedno konto pojedyncze jako jej członkowie. Członkowie mogą zarządzać zestawem pakietów przy zachowaniu jednej tożsamości dla własności. Za pośrednictwem indywidualnego konta możesz być członkiem dowolnej liczby organizacji.

Pakiet może należeć do konta organizacji, tak jak może należeć do indywidualnego konta. Konsumenci pakietów nie widzą żadnej różnicy między kontem indywidualnym `owners`lub kontem organizacji: oba są wyświetlane jako pakiet.

## <a name="api-keys"></a>Klucze interfejsu API

Po opublikowaniu pakietu NuGet *(.nupkg* file) publikujesz go w NuGet.org przy użyciu interfejsu wiersza polecenia nuget.exe lub interfejsu wiersza polecenia dotnet.exe wraz z [kluczem interfejsu API](scoped-api-keys.md) uzyskanym z NuGet.org.

Podczas [publikowania pakietu](../create-packages/creating-a-package.md)należy dołączyć wartość klucza interfejsu API do polecenia CLI.

## <a name="id-prefixes"></a>Prefiksy identyfikatorów

Publikując pakiety, możesz zarezerwować i chronić swoją tożsamość, [rezerwując prefiksy identyfikatorów](id-prefix-reservation.md). Podczas instalowania pakietu, konsumenci pakietów są dostarczane z dodatkowymi informacjami wskazującymi, że pakiet, który zużywają nie jest zwodnicze w jego właściwości identyfikujące.

## <a name="api-endpoint-for-nugetorg"></a>Punkt końcowy interfejsu API dla NuGet.org

Aby użyć NuGet.org jako repozytorium pakietów z klientami NuGet, należy użyć następującego punktu końcowego interfejsu API systemu V3: 

`https://api.nuget.org/v3/index.json`

Starsi klienci mogą nadal używać protokołu V2, aby dotrzeć do NuGet.org. Należy jednak pamiętać, że klienci NuGet 3.0 lub nowsi będą mieli wolniejszą i mniej niezawodną usługę przy użyciu protokołu V2:

`https://www.nuget.org/api/v2`**(V2 prototcol jest przestarzały!**)
