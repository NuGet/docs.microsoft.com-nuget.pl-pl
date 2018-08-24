---
title: Dostawcy poświadczeń programu NuGet dla programu Visual Studio
description: Dostawcy poświadczeń programu NuGet uwierzytelnianie za pomocą źródeł danych, implementując interfejs IVsCredentialProvider w rozszerzeniu Visual Studio.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: e8d8ae22300b55b93badb65864163d959105dca2
ms.sourcegitcommit: 8d5121af528e68789485405e24e2100fda2868d6
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/23/2018
ms.locfileid: "42793906"
---
# <a name="authenticating-feeds-in-visual-studio-with-nuget-credential-providers"></a><span data-ttu-id="538fe-103">Uwierzytelnianie źródła danych w programie Visual Studio za pomocą dostawcy poświadczeń programu NuGet</span><span class="sxs-lookup"><span data-stu-id="538fe-103">Authenticating feeds in Visual Studio with NuGet credential providers</span></span>

<span data-ttu-id="538fe-104">Visual Studio rozszerzenie NuGet 3.6 + obsługuje dostawcy poświadczeń, które umożliwiają NuGet do pracy z uwierzytelnionymi kanałami informacyjnymi.</span><span class="sxs-lookup"><span data-stu-id="538fe-104">The NuGet Visual Studio Extension 3.6+ supports credential providers, which enable NuGet to work with authenticated feeds.</span></span>
<span data-ttu-id="538fe-105">Po zainstalowaniu dostawcy poświadczeń NuGet dla programu Visual Studio, rozszerzenie NuGet w programie Visual Studio automatycznie uzyskać i odświeżyć poświadczenia na potrzeby uwierzytelnione kanały informacyjne zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="538fe-105">After you install a NuGet credential provider for Visual Studio, the NuGet Visual Studio extension will automatically acquire and refresh credentials for authenticated feeds as necessary.</span></span>

