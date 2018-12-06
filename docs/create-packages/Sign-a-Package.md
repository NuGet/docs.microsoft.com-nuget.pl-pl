---
title: Podpisywanie pakietów NuGet
description: Wyjaśnia, jak podpisanych pakietów może służyć do włączyć weryfikację zawartości integralności.
author: rido-min
ms.author: rmpablos
ms.date: 03/06/2018
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: e8955f9d46bab235c8755d5654814a4291d542d6
ms.sourcegitcommit: 673e580ae749544a4a071b4efe7d42fd2bb6d209
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/06/2018
ms.locfileid: "52977566"
---
# <a name="signing-nuget-packages"></a><span data-ttu-id="fe811-103">Podpisywanie pakietów NuGet</span><span class="sxs-lookup"><span data-stu-id="fe811-103">Signing NuGet Packages</span></span>

<span data-ttu-id="fe811-104">Testy weryfikacji integralności zawartości, które zapewnia ochronę przed naruszeniem zawartości umożliwia podpisanych pakietów.</span><span class="sxs-lookup"><span data-stu-id="fe811-104">Signed packages allows for content integrity verification checks which provides protection against content tampering.</span></span> <span data-ttu-id="fe811-105">Podpis pakietu również służy jako pojedyncze źródło prawdziwych informacji o rzeczywistego pochodzenia pakietu i klinowe autentyczności pakietu dla konsumentów.</span><span class="sxs-lookup"><span data-stu-id="fe811-105">The package signature also serves as the single source of truth about the actual origin of the package and bolsters package authenticity for the consumer.</span></span> <span data-ttu-id="fe811-106">W tym przewodniku założono, że już [utworzył pakiet](creating-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="fe811-106">This guide assumes you have already [created a package](creating-a-package.md).</span></span>

## <a name="get-a-code-signing-certificate"></a><span data-ttu-id="fe811-107">Uzyskaj certyfikat podpisywania kodu</span><span class="sxs-lookup"><span data-stu-id="fe811-107">Get a code signing certificate</span></span>

<span data-ttu-id="fe811-108">Prawidłowe certyfikaty mogą być uzyskane z publicznego urzędu certyfikacji takich jak [Symantec](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3), [DigiCert](https://www.digicert.com/code-signing/), [Go Daddy](https://www.godaddy.com/web-security/code-signing-certificate), [globalnego logowania](https://www.globalsign.com/en/code-signing-certificate/), [Comodo](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php), [Certum](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml)itp. Pełną listę urzędy certyfikacji używane przez Windows można uzyskać z [ http://aka.ms/trustcertpartners ](http://aka.ms/trustcertpartners).</span><span class="sxs-lookup"><span data-stu-id="fe811-108">Valid certificates may be obtained from a public certificate authority such as [Symantec](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3), [DigiCert](https://www.digicert.com/code-signing/), [Go Daddy](https://www.godaddy.com/web-security/code-signing-certificate), [Global Sign](https://www.globalsign.com/en/code-signing-certificate/), [Comodo](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php), [Certum](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml), etc. The complete list of certification authorities trusted by Windows can be obtained from [http://aka.ms/trustcertpartners](http://aka.ms/trustcertpartners).</span></span>

<span data-ttu-id="fe811-109">Można użyć własnym wystawionych certyfikatów do celów testowych.</span><span class="sxs-lookup"><span data-stu-id="fe811-109">You can use self-issued certificates for testing purposes.</span></span> <span data-ttu-id="fe811-110">Pakiety podpisany przy użyciu własnym wystawionych certyfikatów nie są akceptowane przez NuGet.org. Dowiedz się więcej o [tworzenia certyfikatu testowego](#create-a-test-certificate)</span><span class="sxs-lookup"><span data-stu-id="fe811-110">However, packages signed using self-issued certificates are not accepted by NuGet.org. Learn more about [creating a test certificate](#create-a-test-certificate)</span></span>

## <a name="export-the-certificate-file"></a><span data-ttu-id="fe811-111">Eksportuj plik certyfikatu</span><span class="sxs-lookup"><span data-stu-id="fe811-111">Export the certificate file</span></span>

* <span data-ttu-id="fe811-112">Możesz wyeksportować istniejący certyfikat na format binarny DER, za pomocą Kreatora eksportu certyfikatów.</span><span class="sxs-lookup"><span data-stu-id="fe811-112">You can export an existing certificate to a binary DER format by using the Certificate Export Wizard.</span></span>

  ![Kreator eksportu certyfikatów](../reference/media/CertificateExportWizard.png)

* <span data-ttu-id="fe811-114">Możesz też wyeksportować certyfikat przy użyciu [polecenia PowerShell eksportu certyfikatu](/powershell/module/pkiclient/export-certificate.md).</span><span class="sxs-lookup"><span data-stu-id="fe811-114">You can also export the certificate using the [Export-Certificate PowerShell command](/powershell/module/pkiclient/export-certificate.md).</span></span>

## <a name="sign-the-package"></a><span data-ttu-id="fe811-115">Podpisywanie pakietu</span><span class="sxs-lookup"><span data-stu-id="fe811-115">Sign the package</span></span>

> [!note]
> <span data-ttu-id="fe811-116">Wymaga nuget.exe 4.6.0 lub nowszej</span><span class="sxs-lookup"><span data-stu-id="fe811-116">Requires nuget.exe 4.6.0 or later</span></span>

<span data-ttu-id="fe811-117">Zaloguj się przy użyciu pakietu [logowania nuget](../tools/cli-ref-sign.md):</span><span class="sxs-lookup"><span data-stu-id="fe811-117">Sign the package using [nuget sign](../tools/cli-ref-sign.md):</span></span>

```cli
nuget sign MyPackage.nupkg -CertificateFilePath <PathToTheCertificate> -Timestamper <TimestampServiceURL>
```

* <span data-ttu-id="fe811-118">Można użyć certyfikatu jest dostępny w magazynie certyfikatów lub używany certyfikat z pliku.</span><span class="sxs-lookup"><span data-stu-id="fe811-118">You can use a certificate available in the certificate store or use a certificate from a file.</span></span> <span data-ttu-id="fe811-119">Zobacz odwołanie do interfejsu wiersza polecenia [logowania nuget](../tools/cli-ref-sign.md).</span><span class="sxs-lookup"><span data-stu-id="fe811-119">See CLI reference for [nuget sign](../tools/cli-ref-sign.md).</span></span>
* <span data-ttu-id="fe811-120">Podpisanych pakietów powinien zawierać sygnaturę czasową, aby upewnić się, że podpis pozostaje ważny, gdy wygasł certyfikat podpisywania.</span><span class="sxs-lookup"><span data-stu-id="fe811-120">Signed packages should include a timestamp to make sure the signature remains valid when the signing certificate has expired.</span></span> <span data-ttu-id="fe811-121">Inne dadzą operacji logowania [ostrzeżenie](../reference/errors-and-warnings/NU3002.md).</span><span class="sxs-lookup"><span data-stu-id="fe811-121">Else the sign operation will produce a [warning](../reference/errors-and-warnings/NU3002.md).</span></span>
* <span data-ttu-id="fe811-122">Można wyświetlić szczegóły podpisu danego pakietu przy użyciu [Sprawdź nuget](../tools/cli-ref-verify.md).</span><span class="sxs-lookup"><span data-stu-id="fe811-122">You can see the signature details of a given package using [nuget verify](../tools/cli-ref-verify.md).</span></span>

## <a name="register-the-certificate-on-nugetorg"></a><span data-ttu-id="fe811-123">Zarejestruj certyfikat w witrynie NuGet.org</span><span class="sxs-lookup"><span data-stu-id="fe811-123">Register the certificate on NuGet.org</span></span>

<span data-ttu-id="fe811-124">Aby opublikować podpisanych pakietów, należy zarejestrować certyfikat za pomocą NuGet.org. Wymagany certyfikat jako `.cer` pliku w formacie binarnym DER.</span><span class="sxs-lookup"><span data-stu-id="fe811-124">To publish a signed package, you must first register the certificate with NuGet.org. You need the certificate as a `.cer` file in a binary DER format.</span></span>

1. <span data-ttu-id="fe811-125">[Zaloguj się](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) na stronie NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="fe811-125">[Sign in](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) to NuGet.org.</span></span>
1. <span data-ttu-id="fe811-126">Przejdź do `Account settings` (lub `Manage Organization` **>** `Edit Organziation` Jeśli chcesz zarejestrować certyfikat przy użyciu konta organizacji).</span><span class="sxs-lookup"><span data-stu-id="fe811-126">Go to `Account settings` (or `Manage Organization` **>** `Edit Organziation` if you would like to register the certificate with an Organization account).</span></span>
1. <span data-ttu-id="fe811-127">Rozwiń `Certificates` i wybierz pozycję `Register new`.</span><span class="sxs-lookup"><span data-stu-id="fe811-127">Expand the `Certificates` section and select `Register new`.</span></span>
1. <span data-ttu-id="fe811-128">Przeglądaj i wybierz wyeksportowany wcześniej plik rozszyfrować przy jego użyciu.</span><span class="sxs-lookup"><span data-stu-id="fe811-128">Browse and select the certficate file that was exported earlier.</span></span>
  <span data-ttu-id="fe811-129">![Certyfikaty zarejestrowane](../reference/media/registered-certs.png)</span><span class="sxs-lookup"><span data-stu-id="fe811-129">![Registered Certificates](../reference/media/registered-certs.png)</span></span>

<span data-ttu-id="fe811-130">**Uwaga**</span><span class="sxs-lookup"><span data-stu-id="fe811-130">**Note**</span></span>
* <span data-ttu-id="fe811-131">Jeden użytkownik może przesłać ten sam certyfikat i wielu certyfikatów, które mogą być rejestrowane przez wielu użytkowników.</span><span class="sxs-lookup"><span data-stu-id="fe811-131">One user can submit multiple certificates and the same certificate can be registered by multiple users.</span></span>
* <span data-ttu-id="fe811-132">Po użytkownik ma zarejestrowane certyfikatu, wszystkie przyszłe pakietu przesłania **musi** być podpisane przy użyciu jednego z certyfikatów.</span><span class="sxs-lookup"><span data-stu-id="fe811-132">Once a user has a certificate registered, all future package submissions **must** be signed with one of the certificates.</span></span> <span data-ttu-id="fe811-133">Zobacz [Zarządzaj podpisywania wymagania dotyczące pakietu w witrynie NuGet.org](#manage-signing-requirements-for-your-package-on-nugetorg)</span><span class="sxs-lookup"><span data-stu-id="fe811-133">See [Manage signing requirements for your package on NuGet.org](#manage-signing-requirements-for-your-package-on-nugetorg)</span></span>
* <span data-ttu-id="fe811-134">Użytkownicy mogą również usuwać certyfikat zarejestrowany z konta.</span><span class="sxs-lookup"><span data-stu-id="fe811-134">Users can also remove a registered certificate from the account.</span></span> <span data-ttu-id="fe811-135">Po usunięciu certyfikatu nie powiedzie się na przesyłanie nowe pakiety podpisany przy użyciu tego certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="fe811-135">Once a certificate is removed, new packages signed with that certificate will fail at submission.</span></span> <span data-ttu-id="fe811-136">Nie ma wpływu na istniejące pakiety.</span><span class="sxs-lookup"><span data-stu-id="fe811-136">Existing packages aren't affected.</span></span>

## <a name="publish-the-package"></a><span data-ttu-id="fe811-137">Publikowanie pakietu</span><span class="sxs-lookup"><span data-stu-id="fe811-137">Publish the package</span></span>

<span data-ttu-id="fe811-138">Teraz można przystąpić do opublikowania pakietu na stronie NuGet.org. Zobacz [publikowania pakietów](Publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="fe811-138">You are now ready to publish the package to NuGet.org. See [Publishing packages](Publish-a-package.md).</span></span>

## <a name="create-a-test-certificate"></a><span data-ttu-id="fe811-139">Utwórz certyfikat testowy</span><span class="sxs-lookup"><span data-stu-id="fe811-139">Create a test certificate</span></span>

<span data-ttu-id="fe811-140">Można użyć własnym wystawionych certyfikatów do celów testowych.</span><span class="sxs-lookup"><span data-stu-id="fe811-140">You can use self-issued certificates for testing purposes.</span></span> <span data-ttu-id="fe811-141">Aby utworzyć własny wystawionego certyfikatu, użyj [polecenia PowerShell New-SelfSignedCertificate](/powershell/module/pkiclient/new-selfsignedcertificate.md).</span><span class="sxs-lookup"><span data-stu-id="fe811-141">To create a self-issued certificate, use the [New-SelfSignedCertificate PowerShell command](/powershell/module/pkiclient/new-selfsignedcertificate.md).</span></span>

```ps
New-SelfSignedCertificate -Subject "CN=NuGet Test Developer, OU=Use for testing purposes ONLY" `
                          -FriendlyName "NuGetTestDeveloper" `
                          -Type CodeSigning `
                          -KeyUsage DigitalSignature `
                          -KeyLength 2048 `
                          -KeyAlgorithm RSA `
                          -HashAlgorithm SHA256 `
                          -Provider "Microsoft Enhanced RSA and AES Cryptographic Provider" `
                          -CertStoreLocation "Cert:\CurrentUser\My" 
```

<span data-ttu-id="fe811-142">To polecenie tworzy certyfikat testowania dostępności w magazynie certyfikatów osobistych bieżącego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="fe811-142">This command creates a testing certificate available in the current user's personal certificate store.</span></span> <span data-ttu-id="fe811-143">Można otworzyć magazynu certyfikatów, uruchamiając `certmgr.msc` aby zobaczyć nowo utworzonego certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="fe811-143">You can open the certificate store by running `certmgr.msc` to see the newly created certificate.</span></span>

> [!Warning]
> <span data-ttu-id="fe811-144">NuGet.org nie akceptuje pakietów podpisany przy użyciu własnym wystawionych certyfikatów.</span><span class="sxs-lookup"><span data-stu-id="fe811-144">NuGet.org does not accept packages signed with self-issued certificates.</span></span>

## <a name="manage-signing-requirements-for-your-package-on-nugetorg"></a><span data-ttu-id="fe811-145">Zarządzanie wymagania podpisywania pakietu w witrynie NuGet.org</span><span class="sxs-lookup"><span data-stu-id="fe811-145">Manage signing requirements for your package on NuGet.org</span></span>
1. <span data-ttu-id="fe811-146">[Zaloguj się](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) na stronie NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="fe811-146">[Sign in](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) to NuGet.org.</span></span>

1. <span data-ttu-id="fe811-147">Przejdź do `Manage Packages`  
    ![Konfigurowanie pakietów, które podpisały](../reference/media/configure-package-signers.png)</span><span class="sxs-lookup"><span data-stu-id="fe811-147">Go to `Manage Packages` 
![Configure package signers](../reference/media/configure-package-signers.png)</span></span>

* <span data-ttu-id="fe811-148">Jeśli jesteś jedynym właścicielem pakietu, są wymagane osoby podpisującej tj służy dowolne zarejestrowane certyfikaty do podpisywania i publikowania pakietów NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="fe811-148">If you are the sole owner of a package, you are the required signer i.e. you can use any of the registered certificates to sign and publish your packages to NuGet.org.</span></span>

* <span data-ttu-id="fe811-149">Jeżeli pakiet zawiera wiele właścicieli, domyślnie, certyfikaty "Dowolna" właściciel może służyć do podpisania pakietu.</span><span class="sxs-lookup"><span data-stu-id="fe811-149">If a package has multiple owners, by default, "Any" owner's certificates can be used to sign the package.</span></span> <span data-ttu-id="fe811-150">Jako współwłaściciela pakietu można zastąpić "Dowolne", przy użyciu samodzielnie lub wszelkie inne współwłaścicielem jako wymagane osoby podpisującej.</span><span class="sxs-lookup"><span data-stu-id="fe811-150">As a co-owner of the package, you can override "Any" with yourself or any other co-owner to be the required signer.</span></span> <span data-ttu-id="fe811-151">W przypadku wprowadzenia właściciela, który nie ma żadnych certyfikatów zarejestrowanych pakietów niepodpisane będą dozwolone.</span><span class="sxs-lookup"><span data-stu-id="fe811-151">If you make an owner  who does not have any certificate registered, then unsigned packages will be allowed.</span></span> 

* <span data-ttu-id="fe811-152">Podobnie, jeśli wartość domyślna "Dowolna" opcja jest zaznaczona dla pakietu, w której jeden właściciel ma certyfikat zarejestrowany i innego właściciela nie ma żadnych certyfikatów zarejestrowanych, następnie NuGet.org akceptuje podpisanych pakietów za pomocą podpisu zarejestrowany za pomocą jednej z jego właścicieli lub Niepodpisany pakietu (ponieważ jest to jeden z właścicieli nie ma żadnych certyfikatów zarejestrowanych).</span><span class="sxs-lookup"><span data-stu-id="fe811-152">Similarly, if the default "Any" option is selected for a package where one owner has a certificate registered and another owner does not have any certificate registered, then NuGet.org accepts either a signed package with a signature registered by one of its owners or an unsigned package (because one of the owners does not have any certificate registered).</span></span>

## <a name="related-articles"></a><span data-ttu-id="fe811-153">Powiązane artykuły</span><span class="sxs-lookup"><span data-stu-id="fe811-153">Related articles</span></span>

- [<span data-ttu-id="fe811-154">Instalowanie pakietów podpisem</span><span class="sxs-lookup"><span data-stu-id="fe811-154">Installing signed packages</span></span>](../consume-packages/installing-signed-packages.md)
- [<span data-ttu-id="fe811-155">Dokumentacja podpisanych pakietów</span><span class="sxs-lookup"><span data-stu-id="fe811-155">Signed Packages Reference</span></span>](../reference/Signed-Packages-Reference.md)
