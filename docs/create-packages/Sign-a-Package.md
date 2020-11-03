---
title: Podpisywanie pakietów NuGet
description: Wyjaśnia, w jaki sposób można używać podpisanych pakietów, aby umożliwić weryfikację integralności zawartości.
author: rido-min
ms.author: rmpablos
ms.date: 03/06/2018
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 81f8695d7b3cec73f3e18f90ddf38dfe6c3ecf4d
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/03/2020
ms.locfileid: "93237591"
---
# <a name="signing-nuget-packages"></a><span data-ttu-id="18afa-103">Podpisywanie pakietów NuGet</span><span class="sxs-lookup"><span data-stu-id="18afa-103">Signing NuGet Packages</span></span>

<span data-ttu-id="18afa-104">Podpisane pakiety umożliwiają sprawdzenie spójności zawartości, co zapewnia ochronę przed manipulacją zawartości.</span><span class="sxs-lookup"><span data-stu-id="18afa-104">Signed packages allows for content integrity verification checks which provides protection against content tampering.</span></span> <span data-ttu-id="18afa-105">Podpis pakietu służy również jako pojedyncze Źródło prawdziwości informacji o rzeczywistym pochodzeniu pakietu i autentyczności pakietu wspomaga dla konsumenta.</span><span class="sxs-lookup"><span data-stu-id="18afa-105">The package signature also serves as the single source of truth about the actual origin of the package and bolsters package authenticity for the consumer.</span></span> <span data-ttu-id="18afa-106">W tym przewodniku przyjęto założenie, że pakiet został już [utworzony](creating-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="18afa-106">This guide assumes you have already [created a package](creating-a-package.md).</span></span>

## <a name="get-a-code-signing-certificate"></a><span data-ttu-id="18afa-107">Pobierz certyfikat podpisywania kodu</span><span class="sxs-lookup"><span data-stu-id="18afa-107">Get a code signing certificate</span></span>

<span data-ttu-id="18afa-108">Prawidłowe certyfikaty można uzyskać od publicznego urzędu certyfikacji, takiego jak [Symantec](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3), [DigiCert](https://www.digicert.com/code-signing/), [Go Daddy](https://www.godaddy.com/web-security/code-signing-certificate), [Global Sign](https://www.globalsign.com/en/code-signing-certificate/), [Comodo](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php), [CERTUM](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml)itp. Pełną listę urzędów certyfikacji zaufanych przez system Windows można uzyskać z programu [http://aka.ms/trustcertpartners](/security/trusted-root/participants-list) .</span><span class="sxs-lookup"><span data-stu-id="18afa-108">Valid certificates may be obtained from a public certificate authority such as [Symantec](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3), [DigiCert](https://www.digicert.com/code-signing/), [Go Daddy](https://www.godaddy.com/web-security/code-signing-certificate), [Global Sign](https://www.globalsign.com/en/code-signing-certificate/), [Comodo](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php), [Certum](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml), etc. The complete list of certification authorities trusted by Windows can be obtained from [http://aka.ms/trustcertpartners](/security/trusted-root/participants-list).</span></span>

<span data-ttu-id="18afa-109">Do celów testowych można użyć certyfikatów wystawionych przez siebie.</span><span class="sxs-lookup"><span data-stu-id="18afa-109">You can use self-issued certificates for testing purposes.</span></span> <span data-ttu-id="18afa-110">Pakiety podpisane przy użyciu certyfikatów z podpisem własnym nie są jednak akceptowane przez NuGet.org. Dowiedz się więcej [na temat tworzenia certyfikatu testowego](#create-a-test-certificate)</span><span class="sxs-lookup"><span data-stu-id="18afa-110">However, packages signed using self-issued certificates are not accepted by NuGet.org. Learn more about [creating a test certificate](#create-a-test-certificate)</span></span>

## <a name="export-the-certificate-file"></a><span data-ttu-id="18afa-111">Eksportowanie pliku certyfikatu</span><span class="sxs-lookup"><span data-stu-id="18afa-111">Export the certificate file</span></span>

* <span data-ttu-id="18afa-112">Istniejący certyfikat można wyeksportować do formatu binarny DER przy użyciu Kreatora eksportu certyfikatów.</span><span class="sxs-lookup"><span data-stu-id="18afa-112">You can export an existing certificate to a binary DER format by using the Certificate Export Wizard.</span></span>

  ![Kreator eksportu certyfikatów](../reference/media/CertificateExportWizard.png)

* <span data-ttu-id="18afa-114">Certyfikat można także wyeksportować za pomocą [polecenia programu PowerShell eksportu certyfikatów](/powershell/module/pkiclient/export-certificate).</span><span class="sxs-lookup"><span data-stu-id="18afa-114">You can also export the certificate using the [Export-Certificate PowerShell command](/powershell/module/pkiclient/export-certificate).</span></span>

## <a name="sign-the-package"></a><span data-ttu-id="18afa-115">Podpisz pakiet</span><span class="sxs-lookup"><span data-stu-id="18afa-115">Sign the package</span></span>

> [!note]
> <span data-ttu-id="18afa-116">Wymaga nuget.exe 4.6.0 lub nowszego.</span><span class="sxs-lookup"><span data-stu-id="18afa-116">Requires nuget.exe 4.6.0 or later.</span></span> <span data-ttu-id="18afa-117">Pomoc techniczna dotnet.exe jest dostępna wkrótce [#7939](https://github.com/NuGet/Home/issues/7939)</span><span class="sxs-lookup"><span data-stu-id="18afa-117">dotnet.exe support is coming soon - [#7939](https://github.com/NuGet/Home/issues/7939)</span></span>

<span data-ttu-id="18afa-118">Podpisz pakiet przy użyciu [znaku NuGet](../reference/cli-reference/cli-ref-sign.md):</span><span class="sxs-lookup"><span data-stu-id="18afa-118">Sign the package using [nuget sign](../reference/cli-reference/cli-ref-sign.md):</span></span>

```cli
nuget sign MyPackage.nupkg -CertificatePath <PathToTheCertificate> -Timestamper <TimestampServiceURL>
```

> [!Tip]
> <span data-ttu-id="18afa-119">Dostawca certyfikatów często zawiera również adres URL serwera sygnatury czasowej, którego można użyć dla `Timestamper` opcjonalnego argumentu Pokaż powyżej.</span><span class="sxs-lookup"><span data-stu-id="18afa-119">The certificate provider often also provides a timestamping server URL which you can use for the `Timestamper` optional argument show above.</span></span> <span data-ttu-id="18afa-120">Zapoznaj się z dokumentacją dostawcy i/lub pomocą techniczną dla tego adresu URL usługi.</span><span class="sxs-lookup"><span data-stu-id="18afa-120">Consult with your provider's documentation and/or support for that service URL.</span></span>

* <span data-ttu-id="18afa-121">Możesz użyć certyfikatu dostępnego w magazynie certyfikatów lub użyć certyfikatu z pliku.</span><span class="sxs-lookup"><span data-stu-id="18afa-121">You can use a certificate available in the certificate store or use a certificate from a file.</span></span> <span data-ttu-id="18afa-122">Zobacz Dokumentacja interfejsu wiersza polecenia dla [znaku NuGet](../reference/cli-reference/cli-ref-sign.md).</span><span class="sxs-lookup"><span data-stu-id="18afa-122">See CLI reference for [nuget sign](../reference/cli-reference/cli-ref-sign.md).</span></span>
* <span data-ttu-id="18afa-123">Podpisane pakiety powinny zawierać sygnaturę czasową, aby upewnić się, że sygnatura jest ważna po wygaśnięciu certyfikatu podpisywania.</span><span class="sxs-lookup"><span data-stu-id="18afa-123">Signed packages should include a timestamp to make sure the signature remains valid when the signing certificate has expired.</span></span> <span data-ttu-id="18afa-124">W przeciwnym razie operacja podpisywania spowoduje wygenerowanie [ostrzeżenia](../reference/errors-and-warnings/NU3002.md).</span><span class="sxs-lookup"><span data-stu-id="18afa-124">Else the sign operation will produce a [warning](../reference/errors-and-warnings/NU3002.md).</span></span>
* <span data-ttu-id="18afa-125">Możesz zobaczyć szczegóły podpisu danego pakietu przy użyciu funkcji [weryfikacji NuGet](../reference/cli-reference/cli-ref-verify.md).</span><span class="sxs-lookup"><span data-stu-id="18afa-125">You can see the signature details of a given package using [nuget verify](../reference/cli-reference/cli-ref-verify.md).</span></span>

## <a name="register-the-certificate-on-nugetorg"></a><span data-ttu-id="18afa-126">Rejestrowanie certyfikatu w usłudze NuGet.org</span><span class="sxs-lookup"><span data-stu-id="18afa-126">Register the certificate on NuGet.org</span></span>

<span data-ttu-id="18afa-127">Aby opublikować podpisany pakiet, należy najpierw zarejestrować certyfikat z NuGet.org. Certyfikat jest potrzebny jako `.cer` plik w formacie binarnym der.</span><span class="sxs-lookup"><span data-stu-id="18afa-127">To publish a signed package, you must first register the certificate with NuGet.org. You need the certificate as a `.cer` file in a binary DER format.</span></span>

1. <span data-ttu-id="18afa-128">[Zaloguj](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) się do NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="18afa-128">[Sign in](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) to NuGet.org.</span></span>
1. <span data-ttu-id="18afa-129">Przejdź do `Account settings` (lub `Manage Organization` **>** `Edit Organziation` Jeśli chcesz zarejestrować certyfikat przy użyciu konta organizacji).</span><span class="sxs-lookup"><span data-stu-id="18afa-129">Go to `Account settings` (or `Manage Organization` **>** `Edit Organziation` if you would like to register the certificate with an Organization account).</span></span>
1. <span data-ttu-id="18afa-130">Rozwiń `Certificates` sekcję i wybierz pozycję `Register new` .</span><span class="sxs-lookup"><span data-stu-id="18afa-130">Expand the `Certificates` section and select `Register new`.</span></span>
1. <span data-ttu-id="18afa-131">Wyszukaj i wybierz plik certyfikacie, który został wyeksportowany wcześniej.</span><span class="sxs-lookup"><span data-stu-id="18afa-131">Browse and select the certficate file that was exported earlier.</span></span>
  <span data-ttu-id="18afa-132">![Zarejestrowane certyfikaty](../reference/media/registered-certs.png)</span><span class="sxs-lookup"><span data-stu-id="18afa-132">![Registered Certificates](../reference/media/registered-certs.png)</span></span>

<span data-ttu-id="18afa-133">**Uwaga**</span><span class="sxs-lookup"><span data-stu-id="18afa-133">**Note**</span></span>
* <span data-ttu-id="18afa-134">Jeden użytkownik może przesłać wiele certyfikatów i ten sam certyfikat może być zarejestrowany przez wielu użytkowników.</span><span class="sxs-lookup"><span data-stu-id="18afa-134">One user can submit multiple certificates and the same certificate can be registered by multiple users.</span></span>
* <span data-ttu-id="18afa-135">Gdy użytkownik ma zarejestrowany certyfikat, wszystkie przyszłe przesłania pakietu **muszą** być podpisane przy użyciu jednego z certyfikatów.</span><span class="sxs-lookup"><span data-stu-id="18afa-135">Once a user has a certificate registered, all future package submissions **must** be signed with one of the certificates.</span></span> <span data-ttu-id="18afa-136">Zobacz [Zarządzanie wymaganiami dotyczącymi podpisywania pakietu w witrynie NuGet.org](#manage-signing-requirements-for-your-package-on-nugetorg)</span><span class="sxs-lookup"><span data-stu-id="18afa-136">See [Manage signing requirements for your package on NuGet.org](#manage-signing-requirements-for-your-package-on-nugetorg)</span></span>
* <span data-ttu-id="18afa-137">Użytkownicy mogą również usunąć zarejestrowany certyfikat z konta.</span><span class="sxs-lookup"><span data-stu-id="18afa-137">Users can also remove a registered certificate from the account.</span></span> <span data-ttu-id="18afa-138">Po usunięciu certyfikatu nowe pakiety podpisane przy użyciu tego certyfikatu będą kończyć się niepowodzeniem podczas wysyłania.</span><span class="sxs-lookup"><span data-stu-id="18afa-138">Once a certificate is removed, new packages signed with that certificate will fail at submission.</span></span> <span data-ttu-id="18afa-139">Nie ma to wpływu na istniejące pakiety.</span><span class="sxs-lookup"><span data-stu-id="18afa-139">Existing packages aren't affected.</span></span>

## <a name="publish-the-package"></a><span data-ttu-id="18afa-140">Publikowanie pakietu</span><span class="sxs-lookup"><span data-stu-id="18afa-140">Publish the package</span></span>

<span data-ttu-id="18afa-141">Teraz można przystąpić do publikowania pakietu w NuGet.org. Zobacz [Publikowanie pakietów](../nuget-org/Publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="18afa-141">You are now ready to publish the package to NuGet.org. See [Publishing packages](../nuget-org/Publish-a-package.md).</span></span>

## <a name="create-a-test-certificate"></a><span data-ttu-id="18afa-142">Tworzenie certyfikatu testowego</span><span class="sxs-lookup"><span data-stu-id="18afa-142">Create a test certificate</span></span>

<span data-ttu-id="18afa-143">Do celów testowych można użyć certyfikatów wystawionych przez siebie.</span><span class="sxs-lookup"><span data-stu-id="18afa-143">You can use self-issued certificates for testing purposes.</span></span> <span data-ttu-id="18afa-144">Aby utworzyć certyfikat z własnym wystawiony, użyj [polecenia New-SelfSignedCertificate programu PowerShell](/powershell/module/pkiclient/new-selfsignedcertificate).</span><span class="sxs-lookup"><span data-stu-id="18afa-144">To create a self-issued certificate, use the [New-SelfSignedCertificate PowerShell command](/powershell/module/pkiclient/new-selfsignedcertificate).</span></span>

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

<span data-ttu-id="18afa-145">To polecenie umożliwia utworzenie certyfikatu testowego dostępnego w osobistym magazynie certyfikatów bieżącego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="18afa-145">This command creates a testing certificate available in the current user's personal certificate store.</span></span> <span data-ttu-id="18afa-146">Można otworzyć magazyn certyfikatów, uruchamiając program `certmgr.msc` w celu wyświetlenia nowo utworzonego certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="18afa-146">You can open the certificate store by running `certmgr.msc` to see the newly created certificate.</span></span>

> [!Warning]
> <span data-ttu-id="18afa-147">Usługa NuGet.org nie akceptuje pakietów podpisanych za pomocą certyfikatów z podpisem własnym.</span><span class="sxs-lookup"><span data-stu-id="18afa-147">NuGet.org does not accept packages signed with self-issued certificates.</span></span>

## <a name="manage-signing-requirements-for-your-package-on-nugetorg"></a><span data-ttu-id="18afa-148">Zarządzanie wymaganiami dotyczącymi podpisywania pakietu w programie NuGet.org</span><span class="sxs-lookup"><span data-stu-id="18afa-148">Manage signing requirements for your package on NuGet.org</span></span>
1. <span data-ttu-id="18afa-149">[Zaloguj](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) się do NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="18afa-149">[Sign in](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) to NuGet.org.</span></span>

1. <span data-ttu-id="18afa-150">Przejdź do `Manage Packages`  
    ![ konfigurowania podpisywania pakietów](../reference/media/configure-package-signers.png)</span><span class="sxs-lookup"><span data-stu-id="18afa-150">Go to `Manage Packages` 
![Configure package signers](../reference/media/configure-package-signers.png)</span></span>

* <span data-ttu-id="18afa-151">Jeśli jesteś jedynym właścicielem pakietu, jest to wymagana osoba podpisująca. możesz użyć dowolnego z zarejestrowanych certyfikatów do podpisywania i publikowania pakietów w usłudze NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="18afa-151">If you are the sole owner of a package, you are the required signer i.e. you can use any of the registered certificates to sign and publish your packages to NuGet.org.</span></span>

* <span data-ttu-id="18afa-152">Jeśli pakiet ma wielu właścicieli, domyślnie do podpisania pakietu mogą służyć "dowolny" certyfikat właściciela.</span><span class="sxs-lookup"><span data-stu-id="18afa-152">If a package has multiple owners, by default, "Any" owner's certificates can be used to sign the package.</span></span> <span data-ttu-id="18afa-153">Jako współwłaściciel pakietu możesz przesłonić "dowolny" samodzielnie lub innym współpracownikom jako wymaganą rejestrację.</span><span class="sxs-lookup"><span data-stu-id="18afa-153">As a co-owner of the package, you can override "Any" with yourself or any other co-owner to be the required signer.</span></span> <span data-ttu-id="18afa-154">Jeśli utworzysz właściciela, który nie ma żadnego zarejestrowanego certyfikatu, niepodpisane pakiety będą dozwolone.</span><span class="sxs-lookup"><span data-stu-id="18afa-154">If you make an owner  who does not have any certificate registered, then unsigned packages will be allowed.</span></span> 

* <span data-ttu-id="18afa-155">Analogicznie, jeśli wybrana jest domyślna opcja "any" dla pakietu, w którym jeden właściciel ma zarejestrowany certyfikat, a inny właściciel nie ma żadnego zarejestrowanego certyfikatu, NuGet.org akceptuje albo podpisany pakiet z podpisem zarejestrowanym przez jednego z jego właścicieli lub niepodpisanym pakietem (ponieważ jeden z właścicieli nie ma żadnego zarejestrowanego certyfikatu).</span><span class="sxs-lookup"><span data-stu-id="18afa-155">Similarly, if the default "Any" option is selected for a package where one owner has a certificate registered and another owner does not have any certificate registered, then NuGet.org accepts either a signed package with a signature registered by one of its owners or an unsigned package (because one of the owners does not have any certificate registered).</span></span>

## <a name="related-articles"></a><span data-ttu-id="18afa-156">Pokrewne artykuły:</span><span class="sxs-lookup"><span data-stu-id="18afa-156">Related articles</span></span>

- [<span data-ttu-id="18afa-157">Zarządzanie granicami zaufania pakietów</span><span class="sxs-lookup"><span data-stu-id="18afa-157">Manage package trust boundaries</span></span>](../consume-packages/installing-signed-packages.md)
- [<span data-ttu-id="18afa-158">Odwołanie do podpisanych pakietów</span><span class="sxs-lookup"><span data-stu-id="18afa-158">Signed Packages Reference</span></span>](../reference/Signed-Packages-Reference.md)