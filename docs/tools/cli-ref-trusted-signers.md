---
title: Polecenie zaufane osoby podpisujące interfejs wiersza polecenia NuGet
description: Dokumentacja dotycząca poleceń zaufane osoby podpisujące nuget.exe
author: patbel
ms.author: patbel
ms.date: 11/12/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: c22c7f0a6b6878bec4f8396e02e2d97998170455
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/28/2019
ms.locfileid: "67425981"
---
# <a name="trusted-signers-command-nuget-cli"></a>polecenie zaufane osoby podpisujące (interfejs wiersza polecenia NuGet)

**Dotyczy:** pakietu zużycie &bullet; **obsługiwane wersje:** 4.9.1+

Pobiera lub ustawia zaufane osoby podpisujące konfiguracji NuGet. Aby uzyskać dodatkowe użycie, zobacz [NuGet typowe konfiguracje](../consume-packages/configuring-nuget-behavior.md). Aby uzyskać szczegółowe informacje na temat sposobu schematu pliku nuget.config wygląda na to, zapoznaj się [odwołanie do pliku config NuGet](../reference/nuget-config-file.md).

## <a name="usage"></a>Użycie

```cli
nuget trusted-signers <list|add|remove|sync> [options]
```

Jeśli żadna z `list|add|remove|sync` jest określony, domyślnie zostanie polecenie `list`.

## <a name="nuget-trusted-signers-list"></a>Lista zaufanych które podpisały nuget

Wyświetla listę wszystkich zaufanych które podpisały w konfiguracji. Ta opcja będzie obejmować wszystkie certyfikaty (przy użyciu linii papilarnych i Algorytm odcisku palca) została każda osoby podpisującej. Jeśli certyfikat ma poprzedzających `[U]`, oznacza to, że wpis certyfikat ma `allowUntrustedRoot` ustawiony jako `true`.

Poniżej przedstawiono przykładowe dane wyjściowe tego polecenia:

```cli
$ nuget trusted-signers
Registered trusted signers:


 1.   nuget.org [repository]
      Service Index: https://api.nuget.org/v3/index.json
      Certificate fingerprint(s):
        SHA256 - 0E5F38F57DC1BCC806D8494F4F90FBCEDD988B46760709CBEEC6F4219AA6157D

 2.   microsoft [author]
      Certificate fingerprint(s):
        SHA256 - 3F9001EA83C560D712C24CF213C3D312CB3BFF51EE89435D3430BD06B5D0EECE

 3.   myUntrustedAuthorSignature [author]
      Certificate fingerprint(s):
        [U] SHA256 - 518F9CF082C0872025EFB2587B6A6AB198208F63EA58DD54D2B9FF6735CA4434
        
```

## <a name="nuget-trusted-signers-add-options"></a>nuget zaufanych — które podpisały Dodaj [opcje]

Dodaje zaufane osoby podpisującej o podanej nazwie do konfiguracji. Ta opcja ma różne gestów, można dodać zaufany autora lub repozytorium.

## <a name="options-for-add-based-on-a-package"></a>Opcje oparte na pakiecie Dodaj

```cli
nuget trusted-signers add <package(s)> -Name <name> [options]
```

gdzie `<package(s)>` ma jeden lub więcej `.nupkg` plików.

| Opcja | Opis |
| --- | --- |
| Autor | Określa podpis Autor pakietów należy ufać. |
| Repozytorium | Określa, że podpis repozytorium lub dokonanym pakiety mają być zaufane. |
| AllowUntrustedRoot | Określa, jeśli certyfikat dla zaufanych osoby podpisującej powinien być dozwolony do tworzenia łańcucha niezaufany certyfikat główny. |
| Właściciele | Rozdzielana średnikami lista zaufanych właścicieli, aby bardziej ograniczyć zaufanie do repozytorium. Prawidłowa tylko w przypadku korzystania z `-Repository` opcji. |

Podanie zarówno `-Author` i `-Repository` nie jest obsługiwany w tym samym czasie.

