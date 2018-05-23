---
title: Podpisanych pakietów
description: Wymagania dotyczące podpisywania pakietu NuGet.
author: rido-min
ms.author: rmpablos
manager: unnir
ms.date: 05/18/2018
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: 72fb1a87c13160c53f632d2ef87a12a4e9bc02a3
ms.sourcegitcommit: 8127dd73ff8481a1a01acd9b7004dd131a9d84e7
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/22/2018
---
# <a name="signed-packages"></a><span data-ttu-id="e1f3a-103">Pakiety podpisem</span><span class="sxs-lookup"><span data-stu-id="e1f3a-103">Signed packages</span></span>

<span data-ttu-id="e1f3a-104">*NuGet 4.6.0+ i Visual Studio 2017 wersji 15.6 i nowsze*</span><span class="sxs-lookup"><span data-stu-id="e1f3a-104">*NuGet 4.6.0+ and Visual Studio 2017 version 15.6 and later*</span></span>

<span data-ttu-id="e1f3a-105">Pakiety NuGet mogą zawierać podpis cyfrowy, który zapewnia ochronę przed zmodyfikowany zawartości.</span><span class="sxs-lookup"><span data-stu-id="e1f3a-105">NuGet packages can include a digital signature that provides protection against tampered content.</span></span> <span data-ttu-id="e1f3a-106">Ta sygnatura jest tworzony z certyfikatu X.509, który dodaje również dowody autentyczności do rzeczywistego źródła pakietu.</span><span class="sxs-lookup"><span data-stu-id="e1f3a-106">This signature is produced from an X.509 certificate that also adds authenticity proofs to the actual origin of the package.</span></span>

<span data-ttu-id="e1f3a-107">Pakiety podpisem udostępnienia najwyższy weryfikacji end-to-end.</span><span class="sxs-lookup"><span data-stu-id="e1f3a-107">Signed packages provide the strongest end-to-end validation.</span></span> <span data-ttu-id="e1f3a-108">Autor podpis gwarantuje, że pakiet nie został zmodyfikowany od czasu autora podpisania pakietu, niezależnie od którego repozytorium lub co metoda jest dostarczany pakiet transportu.</span><span class="sxs-lookup"><span data-stu-id="e1f3a-108">An author signature guarantees that the package has not been modified since the author signed the package, no matter from which repository or what transport method the package is delivered.</span></span>

