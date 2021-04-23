---
title: Podpisywanie pakietów NuGet
description: Wyjaśnia, w jaki sposób podpisane pakiety mogą być używane do włączania weryfikacji integralności zawartości.
author: rido-min
ms.author: rmpablos
ms.date: 03/06/2018
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: c0622520a325000d5fcb8fb884cb509ee4b641f4
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901905"
---
# <a name="signing-nuget-packages"></a><span data-ttu-id="ddc9a-103">Podpisywanie pakietów NuGet</span><span class="sxs-lookup"><span data-stu-id="ddc9a-103">Signing NuGet Packages</span></span>

<span data-ttu-id="ddc9a-104">Podpisane pakiety umożliwiają sprawdzanie integralności zawartości, co zapewnia ochronę przed naruszeniem zawartości.</span><span class="sxs-lookup"><span data-stu-id="ddc9a-104">Signed packages allows for content integrity verification checks which provides protection against content tampering.</span></span> <span data-ttu-id="ddc9a-105">Podpis pakietu służy również jako pojedyncze źródło prawdziwych informacji o rzeczywistym pochodzeniu pakietu i wzmacnia autentyczność pakietu dla konsumenta.</span><span class="sxs-lookup"><span data-stu-id="ddc9a-105">The package signature also serves as the single source of truth about the actual origin of the package and bolsters package authenticity for the consumer.</span></span> <span data-ttu-id="ddc9a-106">W tym przewodniku przyjęto założenie, [że utworzono już pakiet](creating-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="ddc9a-106">This guide assumes you have already [created a package](creating-a-package.md).</span></span>

## <a name="get-a-code-signing-certificate"></a><span data-ttu-id="ddc9a-107">Uzyskiwanie certyfikatu podpisywania kodu</span><span class="sxs-lookup"><span data-stu-id="ddc9a-107">Get a code signing certificate</span></span>

<span data-ttu-id="ddc9a-108">Prawidłowe certyfikaty można uzyskać z publicznego urzędu certyfikacji, takiego jak [DigiCert,](https://www.digicert.com/code-signing/) [Global Sign,](https://www.globalsign.com/en/code-signing-certificate/) [Comodo,](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php) [Certum](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml)itp. Pełną listę urzędów certyfikacji zaufanych przez system Windows można uzyskać na stronie [http://aka.ms/trustcertpartners](/security/trusted-root/participants-list) .</span><span class="sxs-lookup"><span data-stu-id="ddc9a-108">Valid certificates may be obtained from a public certificate authority such as [DigiCert](https://www.digicert.com/code-signing/), [Global Sign](https://www.globalsign.com/en/code-signing-certificate/), [Comodo](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php), [Certum](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml), etc. The complete list of certification authorities trusted by Windows can be obtained from [http://aka.ms/trustcertpartners](/security/trusted-root/participants-list).</span></span>

<span data-ttu-id="ddc9a-109">Certyfikatów wystawionych samodzielnie można używać do celów testowych.</span><span class="sxs-lookup"><span data-stu-id="ddc9a-109">You can use self-issued certificates for testing purposes.</span></span> <span data-ttu-id="ddc9a-110">Jednak pakiety podpisane przy użyciu certyfikatów wystawionych samodzielnie nie są akceptowane przez NuGet.org. Dowiedz się więcej o [tworzeniu certyfikatu testowego](#create-a-test-certificate)</span><span class="sxs-lookup"><span data-stu-id="ddc9a-110">However, packages signed using self-issued certificates are not accepted by NuGet.org. Learn more about [creating a test certificate](#create-a-test-certificate)</span></span>

## <a name="export-the-certificate-file"></a><span data-ttu-id="ddc9a-111">Eksportowanie pliku certyfikatu</span><span class="sxs-lookup"><span data-stu-id="ddc9a-111">Export the certificate file</span></span>

* <span data-ttu-id="ddc9a-112">Istniejący certyfikat można wyeksportować do binarnego formatu DER przy użyciu Kreatora eksportu certyfikatów.</span><span class="sxs-lookup"><span data-stu-id="ddc9a-112">You can export an existing certificate to a binary DER format by using the Certificate Export Wizard.</span></span>

  ![Kreator eksportu certyfikatów](../reference/media/CertificateExportWizard.png)

* <span data-ttu-id="ddc9a-114">Certyfikat można również wyeksportować przy użyciu [polecenia programu PowerShell Export-Certificate](/powershell/module/pkiclient/export-certificate).</span><span class="sxs-lookup"><span data-stu-id="ddc9a-114">You can also export the certificate using the [Export-Certificate PowerShell command](/powershell/module/pkiclient/export-certificate).</span></span>

## <a name="sign-the-package"></a><span data-ttu-id="ddc9a-115">Podpisywanie pakietu</span><span class="sxs-lookup"><span data-stu-id="ddc9a-115">Sign the package</span></span>

> [!note]
> <span data-ttu-id="ddc9a-116">Wymaga nuget.exe 4.6.0 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="ddc9a-116">Requires nuget.exe 4.6.0 or later.</span></span> <span data-ttu-id="ddc9a-117">dotnet.exe wkrótce — #7939 [](https://github.com/NuGet/Home/issues/7939)</span><span class="sxs-lookup"><span data-stu-id="ddc9a-117">dotnet.exe support is coming soon - [#7939](https://github.com/NuGet/Home/issues/7939)</span></span>

<span data-ttu-id="ddc9a-118">Podpisz pakiet przy użyciu [znaku nuget:](../reference/cli-reference/cli-ref-sign.md)</span><span class="sxs-lookup"><span data-stu-id="ddc9a-118">Sign the package using [nuget sign](../reference/cli-reference/cli-ref-sign.md):</span></span>

```cli
nuget sign MyPackage.nupkg -CertificatePath <PathToTheCertificate> -Timestamper <TimestampServiceURL>
```

> [!Tip]
> <span data-ttu-id="ddc9a-119">Dostawca certyfikatów często udostępnia również adres URL serwera ze znacznikiem czasu, którego można użyć dla `Timestamper` opcjonalnego argumentu wyświetlanego powyżej.</span><span class="sxs-lookup"><span data-stu-id="ddc9a-119">The certificate provider often also provides a timestamping server URL which you can use for the `Timestamper` optional argument show above.</span></span> <span data-ttu-id="ddc9a-120">Zapoznaj się z dokumentacją dostawcy i/lub pomocą techniczną dotyczącą tego adresu URL usługi.</span><span class="sxs-lookup"><span data-stu-id="ddc9a-120">Consult with your provider's documentation and/or support for that service URL.</span></span>

* <span data-ttu-id="ddc9a-121">Możesz użyć certyfikatu dostępnego w magazynie certyfikatów lub certyfikatu z pliku.</span><span class="sxs-lookup"><span data-stu-id="ddc9a-121">You can use a certificate available in the certificate store or use a certificate from a file.</span></span> <span data-ttu-id="ddc9a-122">Zobacz cli reference for nuget sign (Informacje dotyczące [interfejsu wiersza polecenia dla znaku nuget).](../reference/cli-reference/cli-ref-sign.md)</span><span class="sxs-lookup"><span data-stu-id="ddc9a-122">See CLI reference for [nuget sign](../reference/cli-reference/cli-ref-sign.md).</span></span>
* <span data-ttu-id="ddc9a-123">Podpisane pakiety powinny zawierać znacznik czasu, aby upewnić się, że podpis pozostaje ważny po wygaśnięciu certyfikatu podpisywania.</span><span class="sxs-lookup"><span data-stu-id="ddc9a-123">Signed packages should include a timestamp to make sure the signature remains valid when the signing certificate has expired.</span></span> <span data-ttu-id="ddc9a-124">W innym przypadku operacja podpisywania [spowoduje](../reference/errors-and-warnings/NU3002.md)ostrzeżenie .</span><span class="sxs-lookup"><span data-stu-id="ddc9a-124">Else the sign operation will produce a [warning](../reference/errors-and-warnings/NU3002.md).</span></span>
* <span data-ttu-id="ddc9a-125">Szczegóły sygnatury danego pakietu można wyświetlić przy użyciu narzędzia [nuget verify](../reference/cli-reference/cli-ref-verify.md).</span><span class="sxs-lookup"><span data-stu-id="ddc9a-125">You can see the signature details of a given package using [nuget verify](../reference/cli-reference/cli-ref-verify.md).</span></span>

## <a name="register-the-certificate-on-nugetorg"></a><span data-ttu-id="ddc9a-126">Zarejestruj certyfikat w NuGet.org</span><span class="sxs-lookup"><span data-stu-id="ddc9a-126">Register the certificate on NuGet.org</span></span>

<span data-ttu-id="ddc9a-127">Aby opublikować podpisany pakiet, należy najpierw zarejestrować certyfikat w NuGet.org. Certyfikat jest potrzebny jako plik `.cer` w binarnym formacie DER.</span><span class="sxs-lookup"><span data-stu-id="ddc9a-127">To publish a signed package, you must first register the certificate with NuGet.org. You need the certificate as a `.cer` file in a binary DER format.</span></span>

1. <span data-ttu-id="ddc9a-128">[Zaloguj się](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) do NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="ddc9a-128">[Sign in](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) to NuGet.org.</span></span>
1. <span data-ttu-id="ddc9a-129">Przejdź do (lub jeśli chcesz zarejestrować certyfikat `Account settings` `Manage Organization` **>** `Edit Organization` przy użyciu konta organizacji).</span><span class="sxs-lookup"><span data-stu-id="ddc9a-129">Go to `Account settings` (or `Manage Organization` **>** `Edit Organization` if you would like to register the certificate with an Organization account).</span></span>
1. <span data-ttu-id="ddc9a-130">Rozwiń `Certificates` sekcję i wybierz pozycję `Register new` .</span><span class="sxs-lookup"><span data-stu-id="ddc9a-130">Expand the `Certificates` section and select `Register new`.</span></span>
1. <span data-ttu-id="ddc9a-131">Przeglądaj i wybierz wyeksportowany wcześniej plik certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="ddc9a-131">Browse and select the certficate file that was exported earlier.</span></span>
  <span data-ttu-id="ddc9a-132">![Zarejestrowane certyfikaty](../reference/media/registered-certs.png)</span><span class="sxs-lookup"><span data-stu-id="ddc9a-132">![Registered Certificates](../reference/media/registered-certs.png)</span></span>

<span data-ttu-id="ddc9a-133">**Uwaga**</span><span class="sxs-lookup"><span data-stu-id="ddc9a-133">**Note**</span></span>
* <span data-ttu-id="ddc9a-134">Jeden użytkownik może przesłać wiele certyfikatów, a ten sam certyfikat może zostać zarejestrowany przez wielu użytkowników.</span><span class="sxs-lookup"><span data-stu-id="ddc9a-134">One user can submit multiple certificates and the same certificate can be registered by multiple users.</span></span>
* <span data-ttu-id="ddc9a-135">Po zarejestrowaniu certyfikatu przez użytkownika wszystkie przyszłe  przesłania pakietów muszą być podpisane przy użyciu jednego z certyfikatów.</span><span class="sxs-lookup"><span data-stu-id="ddc9a-135">Once a user has a certificate registered, all future package submissions **must** be signed with one of the certificates.</span></span> <span data-ttu-id="ddc9a-136">Zobacz Manage signing requirements for your package on NuGet.org (Zarządzanie wymaganiami [podpisywania dla pakietu na NuGet.org](#manage-signing-requirements-for-your-package-on-nugetorg)</span><span class="sxs-lookup"><span data-stu-id="ddc9a-136">See [Manage signing requirements for your package on NuGet.org](#manage-signing-requirements-for-your-package-on-nugetorg)</span></span>
* <span data-ttu-id="ddc9a-137">Użytkownicy mogą również usunąć zarejestrowany certyfikat z konta.</span><span class="sxs-lookup"><span data-stu-id="ddc9a-137">Users can also remove a registered certificate from the account.</span></span> <span data-ttu-id="ddc9a-138">Po usunięciu certyfikatu nowe pakiety podpisane tym certyfikatem nie powiodą się podczas przesyłania.</span><span class="sxs-lookup"><span data-stu-id="ddc9a-138">Once a certificate is removed, new packages signed with that certificate will fail at submission.</span></span> <span data-ttu-id="ddc9a-139">Nie ma to wpływu na istniejące pakiety.</span><span class="sxs-lookup"><span data-stu-id="ddc9a-139">Existing packages aren't affected.</span></span>

## <a name="publish-the-package"></a><span data-ttu-id="ddc9a-140">Publikowanie pakietu</span><span class="sxs-lookup"><span data-stu-id="ddc9a-140">Publish the package</span></span>

<span data-ttu-id="ddc9a-141">Teraz możesz opublikować pakiet w NuGet.org. Zobacz [Publikowanie pakietów](../nuget-org/Publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="ddc9a-141">You are now ready to publish the package to NuGet.org. See [Publishing packages](../nuget-org/Publish-a-package.md).</span></span>

## <a name="create-a-test-certificate"></a><span data-ttu-id="ddc9a-142">Tworzenie certyfikatu testowego</span><span class="sxs-lookup"><span data-stu-id="ddc9a-142">Create a test certificate</span></span>

<span data-ttu-id="ddc9a-143">Certyfikatów wystawionych samodzielnie można używać do celów testowych.</span><span class="sxs-lookup"><span data-stu-id="ddc9a-143">You can use self-issued certificates for testing purposes.</span></span> <span data-ttu-id="ddc9a-144">Aby utworzyć certyfikat wystawiony samodzielnie, użyj polecenia [New-SelfSignedCertificate programu PowerShell.](/powershell/module/pkiclient/new-selfsignedcertificate)</span><span class="sxs-lookup"><span data-stu-id="ddc9a-144">To create a self-issued certificate, use the [New-SelfSignedCertificate PowerShell command](/powershell/module/pkiclient/new-selfsignedcertificate).</span></span>

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

<span data-ttu-id="ddc9a-145">To polecenie tworzy certyfikat testowania dostępny w osobistym magazynie certyfikatów bieżącego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="ddc9a-145">This command creates a testing certificate available in the current user's personal certificate store.</span></span> <span data-ttu-id="ddc9a-146">Możesz otworzyć magazyn certyfikatów, uruchamiając program `certmgr.msc` , aby wyświetlić nowo utworzony certyfikat.</span><span class="sxs-lookup"><span data-stu-id="ddc9a-146">You can open the certificate store by running `certmgr.msc` to see the newly created certificate.</span></span>

> [!Warning]
> <span data-ttu-id="ddc9a-147">NuGet.org nie akceptuje pakietów podpisanych za pomocą samodzielnie wystawionych certyfikatów.</span><span class="sxs-lookup"><span data-stu-id="ddc9a-147">NuGet.org does not accept packages signed with self-issued certificates.</span></span>

## <a name="manage-signing-requirements-for-your-package-on-nugetorg"></a><span data-ttu-id="ddc9a-148">Zarządzanie wymaganiami podpisywania dla pakietu na NuGet.org</span><span class="sxs-lookup"><span data-stu-id="ddc9a-148">Manage signing requirements for your package on NuGet.org</span></span>
1. <span data-ttu-id="ddc9a-149">[Zaloguj się](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) do NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="ddc9a-149">[Sign in](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) to NuGet.org.</span></span>

1. <span data-ttu-id="ddc9a-150">Przejdź do `Manage Packages`  
    ![ konfigurowania osób podpisujących pakiety](../reference/media/configure-package-signers.png)</span><span class="sxs-lookup"><span data-stu-id="ddc9a-150">Go to `Manage Packages` 
![Configure package signers](../reference/media/configure-package-signers.png)</span></span>

* <span data-ttu-id="ddc9a-151">Jeśli jesteś jedynym właścicielem pakietu, jesteś wymaganym podpisicielem, czyli możesz użyć dowolnego zarejestrowanego certyfikatu do podpisania i opublikowania pakietów w NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="ddc9a-151">If you are the sole owner of a package, you are the required signer i.e. you can use any of the registered certificates to sign and publish your packages to NuGet.org.</span></span>

* <span data-ttu-id="ddc9a-152">Jeśli pakiet ma wielu właścicieli, do podpisania pakietu można domyślnie użyć certyfikatów właściciela "Dowolny".</span><span class="sxs-lookup"><span data-stu-id="ddc9a-152">If a package has multiple owners, by default, "Any" owner's certificates can be used to sign the package.</span></span> <span data-ttu-id="ddc9a-153">Jako współwłaściciel pakietu możesz zastąpić "Dowolne" swoim lub innym współwłaścicielem, aby był wymaganym podpisem.</span><span class="sxs-lookup"><span data-stu-id="ddc9a-153">As a co-owner of the package, you can override "Any" with yourself or any other co-owner to be the required signer.</span></span> <span data-ttu-id="ddc9a-154">W przypadku przypisania właściciela, który nie ma zarejestrowanego certyfikatu, pakiety niepodpisane będą dozwolone.</span><span class="sxs-lookup"><span data-stu-id="ddc9a-154">If you make an owner  who does not have any certificate registered, then unsigned packages will be allowed.</span></span> 

* <span data-ttu-id="ddc9a-155">Podobnie, jeśli dla pakietu, w którym jeden właściciel ma zarejestrowany certyfikat, a inny właściciel nie ma zarejestrowanego certyfikatu, wybrana jest domyślna opcja "Dowolne", program NuGet.org akceptuje podpisany pakiet z podpisem zarejestrowanym przez jednego z właścicieli lub pakiet niepodpisany (ponieważ jeden z właścicieli nie ma zarejestrowanego certyfikatu).</span><span class="sxs-lookup"><span data-stu-id="ddc9a-155">Similarly, if the default "Any" option is selected for a package where one owner has a certificate registered and another owner does not have any certificate registered, then NuGet.org accepts either a signed package with a signature registered by one of its owners or an unsigned package (because one of the owners does not have any certificate registered).</span></span>

## <a name="related-articles"></a><span data-ttu-id="ddc9a-156">Pokrewne artykuły:</span><span class="sxs-lookup"><span data-stu-id="ddc9a-156">Related articles</span></span>

- [<span data-ttu-id="ddc9a-157">Zarządzanie granicami zaufania pakietów</span><span class="sxs-lookup"><span data-stu-id="ddc9a-157">Manage package trust boundaries</span></span>](../consume-packages/installing-signed-packages.md)
- [<span data-ttu-id="ddc9a-158">Odwołanie do podpisanych pakietów</span><span class="sxs-lookup"><span data-stu-id="ddc9a-158">Signed Packages Reference</span></span>](../reference/Signed-Packages-Reference.md)
