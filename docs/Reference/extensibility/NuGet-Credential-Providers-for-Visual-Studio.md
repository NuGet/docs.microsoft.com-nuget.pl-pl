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
# <a name="authenticating-feeds-in-visual-studio-with-nuget-credential-providers"></a><span data-ttu-id="1f96f-103">Źródła danych w programie Visual Studio za pomocą NuGet dostawcy poświadczeń uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="1f96f-103">Authenticating feeds in Visual Studio with NuGet credential providers</span></span>

<span data-ttu-id="1f96f-104">NuGet programu Visual Studio rozszerzenia 3,6 + obsługuje dostawcy poświadczeń, umożliwiające NuGet do pracy z uwierzytelnionego źródeł danych.</span><span class="sxs-lookup"><span data-stu-id="1f96f-104">The NuGet Visual Studio Extension 3.6+ supports credential providers, which enable NuGet to work with authenticated feeds.</span></span>
<span data-ttu-id="1f96f-105">Po zainstalowaniu dostawcy poświadczeń NuGet dla programu Visual Studio, rozszerzenie NuGet dla programu Visual Studio automatycznie uzyskać i odświeżyć poświadczenia dla źródeł uwierzytelnionych w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="1f96f-105">After you install a NuGet credential provider for Visual Studio, the NuGet Visual Studio extension will automatically acquire and refresh credentials for authenticated feeds as necessary.</span></span>

