---
title: Dostawcy poświadczeń programu NuGet dla programu Visual Studio
description: Dostawcy poświadczeń NuGet uwierzytelniają się ze źródłami, implementując interfejs IVsCredentialProvider w rozszerzeniu programu Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: 13b6f5abe93a17c809564265990f86f6780aa67e
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/02/2020
ms.locfileid: "78230814"
---
# <a name="authenticating-feeds-in-visual-studio-with-nuget-credential-providers"></a><span data-ttu-id="0ea10-103">Uwierzytelnianie kanałów informacyjnych w programie Visual Studio przy użyciu dostawców poświadczeń NuGet</span><span class="sxs-lookup"><span data-stu-id="0ea10-103">Authenticating feeds in Visual Studio with NuGet credential providers</span></span>

<span data-ttu-id="0ea10-104">Rozszerzenie programu NuGet Visual Studio w wersji 3.6 + obsługuje dostawców poświadczeń, co umożliwia NuGet współpracują z uwierzytelnionymi źródłami danych.</span><span class="sxs-lookup"><span data-stu-id="0ea10-104">The NuGet Visual Studio Extension 3.6+ supports credential providers, which enable NuGet to work with authenticated feeds.</span></span>
<span data-ttu-id="0ea10-105">Po zainstalowaniu dostawcy poświadczeń programu NuGet dla programu Visual Studio rozszerzenie NuGet programu Visual Studio będzie automatycznie pobierać i odświeżać poświadczenia dla uwierzytelnionych źródeł w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="0ea10-105">After you install a NuGet credential provider for Visual Studio, the NuGet Visual Studio extension will automatically acquire and refresh credentials for authenticated feeds as necessary.</span></span>

