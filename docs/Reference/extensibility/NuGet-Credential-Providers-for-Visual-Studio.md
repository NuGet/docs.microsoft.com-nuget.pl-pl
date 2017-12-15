---
title: "Dostawcy poświadczeń NuGet dla programu Visual Studio | Dokumentacja firmy Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 1/9/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 9c7f6d16-f437-47c4-82d4-6c996e0b18ec
description: "NuGet dostawcy poświadczeń uwierzytelniania za pomocą źródła zaimplementowanie interfejsu IVsCredentialProvider rozszerzenia programu Visual Studio."
keywords: "Dostawcy poświadczeń NuGet, uwierzytelniania za pomocą kanału informacyjnego, uwierzytelniania za pomocą galerii NuGet rozszerzenie programu visual studio"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 2b2fac23102865a08509acc1cc3d09f0cd375f26
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/14/2017
---
# <a name="authenticating-feeds-in-visual-studio-with-nuget-credential-providers"></a><span data-ttu-id="b0ae4-104">Źródła danych w programie Visual Studio za pomocą NuGet dostawcy poświadczeń uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="b0ae4-104">Authenticating feeds in Visual Studio with NuGet credential providers</span></span>

<span data-ttu-id="b0ae4-105">NuGet programu Visual Studio rozszerzenia 3,6 + obsługuje dostawcy poświadczeń, umożliwiające NuGet do pracy z uwierzytelnionego źródeł danych.</span><span class="sxs-lookup"><span data-stu-id="b0ae4-105">The NuGet Visual Studio Extension 3.6+ supports credential providers, which enable NuGet to work with authenticated feeds.</span></span>
<span data-ttu-id="b0ae4-106">Po zainstalowaniu dostawcy poświadczeń NuGet dla programu Visual Studio, rozszerzenie NuGet dla programu Visual Studio automatycznie uzyskać i odświeżyć poświadczenia dla źródeł uwierzytelnionych w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="b0ae4-106">After you install a NuGet credential provider for Visual Studio, the NuGet Visual Studio extension will automatically acquire and refresh credentials for authenticated feeds as necessary.</span></span>

