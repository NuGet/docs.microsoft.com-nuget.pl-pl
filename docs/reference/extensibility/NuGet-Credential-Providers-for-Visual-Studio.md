---
title: Dostawcy poświadczeń programu NuGet dla programu Visual Studio
description: Dostawcy poświadczeń programu NuGet uwierzytelnianie za pomocą źródeł danych, implementując interfejs IVsCredentialProvider w rozszerzeniu Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: abe009fee5863c55a188f4d7c71ed0924dd067ff
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547957"
---
# <a name="authenticating-feeds-in-visual-studio-with-nuget-credential-providers"></a>Uwierzytelnianie źródła danych w programie Visual Studio za pomocą dostawcy poświadczeń programu NuGet

Visual Studio rozszerzenie NuGet 3.6 + obsługuje dostawcy poświadczeń, które umożliwiają NuGet do pracy z uwierzytelnionymi kanałami informacyjnymi.
Po zainstalowaniu dostawcy poświadczeń NuGet dla programu Visual Studio, rozszerzenie NuGet w programie Visual Studio automatycznie uzyskać i odświeżyć poświadczenia na potrzeby uwierzytelnione kanały informacyjne zgodnie z potrzebami.

Przykładową implementację można znaleźć w [przykładowe VsCredentialProvider](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).

Począwszy od 4.8 + NuGet w programie Visual Studio obsługuje nowe dla wielu platform uwierzytelniania wtyczki także, ale nie są zalecane podejście do ze względu na wydajność.

> [!Note]
> Dostawcy poświadczeń programu NuGet dla programu Visual Studio musi być zainstalowany jako regularne rozszerzenia programu Visual Studio i będzie wymagać [programu Visual Studio 2017](http://aka.ms/vs/15/release/vs_enterprise.exe) lub nowszej.
>
> Dostawcy poświadczeń programu NuGet dla programu Visual Studio działa tylko w programie Visual Studio (nie w dotnet restore lub nuget.exe). Dostawcy poświadczeń przy użyciu nuget.exe, można zobaczyć [nuget.exe dostawcy poświadczeń](nuget-exe-Credential-providers.md).
> Dla poświadczenia dostawcy w dotnet, jak i msbuild zobacz [NuGet cross platform wtyczek](nuget-cross-platform-authentication-plugin.md)

## <a name="available-nuget-credential-providers-for-visual-studio"></a>Dostępne dostawcy poświadczeń programu NuGet dla programu Visual Studio

Brak dostawcy poświadczeń wbudowaną rozszerzenie NuGet usługi Visual Studio do obsługi programu Visual Studio Team Services.

NuGet rozszerzenia programu Visual Studio używa wewnętrznego `VsCredentialProviderImporter` który również skanuje w poszukiwaniu dostawcy poświadczeń wtyczki. Te dostawcy poświadczeń wtyczka musi być wykrywalne jako eksportu MEF typu `IVsCredentialProvider`.

Dostawcy poświadczeń wtyczki dostępne obejmują:

- [MyGet Credential Provider for Visual Studio 2017](http://docs.myget.org/docs/reference/credential-provider-for-visual-studio)

## <a name="creating-a-nuget-credential-provider-for-visual-studio"></a>Tworzenie dostawcy poświadczeń NuGet dla programu Visual Studio

Visual Studio rozszerzenie NuGet 3.6 + implementuje CredentialService wewnętrzny, który służy do uzyskania poświadczeń. CredentialService zawiera listę dostawców wbudowanych i wtyczka poświadczeń. Każdy dostawca zostanie podjęta próba sekwencyjnie aż drogą kupna poświadczeń.

Podczas pozyskiwanie poświadczeń usługa poświadczeń spróbuje użyć dostawcy poświadczeń w następującej kolejności, zatrzymywanie, tak szybko, jak poświadczenia są nabywane:

1. Poświadczenia zostaną pobrane z plików konfiguracji NuGet (przy użyciu wbudowanych `SettingsCredentialProvider`).
1. Jeśli źródło pakietu znajduje się w Visual Studio Team Services `VisualStudioAccountProvider` będą używane.
1. Wszystkie inne wtyczki programu Visual Studio dostawcy poświadczeń, zostaną sprawdzone sekwencyjnie.
1. Spróbuj użyć NuGet wszystkich cross platform dostawcy poświadczeń sekwencyjnie.
1. Jeśli żadne poświadczenia nie pobrano jeszcze, użytkownik będzie monitowany o poświadczenia, za pomocą okna dialogowego standardowe uwierzytelnianie podstawowe.

### <a name="implementing-ivscredentialprovidergetcredentialsasync"></a>Implementing IVsCredentialProvider.GetCredentialsAsync

Dostawcy poświadczeń NuGet dla programu Visual Studio, utworzyć rozszerzenia programu Visual Studio uwidocznionego przez publiczny eksportu MEF Implementowanie `IVsCredentialProvider` wpisz i działa zgodnie z zasadami przedstawionymi poniżej.

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

Przykładową implementację można znaleźć w [przykładowe VsCredentialProvider](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).

Każdy dostawca poświadczeń NuGet dla programu Visual Studio musi:

1. Ustal, czy jego Podaj poświadczenia dla docelowego identyfikatora URI, przed zainicjowaniem pozyskiwanie poświadczeń. Jeśli dostawca nie można podać poświadczenia dla źródła docelowych, a następnie powinien zostać zwrócony `null`.
1. Jeśli dostawca obsługi żądań dla docelowego identyfikatora URI, ale nie można podać poświadczenia, należy zgłosić wyjątek.

Niestandardowego dostawcy poświadczeń NuGet dla programu Visual Studio musi implementować `IVsCredentialProvider` dostępne w interfejsie [pakietu NuGet.VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/).

#### <a name="getcredentialasync"></a>GetCredentialAsync

| Parametr wejściowy |Opis|
| ----------------|-----------|
| Identyfikator uri identyfikatora URI | Pakiet źródło identyfikator Uri, dla którego wnioskuje się o poświadczenia.|
| Serwer proxy IWebProxy | Serwer proxy sieci Web do użycia przy komunikacji w sieci. Wartość null, jeśli uwierzytelnianie nie jest serwer proxy skonfigurowane. |
| bool isProxyRequest | Wartość true, jeśli żądanie jest uzyskanie poświadczeń uwierzytelniania serwera proxy. Jeśli wdrożenia jest nieprawidłowa dla pobierania poświadczeń serwera proxy, powinna zostać zwrócona wartość null. |
| bool isRetry | Wartość true, jeśli poświadczenia zostały wcześniej zażądany dla tego identyfikatora Uri, ale podane poświadczenia nie zezwala na dostęp do autoryzowanych. |
| wartość logiczna nieinterakcyjnym | W przypadku opcji true Dostawca poświadczeń należy pominąć wszystkie monity użytkownika i zamiast tego użyj wartości domyślnych. |
| CancellationToken token anulowania | Ten token anulowania powinny być sprawdzane w celu ustalenia, jeśli poświadczenia żądania operacja została anulowana. |

**Wartość zwracana**: Implementowanie obiekt poświadczeń [ `System.Net.ICredentials` interfejsu](/dotnet/api/system.net.icredentials?view=netstandard-2.0).