<span data-ttu-id="0ea10-106">Przykładową implementację można znaleźć w [przykładowej VsCredentialProvider](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span><span class="sxs-lookup"><span data-stu-id="0ea10-106">A sample implementation can be found in [the VsCredentialProvider sample](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span></span>

<span data-ttu-id="0ea10-107">W programie Visual Studio NuGet używa wewnętrznego `VsCredentialProviderImporter`, który również skanuje w poszukiwaniu dostawców poświadczeń wtyczki.</span><span class="sxs-lookup"><span data-stu-id="0ea10-107">Within Visual Studio, NuGet uses an internal `VsCredentialProviderImporter` which also scans for plug-in credential providers.</span></span> <span data-ttu-id="0ea10-108">Te dostawcy poświadczeń wtyczki muszą być wykrywalne jako MEF eksportu typu `IVsCredentialProvider`.</span><span class="sxs-lookup"><span data-stu-id="0ea10-108">These plug-in credential providers must be discoverable as a MEF Export of type `IVsCredentialProvider`.</span></span>

<span data-ttu-id="0ea10-109">Począwszy od 4.8 + NuGet w programie Visual Studio obsługuje również nowe wtyczki do uwierzytelniania międzyplatformowego, ale nie są to zalecane podejście ze względu na wydajność.</span><span class="sxs-lookup"><span data-stu-id="0ea10-109">Starting with 4.8+ NuGet in Visual Studio supports the new cross platform authentication plugins as well, but they are not the recommended approach for performance reasons.</span></span>

> [!Note]
> <span data-ttu-id="0ea10-110">Dostawcy poświadczeń NuGet dla programu Visual Studio muszą być instalowani jako zwykłe rozszerzenie programu Visual Studio i wymagać [programu Visual studio 2017](https://aka.ms/vs/15/release/vs_enterprise.exe) lub nowszego.</span><span class="sxs-lookup"><span data-stu-id="0ea10-110">NuGet credential providers for Visual Studio must be installed as a regular Visual Studio extension and will require [Visual Studio 2017](https://aka.ms/vs/15/release/vs_enterprise.exe) or above.</span></span>
>
> <span data-ttu-id="0ea10-111">Dostawcy poświadczeń NuGet dla programu Visual Studio działają tylko w programie Visual Studio (nie w dotnet restore lub NuGet. exe).</span><span class="sxs-lookup"><span data-stu-id="0ea10-111">NuGet credential providers for Visual Studio work only in Visual Studio (not in dotnet restore or nuget.exe).</span></span> <span data-ttu-id="0ea10-112">W przypadku dostawców poświadczeń z pakietem NuGet. exe zobacz [dostawcy poświadczeń NuGet. exe](nuget-exe-Credential-providers.md).</span><span class="sxs-lookup"><span data-stu-id="0ea10-112">For credential providers with nuget.exe, see [nuget.exe Credential Providers](nuget-exe-Credential-providers.md).</span></span>
> <span data-ttu-id="0ea10-113">Dla dostawców poświadczeń w programie dotnet i MSBuild zobacz [wtyczki Międzyplatformowe NuGet](nuget-cross-platform-authentication-plugin.md)</span><span class="sxs-lookup"><span data-stu-id="0ea10-113">For credential providers in dotnet and msbuild see [NuGet cross platform plugins](nuget-cross-platform-authentication-plugin.md)</span></span>

## <a name="creating-a-nuget-credential-provider-for-visual-studio"></a><span data-ttu-id="0ea10-114">Tworzenie dostawcy poświadczeń NuGet dla programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="0ea10-114">Creating a NuGet credential provider for Visual Studio</span></span>

<span data-ttu-id="0ea10-115">Pakiet NuGet Visual Studio Extension 3.6 + implementuje wewnętrzny CredentialService, który jest używany do pozyskiwania poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="0ea10-115">The NuGet Visual Studio Extension 3.6+ implements an internal CredentialService that is used to acquire credentials.</span></span> <span data-ttu-id="0ea10-116">CredentialService zawiera listę wbudowanych dostawców poświadczeń i wtyczek.</span><span class="sxs-lookup"><span data-stu-id="0ea10-116">The CredentialService has a list of built-in and plug-in credential providers.</span></span> <span data-ttu-id="0ea10-117">Każdy dostawca jest wybierany sekwencyjnie, dopóki nie zostaną nabyte poświadczenia.</span><span class="sxs-lookup"><span data-stu-id="0ea10-117">Each provider is tried sequentially until credentials are acquired.</span></span>

<span data-ttu-id="0ea10-118">Podczas pozyskiwania poświadczeń usługa Credential podejmie próbę dostawcy poświadczeń w następującej kolejności, zatrzymując się zaraz po pozyskaniu poświadczeń:</span><span class="sxs-lookup"><span data-stu-id="0ea10-118">During credential acquisition, the credential service will try credential providers in the following order, stopping as soon as credentials are acquired:</span></span>

1. <span data-ttu-id="0ea10-119">Poświadczenia będą pobierane z plików konfiguracji NuGet (przy użyciu wbudowanego `SettingsCredentialProvider`).</span><span class="sxs-lookup"><span data-stu-id="0ea10-119">Credentials will be fetched from NuGet configuration files (using the built-in `SettingsCredentialProvider`).</span></span>
1. <span data-ttu-id="0ea10-120">Jeśli źródło pakietu znajduje się na Visual Studio Team Services, zostanie użyta `VisualStudioAccountProvider`.</span><span class="sxs-lookup"><span data-stu-id="0ea10-120">If the package source is on Visual Studio Team Services, the `VisualStudioAccountProvider` will be used.</span></span>
1. <span data-ttu-id="0ea10-121">Wszystkie inne dostawcy poświadczeń programu Visual Studio są podejmowane sekwencyjnie.</span><span class="sxs-lookup"><span data-stu-id="0ea10-121">All other plug-in Visual Studio credential providers will be tried sequentially.</span></span>
1. <span data-ttu-id="0ea10-122">Spróbuj użyć wszystkich dostawców poświadczeń wielu platform NuGet sekwencyjnie.</span><span class="sxs-lookup"><span data-stu-id="0ea10-122">Try to use all NuGet cross platform credential providers sequentially.</span></span>
1. <span data-ttu-id="0ea10-123">Jeśli nie pobrano jeszcze poświadczeń, użytkownik zostanie poproszony o podanie poświadczeń przy użyciu standardowego okna dialogowego uwierzytelniania podstawowego.</span><span class="sxs-lookup"><span data-stu-id="0ea10-123">If no credentials have been acquired yet, the user will be prompted for credentials using a standard basic authentication dialog.</span></span>

### <a name="implementing-ivscredentialprovidergetcredentialsasync"></a><span data-ttu-id="0ea10-124">Implementing IVsCredentialProvider.GetCredentialsAsync</span><span class="sxs-lookup"><span data-stu-id="0ea10-124">Implementing IVsCredentialProvider.GetCredentialsAsync</span></span>

<span data-ttu-id="0ea10-125">Aby utworzyć dostawcę poświadczeń NuGet dla programu Visual Studio, Utwórz rozszerzenie programu Visual Studio, które ujawnia publiczny eksport MEF implementujący typ `IVsCredentialProvider` i zgodnie z zasadami opisanymi poniżej.</span><span class="sxs-lookup"><span data-stu-id="0ea10-125">To create a NuGet credential provider for Visual Studio, create a Visual Studio Extension that exposes a public MEF Export implementing the `IVsCredentialProvider` type, and adheres to the principles outlined below.</span></span>

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

<span data-ttu-id="0ea10-126">Przykładową implementację można znaleźć w [przykładowej VsCredentialProvider](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span><span class="sxs-lookup"><span data-stu-id="0ea10-126">A sample implementation can be found in [the VsCredentialProvider sample](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span></span>

<span data-ttu-id="0ea10-127">Każdy dostawca poświadczeń NuGet dla programu Visual Studio musi:</span><span class="sxs-lookup"><span data-stu-id="0ea10-127">Each NuGet credential provider for Visual Studio must:</span></span>

1. <span data-ttu-id="0ea10-128">Przed zainicjowaniem pozyskiwania poświadczeń należy określić, czy może podać poświadczenia dla danego identyfikatora URI.</span><span class="sxs-lookup"><span data-stu-id="0ea10-128">Determine whether it can provide credentials for the targeted URI before initiating credential acquisition.</span></span> <span data-ttu-id="0ea10-129">Jeśli dostawca nie może dostarczyć poświadczeń dla źródłowego źródła, powinien zwrócić `null`.</span><span class="sxs-lookup"><span data-stu-id="0ea10-129">If the provider cannot supply credentials for the targeted source, then it should return `null`.</span></span>
1. <span data-ttu-id="0ea10-130">Jeśli dostawca obsługuje żądania dla danego identyfikatora URI, ale nie może dostarczyć poświadczeń, należy zgłaszać wyjątek.</span><span class="sxs-lookup"><span data-stu-id="0ea10-130">If the provider does handle requests for the targeted URI, but cannot supply credentials, an exception should be thrown.</span></span>

<span data-ttu-id="0ea10-131">Niestandardowy dostawca poświadczeń NuGet dla programu Visual Studio musi implementować interfejs `IVsCredentialProvider` dostępny w [pakiecie NuGet. VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/).</span><span class="sxs-lookup"><span data-stu-id="0ea10-131">A custom NuGet credential provider for Visual Studio must implement the `IVsCredentialProvider` interface available in the [NuGet.VisualStudio package](https://www.nuget.org/packages/NuGet.VisualStudio/).</span></span>

#### <a name="getcredentialasync"></a><span data-ttu-id="0ea10-132">GetCredentialAsync</span><span class="sxs-lookup"><span data-stu-id="0ea10-132">GetCredentialAsync</span></span>

| <span data-ttu-id="0ea10-133">Parametr wejściowy</span><span class="sxs-lookup"><span data-stu-id="0ea10-133">Input Parameter</span></span> |<span data-ttu-id="0ea10-134">Opis</span><span class="sxs-lookup"><span data-stu-id="0ea10-134">Description</span></span>|
| ----------------|-----------|
| <span data-ttu-id="0ea10-135">Identyfikator URI identyfikatora URI</span><span class="sxs-lookup"><span data-stu-id="0ea10-135">Uri uri</span></span> | <span data-ttu-id="0ea10-136">Identyfikator URI źródła pakietu, dla którego są wymagane poświadczenia.</span><span class="sxs-lookup"><span data-stu-id="0ea10-136">The package source Uri for which credentials are being requested.</span></span>|
| <span data-ttu-id="0ea10-137">IWebProxy serwer proxy</span><span class="sxs-lookup"><span data-stu-id="0ea10-137">IWebProxy proxy</span></span> | <span data-ttu-id="0ea10-138">Serwer proxy sieci Web, który ma być używany podczas komunikacji w sieci.</span><span class="sxs-lookup"><span data-stu-id="0ea10-138">Web proxy to use when communicating on the network.</span></span> <span data-ttu-id="0ea10-139">Wartość null, jeśli nie skonfigurowano uwierzytelniania serwera proxy.</span><span class="sxs-lookup"><span data-stu-id="0ea10-139">Null if there is no proxy authentication configured.</span></span> |
| <span data-ttu-id="0ea10-140">isProxyRequest bool</span><span class="sxs-lookup"><span data-stu-id="0ea10-140">bool isProxyRequest</span></span> | <span data-ttu-id="0ea10-141">Ma wartość true, jeśli to żądanie służy do uzyskiwania poświadczeń uwierzytelniania serwera proxy.</span><span class="sxs-lookup"><span data-stu-id="0ea10-141">True if this request is to get proxy authentication credentials.</span></span> <span data-ttu-id="0ea10-142">Jeśli implementacja nie jest prawidłowa do uzyskiwania poświadczeń serwera proxy, należy zwrócić wartość null.</span><span class="sxs-lookup"><span data-stu-id="0ea10-142">If the implementation is not valid for acquiring proxy credentials, then null should be returned.</span></span> |
| <span data-ttu-id="0ea10-143">isretry bool</span><span class="sxs-lookup"><span data-stu-id="0ea10-143">bool isRetry</span></span> | <span data-ttu-id="0ea10-144">Prawda, jeśli dla tego identyfikatora URI zażądano wcześniej poświadczeń, ale podane poświadczenia nie zezwalają na autoryzowany dostęp.</span><span class="sxs-lookup"><span data-stu-id="0ea10-144">True if credentials were previously requested for this Uri, but the supplied credentials did not allow authorized access.</span></span> |
| <span data-ttu-id="0ea10-145">bool nieinteraktywny</span><span class="sxs-lookup"><span data-stu-id="0ea10-145">bool nonInteractive</span></span> | <span data-ttu-id="0ea10-146">W przypadku opcji true Dostawca poświadczeń musi pominąć wszystkie monity użytkownika i zamiast tego użyć wartości domyślnych.</span><span class="sxs-lookup"><span data-stu-id="0ea10-146">If true, the credential provider must suppress all user prompts and use default values instead.</span></span> |
| <span data-ttu-id="0ea10-147">CancellationToken cancellationToken</span><span class="sxs-lookup"><span data-stu-id="0ea10-147">CancellationToken cancellationToken</span></span> | <span data-ttu-id="0ea10-148">Ten token anulowania powinien zostać sprawdzony w celu ustalenia, czy operacja żądająca poświadczeń została anulowana.</span><span class="sxs-lookup"><span data-stu-id="0ea10-148">This cancellation token should be checked to determine if the operation requesting credentials has been cancelled.</span></span> |

<span data-ttu-id="0ea10-149">**Wartość zwracana**: obiekt poświadczeń implementujący [interfejs`System.Net.ICredentials`](/dotnet/api/system.net.icredentials?view=netstandard-2.0).</span><span class="sxs-lookup"><span data-stu-id="0ea10-149">**Return value**: A credentials object implementing the [`System.Net.ICredentials` interface](/dotnet/api/system.net.icredentials?view=netstandard-2.0).</span></span>
