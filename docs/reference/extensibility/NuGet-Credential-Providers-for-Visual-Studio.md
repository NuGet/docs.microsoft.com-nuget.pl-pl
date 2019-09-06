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
# <a name="authenticating-feeds-in-visual-studio-with-nuget-credential-providers"></a><span data-ttu-id="a01cf-103">Uwierzytelnianie kanałów informacyjnych w programie Visual Studio przy użyciu dostawców poświadczeń NuGet</span><span class="sxs-lookup"><span data-stu-id="a01cf-103">Authenticating feeds in Visual Studio with NuGet credential providers</span></span>

<span data-ttu-id="a01cf-104">Rozszerzenie programu NuGet Visual Studio w wersji 3.6 + obsługuje dostawców poświadczeń, co umożliwia NuGet współpracują z uwierzytelnionymi źródłami danych.</span><span class="sxs-lookup"><span data-stu-id="a01cf-104">The NuGet Visual Studio Extension 3.6+ supports credential providers, which enable NuGet to work with authenticated feeds.</span></span>
<span data-ttu-id="a01cf-105">Po zainstalowaniu dostawcy poświadczeń programu NuGet dla programu Visual Studio rozszerzenie NuGet programu Visual Studio będzie automatycznie pobierać i odświeżać poświadczenia dla uwierzytelnionych źródeł w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="a01cf-105">After you install a NuGet credential provider for Visual Studio, the NuGet Visual Studio extension will automatically acquire and refresh credentials for authenticated feeds as necessary.</span></span>