## <a name="options-for-add-based-on-a-service-index"></a>Opcje przeznaczony do dodania, w oparciu o indeks usług

```cli
nuget trusted-signers add -Name <name> [options]
```

_Uwaga_: Ta opcja doda tylko zaufane repozytoriów. 

| Opcja | Opis |
| --- | --- |
| ServiceIndex | Określa indeks usługi V3 repozytorium jako zaufane. To repozytorium musi obsługiwać zasób podpisów repozytorium. Jeśli nie zostanie podana, polecenie będzie szukać źródło pakietu z takimi samymi `-Name` i uzyskać indeks usług, w tym miejscu. |
| AllowUntrustedRoot | Określa, jeśli certyfikat dla zaufanych osoby podpisującej powinien być dozwolony do tworzenia łańcucha niezaufany certyfikat główny. |
| Właściciele | Rozdzielana średnikami lista zaufanych właścicieli, aby bardziej ograniczyć zaufanie do repozytorium. |

## <a name="options-for-add-based-on-the-certificate-information"></a>Opcje przeznaczony do dodania, w oparciu o informacje o certyfikacie

```cli
nuget trusted-signers add -Name <name> [options]
```

_Uwaga_: Jeśli zaufane osoby podpisującej o podanej nazwie już istnieje, elementu certyfikatu zostanie dodany do tej osoby podpisującej. W przeciwnym razie zostanie utworzony zaufanych autor elementu certyfikatu z podanych informacji o certyfikacie.

| Opcja | Opis |
| --- | --- |
| CertificateFingerprint | Określa certyfikat, który musi być podpisany odciski palców certyfikatu, który podpisał pakietów. Odcisk palca certyfikatu jest skrót certyfikatu. Określa algorytm wyznaczania wartości skrótu służące do obliczania, ten skrót powinien być `FingerprintAlgorithm` opcji. |
| FingerprintAlgorithm | Określa algorytm wyznaczania wartości skrótu, używane do obliczania odcisk palca certyfikatu. Wartość domyślna to `SHA256`. Obsługiwane wartości `SHA256`, `SHA384` i `SHA512` |
| AllowUntrustedRoot | Określa, jeśli certyfikat dla zaufanych osoby podpisującej powinien być dozwolony do tworzenia łańcucha niezaufany certyfikat główny. |

## <a name="nuget-trusted-signers-remove--name-name"></a>Usuń nuget zaufanych — które podpisały — nazwa <name>

Usuwa zaufane osoby podpisujące, zgodnych z podaną nazwą.

## <a name="nuget-trusted-signers-sync--name-name"></a>Synchronizowanie nuget zaufanych — które podpisały — nazwa <name>

Żąda najnowszą listę certyfikatów używanych w zaufana repozytorium, aby zaktualizować istniejące listy certyfikatów w zaufane osoby podpisującej.

_Uwaga_: Ten gest będzie usunąć bieżącą listę certyfikatów i zastąp je aktualną listę z repozytorium.

## <a name="options"></a>Opcje

| Opcja | Opis |
| --- | --- |
| ConfigFile | Plik konfiguracyjny NuGet do zastosowania. Jeśli nie zostanie określony, `%AppData%\NuGet\NuGet.Config` (Windows) lub `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) jest używany.|
| ForceEnglishOutput | Wymusza nuget.exe do uruchamiania przy użyciu kultury niezmiennej, oparte na język angielski. |
| Help | Wyświetla Pomoc dla polecenia. |
| Verbosity | Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *cichy*, *szczegółowe*. |

## <a name="examples"></a>Przykłady

```cli
nuget trusted-signers list

nuget trusted-signers Add -Name existingSource

nuget trusted-signers Add -Name trustedRepo -ServiceIndex https://trustedRepo.test/v3ServiceIndex

nuget trusted-signers Add -Name author1 -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039 -FingerprintAlgorithm SHA256

nuget trusted-signers Add -Repository .\..\MyRepositorySignedPackage.nupkg -Name TrustedRepo

nuget-trusted-signers Remove -Name TrustedRepo

nuget-trusted-signers Sync -Name TrustedRepo
```