<span data-ttu-id="b0ae4-107">Przykładowe zastosowanie znajdują się w [próbki VsCredentialProvider](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span><span class="sxs-lookup"><span data-stu-id="b0ae4-107">A sample implementation can be found in [the VsCredentialProvider sample](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span></span>

> [!Note]
> <span data-ttu-id="b0ae4-108">Dostawcy poświadczeń NuGet dla programu Visual Studio musi zostać zainstalowana jako prawidłowe rozszerzenie programu Visual Studio i będzie wymagać [programu Visual Studio 2017](https://aka.ms/vs/15/preview/vs_enterprise) (obecnie w wersji zapoznawczej) lub nowszy.</span><span class="sxs-lookup"><span data-stu-id="b0ae4-108">NuGet credential providers for Visual Studio must be installed as a regular Visual Studio extension and will require [Visual Studio 2017](https://aka.ms/vs/15/preview/vs_enterprise) (currently in preview) or above.</span></span>
>
> <span data-ttu-id="b0ae4-109">Dostawcy poświadczeń NuGet dla programu Visual Studio działa tylko w programie Visual Studio (nie w przywracania dotnet lub nuget.exe).</span><span class="sxs-lookup"><span data-stu-id="b0ae4-109">NuGet credential providers for Visual Studio work only in Visual Studio (not in dotnet restore or nuget.exe).</span></span> <span data-ttu-id="b0ae4-110">Dla dostawcy poświadczeń z nuget.exe, zobacz [nuget.exe dostawcy poświadczeń](nuget-exe-Credential-providers.md).</span><span class="sxs-lookup"><span data-stu-id="b0ae4-110">For credential providers with nuget.exe, see [nuget.exe Credential Providers](nuget-exe-Credential-providers.md).</span></span>

## <a name="available-nuget-credential-providers-for-visual-studio"></a><span data-ttu-id="b0ae4-111">Dostępne dostawcy poświadczeń NuGet dla programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="b0ae4-111">Available NuGet credential providers for Visual Studio</span></span>

<span data-ttu-id="b0ae4-112">Brak dostawcy poświadczeń wbudowane rozszerzenia programu Visual Studio NuGet do obsługi programu Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="b0ae4-112">There is a credential provider built into the Visual Studio NuGet extension to support Visual Studio Team Services.</span></span>

<span data-ttu-id="b0ae4-113">Rozszerzenia NuGet programu Visual Studio korzysta z wewnętrznego `VsCredentialProviderImporter` powoduje skanowanie dla dostawcy poświadczeń wtyczki.</span><span class="sxs-lookup"><span data-stu-id="b0ae4-113">The NuGet Visual Studio Extension uses an internal `VsCredentialProviderImporter` which also scans for plug-in credential providers.</span></span> <span data-ttu-id="b0ae4-114">Dostawcy te wtyczka poświadczeń musi być wykrywalny jako eksportu MEF typu `IVsCredentialProvider`.</span><span class="sxs-lookup"><span data-stu-id="b0ae4-114">These plug-in credential providers must be discoverable as a MEF Export of type `IVsCredentialProvider`.</span></span>

<span data-ttu-id="b0ae4-115">Dostawcy poświadczeń wtyczki dostępne są następujące:</span><span class="sxs-lookup"><span data-stu-id="b0ae4-115">Available plug-in credential providers include:</span></span>

- [<span data-ttu-id="b0ae4-116">MyGet Credential Provider for Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="b0ae4-116">MyGet Credential Provider for Visual Studio 2017</span></span>](http://docs.myget.org/docs/reference/credential-provider-for-visual-studio)

## <a name="creating-a-nuget-credential-provider-for-visual-studio"></a><span data-ttu-id="b0ae4-117">Tworzenie dostawcy poświadczeń NuGet dla programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="b0ae4-117">Creating a NuGet credential provider for Visual Studio</span></span>

<span data-ttu-id="b0ae4-118">NuGet programu Visual Studio rozszerzenia 3,6 + implementuje wewnętrzny CredentialService, który jest używany w celu uzyskania poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="b0ae4-118">The NuGet Visual Studio Extension 3.6+ implements an internal CredentialService that is used to acquire credentials.</span></span> <span data-ttu-id="b0ae4-119">CredentialService zawiera listę dostawców wbudowanych i wtyczki poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="b0ae4-119">The CredentialService has a list of built-in and plug-in credential providers.</span></span> <span data-ttu-id="b0ae4-120">Każdy dostawca sprawdzane są sekwencyjnie, aż do drogą kupna poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="b0ae4-120">Each provider is tried sequentially until credentials are acquired.</span></span>

<span data-ttu-id="b0ae4-121">Podczas przejęcia poświadczeń usługa poświadczeń spróbuje dostawcy poświadczeń w następującej kolejności, zatrzymywanie, jak poświadczenia są nabywane:</span><span class="sxs-lookup"><span data-stu-id="b0ae4-121">During credential acquisition, the credential service will try credential providers in the following order, stopping as soon as credentials are acquired:</span></span>

1. <span data-ttu-id="b0ae4-122">Poświadczenia będą pobierane z plików konfiguracyjnych NuGet (przy użyciu wbudowanych `SettingsCredentialProvider`).</span><span class="sxs-lookup"><span data-stu-id="b0ae4-122">Credentials will be fetched from NuGet configuration files (using the built-in `SettingsCredentialProvider`).</span></span>
1. <span data-ttu-id="b0ae4-123">Jeśli źródło pakietu znajduje się w Visual Studio Team Services `VisualStudioAccountProvider` będą używane.</span><span class="sxs-lookup"><span data-stu-id="b0ae4-123">If the package source is on Visual Studio Team Services, the `VisualStudioAccountProvider` will be used.</span></span>
1. <span data-ttu-id="b0ae4-124">Wszyscy inni dostawcy poświadczeń wtyczki zostaną sprawdzone po kolei.</span><span class="sxs-lookup"><span data-stu-id="b0ae4-124">All other plug-in credential providers will be tried sequentially.</span></span>
1. <span data-ttu-id="b0ae4-125">Jeśli żadne poświadczenia nie zostały nabyte jeszcze, użytkownik będzie monitowany o poświadczenia, za pomocą okna dialogowego standardowe uwierzytelnianie podstawowe.</span><span class="sxs-lookup"><span data-stu-id="b0ae4-125">If no credentials have been acquired yet, the user will be prompted for credentials using a standard basic authentication dialog.</span></span>

### <a name="implementing-ivscredentialprovidergetcredentialsasync"></a><span data-ttu-id="b0ae4-126">Implementowanie IVsCredentialProvider.GetCredentialsAsync</span><span class="sxs-lookup"><span data-stu-id="b0ae4-126">Implementing IVsCredentialProvider.GetCredentialsAsync</span></span>

<span data-ttu-id="b0ae4-127">Aby utworzyć dostawcę poświadczeń NuGet dla programu Visual Studio, utworzyć rozszerzenie Visual Studio, które udostępnia publiczne eksportu MEF implementacja `IVsCredentialProvider` wpisz i stosuje zasady opisane poniżej.</span><span class="sxs-lookup"><span data-stu-id="b0ae4-127">To create a NuGet credential provider for Visual Studio, create a Visual Studio Extension that exposes a public MEF Export implementing the `IVsCredentialProvider` type, and adheres to the principles outlined below.</span></span>

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

<span data-ttu-id="b0ae4-128">Przykładowe zastosowanie znajdują się w [próbki VsCredentialProvider](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span><span class="sxs-lookup"><span data-stu-id="b0ae4-128">A sample implementation can be found in [the VsCredentialProvider sample](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span></span>

<span data-ttu-id="b0ae4-129">Każdy dostawca poświadczeń NuGet dla programu Visual Studio musi:</span><span class="sxs-lookup"><span data-stu-id="b0ae4-129">Each NuGet credential provider for Visual Studio must:</span></span>

1. <span data-ttu-id="b0ae4-130">Ustal, czy jego Podaj poświadczenia dla docelowego identyfikatora URI przed zainicjowaniem przejęcie poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="b0ae4-130">Determine whether it can provide credentials for the targeted URI before initiating credential acquisition.</span></span> <span data-ttu-id="b0ae4-131">Jeśli dostawca nie może dostarczyć poświadczenia dla źródła docelowych, powinien on zwrócić `null`.</span><span class="sxs-lookup"><span data-stu-id="b0ae4-131">If the provider cannot supply credentials for the targeted source, then it should return `null`.</span></span>
1. <span data-ttu-id="b0ae4-132">Jeśli dostawca obsługuje żądania dla docelowego identyfikatora URI, ale nie można podać poświadczenia, powinny być wyjątek.</span><span class="sxs-lookup"><span data-stu-id="b0ae4-132">If the provider does handle requests for the targeted URI, but cannot supply credentials, an exception should be thrown.</span></span>

<span data-ttu-id="b0ae4-133">Niestandardowy Dostawca poświadczeń NuGet dla programu Visual Studio musi implementować `IVsCredentialProvider` dostępne w interfejsie [pakietu NuGet.VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/).</span><span class="sxs-lookup"><span data-stu-id="b0ae4-133">A custom NuGet credential provider for Visual Studio must implement the `IVsCredentialProvider` interface available in the [NuGet.VisualStudio package](https://www.nuget.org/packages/NuGet.VisualStudio/).</span></span>

#### <a name="getcredentialasync"></a><span data-ttu-id="b0ae4-134">GetCredentialAsync</span><span class="sxs-lookup"><span data-stu-id="b0ae4-134">GetCredentialAsync</span></span>

| <span data-ttu-id="b0ae4-135">Parametr wejściowy</span><span class="sxs-lookup"><span data-stu-id="b0ae4-135">Input Parameter</span></span> |<span data-ttu-id="b0ae4-136">Opis</span><span class="sxs-lookup"><span data-stu-id="b0ae4-136">Description</span></span>|
| ----------------|-----------|
| <span data-ttu-id="b0ae4-137">Identyfikator uri identyfikatora URI</span><span class="sxs-lookup"><span data-stu-id="b0ae4-137">Uri uri</span></span> | <span data-ttu-id="b0ae4-138">Źródło pakietu Uri, dla których wymagane są poświadczenia.</span><span class="sxs-lookup"><span data-stu-id="b0ae4-138">The package source Uri for which credentials are being requested.</span></span>|
| <span data-ttu-id="b0ae4-139">IWebProxy serwera proxy</span><span class="sxs-lookup"><span data-stu-id="b0ae4-139">IWebProxy proxy</span></span> | <span data-ttu-id="b0ae4-140">Serwer proxy sieci Web do użycia przy komunikacji w sieci.</span><span class="sxs-lookup"><span data-stu-id="b0ae4-140">Web proxy to use when communicating on the network.</span></span> <span data-ttu-id="b0ae4-141">Wartość null, jeśli uwierzytelnianie nie jest serwer proxy skonfigurowane.</span><span class="sxs-lookup"><span data-stu-id="b0ae4-141">Null if there is no proxy authentication configured.</span></span> |
| <span data-ttu-id="b0ae4-142">wartość logiczna isProxyRequest</span><span class="sxs-lookup"><span data-stu-id="b0ae4-142">bool isProxyRequest</span></span> | <span data-ttu-id="b0ae4-143">Wartość true, jeśli żądanie jest uzyskanie poświadczeń uwierzytelniania serwera proxy.</span><span class="sxs-lookup"><span data-stu-id="b0ae4-143">True if this request is to get proxy authentication credentials.</span></span> <span data-ttu-id="b0ae4-144">Jeśli wdrożenia jest nieprawidłowa dla pobierania poświadczeń serwera proxy, powinna zostać zwrócona wartość null.</span><span class="sxs-lookup"><span data-stu-id="b0ae4-144">If the implementation is not valid for acquiring proxy credentials, then null should be returned.</span></span> |
| <span data-ttu-id="b0ae4-145">wartość logiczna isRetry</span><span class="sxs-lookup"><span data-stu-id="b0ae4-145">bool isRetry</span></span> | <span data-ttu-id="b0ae4-146">Wartość true, jeśli poświadczenia zostały wcześniej żądał dla tego identyfikatora Uri, ale podane poświadczenia nie zezwala na dostęp do autoryzowanych.</span><span class="sxs-lookup"><span data-stu-id="b0ae4-146">True if credentials were previously requested for this Uri, but the supplied credentials did not allow authorized access.</span></span> |
| <span data-ttu-id="b0ae4-147">wartość logiczna nieinterakcyjne</span><span class="sxs-lookup"><span data-stu-id="b0ae4-147">bool nonInteractive</span></span> | <span data-ttu-id="b0ae4-148">Jeśli PRAWDA, Dostawca poświadczeń należy pominąć wszystkie monity użytkownika i zamiast tego użyj wartości domyślnych.</span><span class="sxs-lookup"><span data-stu-id="b0ae4-148">If true, the credential provider must suppress all user prompts and use default values instead.</span></span> |
| <span data-ttu-id="b0ae4-149">CancellationToken cancellationToken</span><span class="sxs-lookup"><span data-stu-id="b0ae4-149">CancellationToken cancellationToken</span></span> | <span data-ttu-id="b0ae4-150">Ten token anulowania powinny być sprawdzane w celu ustalenia, jeśli poświadczenia żądania operacja została anulowana.</span><span class="sxs-lookup"><span data-stu-id="b0ae4-150">This cancellation token should be checked to determine if the operation requesting credentials has been cancelled.</span></span> |
  
<span data-ttu-id="b0ae4-151">**Wartość zwracana**: implementacja obiektu poświadczeń [ `System.Net.ICredentials` interfejsu](https://msdn.microsoft.com/library/system.net.icredentials.aspx).</span><span class="sxs-lookup"><span data-stu-id="b0ae4-151">**Return value**: A credentials object implementing the [`System.Net.ICredentials` interface](https://msdn.microsoft.com/library/system.net.icredentials.aspx).</span></span>
