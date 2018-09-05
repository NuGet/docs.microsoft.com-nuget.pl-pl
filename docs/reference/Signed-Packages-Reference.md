---
title: Podpisanych pakietów
description: Wymagania dotyczące podpisywania pakietu NuGet.
author: rido-min
ms.author: rmpablos
ms.date: 05/18/2018
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: c36db9486ad787f19430c75fc38a2e9dd8ba6e37
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550424"
---
# <a name="signed-packages"></a><span data-ttu-id="4c50a-103">Podpisanych pakietów</span><span class="sxs-lookup"><span data-stu-id="4c50a-103">Signed packages</span></span>

<span data-ttu-id="4c50a-104">*NuGet 4.6.0+ i Visual Studio 2017 w wersji 15.6 i nowszych*</span><span class="sxs-lookup"><span data-stu-id="4c50a-104">*NuGet 4.6.0+ and Visual Studio 2017 version 15.6 and later*</span></span>

<span data-ttu-id="4c50a-105">Pakiety NuGet może zawierać podpis cyfrowy, który zapewnia ochronę przed zmodyfikowany zawartości.</span><span class="sxs-lookup"><span data-stu-id="4c50a-105">NuGet packages can include a digital signature that provides protection against tampered content.</span></span> <span data-ttu-id="4c50a-106">Ta sygnatura jest generowany z certyfikat X.509, który dodaje również autentyczności dowody do rzeczywistego źródła pakietu.</span><span class="sxs-lookup"><span data-stu-id="4c50a-106">This signature is produced from an X.509 certificate that also adds authenticity proofs to the actual origin of the package.</span></span>

