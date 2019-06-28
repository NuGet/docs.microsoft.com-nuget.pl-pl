---
title: Omówienie NuGet.org
description: Omówienie NuGet.org
author: mikejo5000
ms.author: mikejo
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: 9a75ecbc589afa664e5684005e077b02913e8039
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/28/2019
ms.locfileid: "67427522"
---
# <a name="overview-of-nugetorg"></a>Omówienie NuGet.org

NuGet.org jest hostem publicznych pakietów NuGet, które są wykorzystywane przez miliony deweloperów platformy .NET i .NET Core, każdego dnia.

## <a name="role-of-nugetorg-in-the-nuget-ecosystem"></a>Rola NuGet.org należący do ekosystemu NuGet

W roli jako publiczny hosta NuGet.org, sam przechowuje centralne repozytorium ponad 100 000 pakietów unikatowy w [nuget.org](https://www.nuget.org). NuGet.org nie jest możliwa tylko hosta dla pakietów. Technologia NuGet można również do hostowania pakietów przez użytkowników w chmurze (takie jak na DevOps platformy Azure), w sieci prywatnej lub nawet po prostu lokalnego systemu plików. Jeśli interesuje Cię inny host lub opcji hostingu, zobacz [hostingu źródła NuGet](../hosting-packages/overview.md).

NuGet.org, takich jak dowolnego hosta, w przypadku pakietów NuGet służy jako punkt połączenia między pakietu *twórców* i pakietu *konsumentów*. Twórcy tworzenie przydatne pakietów NuGet i opublikuj je. Konsumenci Wyszukaj pakiety przydatne i są zgodne na hostach dostępny, pobieranie oraz w swoich projektach, takich jak te pakiety. Po zainstalowaniu w projekcie, interfejsy API te pakiety są dostępne w pozostałej części kodu projektu.

![Relacja między pakietu dla twórców, hosty pakietu oraz klientów pakietu](media/nuget-roles.png)

## <a name="accounts"></a>Konta

Aby opublikować pakiety w witrynie NuGet.org, należy najpierw utworzyć [konta osoby (użytkownik)](individual-accounts.md). Staje się on swoją tożsamość w witrynie NuGet.org.

NuGet.org umożliwia również tworzenie [konto organizacji](organizations-on-nuget-org.md). Konto organizacji ma co najmniej jeden z indywidualnych kont jako elementy członkowskie. Zestaw pakietów przy zachowaniu jednej tożsamości dla własności mogą zarządzać elementy członkowskie. Za pomocą indywidualnego konta może być członkiem dowolnej liczby organizacji.

Pakiet może należeć do organizacji, takich jak mogą należeć do indywidualnych kont. Konsumentów pakietu nie jest widoczna różnica między indywidualne konto lub konta organizacji: oba są wyświetlane jako pakiet `owners`.

## <a name="api-keys"></a>Klucze interfejsu API

Po utworzeniu pakietu NuGet ( *.nupkg* plików) do publikowania, opublikujesz go w witrynie NuGet.org, przy użyciu interfejsu wiersza polecenia nuget.exe lub dotnet.exe interfejsu wiersza polecenia, wraz z [klucz interfejsu API](scoped-api-keys.md) uzyskanych z repozytorium NuGet.org.

Gdy użytkownik [publikowanie pakietu](../create-packages/creating-a-package.md), wartość klucza interfejsu API są objęte polecenia interfejsu wiersza polecenia.

## <a name="id-prefixes"></a>Identyfikator prefiksów

Podczas publikowania pakietów, możesz zarezerwować i chronić swoją tożsamość za [rezerwowanie prefiksów identyfikator](id-prefix-reservation.md). Podczas instalowania pakietu, konsumentów pakietu znajdują się dodatkowe informacje, co oznacza, że pakiet, w którym są one używania nie oszukańczym w jego właściwościach identyfikacyjne.

## <a name="api-endpoint-for-nugetorg"></a>Punkt końcowy interfejsu API dla NuGet.org

Aby użyć NuGet.org jako repozytorium pakietów NuGet klientów, należy użyć następujący punkt końcowy interfejsu API w wersji 3: 

`https://api.nuget.org/v3/index.json`

Starsi klienci mogą nadal używać protokołu V2 nawiązać NuGet.org. Jednak należy pamiętać, NuGet klientów 3.0 lub nowszej odniesie wolniej, a mniej niezawodnej usługi przy użyciu protokołu V2:

`https://www.nuget.org/api/v2` (**Protokół w wersji 2 jest przestarzała!** )
