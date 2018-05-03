---
title: Dostawcy poświadczeń NuGet dla programu Visual Studio
description: NuGet dostawcy poświadczeń uwierzytelniania za pomocą źródła zaimplementowanie interfejsu IVsCredentialProvider rozszerzenia programu Visual Studio.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: 740df87b0d663aac482d888e916662528ce27030
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/26/2018
---
# <a name="authenticating-feeds-in-visual-studio-with-nuget-credential-providers"></a>Źródła danych w programie Visual Studio za pomocą NuGet dostawcy poświadczeń uwierzytelniania

NuGet programu Visual Studio rozszerzenia 3,6 + obsługuje dostawcy poświadczeń, umożliwiające NuGet do pracy z uwierzytelnionego źródeł danych.
Po zainstalowaniu dostawcy poświadczeń NuGet dla programu Visual Studio, rozszerzenie NuGet dla programu Visual Studio automatycznie uzyskać i odświeżyć poświadczenia dla źródeł uwierzytelnionych w razie potrzeby.

Przykładowe zastosowanie znajdują się w [próbki VsCredentialProvider](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).

> [!Note]
> Dostawcy poświadczeń NuGet dla programu Visual Studio musi zostać zainstalowana jako prawidłowe rozszerzenie programu Visual Studio i będzie wymagać [programu Visual Studio 2017](https://aka.ms/vs/15/preview/vs_enterprise) (obecnie w wersji zapoznawczej) lub nowszy.
>
> Dostawcy poświadczeń NuGet dla programu Visual Studio działa tylko w programie Visual Studio (nie w przywracania dotnet lub nuget.exe). Dla dostawcy poświadczeń z nuget.exe, zobacz [nuget.exe dostawcy poświadczeń](nuget-exe-Credential-providers.md).

## <a name="available-nuget-credential-providers-for-visual-studio"></a>Dostępne dostawcy poświadczeń NuGet dla programu Visual Studio

Brak dostawcy poświadczeń wbudowane rozszerzenia programu Visual Studio NuGet do obsługi programu Visual Studio Team Services.

Rozszerzenia NuGet programu Visual Studio korzysta z wewnętrznego `VsCredentialProviderImporter` powoduje skanowanie dla dostawcy poświadczeń wtyczki. Dostawcy te wtyczka poświadczeń musi być wykrywalny jako eksportu MEF typu `IVsCredentialProvider`.

Dostawcy poświadczeń wtyczki dostępne są następujące:

- [MyGet Credential Provider for Visual Studio 2017](http://docs.myget.org/docs/reference/credential-provider-for-visual-studio)

## <a name="creating-a-nuget-credential-provider-for-visual-studio"></a>Tworzenie dostawcy poświadczeń NuGet dla programu Visual Studio

NuGet programu Visual Studio rozszerzenia 3,6 + implementuje wewnętrzny CredentialService, który jest używany w celu uzyskania poświadczeń. CredentialService zawiera listę dostawców wbudowanych i wtyczki poświadczeń. Każdy dostawca sprawdzane są sekwencyjnie, aż do drogą kupna poświadczeń.

Podczas przejęcia poświadczeń usługa poświadczeń spróbuje dostawcy poświadczeń w następującej kolejności, zatrzymywanie, jak poświadczenia są nabywane:

1. Poświadczenia będą pobierane z plików konfiguracyjnych NuGet (przy użyciu wbudowanych `SettingsCredentialProvider`).
1. Jeśli źródło pakietu znajduje się w Visual Studio Team Services `VisualStudioAccountProvider` będą używane.
1. Wszyscy inni dostawcy poświadczeń wtyczki zostaną sprawdzone po kolei.
1. Jeśli żadne poświadczenia nie zostały nabyte jeszcze, użytkownik będzie monitowany o poświadczenia, za pomocą okna dialogowego standardowe uwierzytelnianie podstawowe.

### <a name="implementing-ivscredentialprovidergetcredentialsasync"></a>Implementing IVsCredentialProvider.GetCredentialsAsync

Aby utworzyć dostawcę poświadczeń NuGet dla programu Visual Studio, utworzyć rozszerzenie Visual Studio, które udostępnia publiczne eksportu MEF implementacja `IVsCredentialProvider` wpisz i stosuje zasady opisane poniżej.

```cs
public interface IVsCredentialProvider
{
    Task<ICredentials> GetCredentialsAsync(
        Uri uri,
        IWebProxy proxy,
        bool isProxyRequest,
        bool isRetry,
        bool nonInteractive,
        CancellationToken cancellationToken);
}
```

Przykładowe zastosowanie znajdują się w [próbki VsCredentialProvider](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).

Każdy dostawca poświadczeń NuGet dla programu Visual Studio musi:

1. Ustal, czy jego Podaj poświadczenia dla docelowego identyfikatora URI przed zainicjowaniem przejęcie poświadczeń. Jeśli dostawca nie może dostarczyć poświadczenia dla źródła docelowych, powinien on zwrócić `null`.
1. Jeśli dostawca obsługuje żądania dla docelowego identyfikatora URI, ale nie można podać poświadczenia, powinny być wyjątek.

Niestandardowy Dostawca poświadczeń NuGet dla programu Visual Studio musi implementować `IVsCredentialProvider` dostępne w interfejsie [pakietu NuGet.VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/).

#### <a name="getcredentialasync"></a>GetCredentialAsync

| Parametr wejściowy |Opis|
| ----------------|-----------|
| Identyfikator uri identyfikatora URI | Źródło pakietu Uri, dla których wymagane są poświadczenia.|
| IWebProxy serwera proxy | Serwer proxy sieci Web do użycia przy komunikacji w sieci. Wartość null, jeśli uwierzytelnianie nie jest serwer proxy skonfigurowane. |
| wartość logiczna isProxyRequest | Wartość true, jeśli żądanie jest uzyskanie poświadczeń uwierzytelniania serwera proxy. Jeśli wdrożenia jest nieprawidłowa dla pobierania poświadczeń serwera proxy, powinna zostać zwrócona wartość null. |
| wartość logiczna isRetry | Wartość true, jeśli poświadczenia zostały wcześniej żądał dla tego identyfikatora Uri, ale podane poświadczenia nie zezwala na dostęp do autoryzowanych. |
| wartość logiczna nieinterakcyjne | Jeśli PRAWDA, Dostawca poświadczeń należy pominąć wszystkie monity użytkownika i zamiast tego użyj wartości domyślnych. |
| CancellationToken cancellationToken | Ten token anulowania powinny być sprawdzane w celu ustalenia, jeśli poświadczenia żądania operacja została anulowana. |

**Wartość zwracana**: implementacja obiektu poświadczeń [ `System.Net.ICredentials` interfejsu](/dotnet/api/system.net.icredentials?view=netstandard-2.0).