<span data-ttu-id="1f96f-106">Przykładowe zastosowanie znajdują się w [próbki VsCredentialProvider](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span><span class="sxs-lookup"><span data-stu-id="1f96f-106">A sample implementation can be found in [the VsCredentialProvider sample](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span></span>

> [!Note]
> <span data-ttu-id="1f96f-107">Dostawcy poświadczeń NuGet dla programu Visual Studio musi zostać zainstalowana jako prawidłowe rozszerzenie programu Visual Studio i będzie wymagać [programu Visual Studio 2017](https://aka.ms/vs/15/preview/vs_enterprise) (obecnie w wersji zapoznawczej) lub nowszy.</span><span class="sxs-lookup"><span data-stu-id="1f96f-107">NuGet credential providers for Visual Studio must be installed as a regular Visual Studio extension and will require [Visual Studio 2017](https://aka.ms/vs/15/preview/vs_enterprise) (currently in preview) or above.</span></span>
>
> <span data-ttu-id="1f96f-108">Dostawcy poświadczeń NuGet dla programu Visual Studio działa tylko w programie Visual Studio (nie w przywracania dotnet lub nuget.exe).</span><span class="sxs-lookup"><span data-stu-id="1f96f-108">NuGet credential providers for Visual Studio work only in Visual Studio (not in dotnet restore or nuget.exe).</span></span> <span data-ttu-id="1f96f-109">Dla dostawcy poświadczeń z nuget.exe, zobacz [nuget.exe dostawcy poświadczeń](nuget-exe-Credential-providers.md).</span><span class="sxs-lookup"><span data-stu-id="1f96f-109">For credential providers with nuget.exe, see [nuget.exe Credential Providers](nuget-exe-Credential-providers.md).</span></span>

## <a name="available-nuget-credential-providers-for-visual-studio"></a><span data-ttu-id="1f96f-110">Dostępne dostawcy poświadczeń NuGet dla programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1f96f-110">Available NuGet credential providers for Visual Studio</span></span>

<span data-ttu-id="1f96f-111">Brak dostawcy poświadczeń wbudowane rozszerzenia programu Visual Studio NuGet do obsługi programu Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="1f96f-111">There is a credential provider built into the Visual Studio NuGet extension to support Visual Studio Team Services.</span></span>

<span data-ttu-id="1f96f-112">Rozszerzenia NuGet programu Visual Studio korzysta z wewnętrznego `VsCredentialProviderImporter` powoduje skanowanie dla dostawcy poświadczeń wtyczki.</span><span class="sxs-lookup"><span data-stu-id="1f96f-112">The NuGet Visual Studio Extension uses an internal `VsCredentialProviderImporter` which also scans for plug-in credential providers.</span></span> <span data-ttu-id="1f96f-113">Dostawcy te wtyczka poświadczeń musi być wykrywalny jako eksportu MEF typu `IVsCredentialProvider`.</span><span class="sxs-lookup"><span data-stu-id="1f96f-113">These plug-in credential providers must be discoverable as a MEF Export of type `IVsCredentialProvider`.</span></span>

<span data-ttu-id="1f96f-114">Dostawcy poświadczeń wtyczki dostępne są następujące:</span><span class="sxs-lookup"><span data-stu-id="1f96f-114">Available plug-in credential providers include:</span></span>

- [<span data-ttu-id="1f96f-115">MyGet Credential Provider for Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="1f96f-115">MyGet Credential Provider for Visual Studio 2017</span></span>](http://docs.myget.org/docs/reference/credential-provider-for-visual-studio)

## <a name="creating-a-nuget-credential-provider-for-visual-studio"></a><span data-ttu-id="1f96f-116">Tworzenie dostawcy poświadczeń NuGet dla programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1f96f-116">Creating a NuGet credential provider for Visual Studio</span></span>

<span data-ttu-id="1f96f-117">NuGet programu Visual Studio rozszerzenia 3,6 + implementuje wewnętrzny CredentialService, który jest używany w celu uzyskania poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="1f96f-117">The NuGet Visual Studio Extension 3.6+ implements an internal CredentialService that is used to acquire credentials.</span></span> <span data-ttu-id="1f96f-118">CredentialService zawiera listę dostawców wbudowanych i wtyczki poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="1f96f-118">The CredentialService has a list of built-in and plug-in credential providers.</span></span> <span data-ttu-id="1f96f-119">Każdy dostawca sprawdzane są sekwencyjnie, aż do drogą kupna poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="1f96f-119">Each provider is tried sequentially until credentials are acquired.</span></span>

<span data-ttu-id="1f96f-120">Podczas przejęcia poświadczeń usługa poświadczeń spróbuje dostawcy poświadczeń w następującej kolejności, zatrzymywanie, jak poświadczenia są nabywane:</span><span class="sxs-lookup"><span data-stu-id="1f96f-120">During credential acquisition, the credential service will try credential providers in the following order, stopping as soon as credentials are acquired:</span></span>

1. <span data-ttu-id="1f96f-121">Poświadczenia będą pobierane z plików konfiguracyjnych NuGet (przy użyciu wbudowanych `SettingsCredentialProvider`).</span><span class="sxs-lookup"><span data-stu-id="1f96f-121">Credentials will be fetched from NuGet configuration files (using the built-in `SettingsCredentialProvider`).</span></span>
1. <span data-ttu-id="1f96f-122">Jeśli źródło pakietu znajduje się w Visual Studio Team Services `VisualStudioAccountProvider` będą używane.</span><span class="sxs-lookup"><span data-stu-id="1f96f-122">If the package source is on Visual Studio Team Services, the `VisualStudioAccountProvider` will be used.</span></span>
1. <span data-ttu-id="1f96f-123">Wszyscy inni dostawcy poświadczeń wtyczki zostaną sprawdzone po kolei.</span><span class="sxs-lookup"><span data-stu-id="1f96f-123">All other plug-in credential providers will be tried sequentially.</span></span>
1. <span data-ttu-id="1f96f-124">Jeśli żadne poświadczenia nie zostały nabyte jeszcze, użytkownik będzie monitowany o poświadczenia, za pomocą okna dialogowego standardowe uwierzytelnianie podstawowe.</span><span class="sxs-lookup"><span data-stu-id="1f96f-124">If no credentials have been acquired yet, the user will be prompted for credentials using a standard basic authentication dialog.</span></span>

### <a name="implementing-ivscredentialprovidergetcredentialsasync"></a><span data-ttu-id="1f96f-125">Implementing IVsCredentialProvider.GetCredentialsAsync</span><span class="sxs-lookup"><span data-stu-id="1f96f-125">Implementing IVsCredentialProvider.GetCredentialsAsync</span></span>

<span data-ttu-id="1f96f-126">Aby utworzyć dostawcę poświadczeń NuGet dla programu Visual Studio, utworzyć rozszerzenie Visual Studio, które udostępnia publiczne eksportu MEF implementacja `IVsCredentialProvider` wpisz i stosuje zasady opisane poniżej.</span><span class="sxs-lookup"><span data-stu-id="1f96f-126">To create a NuGet credential provider for Visual Studio, create a Visual Studio Extension that exposes a public MEF Export implementing the `IVsCredentialProvider` type, and adheres to the principles outlined below.</span></span>

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

<span data-ttu-id="1f96f-127">Przykładowe zastosowanie znajdują się w [próbki VsCredentialProvider](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span><span class="sxs-lookup"><span data-stu-id="1f96f-127">A sample implementation can be found in [the VsCredentialProvider sample](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span></span>

<span data-ttu-id="1f96f-128">Każdy dostawca poświadczeń NuGet dla programu Visual Studio musi:</span><span class="sxs-lookup"><span data-stu-id="1f96f-128">Each NuGet credential provider for Visual Studio must:</span></span>

1. <span data-ttu-id="1f96f-129">Ustal, czy jego Podaj poświadczenia dla docelowego identyfikatora URI przed zainicjowaniem przejęcie poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="1f96f-129">Determine whether it can provide credentials for the targeted URI before initiating credential acquisition.</span></span> <span data-ttu-id="1f96f-130">Jeśli dostawca nie może dostarczyć poświadczenia dla źródła docelowych, powinien on zwrócić `null`.</span><span class="sxs-lookup"><span data-stu-id="1f96f-130">If the provider cannot supply credentials for the targeted source, then it should return `null`.</span></span>
1. <span data-ttu-id="1f96f-131">Jeśli dostawca obsługuje żądania dla docelowego identyfikatora URI, ale nie można podać poświadczenia, powinny być wyjątek.</span><span class="sxs-lookup"><span data-stu-id="1f96f-131">If the provider does handle requests for the targeted URI, but cannot supply credentials, an exception should be thrown.</span></span>

<span data-ttu-id="1f96f-132">Niestandardowy Dostawca poświadczeń NuGet dla programu Visual Studio musi implementować `IVsCredentialProvider` dostępne w interfejsie [pakietu NuGet.VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/).</span><span class="sxs-lookup"><span data-stu-id="1f96f-132">A custom NuGet credential provider for Visual Studio must implement the `IVsCredentialProvider` interface available in the [NuGet.VisualStudio package](https://www.nuget.org/packages/NuGet.VisualStudio/).</span></span>

#### <a name="getcredentialasync"></a><span data-ttu-id="1f96f-133">GetCredentialAsync</span><span class="sxs-lookup"><span data-stu-id="1f96f-133">GetCredentialAsync</span></span>

| <span data-ttu-id="1f96f-134">Parametr wejściowy</span><span class="sxs-lookup"><span data-stu-id="1f96f-134">Input Parameter</span></span> |<span data-ttu-id="1f96f-135">Opis</span><span class="sxs-lookup"><span data-stu-id="1f96f-135">Description</span></span>|
| ----------------|-----------|
| <span data-ttu-id="1f96f-136">Identyfikator uri identyfikatora URI</span><span class="sxs-lookup"><span data-stu-id="1f96f-136">Uri uri</span></span> | <span data-ttu-id="1f96f-137">Źródło pakietu Uri, dla których wymagane są poświadczenia.</span><span class="sxs-lookup"><span data-stu-id="1f96f-137">The package source Uri for which credentials are being requested.</span></span>|
| <span data-ttu-id="1f96f-138">IWebProxy serwera proxy</span><span class="sxs-lookup"><span data-stu-id="1f96f-138">IWebProxy proxy</span></span> | <span data-ttu-id="1f96f-139">Serwer proxy sieci Web do użycia przy komunikacji w sieci.</span><span class="sxs-lookup"><span data-stu-id="1f96f-139">Web proxy to use when communicating on the network.</span></span> <span data-ttu-id="1f96f-140">Wartość null, jeśli uwierzytelnianie nie jest serwer proxy skonfigurowane.</span><span class="sxs-lookup"><span data-stu-id="1f96f-140">Null if there is no proxy authentication configured.</span></span> |
| <span data-ttu-id="1f96f-141">wartość logiczna isProxyRequest</span><span class="sxs-lookup"><span data-stu-id="1f96f-141">bool isProxyRequest</span></span> | <span data-ttu-id="1f96f-142">Wartość true, jeśli żądanie jest uzyskanie poświadczeń uwierzytelniania serwera proxy.</span><span class="sxs-lookup"><span data-stu-id="1f96f-142">True if this request is to get proxy authentication credentials.</span></span> <span data-ttu-id="1f96f-143">Jeśli wdrożenia jest nieprawidłowa dla pobierania poświadczeń serwera proxy, powinna zostać zwrócona wartość null.</span><span class="sxs-lookup"><span data-stu-id="1f96f-143">If the implementation is not valid for acquiring proxy credentials, then null should be returned.</span></span> |
| <span data-ttu-id="1f96f-144">wartość logiczna isRetry</span><span class="sxs-lookup"><span data-stu-id="1f96f-144">bool isRetry</span></span> | <span data-ttu-id="1f96f-145">Wartość true, jeśli poświadczenia zostały wcześniej żądał dla tego identyfikatora Uri, ale podane poświadczenia nie zezwala na dostęp do autoryzowanych.</span><span class="sxs-lookup"><span data-stu-id="1f96f-145">True if credentials were previously requested for this Uri, but the supplied credentials did not allow authorized access.</span></span> |
| <span data-ttu-id="1f96f-146">wartość logiczna nieinterakcyjne</span><span class="sxs-lookup"><span data-stu-id="1f96f-146">bool nonInteractive</span></span> | <span data-ttu-id="1f96f-147">Jeśli PRAWDA, Dostawca poświadczeń należy pominąć wszystkie monity użytkownika i zamiast tego użyj wartości domyślnych.</span><span class="sxs-lookup"><span data-stu-id="1f96f-147">If true, the credential provider must suppress all user prompts and use default values instead.</span></span> |
| <span data-ttu-id="1f96f-148">CancellationToken cancellationToken</span><span class="sxs-lookup"><span data-stu-id="1f96f-148">CancellationToken cancellationToken</span></span> | <span data-ttu-id="1f96f-149">Ten token anulowania powinny być sprawdzane w celu ustalenia, jeśli poświadczenia żądania operacja została anulowana.</span><span class="sxs-lookup"><span data-stu-id="1f96f-149">This cancellation token should be checked to determine if the operation requesting credentials has been cancelled.</span></span> |

<span data-ttu-id="1f96f-150">**Wartość zwracana**: implementacja obiektu poświadczeń [ `System.Net.ICredentials` interfejsu](/dotnet/api/system.net.icredentials?view=netstandard-2.0).</span><span class="sxs-lookup"><span data-stu-id="1f96f-150">**Return value**: A credentials object implementing the [`System.Net.ICredentials` interface](/dotnet/api/system.net.icredentials?view=netstandard-2.0).</span></span>