<span data-ttu-id="4c50a-107">Podpisanych pakietów zapewnia najsilniejszą weryfikacji end-to-end.</span><span class="sxs-lookup"><span data-stu-id="4c50a-107">Signed packages provide the strongest end-to-end validation.</span></span> <span data-ttu-id="4c50a-108">Istnieją dwa różne typy podpisów NuGet:</span><span class="sxs-lookup"><span data-stu-id="4c50a-108">There are two different types of NuGet signatures:</span></span>
- <span data-ttu-id="4c50a-109">**Tworzenie sygnatury**.</span><span class="sxs-lookup"><span data-stu-id="4c50a-109">**Author Signature**.</span></span> <span data-ttu-id="4c50a-110">Autor podpis gwarantuje, że pakiet nie został zmodyfikowany od czasu Autor podpisania pakietu, niezależnie od którego repozytorium lub co transportu metody jest dostarczany w pakiecie.</span><span class="sxs-lookup"><span data-stu-id="4c50a-110">An author signature guarantees that the package has not been modified since the author signed the package, no matter from which repository or what transport method the package is delivered.</span></span> <span data-ttu-id="4c50a-111">Ponadto podpisane przez autora pakietów zapewniają mechanizm uwierzytelniania dodatkowego do potoku publikowania w witrynie nuget.org, ponieważ certyfikatu podpisywania musi być zarejestrowany wcześniej.</span><span class="sxs-lookup"><span data-stu-id="4c50a-111">Additionally, author-signed packages provide an extra authentication mechanism to the nuget.org publishing pipeline because the signing certificate must be registered ahead of time.</span></span> <span data-ttu-id="4c50a-112">Aby uzyskać więcej informacji, zobacz [rejestrowanie certyfikatów](#register-certificate-on-nugetorg).</span><span class="sxs-lookup"><span data-stu-id="4c50a-112">For more information, see [Register certificates](#register-certificate-on-nugetorg).</span></span>
- <span data-ttu-id="4c50a-113">**Podpis repozytorium**.</span><span class="sxs-lookup"><span data-stu-id="4c50a-113">**Repository Signature**.</span></span> <span data-ttu-id="4c50a-114">Podpisy repozytorium zapewniają gwarancji spójności dla **wszystkich** pakietów w repozytorium, czy są one podpisane lub nie, autor, nawet wtedy, gdy te pakiety są uzyskiwane z innej lokalizacji niż oryginalny repozytorium, gdzie znajdowały się podpisany.</span><span class="sxs-lookup"><span data-stu-id="4c50a-114">Repository signatures provide an integrity guarantee for **all** packages in a repository whether they are author signed or not, even if those packages are obtained from a different location than the original repository where they were signed.</span></span>   

<span data-ttu-id="4c50a-115">Aby uzyskać szczegółowe informacje na temat tworzenia pakietu podpisem autora, zobacz [podpisywanie pakietów](../create-packages/Sign-a-package.md) i [polecenie logowania nuget](../tools/cli-ref-sign.md).</span><span class="sxs-lookup"><span data-stu-id="4c50a-115">For details on creating an author signed package, see [Signing Packages](../create-packages/Sign-a-package.md) and the [nuget sign command](../tools/cli-ref-sign.md).</span></span>

> [!Important]
> <span data-ttu-id="4c50a-116">Podpisywanie pakietów jest obecnie obsługiwana tylko wtedy, gdy za pomocą nuget.exe na Windows.</span><span class="sxs-lookup"><span data-stu-id="4c50a-116">Package signing is currently supported only when using nuget.exe on Windows.</span></span> <span data-ttu-id="4c50a-117">Weryfikacja podpisanych pakietów jest obecnie obsługiwana tylko wtedy, gdy za pomocą nuget.exe lub Visual Studio na Windows.</span><span class="sxs-lookup"><span data-stu-id="4c50a-117">Verification of signed packages is currently supported only when using nuget.exe or Visual Studio on Windows.</span></span>

## <a name="certificate-requirements"></a><span data-ttu-id="4c50a-118">Wymagania certyfikatu</span><span class="sxs-lookup"><span data-stu-id="4c50a-118">Certificate requirements</span></span>

<span data-ttu-id="4c50a-119">Podpisywanie pakietów wymaga podpisywania certyfikatu, który to specjalny typ certyfikatu, który nadaje się do kodu `id-kp-codeSigning` cel [[RFC 5280 sekcji 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span><span class="sxs-lookup"><span data-stu-id="4c50a-119">Package signing requires a code signing certificate, which is a special type of certificate that is valid for the `id-kp-codeSigning` purpose [[RFC 5280 section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span></span> <span data-ttu-id="4c50a-120">Ponadto certyfikat musi mieć publicznego długość klucza RSA 2048 bitów lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="4c50a-120">Additionally, the certificate must have an RSA public key length of 2048 bits or higher.</span></span>

## <a name="get-a-code-signing-certificate"></a><span data-ttu-id="4c50a-121">Uzyskaj certyfikat podpisywania kodu</span><span class="sxs-lookup"><span data-stu-id="4c50a-121">Get a code signing certificate</span></span>

<span data-ttu-id="4c50a-122">Prawidłowe certyfikaty mogą być uzyskane z publicznego urzędu certyfikacji takich jak:</span><span class="sxs-lookup"><span data-stu-id="4c50a-122">Valid certificates may be obtained from a public certificate authority like:</span></span>

- [<span data-ttu-id="4c50a-123">Symantec</span><span class="sxs-lookup"><span data-stu-id="4c50a-123">Symantec</span></span>](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3)
- [<span data-ttu-id="4c50a-124">DigiCert</span><span class="sxs-lookup"><span data-stu-id="4c50a-124">DigiCert</span></span>](https://www.digicert.com/code-signing/)
- [<span data-ttu-id="4c50a-125">Go Daddy</span><span class="sxs-lookup"><span data-stu-id="4c50a-125">Go Daddy</span></span>](https://www.godaddy.com/web-security/code-signing-certificate)
- [<span data-ttu-id="4c50a-126">Globalne logowania</span><span class="sxs-lookup"><span data-stu-id="4c50a-126">Global Sign</span></span>](https://www.globalsign.com/en/code-signing-certificate/)
- [<span data-ttu-id="4c50a-127">Comodo</span><span class="sxs-lookup"><span data-stu-id="4c50a-127">Comodo</span></span>](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php)
- [<span data-ttu-id="4c50a-128">Certum</span><span class="sxs-lookup"><span data-stu-id="4c50a-128">Certum</span></span>](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml) 

<span data-ttu-id="4c50a-129">Pełną listę urzędy certyfikacji używane przez Windows można uzyskać z [ http://aka.ms/trustcertpartners ](http://aka.ms/trustcertpartners).</span><span class="sxs-lookup"><span data-stu-id="4c50a-129">The complete list of certification authorities trusted by Windows can be obtained from [http://aka.ms/trustcertpartners](http://aka.ms/trustcertpartners).</span></span>

## <a name="create-a-test-certificate"></a><span data-ttu-id="4c50a-130">Utwórz certyfikat testowy</span><span class="sxs-lookup"><span data-stu-id="4c50a-130">Create a test certificate</span></span>

<span data-ttu-id="4c50a-131">Można użyć własnym wystawionych certyfikatów do celów testowych.</span><span class="sxs-lookup"><span data-stu-id="4c50a-131">You can use self-issued certificates for testing purposes.</span></span> <span data-ttu-id="4c50a-132">Aby utworzyć własny wystawionego certyfikatu, użyj [polecenia PowerShell New-SelfSignedCertificate](/powershell/module/pkiclient/new-selfsignedcertificate.md).</span><span class="sxs-lookup"><span data-stu-id="4c50a-132">To create a self-issued certificate, use the [New-SelfSignedCertificate PowerShell command](/powershell/module/pkiclient/new-selfsignedcertificate.md).</span></span>

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

<span data-ttu-id="4c50a-133">To polecenie tworzy certyfikat testowania dostępności w magazynie certyfikatów osobistych bieżącego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="4c50a-133">This command creates a testing certificate available in the current user's personal certificate store.</span></span> <span data-ttu-id="4c50a-134">Można otworzyć magazynu certyfikatów, uruchamiając `certmgr.msc` aby zobaczyć nowo utworzonego certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="4c50a-134">You can open the certificate store by running `certmgr.msc` to see the newly created certificate.</span></span>

> [!Warning]
> <span data-ttu-id="4c50a-135">nuget.org nie akceptuje pakietów podpisany przy użyciu własnym wystawionych certyfikatów.</span><span class="sxs-lookup"><span data-stu-id="4c50a-135">nuget.org does not accept packages signed with self-issued certificates.</span></span>

## <a name="timestamp-requirements"></a><span data-ttu-id="4c50a-136">Wymagania dotyczące znacznik czasu:</span><span class="sxs-lookup"><span data-stu-id="4c50a-136">Timestamp requirements</span></span>

<span data-ttu-id="4c50a-137">Podpisanych pakietów powinien zawierać znacznik czasu RFC 3161 w celu zapewnienia walidacji podpisu poza podpisywania okresu ważności certyfikatu pakietu.</span><span class="sxs-lookup"><span data-stu-id="4c50a-137">Signed packages should include an RFC 3161 timestamp to ensure signature validity beyond the package signing certificate's validity period.</span></span> <span data-ttu-id="4c50a-138">Certyfikat używany do podpisywania to sygnatura czasowa muszą być prawidłowe dla `id-kp-timeStamping` cel [[RFC 5280 sekcji 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span><span class="sxs-lookup"><span data-stu-id="4c50a-138">The certificate used to sign the timestamp must be valid for the `id-kp-timeStamping` purpose [[RFC 5280 section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span></span> <span data-ttu-id="4c50a-139">Ponadto certyfikat musi mieć publicznego długość klucza RSA 2048 bitów lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="4c50a-139">Additionally, the certificate must have an RSA public key length of 2048 bits or higher.</span></span>

<span data-ttu-id="4c50a-140">Dodatkowe szczegóły techniczne można znaleźć w [specyfikacje techniczne podpisu pakietu](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) (GitHub).</span><span class="sxs-lookup"><span data-stu-id="4c50a-140">Additional technical details can be found in the [package signature technical specs](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) (GitHub).</span></span>

## <a name="signature-requirements-on-nugetorg"></a><span data-ttu-id="4c50a-141">Wymagania dotyczące podpisu w witrynie nuget.org</span><span class="sxs-lookup"><span data-stu-id="4c50a-141">Signature requirements on nuget.org</span></span>

<span data-ttu-id="4c50a-142">nuget.org ma dodatkowe wymagania dotyczące zaakceptowanie podpisanych pakietów:</span><span class="sxs-lookup"><span data-stu-id="4c50a-142">nuget.org has additional requirements for accepting a signed package:</span></span>

- <span data-ttu-id="4c50a-143">Podpis podstawowy musi mieć podpis autora.</span><span class="sxs-lookup"><span data-stu-id="4c50a-143">The primary signature must be an author signature.</span></span>
- <span data-ttu-id="4c50a-144">Podpis podstawowy musi mieć pojedynczy prawidłową sygnaturę czasową.</span><span class="sxs-lookup"><span data-stu-id="4c50a-144">The primary signature must have a single valid timestamp.</span></span>
- <span data-ttu-id="4c50a-145">Certyfikaty X.509 dla podpisu autora i jeho signatura sygnatura czasowa:</span><span class="sxs-lookup"><span data-stu-id="4c50a-145">The X.509 certificates for both the author signature and its timestamp signature:</span></span>
  - <span data-ttu-id="4c50a-146">Musi mieć klucz publiczny RSA 2048 bitów lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="4c50a-146">Must have an RSA public key 2048 bits or greater.</span></span>
  - <span data-ttu-id="4c50a-147">Musi być w okresie ważności na bieżący czas UTC, podczas weryfikacji pakietu w witrynie nuget.org.</span><span class="sxs-lookup"><span data-stu-id="4c50a-147">Must be within its validity period per current UTC time at time of package validation on nuget.org.</span></span>
  - <span data-ttu-id="4c50a-148">Muszą być powiązane z zaufanego głównego urzędu certyfikacji, który jest zaufany domyślnie w systemie Windows.</span><span class="sxs-lookup"><span data-stu-id="4c50a-148">Must chain to a trusted root authority that is trusted by default on Windows.</span></span> <span data-ttu-id="4c50a-149">Pakiety podpisany przy użyciu własnym wystawionych certyfikatów są odrzucane.</span><span class="sxs-lookup"><span data-stu-id="4c50a-149">Packages signed with self-issued certificates are rejected.</span></span>
  - <span data-ttu-id="4c50a-150">Musi być ważny przez jej przeznaczenie:</span><span class="sxs-lookup"><span data-stu-id="4c50a-150">Must be valid for its purpose:</span></span> 
    - <span data-ttu-id="4c50a-151">Tworzenie certyfikatu podpisywania musi być prawidłowy do podpisywania kodu.</span><span class="sxs-lookup"><span data-stu-id="4c50a-151">The author signing certificate must be valid for code signing.</span></span>
    - <span data-ttu-id="4c50a-152">Znacznik czasu: musi to być nieprawidłowy dla użycia.</span><span class="sxs-lookup"><span data-stu-id="4c50a-152">The timestamp certificate must be valid for timestamping.</span></span>
  - <span data-ttu-id="4c50a-153">Nie musi zostać cofnięta podczas podpisywania czasu.</span><span class="sxs-lookup"><span data-stu-id="4c50a-153">Must not be revoked at signing time.</span></span> <span data-ttu-id="4c50a-154">(To nie będzie knowable w chwili przesyłania, więc nuget.org okresowo sprawdza ponownie stanu odwołania).</span><span class="sxs-lookup"><span data-stu-id="4c50a-154">(This may not be knowable at submission time, so nuget.org periodically rechecks revocation status).</span></span>

## <a name="register-certificate-on-nugetorg"></a><span data-ttu-id="4c50a-155">Zarejestruj certyfikat w witrynie nuget.org</span><span class="sxs-lookup"><span data-stu-id="4c50a-155">Register certificate on nuget.org</span></span>

<span data-ttu-id="4c50a-156">Aby przesłać pakiet podpisem, należy zarejestrować certyfikat za pomocą nuget.org. Wymagany certyfikat jako `.cer` pliku w formacie binarnym DER.</span><span class="sxs-lookup"><span data-stu-id="4c50a-156">To submit a signed package, you must first register the certificate with nuget.org. You need the certificate as a `.cer` file in a binary DER format.</span></span> <span data-ttu-id="4c50a-157">Możesz wyeksportować istniejący certyfikat na format binarny DER, za pomocą Kreatora eksportu certyfikatów.</span><span class="sxs-lookup"><span data-stu-id="4c50a-157">You can export an existing certificate to a binary DER format by using the Certificate Export Wizard.</span></span>

![Kreator eksportu certyfikatów](media/CertificateExportWizard.png)

<span data-ttu-id="4c50a-159">Zaawansowani użytkownicy można wyeksportować certyfikatu za pomocą [polecenia PowerShell eksportu certyfikatu](/powershell/module/pkiclient/export-certificate.md).</span><span class="sxs-lookup"><span data-stu-id="4c50a-159">Advanced users can export the certificate using the [Export-Certificate PowerShell command](/powershell/module/pkiclient/export-certificate.md).</span></span>

<span data-ttu-id="4c50a-160">Aby zarejestrować certyfikat za pomocą nuget.org, przejdź do `Certificates` sekcji na `Account settings` stronie (lub na stronie Ustawienia w organizacji) i wybierz `Register new certificate`.</span><span class="sxs-lookup"><span data-stu-id="4c50a-160">To register the certificate with nuget.org, go to `Certificates` section on `Account settings` page (or the Organization's settings page) and select `Register new certificate`.</span></span>

![Certyfikaty zarejestrowane](media/registered-certs.png)

> [!Tip]
> <span data-ttu-id="4c50a-162">Jeden użytkownik może przesłać ten sam certyfikat i wielu certyfikatów, które mogą być rejestrowane przez wielu użytkowników.</span><span class="sxs-lookup"><span data-stu-id="4c50a-162">One user can submit multiple certificates and the same certificate can be registered by multiple users.</span></span>

<span data-ttu-id="4c50a-163">Po użytkownik ma zarejestrowane certyfikatu, wszystkie przyszłe pakietu przesłania **musi** być podpisane przy użyciu jednego z certyfikatów.</span><span class="sxs-lookup"><span data-stu-id="4c50a-163">Once a user has a certificate registered, all future package submissions **must** be signed with one of the certificates.</span></span>

<span data-ttu-id="4c50a-164">Użytkownicy mogą również usuwać certyfikat zarejestrowany z konta.</span><span class="sxs-lookup"><span data-stu-id="4c50a-164">Users can also remove a registered certificate from the account.</span></span> <span data-ttu-id="4c50a-165">Po usunięciu certyfikatu na przesłanie się nie powieść pakietów podpisane przy użyciu tego certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="4c50a-165">Once a certificate is removed, packages signed with that certificate fail at submission.</span></span> <span data-ttu-id="4c50a-166">Nie ma wpływu na istniejące pakiety.</span><span class="sxs-lookup"><span data-stu-id="4c50a-166">Existing packages aren't affected.</span></span>

## <a name="configure-package-signing-requirements"></a><span data-ttu-id="4c50a-167">Skonfiguruj wymagania dotyczące podpisywania pakietu</span><span class="sxs-lookup"><span data-stu-id="4c50a-167">Configure package signing requirements</span></span>

<span data-ttu-id="4c50a-168">Jeśli jesteś jedynym właścicielem pakietu, jest to wymagane osoby podpisującej.</span><span class="sxs-lookup"><span data-stu-id="4c50a-168">If you are the sole owner of a package, you are the required signer.</span></span> <span data-ttu-id="4c50a-169">Oznacza to, że umożliwia dowolny zarejestrowane certyfikaty podpisywania pakietów i przekazywania na stronie nuget.org.</span><span class="sxs-lookup"><span data-stu-id="4c50a-169">That is, you can use any of the registered certificates to sign your packages and submit to nuget.org.</span></span>

<span data-ttu-id="4c50a-170">Jeżeli pakiet zawiera wiele właścicieli, domyślnie, certyfikaty "Dowolna" właściciel może służyć do podpisania pakietu.</span><span class="sxs-lookup"><span data-stu-id="4c50a-170">If a package has multiple owners, by default, "Any" owner's certificates can be used to sign the package.</span></span> <span data-ttu-id="4c50a-171">Jako współwłaściciela pakietu można zastąpić "Dowolne", przy użyciu samodzielnie lub wszelkie inne współwłaścicielem jako wymagane osoby podpisującej.</span><span class="sxs-lookup"><span data-stu-id="4c50a-171">As a co-owner of the package, you can override "Any" with yourself or any other co-owner to be the required signer.</span></span> <span data-ttu-id="4c50a-172">W przypadku wprowadzenia właściciela, który nie ma żadnych certyfikatów zarejestrowanych pakietów niepodpisane będą dozwolone.</span><span class="sxs-lookup"><span data-stu-id="4c50a-172">If you make an owner  who does not have any certificate registered, then unsigned packages will be allowed.</span></span> 

<span data-ttu-id="4c50a-173">Podobnie, jeśli wartość domyślna "Dowolna" opcja jest zaznaczona dla pakietu, w której jeden właściciel ma certyfikat zarejestrowany i innego właściciela nie ma żadnych certyfikatów zarejestrowanych, następnie nuget.org akceptuje podpisanych pakietów za pomocą podpisu zarejestrowany za pomocą jednej z jego właścicieli lub Niepodpisany pakietu (ponieważ jest to jeden z właścicieli nie ma żadnych certyfikatów zarejestrowanych).</span><span class="sxs-lookup"><span data-stu-id="4c50a-173">Similarly, if the default "Any" option is selected for a package where one owner has a certificate registered and another owner does not have any certificate registered, then nuget.org accepts either a signed package with a signature registered by one of its owners or an unsigned package (because one of the owners does not have any certificate registered).</span></span>

![Konfigurowanie pakietów, które podpisały](media/configure-package-signers.png)