<span data-ttu-id="a01cf-106">Przykładową implementację można znaleźć w [przykładowej VsCredentialProvider](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span><span class="sxs-lookup"><span data-stu-id="a01cf-106">A sample implementation can be found in [the VsCredentialProvider sample](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span></span>

<span data-ttu-id="a01cf-107">Począwszy od 4.8 + NuGet w programie Visual Studio obsługuje również nowe wtyczki do uwierzytelniania międzyplatformowego, ale nie są to zalecane podejście ze względu na wydajność.</span><span class="sxs-lookup"><span data-stu-id="a01cf-107">Starting with 4.8+ NuGet in Visual Studio supports the new cross platform authentication plugins as well, but they are not the recommended approach for performance reasons.</span></span>

> [!Note]
> <span data-ttu-id="a01cf-108">Dostawcy poświadczeń NuGet dla programu Visual Studio muszą być instalowani jako zwykłe rozszerzenie programu Visual Studio i wymagać [programu Visual studio 2017](http://aka.ms/vs/15/release/vs_enterprise.exe) lub nowszego.</span><span class="sxs-lookup"><span data-stu-id="a01cf-108">NuGet credential providers for Visual Studio must be installed as a regular Visual Studio extension and will require [Visual Studio 2017](http://aka.ms/vs/15/release/vs_enterprise.exe) or above.</span></span>
>
> <span data-ttu-id="a01cf-109">Dostawcy poświadczeń NuGet dla programu Visual Studio działają tylko w programie Visual Studio (nie w dotnet restore lub NuGet. exe).</span><span class="sxs-lookup"><span data-stu-id="a01cf-109">NuGet credential providers for Visual Studio work only in Visual Studio (not in dotnet restore or nuget.exe).</span></span> <span data-ttu-id="a01cf-110">W przypadku dostawców poświadczeń z pakietem NuGet. exe zobacz [dostawcy poświadczeń NuGet. exe](nuget-exe-Credential-providers.md).</span><span class="sxs-lookup"><span data-stu-id="a01cf-110">For credential providers with nuget.exe, see [nuget.exe Credential Providers](nuget-exe-Credential-providers.md).</span></span>
> <span data-ttu-id="a01cf-111">Dla dostawców poświadczeń w programie dotnet i MSBuild zobacz [wtyczki Międzyplatformowe NuGet](nuget-cross-platform-authentication-plugin.md)</span><span class="sxs-lookup"><span data-stu-id="a01cf-111">For credential providers in dotnet and msbuild see [NuGet cross platform plugins](nuget-cross-platform-authentication-plugin.md)</span></span>

## <a name="available-nuget-credential-providers-for-visual-studio"></a><span data-ttu-id="a01cf-112">Dostępni dostawcy poświadczeń NuGet dla programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a01cf-112">Available NuGet credential providers for Visual Studio</span></span>

<span data-ttu-id="a01cf-113">Istnieje Dostawca poświadczeń wbudowany w rozszerzenie NuGet programu Visual Studio w celu obsługi Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="a01cf-113">There is a credential provider built into the Visual Studio NuGet extension to support Visual Studio Team Services.</span></span>

<span data-ttu-id="a01cf-114">Rozszerzenie NuGet programu Visual Studio używa wewnętrznego `VsCredentialProviderImporter` , który również skanuje w poszukiwaniu dostawców poświadczeń wtyczki.</span><span class="sxs-lookup"><span data-stu-id="a01cf-114">The NuGet Visual Studio Extension uses an internal `VsCredentialProviderImporter` which also scans for plug-in credential providers.</span></span> <span data-ttu-id="a01cf-115">Te dostawcy poświadczeń wtyczki muszą być wykrywalne jako MEF eksportu typu `IVsCredentialProvider`.</span><span class="sxs-lookup"><span data-stu-id="a01cf-115">These plug-in credential providers must be discoverable as a MEF Export of type `IVsCredentialProvider`.</span></span>

<span data-ttu-id="a01cf-116">Dostępne są następujące dostawcy poświadczeń wtyczek:</span><span class="sxs-lookup"><span data-stu-id="a01cf-116">Available plug-in credential providers include:</span></span>

- [<span data-ttu-id="a01cf-117">Dostawca poświadczeń MyGet dla programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a01cf-117">MyGet Credential Provider for Visual Studio</span></span>](http://docs.myget.org/docs/reference/credential-provider-for-visual-studio)

## <a name="creating-a-nuget-credential-provider-for-visual-studio"></a><span data-ttu-id="a01cf-118">Tworzenie dostawcy poświadczeń NuGet dla programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a01cf-118">Creating a NuGet credential provider for Visual Studio</span></span>

<span data-ttu-id="a01cf-119">Pakiet NuGet Visual Studio Extension 3.6 + implementuje wewnętrzny CredentialService, który jest używany do pozyskiwania poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="a01cf-119">The NuGet Visual Studio Extension 3.6+ implements an internal CredentialService that is used to acquire credentials.</span></span> <span data-ttu-id="a01cf-120">CredentialService zawiera listę wbudowanych dostawców poświadczeń i wtyczek.</span><span class="sxs-lookup"><span data-stu-id="a01cf-120">The CredentialService has a list of built-in and plug-in credential providers.</span></span> <span data-ttu-id="a01cf-121">Każdy dostawca jest wybierany sekwencyjnie, dopóki nie zostaną nabyte poświadczenia.</span><span class="sxs-lookup"><span data-stu-id="a01cf-121">Each provider is tried sequentially until credentials are acquired.</span></span>

<span data-ttu-id="a01cf-122">Podczas pozyskiwania poświadczeń usługa Credential podejmie próbę dostawcy poświadczeń w następującej kolejności, zatrzymując się zaraz po pozyskaniu poświadczeń:</span><span class="sxs-lookup"><span data-stu-id="a01cf-122">During credential acquisition, the credential service will try credential providers in the following order, stopping as soon as credentials are acquired:</span></span>

1. <span data-ttu-id="a01cf-123">Poświadczenia będą pobierane z plików konfiguracji NuGet (przy użyciu wbudowanego `SettingsCredentialProvider`).</span><span class="sxs-lookup"><span data-stu-id="a01cf-123">Credentials will be fetched from NuGet configuration files (using the built-in `SettingsCredentialProvider`).</span></span>
1. <span data-ttu-id="a01cf-124">Jeśli źródło pakietu znajduje się na Visual Studio Team Services, `VisualStudioAccountProvider` będzie używane.</span><span class="sxs-lookup"><span data-stu-id="a01cf-124">If the package source is on Visual Studio Team Services, the `VisualStudioAccountProvider` will be used.</span></span>
1. <span data-ttu-id="a01cf-125">Wszystkie inne dostawcy poświadczeń programu Visual Studio są podejmowane sekwencyjnie.</span><span class="sxs-lookup"><span data-stu-id="a01cf-125">All other plug-in Visual Studio credential providers will be tried sequentially.</span></span>
1. <span data-ttu-id="a01cf-126">Spróbuj użyć wszystkich dostawców poświadczeń wielu platform NuGet sekwencyjnie.</span><span class="sxs-lookup"><span data-stu-id="a01cf-126">Try to use all NuGet cross platform credential providers sequentially.</span></span>
1. <span data-ttu-id="a01cf-127">Jeśli nie pobrano jeszcze poświadczeń, użytkownik zostanie poproszony o podanie poświadczeń przy użyciu standardowego okna dialogowego uwierzytelniania podstawowego.</span><span class="sxs-lookup"><span data-stu-id="a01cf-127">If no credentials have been acquired yet, the user will be prompted for credentials using a standard basic authentication dialog.</span></span>

### <a name="implementing-ivscredentialprovidergetcredentialsasync"></a><span data-ttu-id="a01cf-128">Implementing IVsCredentialProvider.GetCredentialsAsync</span><span class="sxs-lookup"><span data-stu-id="a01cf-128">Implementing IVsCredentialProvider.GetCredentialsAsync</span></span>

<span data-ttu-id="a01cf-129">Aby utworzyć dostawcę poświadczeń NuGet dla programu Visual Studio, Utwórz rozszerzenie programu Visual Studio, które ujawnia publiczny eksport MEF, który `IVsCredentialProvider` implementuje typ, i zgodnie z zasadami opisanymi poniżej.</span><span class="sxs-lookup"><span data-stu-id="a01cf-129">To create a NuGet credential provider for Visual Studio, create a Visual Studio Extension that exposes a public MEF Export implementing the `IVsCredentialProvider` type, and adheres to the principles outlined below.</span></span>

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

<span data-ttu-id="a01cf-130">Przykładową implementację można znaleźć w [przykładowej VsCredentialProvider](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span><span class="sxs-lookup"><span data-stu-id="a01cf-130">A sample implementation can be found in [the VsCredentialProvider sample](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span></span>

<span data-ttu-id="a01cf-131">Każdy dostawca poświadczeń NuGet dla programu Visual Studio musi:</span><span class="sxs-lookup"><span data-stu-id="a01cf-131">Each NuGet credential provider for Visual Studio must:</span></span>

1. <span data-ttu-id="a01cf-132">Przed zainicjowaniem pozyskiwania poświadczeń należy określić, czy może podać poświadczenia dla danego identyfikatora URI.</span><span class="sxs-lookup"><span data-stu-id="a01cf-132">Determine whether it can provide credentials for the targeted URI before initiating credential acquisition.</span></span> <span data-ttu-id="a01cf-133">Jeśli dostawca nie może dostarczyć poświadczeń dla źródłowego źródła, powinien zwrócić `null`.</span><span class="sxs-lookup"><span data-stu-id="a01cf-133">If the provider cannot supply credentials for the targeted source, then it should return `null`.</span></span>
1. <span data-ttu-id="a01cf-134">Jeśli dostawca obsługuje żądania dla danego identyfikatora URI, ale nie może dostarczyć poświadczeń, należy zgłaszać wyjątek.</span><span class="sxs-lookup"><span data-stu-id="a01cf-134">If the provider does handle requests for the targeted URI, but cannot supply credentials, an exception should be thrown.</span></span>

<span data-ttu-id="a01cf-135">Niestandardowy dostawca poświadczeń NuGet dla programu Visual Studio musi implementować `IVsCredentialProvider` interfejs dostępny w [pakiecie NuGet. VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/).</span><span class="sxs-lookup"><span data-stu-id="a01cf-135">A custom NuGet credential provider for Visual Studio must implement the `IVsCredentialProvider` interface available in the [NuGet.VisualStudio package](https://www.nuget.org/packages/NuGet.VisualStudio/).</span></span>

#### <a name="getcredentialasync"></a><span data-ttu-id="a01cf-136">GetCredentialAsync</span><span class="sxs-lookup"><span data-stu-id="a01cf-136">GetCredentialAsync</span></span>

| <span data-ttu-id="a01cf-137">Parametr wejściowy</span><span class="sxs-lookup"><span data-stu-id="a01cf-137">Input Parameter</span></span> |<span data-ttu-id="a01cf-138">Opis</span><span class="sxs-lookup"><span data-stu-id="a01cf-138">Description</span></span>|
| ----------------|-----------|
| <span data-ttu-id="a01cf-139">Identyfikator URI identyfikatora URI</span><span class="sxs-lookup"><span data-stu-id="a01cf-139">Uri uri</span></span> | <span data-ttu-id="a01cf-140">Identyfikator URI źródła pakietu, dla którego są wymagane poświadczenia.</span><span class="sxs-lookup"><span data-stu-id="a01cf-140">The package source Uri for which credentials are being requested.</span></span>|
| <span data-ttu-id="a01cf-141">IWebProxy serwer proxy</span><span class="sxs-lookup"><span data-stu-id="a01cf-141">IWebProxy proxy</span></span> | <span data-ttu-id="a01cf-142">Serwer proxy sieci Web, który ma być używany podczas komunikacji w sieci.</span><span class="sxs-lookup"><span data-stu-id="a01cf-142">Web proxy to use when communicating on the network.</span></span> <span data-ttu-id="a01cf-143">Wartość null, jeśli nie skonfigurowano uwierzytelniania serwera proxy.</span><span class="sxs-lookup"><span data-stu-id="a01cf-143">Null if there is no proxy authentication configured.</span></span> |
| <span data-ttu-id="a01cf-144">isProxyRequest bool</span><span class="sxs-lookup"><span data-stu-id="a01cf-144">bool isProxyRequest</span></span> | <span data-ttu-id="a01cf-145">Ma wartość true, jeśli to żądanie służy do uzyskiwania poświadczeń uwierzytelniania serwera proxy.</span><span class="sxs-lookup"><span data-stu-id="a01cf-145">True if this request is to get proxy authentication credentials.</span></span> <span data-ttu-id="a01cf-146">Jeśli implementacja nie jest prawidłowa do uzyskiwania poświadczeń serwera proxy, należy zwrócić wartość null.</span><span class="sxs-lookup"><span data-stu-id="a01cf-146">If the implementation is not valid for acquiring proxy credentials, then null should be returned.</span></span> |
| <span data-ttu-id="a01cf-147">isretry bool</span><span class="sxs-lookup"><span data-stu-id="a01cf-147">bool isRetry</span></span> | <span data-ttu-id="a01cf-148">Prawda, jeśli dla tego identyfikatora URI zażądano wcześniej poświadczeń, ale podane poświadczenia nie zezwalają na autoryzowany dostęp.</span><span class="sxs-lookup"><span data-stu-id="a01cf-148">True if credentials were previously requested for this Uri, but the supplied credentials did not allow authorized access.</span></span> |
| <span data-ttu-id="a01cf-149">bool nieinteraktywny</span><span class="sxs-lookup"><span data-stu-id="a01cf-149">bool nonInteractive</span></span> | <span data-ttu-id="a01cf-150">W przypadku opcji true Dostawca poświadczeń musi pominąć wszystkie monity użytkownika i zamiast tego użyć wartości domyślnych.</span><span class="sxs-lookup"><span data-stu-id="a01cf-150">If true, the credential provider must suppress all user prompts and use default values instead.</span></span> |
| <span data-ttu-id="a01cf-151">CancellationToken cancellationToken</span><span class="sxs-lookup"><span data-stu-id="a01cf-151">CancellationToken cancellationToken</span></span> | <span data-ttu-id="a01cf-152">Ten token anulowania powinien zostać sprawdzony w celu ustalenia, czy operacja żądająca poświadczeń została anulowana.</span><span class="sxs-lookup"><span data-stu-id="a01cf-152">This cancellation token should be checked to determine if the operation requesting credentials has been cancelled.</span></span> |

<span data-ttu-id="a01cf-153">**Wartość zwracana**: Obiekt poświadczeń implementujący [ `System.Net.ICredentials` interfejs](/dotnet/api/system.net.icredentials?view=netstandard-2.0).</span><span class="sxs-lookup"><span data-stu-id="a01cf-153">**Return value**: A credentials object implementing the [`System.Net.ICredentials` interface](/dotnet/api/system.net.icredentials?view=netstandard-2.0).</span></span>
