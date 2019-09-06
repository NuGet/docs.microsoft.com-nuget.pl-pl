---
title: Dostawcy poświadczeń programu NuGet dla programu Visual Studio
description: Dostawcy poświadczeń NuGet uwierzytelniają się ze źródłami, implementując interfejs IVsCredentialProvider w rozszerzeniu programu Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: 4e781a2462871bceeb1c7f02220320daabdab98a
ms.sourcegitcommit: a0807671386782021acb7588741390e6f07e94e1
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/05/2019
ms.locfileid: "70384430"
---
# <a name="authenticating-feeds-in-visual-studio-with-nuget-credential-providers"></a>Uwierzytelnianie kanałów informacyjnych w programie Visual Studio przy użyciu dostawców poświadczeń NuGet

Rozszerzenie programu NuGet Visual Studio w wersji 3.6 + obsługuje dostawców poświadczeń, co umożliwia NuGet współpracują z uwierzytelnionymi źródłami danych.
Po zainstalowaniu dostawcy poświadczeń programu NuGet dla programu Visual Studio rozszerzenie NuGet programu Visual Studio będzie automatycznie pobierać i odświeżać poświadczenia dla uwierzytelnionych źródeł w razie potrzeby.

Przykładową implementację można znaleźć w [przykładowej VsCredentialProvider](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).

Począwszy od 4.8 + NuGet w programie Visual Studio obsługuje również nowe wtyczki do uwierzytelniania międzyplatformowego, ale nie są to zalecane podejście ze względu na wydajność.

> [!Note]
> Dostawcy poświadczeń NuGet dla programu Visual Studio muszą być instalowani jako zwykłe rozszerzenie programu Visual Studio i wymagać [programu Visual studio 2017](http://aka.ms/vs/15/release/vs_enterprise.exe) lub nowszego.
>
> Dostawcy poświadczeń NuGet dla programu Visual Studio działają tylko w programie Visual Studio (nie w dotnet restore lub NuGet. exe). W przypadku dostawców poświadczeń z pakietem NuGet. exe zobacz [dostawcy poświadczeń NuGet. exe](nuget-exe-Credential-providers.md).
> Dla dostawców poświadczeń w programie dotnet i MSBuild zobacz [wtyczki Międzyplatformowe NuGet](nuget-cross-platform-authentication-plugin.md)

## <a name="available-nuget-credential-providers-for-visual-studio"></a>Dostępni dostawcy poświadczeń NuGet dla programu Visual Studio

Istnieje Dostawca poświadczeń wbudowany w rozszerzenie NuGet programu Visual Studio w celu obsługi Visual Studio Team Services.

Rozszerzenie NuGet programu Visual Studio używa wewnętrznego `VsCredentialProviderImporter` , który również skanuje w poszukiwaniu dostawców poświadczeń wtyczki. Te dostawcy poświadczeń wtyczki muszą być wykrywalne jako MEF eksportu typu `IVsCredentialProvider`.

Dostępne są następujące dostawcy poświadczeń wtyczek:

- [Dostawca poświadczeń MyGet dla programu Visual Studio](http://docs.myget.org/docs/reference/credential-provider-for-visual-studio)

## <a name="creating-a-nuget-credential-provider-for-visual-studio"></a>Tworzenie dostawcy poświadczeń NuGet dla programu Visual Studio

Pakiet NuGet Visual Studio Extension 3.6 + implementuje wewnętrzny CredentialService, który jest używany do pozyskiwania poświadczeń. CredentialService zawiera listę wbudowanych dostawców poświadczeń i wtyczek. Każdy dostawca jest wybierany sekwencyjnie, dopóki nie zostaną nabyte poświadczenia.

Podczas pozyskiwania poświadczeń usługa Credential podejmie próbę dostawcy poświadczeń w następującej kolejności, zatrzymując się zaraz po pozyskaniu poświadczeń:

1. Poświadczenia będą pobierane z plików konfiguracji NuGet (przy użyciu wbudowanego `SettingsCredentialProvider`).
1. Jeśli źródło pakietu znajduje się na Visual Studio Team Services, `VisualStudioAccountProvider` będzie używane.
1. Wszystkie inne dostawcy poświadczeń programu Visual Studio są podejmowane sekwencyjnie.
1. Spróbuj użyć wszystkich dostawców poświadczeń wielu platform NuGet sekwencyjnie.
1. Jeśli nie pobrano jeszcze poświadczeń, użytkownik zostanie poproszony o podanie poświadczeń przy użyciu standardowego okna dialogowego uwierzytelniania podstawowego.

### <a name="implementing-ivscredentialprovidergetcredentialsasync"></a>Implementing IVsCredentialProvider.GetCredentialsAsync

Aby utworzyć dostawcę poświadczeń NuGet dla programu Visual Studio, Utwórz rozszerzenie programu Visual Studio, które ujawnia publiczny eksport MEF, który `IVsCredentialProvider` implementuje typ, i zgodnie z zasadami opisanymi poniżej.

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

Przykładową implementację można znaleźć w [przykładowej VsCredentialProvider](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).

Każdy dostawca poświadczeń NuGet dla programu Visual Studio musi:

1. Przed zainicjowaniem pozyskiwania poświadczeń należy określić, czy może podać poświadczenia dla danego identyfikatora URI. Jeśli dostawca nie może dostarczyć poświadczeń dla źródłowego źródła, powinien zwrócić `null`.
1. Jeśli dostawca obsługuje żądania dla danego identyfikatora URI, ale nie może dostarczyć poświadczeń, należy zgłaszać wyjątek.

Niestandardowy dostawca poświadczeń NuGet dla programu Visual Studio musi implementować `IVsCredentialProvider` interfejs dostępny w [pakiecie NuGet. VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/).

#### <a name="getcredentialasync"></a>GetCredentialAsync

| Parametr wejściowy |Opis|
| ----------------|-----------|
| Identyfikator URI identyfikatora URI | Identyfikator URI źródła pakietu, dla którego są wymagane poświadczenia.|
| IWebProxy serwer proxy | Serwer proxy sieci Web, który ma być używany podczas komunikacji w sieci. Wartość null, jeśli nie skonfigurowano uwierzytelniania serwera proxy. |
| isProxyRequest bool | Ma wartość true, jeśli to żądanie służy do uzyskiwania poświadczeń uwierzytelniania serwera proxy. Jeśli implementacja nie jest prawidłowa do uzyskiwania poświadczeń serwera proxy, należy zwrócić wartość null. |
| isretry bool | Prawda, jeśli dla tego identyfikatora URI zażądano wcześniej poświadczeń, ale podane poświadczenia nie zezwalają na autoryzowany dostęp. |
| bool nieinteraktywny | W przypadku opcji true Dostawca poświadczeń musi pominąć wszystkie monity użytkownika i zamiast tego użyć wartości domyślnych. |
| CancellationToken cancellationToken | Ten token anulowania powinien zostać sprawdzony w celu ustalenia, czy operacja żądająca poświadczeń została anulowana. |

**Wartość zwracana**: Obiekt poświadczeń implementujący [ `System.Net.ICredentials` interfejs](/dotnet/api/system.net.icredentials?view=netstandard-2.0).
