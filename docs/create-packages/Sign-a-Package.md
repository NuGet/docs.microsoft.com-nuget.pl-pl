---
title: Podpisywanie pakietów NuGet
description: W tym artykule wyjaśniono, jak podpisane pakiety mogą służyć do włączania weryfikacji integralności zawartości.
author: rido-min
ms.author: rmpablos
ms.date: 03/06/2018
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 00fe1d5fa81132b5d6826203a0d26e56aa8d4755
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "79429004"
---
# <a name="signing-nuget-packages"></a><span data-ttu-id="c7e6b-103">Podpisywanie pakietów NuGet</span><span class="sxs-lookup"><span data-stu-id="c7e6b-103">Signing NuGet Packages</span></span>

<span data-ttu-id="c7e6b-104">Podpisane pakiety umożliwiają sprawdzanie integralności zawartości, co zapewnia ochronę przed manipulowaniem zawartością.</span><span class="sxs-lookup"><span data-stu-id="c7e6b-104">Signed packages allows for content integrity verification checks which provides protection against content tampering.</span></span> <span data-ttu-id="c7e6b-105">Podpis pakietu służy również jako jedno źródło prawdy o rzeczywistym pochodzeniu pakietu i wzmacnia autentyczność pakietu dla konsumenta.</span><span class="sxs-lookup"><span data-stu-id="c7e6b-105">The package signature also serves as the single source of truth about the actual origin of the package and bolsters package authenticity for the consumer.</span></span> <span data-ttu-id="c7e6b-106">W tym przewodniku założono, że pakiet został już [utworzony.](creating-a-package.md)</span><span class="sxs-lookup"><span data-stu-id="c7e6b-106">This guide assumes you have already [created a package](creating-a-package.md).</span></span>

## <a name="get-a-code-signing-certificate"></a><span data-ttu-id="c7e6b-107">Uzyskaj certyfikat podpisywania kodu</span><span class="sxs-lookup"><span data-stu-id="c7e6b-107">Get a code signing certificate</span></span>