<span data-ttu-id="538fe-106">Przykładową implementację można znaleźć w [przykładowe VsCredentialProvider](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span><span class="sxs-lookup"><span data-stu-id="538fe-106">A sample implementation can be found in [the VsCredentialProvider sample](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span></span>

<span data-ttu-id="538fe-107">Począwszy od 4.8 + NuGet w programie Visual Studio obsługuje nowe dla wielu platform uwierzytelniania wtyczki także, ale nie są zalecane podejście do ze względu na wydajność.</span><span class="sxs-lookup"><span data-stu-id="538fe-107">Starting with 4.8+ NuGet in Visual Studio supports the new cross platform authentication plugins as well, but they are not the recommended approach for performance reasons.</span></span>

> [!Note]
> <span data-ttu-id="538fe-108">Dostawcy poświadczeń programu NuGet dla programu Visual Studio musi być zainstalowany jako regularne rozszerzenia programu Visual Studio i będzie wymagać [programu Visual Studio 2017](http://aka.ms/vs/15/release/vs_enterprise.exe) lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="538fe-108">NuGet credential providers for Visual Studio must be installed as a regular Visual Studio extension and will require [Visual Studio 2017](http://aka.ms/vs/15/release/vs_enterprise.exe) or above.</span></span>
>
> <span data-ttu-id="538fe-109">Dostawcy poświadczeń programu NuGet dla programu Visual Studio działa tylko w programie Visual Studio (nie w dotnet restore lub nuget.exe).</span><span class="sxs-lookup"><span data-stu-id="538fe-109">NuGet credential providers for Visual Studio work only in Visual Studio (not in dotnet restore or nuget.exe).</span></span> <span data-ttu-id="538fe-110">Dostawcy poświadczeń przy użyciu nuget.exe, można zobaczyć [nuget.exe dostawcy poświadczeń](nuget-exe-Credential-providers.md).</span><span class="sxs-lookup"><span data-stu-id="538fe-110">For credential providers with nuget.exe, see [nuget.exe Credential Providers](nuget-exe-Credential-providers.md).</span></span>
> <span data-ttu-id="538fe-111">Dla poświadczenia dostawcy w dotnet, jak i msbuild zobacz [NuGet cross platform wtyczek](nuget-cross-platform-authentication-plugin.md)</span><span class="sxs-lookup"><span data-stu-id="538fe-111">For credential providers in dotnet and msbuild see [NuGet cross platform plugins](nuget-cross-platform-authentication-plugin.md)</span></span>

## <a name="available-nuget-credential-providers-for-visual-studio"></a><span data-ttu-id="538fe-112">Dostępne dostawcy poświadczeń programu NuGet dla programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="538fe-112">Available NuGet credential providers for Visual Studio</span></span>

<span data-ttu-id="538fe-113">Brak dostawcy poświadczeń wbudowaną rozszerzenie NuGet usługi Visual Studio do obsługi programu Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="538fe-113">There is a credential provider built into the Visual Studio NuGet extension to support Visual Studio Team Services.</span></span>

<span data-ttu-id="538fe-114">NuGet rozszerzenia programu Visual Studio używa wewnętrznego `VsCredentialProviderImporter` który również skanuje w poszukiwaniu dostawcy poświadczeń wtyczki.</span><span class="sxs-lookup"><span data-stu-id="538fe-114">The NuGet Visual Studio Extension uses an internal `VsCredentialProviderImporter` which also scans for plug-in credential providers.</span></span> <span data-ttu-id="538fe-115">Te dostawcy poświadczeń wtyczka musi być wykrywalne jako eksportu MEF typu `IVsCredentialProvider`.</span><span class="sxs-lookup"><span data-stu-id="538fe-115">These plug-in credential providers must be discoverable as a MEF Export of type `IVsCredentialProvider`.</span></span>

<span data-ttu-id="538fe-116">Dostawcy poświadczeń wtyczki dostępne obejmują:</span><span class="sxs-lookup"><span data-stu-id="538fe-116">Available plug-in credential providers include:</span></span>

- [<span data-ttu-id="538fe-117">MyGet Credential Provider for Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="538fe-117">MyGet Credential Provider for Visual Studio 2017</span></span>](http://docs.myget.org/docs/reference/credential-provider-for-visual-studio)

## <a name="creating-a-nuget-credential-provider-for-visual-studio"></a><span data-ttu-id="538fe-118">Tworzenie dostawcy poświadczeń NuGet dla programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="538fe-118">Creating a NuGet credential provider for Visual Studio</span></span>

<span data-ttu-id="538fe-119">Visual Studio rozszerzenie NuGet 3.6 + implementuje CredentialService wewnętrzny, który służy do uzyskania poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="538fe-119">The NuGet Visual Studio Extension 3.6+ implements an internal CredentialService that is used to acquire credentials.</span></span> <span data-ttu-id="538fe-120">CredentialService zawiera listę dostawców wbudowanych i wtyczka poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="538fe-120">The CredentialService has a list of built-in and plug-in credential providers.</span></span> <span data-ttu-id="538fe-121">Każdy dostawca zostanie podjęta próba sekwencyjnie aż drogą kupna poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="538fe-121">Each provider is tried sequentially until credentials are acquired.</span></span>

<span data-ttu-id="538fe-122">Podczas pozyskiwanie poświadczeń usługa poświadczeń spróbuje użyć dostawcy poświadczeń w następującej kolejności, zatrzymywanie, tak szybko, jak poświadczenia są nabywane:</span><span class="sxs-lookup"><span data-stu-id="538fe-122">During credential acquisition, the credential service will try credential providers in the following order, stopping as soon as credentials are acquired:</span></span>

1. <span data-ttu-id="538fe-123">Poświadczenia zostaną pobrane z plików konfiguracji NuGet (przy użyciu wbudowanych `SettingsCredentialProvider`).</span><span class="sxs-lookup"><span data-stu-id="538fe-123">Credentials will be fetched from NuGet configuration files (using the built-in `SettingsCredentialProvider`).</span></span>
1. <span data-ttu-id="538fe-124">Jeśli źródło pakietu znajduje się w Visual Studio Team Services `VisualStudioAccountProvider` będą używane.</span><span class="sxs-lookup"><span data-stu-id="538fe-124">If the package source is on Visual Studio Team Services, the `VisualStudioAccountProvider` will be used.</span></span>
1. <span data-ttu-id="538fe-125">Wszystkie inne wtyczki programu Visual Studio dostawcy poświadczeń, zostaną sprawdzone sekwencyjnie.</span><span class="sxs-lookup"><span data-stu-id="538fe-125">All other plug-in Visual Studio credential providers will be tried sequentially.</span></span>
1. <span data-ttu-id="538fe-126">Spróbuj użyć NuGet wszystkich cross platform dostawcy poświadczeń sekwencyjnie.</span><span class="sxs-lookup"><span data-stu-id="538fe-126">Try to use all NuGet cross platform credential providers sequentially.</span></span>
1. <span data-ttu-id="538fe-127">Jeśli żadne poświadczenia nie pobrano jeszcze, użytkownik będzie monitowany o poświadczenia, za pomocą okna dialogowego standardowe uwierzytelnianie podstawowe.</span><span class="sxs-lookup"><span data-stu-id="538fe-127">If no credentials have been acquired yet, the user will be prompted for credentials using a standard basic authentication dialog.</span></span>

### <a name="implementing-ivscredentialprovidergetcredentialsasync"></a><span data-ttu-id="538fe-128">Implementing IVsCredentialProvider.GetCredentialsAsync</span><span class="sxs-lookup"><span data-stu-id="538fe-128">Implementing IVsCredentialProvider.GetCredentialsAsync</span></span>

<span data-ttu-id="538fe-129">Dostawcy poświadczeń NuGet dla programu Visual Studio, utworzyć rozszerzenia programu Visual Studio uwidocznionego przez publiczny eksportu MEF Implementowanie `IVsCredentialProvider` wpisz i działa zgodnie z zasadami przedstawionymi poniżej.</span><span class="sxs-lookup"><span data-stu-id="538fe-129">To create a NuGet credential provider for Visual Studio, create a Visual Studio Extension that exposes a public MEF Export implementing the `IVsCredentialProvider` type, and adheres to the principles outlined below.</span></span>

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

<span data-ttu-id="538fe-130">Przykładową implementację można znaleźć w [przykładowe VsCredentialProvider](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span><span class="sxs-lookup"><span data-stu-id="538fe-130">A sample implementation can be found in [the VsCredentialProvider sample](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span></span>

<span data-ttu-id="538fe-131">Każdy dostawca poświadczeń NuGet dla programu Visual Studio musi:</span><span class="sxs-lookup"><span data-stu-id="538fe-131">Each NuGet credential provider for Visual Studio must:</span></span>

1. <span data-ttu-id="538fe-132">Ustal, czy jego Podaj poświadczenia dla docelowego identyfikatora URI, przed zainicjowaniem pozyskiwanie poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="538fe-132">Determine whether it can provide credentials for the targeted URI before initiating credential acquisition.</span></span> <span data-ttu-id="538fe-133">Jeśli dostawca nie można podać poświadczenia dla źródła docelowych, a następnie powinien zostać zwrócony `null`.</span><span class="sxs-lookup"><span data-stu-id="538fe-133">If the provider cannot supply credentials for the targeted source, then it should return `null`.</span></span>
1. <span data-ttu-id="538fe-134">Jeśli dostawca obsługi żądań dla docelowego identyfikatora URI, ale nie można podać poświadczenia, należy zgłosić wyjątek.</span><span class="sxs-lookup"><span data-stu-id="538fe-134">If the provider does handle requests for the targeted URI, but cannot supply credentials, an exception should be thrown.</span></span>

<span data-ttu-id="538fe-135">Niestandardowego dostawcy poświadczeń NuGet dla programu Visual Studio musi implementować `IVsCredentialProvider` dostępne w interfejsie [pakietu NuGet.VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/).</span><span class="sxs-lookup"><span data-stu-id="538fe-135">A custom NuGet credential provider for Visual Studio must implement the `IVsCredentialProvider` interface available in the [NuGet.VisualStudio package](https://www.nuget.org/packages/NuGet.VisualStudio/).</span></span>

#### <a name="getcredentialasync"></a><span data-ttu-id="538fe-136">GetCredentialAsync</span><span class="sxs-lookup"><span data-stu-id="538fe-136">GetCredentialAsync</span></span>

| <span data-ttu-id="538fe-137">Parametr wejściowy</span><span class="sxs-lookup"><span data-stu-id="538fe-137">Input Parameter</span></span> |<span data-ttu-id="538fe-138">Opis</span><span class="sxs-lookup"><span data-stu-id="538fe-138">Description</span></span>|
| ----------------|-----------|
| <span data-ttu-id="538fe-139">Identyfikator uri identyfikatora URI</span><span class="sxs-lookup"><span data-stu-id="538fe-139">Uri uri</span></span> | <span data-ttu-id="538fe-140">Pakiet źródło identyfikator Uri, dla którego wnioskuje się o poświadczenia.</span><span class="sxs-lookup"><span data-stu-id="538fe-140">The package source Uri for which credentials are being requested.</span></span>|
| <span data-ttu-id="538fe-141">Serwer proxy IWebProxy</span><span class="sxs-lookup"><span data-stu-id="538fe-141">IWebProxy proxy</span></span> | <span data-ttu-id="538fe-142">Serwer proxy sieci Web do użycia przy komunikacji w sieci.</span><span class="sxs-lookup"><span data-stu-id="538fe-142">Web proxy to use when communicating on the network.</span></span> <span data-ttu-id="538fe-143">Wartość null, jeśli uwierzytelnianie nie jest serwer proxy skonfigurowane.</span><span class="sxs-lookup"><span data-stu-id="538fe-143">Null if there is no proxy authentication configured.</span></span> |
| <span data-ttu-id="538fe-144">bool isProxyRequest</span><span class="sxs-lookup"><span data-stu-id="538fe-144">bool isProxyRequest</span></span> | <span data-ttu-id="538fe-145">Wartość true, jeśli żądanie jest uzyskanie poświadczeń uwierzytelniania serwera proxy.</span><span class="sxs-lookup"><span data-stu-id="538fe-145">True if this request is to get proxy authentication credentials.</span></span> <span data-ttu-id="538fe-146">Jeśli wdrożenia jest nieprawidłowa dla pobierania poświadczeń serwera proxy, powinna zostać zwrócona wartość null.</span><span class="sxs-lookup"><span data-stu-id="538fe-146">If the implementation is not valid for acquiring proxy credentials, then null should be returned.</span></span> |
| <span data-ttu-id="538fe-147">bool isRetry</span><span class="sxs-lookup"><span data-stu-id="538fe-147">bool isRetry</span></span> | <span data-ttu-id="538fe-148">Wartość true, jeśli poświadczenia zostały wcześniej zażądany dla tego identyfikatora Uri, ale podane poświadczenia nie zezwala na dostęp do autoryzowanych.</span><span class="sxs-lookup"><span data-stu-id="538fe-148">True if credentials were previously requested for this Uri, but the supplied credentials did not allow authorized access.</span></span> |
| <span data-ttu-id="538fe-149">wartość logiczna nieinterakcyjnym</span><span class="sxs-lookup"><span data-stu-id="538fe-149">bool nonInteractive</span></span> | <span data-ttu-id="538fe-150">W przypadku opcji true Dostawca poświadczeń należy pominąć wszystkie monity użytkownika i zamiast tego użyj wartości domyślnych.</span><span class="sxs-lookup"><span data-stu-id="538fe-150">If true, the credential provider must suppress all user prompts and use default values instead.</span></span> |
| <span data-ttu-id="538fe-151">CancellationToken token anulowania</span><span class="sxs-lookup"><span data-stu-id="538fe-151">CancellationToken cancellationToken</span></span> | <span data-ttu-id="538fe-152">Ten token anulowania powinny być sprawdzane w celu ustalenia, jeśli poświadczenia żądania operacja została anulowana.</span><span class="sxs-lookup"><span data-stu-id="538fe-152">This cancellation token should be checked to determine if the operation requesting credentials has been cancelled.</span></span> |

<span data-ttu-id="538fe-153">**Wartość zwracana**: Implementowanie obiekt poświadczeń [ `System.Net.ICredentials` interfejsu](/dotnet/api/system.net.icredentials?view=netstandard-2.0).</span><span class="sxs-lookup"><span data-stu-id="538fe-153">**Return value**: A credentials object implementing the [`System.Net.ICredentials` interface](/dotnet/api/system.net.icredentials?view=netstandard-2.0).</span></span>