<span data-ttu-id="e1f3a-109">Ponadto pakiety podpisane przez autora udostępniają mechanizm uwierzytelniania dodatkowego do potoku publikowania nuget.org, ponieważ certyfikat podpisywania musi być zarejestrowana wcześniejsze.</span><span class="sxs-lookup"><span data-stu-id="e1f3a-109">Additionally, author-signed packages provide an extra authentication mechanism to the nuget.org publishing pipeline because the signing certificate must be registered ahead of time.</span></span> <span data-ttu-id="e1f3a-110">Aby uzyskać więcej informacji, zobacz [rejestrowanie certyfikatów](#register-certificate-on-nugetorg).</span><span class="sxs-lookup"><span data-stu-id="e1f3a-110">For more information, see [Register certificates](#register-certificate-on-nugetorg).</span></span>

<span data-ttu-id="e1f3a-111">Aby uzyskać więcej informacji na temat tworzenia podpisanego pakietu, zobacz [podpisywania pakietów](../create-packages/Sign-a-package.md) i [polecenia nuget znak](../tools/cli-ref-sign.md).</span><span class="sxs-lookup"><span data-stu-id="e1f3a-111">For details on creating a signed package, see [Signing Packages](../create-packages/Sign-a-package.md) and the [nuget sign command](../tools/cli-ref-sign.md).</span></span>

> [!Important]
> <span data-ttu-id="e1f3a-112">Podpisywanie pakietu jest obecnie obsługiwany tylko w przypadku używania nuget.exe w systemie Windows.</span><span class="sxs-lookup"><span data-stu-id="e1f3a-112">Package signing is currently supported only when using nuget.exe on Windows.</span></span> <span data-ttu-id="e1f3a-113">Weryfikacja podpisanych pakietów jest obecnie obsługiwany tylko w przypadku używania nuget.exe lub Visual Studio w systemie Windows.</span><span class="sxs-lookup"><span data-stu-id="e1f3a-113">Verification of signed packages is currently supported only when using nuget.exe or Visual Studio on Windows.</span></span>

## <a name="certificate-requirements"></a><span data-ttu-id="e1f3a-114">Wymagania certyfikatu</span><span class="sxs-lookup"><span data-stu-id="e1f3a-114">Certificate requirements</span></span>

<span data-ttu-id="e1f3a-115">Podpisywanie pakietu wymaga podpisywania certyfikatu, który jest specjalny typ certyfikatu, który jest prawidłowy dla kodu `id-kp-codeSigning` cel [[RFC 5280 sekcji 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span><span class="sxs-lookup"><span data-stu-id="e1f3a-115">Package signing requires a code signing certificate, which is a special type of certificate that is valid for the `id-kp-codeSigning` purpose [[RFC 5280 section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span></span> <span data-ttu-id="e1f3a-116">Ponadto certyfikat musi mieć publiczny długość klucza RSA 2048 bitów lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="e1f3a-116">Additionally, the certificate must have an RSA public key length of 2048 bits or higher.</span></span>

## <a name="get-a-code-signing-certificate"></a><span data-ttu-id="e1f3a-117">Uzyskaj certyfikat podpisywania kodu</span><span class="sxs-lookup"><span data-stu-id="e1f3a-117">Get a code signing certificate</span></span>

<span data-ttu-id="e1f3a-118">Prawidłowe certyfikaty można uzyskać od urzędu certyfikacji publicznej, takich jak:</span><span class="sxs-lookup"><span data-stu-id="e1f3a-118">Valid certificates may be obtained from a public certificate authority like:</span></span>

- [<span data-ttu-id="e1f3a-119">Symantec</span><span class="sxs-lookup"><span data-stu-id="e1f3a-119">Symantec</span></span>](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3)
- [<span data-ttu-id="e1f3a-120">DigiCert</span><span class="sxs-lookup"><span data-stu-id="e1f3a-120">DigiCert</span></span>](https://www.digicert.com/code-signing/)
- [<span data-ttu-id="e1f3a-121">Go Daddy</span><span class="sxs-lookup"><span data-stu-id="e1f3a-121">Go Daddy</span></span>](https://www.godaddy.com/web-security/code-signing-certificate)
- [<span data-ttu-id="e1f3a-122">Globalne logowania</span><span class="sxs-lookup"><span data-stu-id="e1f3a-122">Global Sign</span></span>](https://www.globalsign.com/en/code-signing-certificate/)
- [<span data-ttu-id="e1f3a-123">Comodo</span><span class="sxs-lookup"><span data-stu-id="e1f3a-123">Comodo</span></span>](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php)
- [<span data-ttu-id="e1f3a-124">Certum</span><span class="sxs-lookup"><span data-stu-id="e1f3a-124">Certum</span></span>](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml) 

<span data-ttu-id="e1f3a-125">Pełna lista urzędów certyfikacji ufa systemu Windows można uzyskać z [ http://aka.ms/trustcertpartners ](http://aka.ms/trustcertpartners).</span><span class="sxs-lookup"><span data-stu-id="e1f3a-125">The complete list of certification authorities trusted by Windows can be obtained from [http://aka.ms/trustcertpartners](http://aka.ms/trustcertpartners).</span></span>

## <a name="create-a-test-certificate"></a><span data-ttu-id="e1f3a-126">Tworzenie certyfikatu testowego</span><span class="sxs-lookup"><span data-stu-id="e1f3a-126">Create a test certificate</span></span>

<span data-ttu-id="e1f3a-127">Wystawiony samodzielnie Certyfikaty służy do celów testowych.</span><span class="sxs-lookup"><span data-stu-id="e1f3a-127">You can use self-issued certificates for testing purposes.</span></span> <span data-ttu-id="e1f3a-128">Aby utworzyć certyfikat wystawiony samodzielnie, użyj [polecenia New-SelfSignedCertificate PowerShell](/powershell/module/pkiclient/new-selfsignedcertificate.md).</span><span class="sxs-lookup"><span data-stu-id="e1f3a-128">To create a self-issued certificate, use the [New-SelfSignedCertificate PowerShell command](/powershell/module/pkiclient/new-selfsignedcertificate.md).</span></span>

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

<span data-ttu-id="e1f3a-129">To polecenie tworzy testowania dostępny certyfikat w magazynie certyfikatów osobistych bieżącego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="e1f3a-129">This command creates a testing certificate available in the current user's personal certificate store.</span></span> <span data-ttu-id="e1f3a-130">Można otworzyć magazynu certyfikatów, uruchamiając `certmgr.msc` wyświetlić nowo utworzony certyfikat.</span><span class="sxs-lookup"><span data-stu-id="e1f3a-130">You can open the certificate store by running `certmgr.msc` to see the newly created certificate.</span></span>

> [!Warning]
> <span data-ttu-id="e1f3a-131">nuget.org nie akceptuje pakietów podpisane własnym wystawionych certyfikatów.</span><span class="sxs-lookup"><span data-stu-id="e1f3a-131">nuget.org does not accept packages signed with self-issued certificates.</span></span>

## <a name="timestamp-requirements"></a><span data-ttu-id="e1f3a-132">Wymagania dotyczące sygnatury czasowej</span><span class="sxs-lookup"><span data-stu-id="e1f3a-132">Timestamp requirements</span></span>

<span data-ttu-id="e1f3a-133">Pakiety podpisem powinna zawierać znaczników czasu RFC 3161 do zapewnienia walidacji podpisu poza okres ważności certyfikatu podpisywania pakietu.</span><span class="sxs-lookup"><span data-stu-id="e1f3a-133">Signed packages should include an RFC 3161 timestamp to ensure signature validity beyond the package signing certificate's validity period.</span></span> <span data-ttu-id="e1f3a-134">Certyfikat używany do podpisywania sygnatura czasowa musi być prawidłowy dla `id-kp-timeStamping` cel [[RFC 5280 sekcji 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span><span class="sxs-lookup"><span data-stu-id="e1f3a-134">The certificate used to sign the timestamp must be valid for the `id-kp-timeStamping` purpose [[RFC 5280 section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span></span> <span data-ttu-id="e1f3a-135">Ponadto certyfikat musi mieć publiczny długość klucza RSA 2048 bitów lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="e1f3a-135">Additionally, the certificate must have an RSA public key length of 2048 bits or higher.</span></span>

<span data-ttu-id="e1f3a-136">Dodatkowe szczegóły techniczne można znaleźć w [specyfikacji technicznej podpisu pakietu](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) (GitHub).</span><span class="sxs-lookup"><span data-stu-id="e1f3a-136">Additional technical details can be found in the [package signature technical specs](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) (GitHub).</span></span>

## <a name="signature-requirements-on-nugetorg"></a><span data-ttu-id="e1f3a-137">Wymagania dotyczące podpisu na nuget.org</span><span class="sxs-lookup"><span data-stu-id="e1f3a-137">Signature requirements on nuget.org</span></span>

<span data-ttu-id="e1f3a-138">nuget.org ma dodatkowe wymagania dotyczące akceptowania podpisanego pakietu:</span><span class="sxs-lookup"><span data-stu-id="e1f3a-138">nuget.org has additional requirements for accepting a signed package:</span></span>

- <span data-ttu-id="e1f3a-139">Podpis podstawowy musi być podpis autora.</span><span class="sxs-lookup"><span data-stu-id="e1f3a-139">The primary signature must be an author signature.</span></span>
- <span data-ttu-id="e1f3a-140">Podpis podstawowy musi mieć pojedynczy prawidłowy sygnatury czasowej.</span><span class="sxs-lookup"><span data-stu-id="e1f3a-140">The primary signature must have a single valid timestamp.</span></span>
- <span data-ttu-id="e1f3a-141">Certyfikaty X.509 dla podpisu autora i podpis sygnatura czasowa:</span><span class="sxs-lookup"><span data-stu-id="e1f3a-141">The X.509 certificates for both the author signature and its timestamp signature:</span></span>
  - <span data-ttu-id="e1f3a-142">Musi mieć klucza publicznego RSA 2048 bitów lub większej.</span><span class="sxs-lookup"><span data-stu-id="e1f3a-142">Must have an RSA public key 2048 bits or greater.</span></span>
  - <span data-ttu-id="e1f3a-143">Musi być w okresie ważności na bieżący czas UTC podczas sprawdzania poprawności pakietu na nuget.org.</span><span class="sxs-lookup"><span data-stu-id="e1f3a-143">Must be within its validity period per current UTC time at time of package validation on nuget.org.</span></span>
  - <span data-ttu-id="e1f3a-144">Muszą być powiązane z zaufanego głównego urzędu zaufanej domyślnie w systemie Windows.</span><span class="sxs-lookup"><span data-stu-id="e1f3a-144">Must chain to a trusted root authority that is trusted by default on Windows.</span></span> <span data-ttu-id="e1f3a-145">Pakiety podpisane własnym wystawione certyfikaty są odrzucane.</span><span class="sxs-lookup"><span data-stu-id="e1f3a-145">Packages signed with self-issued certificates are rejected.</span></span>
  - <span data-ttu-id="e1f3a-146">Musi być prawidłową celowi:</span><span class="sxs-lookup"><span data-stu-id="e1f3a-146">Must be valid for its purpose:</span></span> 
    - <span data-ttu-id="e1f3a-147">Tworzenie certyfikatu podpisywania musi być prawidłowy do podpisywania kodu.</span><span class="sxs-lookup"><span data-stu-id="e1f3a-147">The author signing certificate must be valid for code signing.</span></span>
    - <span data-ttu-id="e1f3a-148">Sygnatura czasowa certyfikatu musi być prawidłowy dla użycia.</span><span class="sxs-lookup"><span data-stu-id="e1f3a-148">The timestamp certificate must be valid for timestamping.</span></span>
  - <span data-ttu-id="e1f3a-149">Nie musi zostać odwołany podczas podpisywania czasu.</span><span class="sxs-lookup"><span data-stu-id="e1f3a-149">Must not be revoked at signing time.</span></span> <span data-ttu-id="e1f3a-150">(To nie będzie knowable podczas przesyłania, więc nuget.org okresowo sprawdza ponownie stanu odwołania).</span><span class="sxs-lookup"><span data-stu-id="e1f3a-150">(This may not be knowable at submission time, so nuget.org periodically rechecks revocation status).</span></span>

## <a name="register-certificate-on-nugetorg"></a><span data-ttu-id="e1f3a-151">Zarejestruj certyfikat na nuget.org</span><span class="sxs-lookup"><span data-stu-id="e1f3a-151">Register certificate on nuget.org</span></span>

<span data-ttu-id="e1f3a-152">Aby przesłać pakiet podpisem, najpierw należy zarejestrować certyfikat z nuget.org. Wymagany jest certyfikat jako `.cer` pliku w formacie binarnym DER.</span><span class="sxs-lookup"><span data-stu-id="e1f3a-152">To submit a signed package, you must first register the certificate with nuget.org. You need the certificate as a `.cer` file in a binary DER format.</span></span> <span data-ttu-id="e1f3a-153">Możesz wyeksportować istniejącego certyfikatu na format binarny DER przy użyciu Kreatora eksportu certyfikatów.</span><span class="sxs-lookup"><span data-stu-id="e1f3a-153">You can export an existing certificate to a binary DER format by using the Certificate Export Wizard.</span></span>

![Kreator eksportu certyfikatów](media/CertificateExportWizard.png)

<span data-ttu-id="e1f3a-155">Użytkownicy wersji Advanced można wyeksportować certyfikat przy użyciu [polecenia programu PowerShell eksportu certyfikatu](/powershell/module/pkiclient/export-certificate.md).</span><span class="sxs-lookup"><span data-stu-id="e1f3a-155">Advanced users can export the certificate using the [Export-Certificate PowerShell command](/powershell/module/pkiclient/export-certificate.md).</span></span>

<span data-ttu-id="e1f3a-156">Aby zarejestrować certyfikat z nuget.org, przejdź do `Certificates` sekcji na `Account settings` (lub strona Ustawienia organizacji) i wybierz `Register new certificate`.</span><span class="sxs-lookup"><span data-stu-id="e1f3a-156">To register the certificate with nuget.org, go to `Certificates` section on `Account settings` page (or the Organization's settings page) and select `Register new certificate`.</span></span>

![Zarejestrowane certyfikaty](media/registered-certs.png)

> [!Tip]
> <span data-ttu-id="e1f3a-158">Jeden z użytkowników mogą przesyłać wiele certyfikatów i tego samego certyfikatu można zarejestrowanych przez wielu użytkowników.</span><span class="sxs-lookup"><span data-stu-id="e1f3a-158">One user can submit multiple certificates and the same certificate can be registered by multiple users.</span></span>

<span data-ttu-id="e1f3a-159">Gdy użytkownik ma certyfikat zarejestrowany, wszystkie przyszłe pakietu przesłanych **musi** podpisywany z jednego z certyfikatów.</span><span class="sxs-lookup"><span data-stu-id="e1f3a-159">Once a user has a certificate registered, all future package submissions **must** be signed with one of the certificates.</span></span>

<span data-ttu-id="e1f3a-160">Użytkownicy mogą również usuwać zarejestrowany certyfikat z konta.</span><span class="sxs-lookup"><span data-stu-id="e1f3a-160">Users can also remove a registered certificate from the account.</span></span> <span data-ttu-id="e1f3a-161">Po usunięciu certyfikatu z takim podpisem pakietów się nie powieść w przesyłania.</span><span class="sxs-lookup"><span data-stu-id="e1f3a-161">Once a certificate is removed, packages signed with that certificate fail at submission.</span></span> <span data-ttu-id="e1f3a-162">Nie ma wpływu na istniejące pakiety.</span><span class="sxs-lookup"><span data-stu-id="e1f3a-162">Existing packages aren't affected.</span></span>

## <a name="configure-package-signing-requirements"></a><span data-ttu-id="e1f3a-163">Skonfiguruj wymagania dotyczące podpisywania pakietu</span><span class="sxs-lookup"><span data-stu-id="e1f3a-163">Configure package signing requirements</span></span>

<span data-ttu-id="e1f3a-164">Jeśli jesteś jedynym właścicielem pakietu jest wymagany podpis.</span><span class="sxs-lookup"><span data-stu-id="e1f3a-164">If you are the sole owner of a package, you are the required signer.</span></span> <span data-ttu-id="e1f3a-165">Oznacza to, że służy wszelkie zarejestrowane certyfikaty do podpisywania pakietów i przedstawia nuget.org.</span><span class="sxs-lookup"><span data-stu-id="e1f3a-165">That is, you can use any of the registered certificates to sign your packages and submit to nuget.org.</span></span>

<span data-ttu-id="e1f3a-166">Jeżeli pakiet zawiera wiele właścicieli, domyślnie, "Wszystkie" właściciel certyfikaty mogą służyć do podpisania pakietu.</span><span class="sxs-lookup"><span data-stu-id="e1f3a-166">If a package has multiple owners, by default, "Any" owner's certificates can be used to sign the package.</span></span> <span data-ttu-id="e1f3a-167">Jako współwłaściciel pakietu można zastąpić "Dowolnego" siebie lub wszelkie inne współwłaściciel jako wymagany podpis.</span><span class="sxs-lookup"><span data-stu-id="e1f3a-167">As a co-owner of the package, you can override "Any" with yourself or any other co-owner to be the required signer.</span></span> <span data-ttu-id="e1f3a-168">Jeśli wprowadzisz właściciela, który nie ma żadnych certyfikatów zarejestrowanych pakietów niepodpisane będą dozwolone.</span><span class="sxs-lookup"><span data-stu-id="e1f3a-168">If you make an owner  who does not have any certificate registered, then unsigned packages will be allowed.</span></span> 

<span data-ttu-id="e1f3a-169">Podobnie, jeśli wartość domyślna "Wszystkie" zaznaczono opcję pakiet gdzie jednego właściciela ma certyfikat, który został zarejestrowany i innemu właścicielowi nie ma żadnych certyfikatów zarejestrowanych, następnie nuget.org akceptuje podpisanego pakietu za pomocą podpisu w zarejestrowany za pomocą jednej z jego właścicieli lub Niepodpisany pakiet (ponieważ jeden właścicieli nie ma żadnych certyfikatów zarejestrowanych).</span><span class="sxs-lookup"><span data-stu-id="e1f3a-169">Similarly, if the default "Any" option is selected for a package where one owner has a certificate registered and another owner does not have any certificate registered, then nuget.org accepts either a signed package with a signature registered by one of its owners or an unsigned package (because one of the owners does not have any certificate registered).</span></span>

![Skonfiguruj pakietów osoby podpisujące](media/configure-package-signers.png)
