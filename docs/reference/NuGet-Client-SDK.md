---
title: Zestaw SDK klienta programu NuGet
description: Interfejs API jest rozwijającą się i nie jest jeszcze udokumentowane, ale przykłady są dostępne na blogu Dave Glick.
author: karann-msft
ms.author: karann
ms.date: 01/09/2018
ms.topic: conceptual
ms.openlocfilehash: 8f96bf289e8121fd25262fb95c2f36dfc89045c5
ms.sourcegitcommit: 573af6133a39601136181c1d98c09303f51a1ab2
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/18/2019
ms.locfileid: "58911039"
---
# <a name="nuget-client-sdk"></a>Zestaw SDK klienta programu NuGet

> [!Note]
> Nie należy mylić z [NuGet *Web* interfejsu API](https://docs.microsoft.com/en-us/nuget/api/overview)

*Zestawu SDK klienta usługi NuGet* odnosi się do grupy bibliotek .NET, a ich tematyka wokół [NuGet.Commands](https://www.nuget.org/packages/NuGet.Commands), [Nuget.Packaging](https://www.nuget.org/packages/NuGet.Packaging), i [NuGet.Protocol](https://www.nuget.org/packages/NuGet.Protocol). Te pakiety Zastąp wcześniej [NuGet.Core](https://www.nuget.org/packages/NuGet.Core/) biblioteki.

Pracujemy nad o stabilne powierzchni, firma Microsoft wkrótce dokumentu.

## <a name="source-code"></a>Kod źródłowy

Kod źródłowy jest opublikowany w usłudze GitHub w projekcie [NuGet/NuGet.Client](https://github.com/NuGet/NuGet.Client).

## <a name="third-party-documentation"></a>Dokumentacja usługi innych firm

Przykłady i dokumentację dla niektórych interfejsu API można znaleźć w następującego cyklu blogów przez Dave Glick, opublikowane 2016:

- [Eksplorowanie NuGet w wersji 3 biblioteki, część 1: Wprowadzenie i pojęcia](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-1)
- [Eksplorowanie NuGet w wersji 3 biblioteki, część 2: Wyszukiwanie pakietów](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-2)
- [Eksplorowanie NuGet w wersji 3 biblioteki, część 3: Instalowanie pakietów](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-3)

> [!Note]
> Wpisy na blogu zostały napisane wkrótce po **3.4.3** wersji pakietu NuGet zostały wydane pakiety zestawu SDK klienta.
> Nowsze wersje pakietów mogą być niezgodne z informacjami w wpisów w blogu.

Martin Björkström czy wpis w blogu monitowania na serię wpisów w blogu Dave Glick, gdzie przedstawia różne podejście na temat używania zestawu SDK klienta NuGet na instalowanie pakietów NuGet:

- [Ponowne spojrzenie na NuGet biblioteki v3](https://martinbjorkstrom.com/posts/2018-09-19-revisiting-nuget-client-libraries)