<span data-ttu-id="c7e6b-108">Ważne certyfikaty mogą być uzyskane z publicznego urzędu certyfikacji, takiego jak [Symantec](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3), [DigiCert](https://www.digicert.com/code-signing/), [Go Daddy](https://www.godaddy.com/web-security/code-signing-certificate), [Global Sign](https://www.globalsign.com/en/code-signing-certificate/), [Comodo](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php), [Certum](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml)itp. Pełną listę urzędów certyfikacji zaufanych [http://aka.ms/trustcertpartners](https://aka.ms/trustcertpartners)przez system Windows można uzyskać z programu .</span><span class="sxs-lookup"><span data-stu-id="c7e6b-108">Valid certificates may be obtained from a public certificate authority such as [Symantec](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3), [DigiCert](https://www.digicert.com/code-signing/), [Go Daddy](https://www.godaddy.com/web-security/code-signing-certificate), [Global Sign](https://www.globalsign.com/en/code-signing-certificate/), [Comodo](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php), [Certum](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml), etc. The complete list of certification authorities trusted by Windows can be obtained from [http://aka.ms/trustcertpartners](https://aka.ms/trustcertpartners).</span></span>

<span data-ttu-id="c7e6b-109">Do celów testowych można używać certyfikatów wystawionych samodzielnie.</span><span class="sxs-lookup"><span data-stu-id="c7e6b-109">You can use self-issued certificates for testing purposes.</span></span> <span data-ttu-id="c7e6b-110">Jednak pakiety podpisane przy użyciu certyfikatów wystawionych samodzielnie nie są akceptowane przez NuGet.org. Dowiedz się więcej o [tworzeniu certyfikatu testowego](#create-a-test-certificate)</span><span class="sxs-lookup"><span data-stu-id="c7e6b-110">However, packages signed using self-issued certificates are not accepted by NuGet.org. Learn more about [creating a test certificate](#create-a-test-certificate)</span></span>

## <a name="export-the-certificate-file"></a><span data-ttu-id="c7e6b-111">Eksportowanie pliku certyfikatu</span><span class="sxs-lookup"><span data-stu-id="c7e6b-111">Export the certificate file</span></span>

* <span data-ttu-id="c7e6b-112">Istniejący certyfikat można wyeksportować do binarnego formatu DER za pomocą Kreatora eksportu certyfikatów.</span><span class="sxs-lookup"><span data-stu-id="c7e6b-112">You can export an existing certificate to a binary DER format by using the Certificate Export Wizard.</span></span>

  ![Kreator eksportu certyfikatów](../reference/media/CertificateExportWizard.png)

* <span data-ttu-id="c7e6b-114">Certyfikat można również wyeksportować za pomocą [polecenia Programu PowerShell certyfikat eksportu](/powershell/module/pkiclient/export-certificate).</span><span class="sxs-lookup"><span data-stu-id="c7e6b-114">You can also export the certificate using the [Export-Certificate PowerShell command](/powershell/module/pkiclient/export-certificate).</span></span>

## <a name="sign-the-package"></a><span data-ttu-id="c7e6b-115">Podpisz paczkę</span><span class="sxs-lookup"><span data-stu-id="c7e6b-115">Sign the package</span></span>

> [!note]
> <span data-ttu-id="c7e6b-116">Wymaga nuget.exe 4.6.0 lub nowszego.</span><span class="sxs-lookup"><span data-stu-id="c7e6b-116">Requires nuget.exe 4.6.0 or later.</span></span> <span data-ttu-id="c7e6b-117">dotnet.exe wsparcie już wkrótce - [#7939](https://github.com/NuGet/Home/issues/7939)</span><span class="sxs-lookup"><span data-stu-id="c7e6b-117">dotnet.exe support is coming soon - [#7939](https://github.com/NuGet/Home/issues/7939)</span></span>

<span data-ttu-id="c7e6b-118">Podpisz pakiet za pomocą [znaku nuget:](../reference/cli-reference/cli-ref-sign.md)</span><span class="sxs-lookup"><span data-stu-id="c7e6b-118">Sign the package using [nuget sign](../reference/cli-reference/cli-ref-sign.md):</span></span>

```cli
nuget sign MyPackage.nupkg -CertificatePath <PathToTheCertificate> -Timestamper <TimestampServiceURL>
```

> [!Tip]
> <span data-ttu-id="c7e6b-119">Dostawca certyfikatów często udostępnia również adres URL serwera sygnatury czasowej, którego można użyć w przypadku opcjonalnego argumentu `Timestamper` wyświetlenia powyżej.</span><span class="sxs-lookup"><span data-stu-id="c7e6b-119">The certificate provider often also provides a timestamping server URL which you can use for the `Timestamper` optional argument show above.</span></span> <span data-ttu-id="c7e6b-120">Zapoznaj się z dokumentacją dostawcy i/lub pomocą techniczną dotyczącą tego adresu URL usługi.</span><span class="sxs-lookup"><span data-stu-id="c7e6b-120">Consult with your provider's documentation and/or support for that service URL.</span></span>

* <span data-ttu-id="c7e6b-121">Można użyć certyfikatu dostępnego w magazynie certyfikatów lub użyć certyfikatu z pliku.</span><span class="sxs-lookup"><span data-stu-id="c7e6b-121">You can use a certificate available in the certificate store or use a certificate from a file.</span></span> <span data-ttu-id="c7e6b-122">Zobacz odwołanie do interfejsu wiersza polecenia dla [znaku nuget](../reference/cli-reference/cli-ref-sign.md).</span><span class="sxs-lookup"><span data-stu-id="c7e6b-122">See CLI reference for [nuget sign](../reference/cli-reference/cli-ref-sign.md).</span></span>
* <span data-ttu-id="c7e6b-123">Podpisane pakiety powinny zawierać sygnaturę czasową, aby upewnić się, że podpis pozostaje ważny po wygaśnięciu certyfikatu podpisywania.</span><span class="sxs-lookup"><span data-stu-id="c7e6b-123">Signed packages should include a timestamp to make sure the signature remains valid when the signing certificate has expired.</span></span> <span data-ttu-id="c7e6b-124">W przeciwnym razie operacja znaku spowoduje [ostrzeżenie](../reference/errors-and-warnings/NU3002.md).</span><span class="sxs-lookup"><span data-stu-id="c7e6b-124">Else the sign operation will produce a [warning](../reference/errors-and-warnings/NU3002.md).</span></span>
* <span data-ttu-id="c7e6b-125">Możesz zobaczyć szczegóły podpisu danego pakietu za pomocą [nuget verify](../reference/cli-reference/cli-ref-verify.md).</span><span class="sxs-lookup"><span data-stu-id="c7e6b-125">You can see the signature details of a given package using [nuget verify](../reference/cli-reference/cli-ref-verify.md).</span></span>

## <a name="register-the-certificate-on-nugetorg"></a><span data-ttu-id="c7e6b-126">Zarejestruj certyfikat na NuGet.org</span><span class="sxs-lookup"><span data-stu-id="c7e6b-126">Register the certificate on NuGet.org</span></span>

<span data-ttu-id="c7e6b-127">Aby opublikować podpisany pakiet, należy najpierw zarejestrować certyfikat w NuGet.org. Certyfikat jest potrzebny `.cer` jako plik w binarnym formacie DER.</span><span class="sxs-lookup"><span data-stu-id="c7e6b-127">To publish a signed package, you must first register the certificate with NuGet.org. You need the certificate as a `.cer` file in a binary DER format.</span></span>

1. <span data-ttu-id="c7e6b-128">[Zaloguj się,](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) aby NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="c7e6b-128">[Sign in](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) to NuGet.org.</span></span>
1. <span data-ttu-id="c7e6b-129">Przejdź `Account settings` do `Manage Organization` **>** `Edit Organziation` (lub jeśli chcesz zarejestrować certyfikat na koncie organizacji).</span><span class="sxs-lookup"><span data-stu-id="c7e6b-129">Go to `Account settings` (or `Manage Organization` **>** `Edit Organziation` if you would like to register the certificate with an Organization account).</span></span>
1. <span data-ttu-id="c7e6b-130">Rozwiń `Certificates` sekcję `Register new`i wybierz opcję .</span><span class="sxs-lookup"><span data-stu-id="c7e6b-130">Expand the `Certificates` section and select `Register new`.</span></span>
1. <span data-ttu-id="c7e6b-131">Przeglądaj i wybierz plik certficate, który został wyeksportowany wcześniej.</span><span class="sxs-lookup"><span data-stu-id="c7e6b-131">Browse and select the certficate file that was exported earlier.</span></span>
  <span data-ttu-id="c7e6b-132">![Zarejestrowane certyfikaty](../reference/media/registered-certs.png)</span><span class="sxs-lookup"><span data-stu-id="c7e6b-132">![Registered Certificates](../reference/media/registered-certs.png)</span></span>

<span data-ttu-id="c7e6b-133">**Uwaga**</span><span class="sxs-lookup"><span data-stu-id="c7e6b-133">**Note**</span></span>
* <span data-ttu-id="c7e6b-134">Jeden użytkownik może przesłać wiele certyfikatów, a ten sam certyfikat może być zarejestrowany przez wielu użytkowników.</span><span class="sxs-lookup"><span data-stu-id="c7e6b-134">One user can submit multiple certificates and the same certificate can be registered by multiple users.</span></span>
* <span data-ttu-id="c7e6b-135">Gdy użytkownik ma zarejestrowany certyfikat, wszystkie przyszłe zgłoszenia pakietów **muszą** być podpisane za pomocą jednego z certyfikatów.</span><span class="sxs-lookup"><span data-stu-id="c7e6b-135">Once a user has a certificate registered, all future package submissions **must** be signed with one of the certificates.</span></span> <span data-ttu-id="c7e6b-136">Zobacz [Zarządzanie wymaganiami dotyczącymi podpisywania pakietu na NuGet.org](#manage-signing-requirements-for-your-package-on-nugetorg)</span><span class="sxs-lookup"><span data-stu-id="c7e6b-136">See [Manage signing requirements for your package on NuGet.org](#manage-signing-requirements-for-your-package-on-nugetorg)</span></span>
* <span data-ttu-id="c7e6b-137">Użytkownicy mogą również usunąć zarejestrowany certyfikat z konta.</span><span class="sxs-lookup"><span data-stu-id="c7e6b-137">Users can also remove a registered certificate from the account.</span></span> <span data-ttu-id="c7e6b-138">Po usunięciu certyfikatu nowe pakiety podpisane za pomocą tego certyfikatu nie powiedzie się podczas przesyłania.</span><span class="sxs-lookup"><span data-stu-id="c7e6b-138">Once a certificate is removed, new packages signed with that certificate will fail at submission.</span></span> <span data-ttu-id="c7e6b-139">Nie ma to wpływu na istniejące pakiety.</span><span class="sxs-lookup"><span data-stu-id="c7e6b-139">Existing packages aren't affected.</span></span>

## <a name="publish-the-package"></a><span data-ttu-id="c7e6b-140">Publikowanie pakietu</span><span class="sxs-lookup"><span data-stu-id="c7e6b-140">Publish the package</span></span>

<span data-ttu-id="c7e6b-141">Teraz możesz opublikować pakiet, aby NuGet.org. Zobacz [Publikowanie pakietów](../nuget-org/Publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="c7e6b-141">You are now ready to publish the package to NuGet.org. See [Publishing packages](../nuget-org/Publish-a-package.md).</span></span>

## <a name="create-a-test-certificate"></a><span data-ttu-id="c7e6b-142">Tworzenie certyfikatu testowego</span><span class="sxs-lookup"><span data-stu-id="c7e6b-142">Create a test certificate</span></span>

<span data-ttu-id="c7e6b-143">Do celów testowych można używać certyfikatów wystawionych samodzielnie.</span><span class="sxs-lookup"><span data-stu-id="c7e6b-143">You can use self-issued certificates for testing purposes.</span></span> <span data-ttu-id="c7e6b-144">Aby utworzyć certyfikat wystawiony samodzielnie, należy użyć [polecenia New-SelfSignedCertificate PowerShell](/powershell/module/pkiclient/new-selfsignedcertificate).</span><span class="sxs-lookup"><span data-stu-id="c7e6b-144">To create a self-issued certificate, use the [New-SelfSignedCertificate PowerShell command](/powershell/module/pkiclient/new-selfsignedcertificate).</span></span>

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

<span data-ttu-id="c7e6b-145">To polecenie tworzy certyfikat testowania dostępny w magazynie certyfikatów osobistych bieżącego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="c7e6b-145">This command creates a testing certificate available in the current user's personal certificate store.</span></span> <span data-ttu-id="c7e6b-146">Magazyn certyfikatów można otworzyć, uruchamiając `certmgr.msc` nowo utworzony certyfikat.</span><span class="sxs-lookup"><span data-stu-id="c7e6b-146">You can open the certificate store by running `certmgr.msc` to see the newly created certificate.</span></span>

> [!Warning]
> <span data-ttu-id="c7e6b-147">NuGet.org nie akceptuje pakietów podpisanych certyfikatami wystawionymi samodzielnie.</span><span class="sxs-lookup"><span data-stu-id="c7e6b-147">NuGet.org does not accept packages signed with self-issued certificates.</span></span>

## <a name="manage-signing-requirements-for-your-package-on-nugetorg"></a><span data-ttu-id="c7e6b-148">Zarządzanie wymaganiami dotyczącymi podpisywania pakietu na NuGet.org</span><span class="sxs-lookup"><span data-stu-id="c7e6b-148">Manage signing requirements for your package on NuGet.org</span></span>
1. <span data-ttu-id="c7e6b-149">[Zaloguj się,](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) aby NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="c7e6b-149">[Sign in](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) to NuGet.org.</span></span>

1. <span data-ttu-id="c7e6b-150">Przejdź `Manage Packages`  
    ![do konfigurowania sygnatariuszy pakietu](../reference/media/configure-package-signers.png)</span><span class="sxs-lookup"><span data-stu-id="c7e6b-150">Go to `Manage Packages` 
![Configure package signers](../reference/media/configure-package-signers.png)</span></span>

* <span data-ttu-id="c7e6b-151">Jeśli jesteś jedynym właścicielem pakietu, jesteś wymaganym sygnatariuszem, czyli możesz użyć dowolnego z zarejestrowanych certyfikatów do podpisania i opublikowania swoich paczek, aby NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="c7e6b-151">If you are the sole owner of a package, you are the required signer i.e. you can use any of the registered certificates to sign and publish your packages to NuGet.org.</span></span>

* <span data-ttu-id="c7e6b-152">Jeśli pakiet ma wielu właścicieli, domyślnie certyfikaty właściciela "Dowolna" mogą być używane do podpisywania pakietu.</span><span class="sxs-lookup"><span data-stu-id="c7e6b-152">If a package has multiple owners, by default, "Any" owner's certificates can be used to sign the package.</span></span> <span data-ttu-id="c7e6b-153">Jako współwłaściciel pakietu możesz zastąpić "Dowolny" ze sobą lub innym współwłaścicielem, aby być wymaganym sygnatariuszem.</span><span class="sxs-lookup"><span data-stu-id="c7e6b-153">As a co-owner of the package, you can override "Any" with yourself or any other co-owner to be the required signer.</span></span> <span data-ttu-id="c7e6b-154">Jeśli zrobisz właściciela, który nie ma żadnego certyfikatu zarejestrowanego, niepodpisane pakiety będą dozwolone.</span><span class="sxs-lookup"><span data-stu-id="c7e6b-154">If you make an owner  who does not have any certificate registered, then unsigned packages will be allowed.</span></span> 

* <span data-ttu-id="c7e6b-155">Podobnie, jeśli domyślna opcja "Dowolna" jest zaznaczona dla pakietu, w którym jeden właściciel ma zarejestrowany certyfikat, a inny właściciel nie ma zarejestrowanego certyfikatu, NuGet.org akceptuje podpisany pakiet z podpisem zarejestrowanym przez jednego z jego właścicieli lub niepodpisany pakiet (ponieważ jeden z właścicieli nie ma żadnego certyfikatu zarejestrowanego).</span><span class="sxs-lookup"><span data-stu-id="c7e6b-155">Similarly, if the default "Any" option is selected for a package where one owner has a certificate registered and another owner does not have any certificate registered, then NuGet.org accepts either a signed package with a signature registered by one of its owners or an unsigned package (because one of the owners does not have any certificate registered).</span></span>

## <a name="related-articles"></a><span data-ttu-id="c7e6b-156">Pokrewne artykuły:</span><span class="sxs-lookup"><span data-stu-id="c7e6b-156">Related articles</span></span>

- [<span data-ttu-id="c7e6b-157">Zarządzanie granicami zaufania pakietów</span><span class="sxs-lookup"><span data-stu-id="c7e6b-157">Manage package trust boundaries</span></span>](../consume-packages/installing-signed-packages.md)
- [<span data-ttu-id="c7e6b-158">Odwołanie do pakietów podpisanych</span><span class="sxs-lookup"><span data-stu-id="c7e6b-158">Signed Packages Reference</span></span>](../reference/Signed-Packages-Reference.md)
