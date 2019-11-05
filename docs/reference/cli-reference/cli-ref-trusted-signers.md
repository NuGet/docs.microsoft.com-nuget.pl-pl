---
title: Polecenie zaufanych-podpisywania interfejsu wiersza polecenia NuGet
description: Odwołanie do polecenia Trusted-signers programu NuGet. exe
author: patbel
ms.author: patbel
ms.date: 11/12/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 94c4c6524c1870898893b80be914477af5a14e8b
ms.sourcegitcommit: 39f2ae79fbbc308e06acf67ee8e24cfcdb2c831b
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/05/2019
ms.locfileid: "73610334"
---
# <a name="trusted-signers-command-nuget-cli"></a>Zaufane-podpisujące — polecenie (interfejs wiersza polecenia NuGet)

**Dotyczy:** użycie pakietu &bullet; **obsługiwane wersje:** 4.9.1 +

Pobiera lub ustawia zaufane osoby podpisujące do konfiguracji programu NuGet. Aby uzyskać dodatkowe użycie, zobacz [typowe konfiguracje NuGet](../../consume-packages/configuring-nuget-behavior.md). Aby uzyskać szczegółowe informacje o tym, jak wygląda schemat NuGet. config, zapoznaj się z tematem [Dokumentacja pliku konfiguracji programu NuGet](../nuget-config-file.md).

## <a name="usage"></a>Użycie

```cli
nuget trusted-signers <list|add|remove|sync> [options]
```

Jeśli żadna z `list|add|remove|sync` nie zostanie określona, polecenie będzie domyślnie `list`.

## <a name="nuget-trusted-signers-list"></a>Lista zaufanych nadawców NuGet

Wyświetla listę wszystkich zaufanych podpisów w konfiguracji. Ta opcja spowoduje uwzględnienie wszystkich certyfikatów (z użyciem algorytmu odcisku palca i odcisku palca) każdego osoby podpisującej. Jeśli certyfikat ma wcześniejszą `[U]`, oznacza to, że wpis certyfikatu ma `allowUntrustedRoot` ustawiony jako `true`.

Poniżej znajduje się przykładowe dane wyjściowe z tego polecenia:

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

## <a name="nuget-trusted-signers-add-options"></a>zaufane osoby podpisujące NuGet — Dodawanie [opcje]

Dodaje do konfiguracji nazwę zaufanego podpisującego o danej nazwie. Ta opcja ma inne gesty umożliwiające dodanie zaufanego autora lub repozytorium.

## <a name="options-for-add-based-on-a-package"></a>Opcje dodawania w oparciu o pakiet

```cli
nuget trusted-signers add <package(s)> -Name <name> [options]
```

gdzie `<package(s)>` to co najmniej jeden plik `.nupkg`.

| Opcja | Opis |
| --- | --- |
| Tworzone | Określa, że podpis autora pakietów powinien być zaufany. |
| Kopie | Określa, że podpis repozytorium lub kontrpodpis pakietów powinien być zaufany. |
| AllowUntrustedRoot | Określa, czy certyfikat zaufanego podpisującego ma być dozwolony w łańcuchu do niezaufanego certyfikatu głównego. |
| rzecz | Rozdzielana średnikami lista zaufanych właścicieli, aby bardziej ograniczyć zaufanie do repozytorium. Prawidłowy tylko przy użyciu opcji `-Repository`. |

Udostępnianie jednocześnie `-Author` i `-Repository` nie jest obsługiwane.

## <a name="options-for-add-based-on-a-service-index"></a>Opcje dodawania oparte na indeksie usługi

```cli
nuget trusted-signers add -Name <name> [options]
```

_Uwaga_: Ta opcja spowoduje dodanie tylko zaufanych repozytoriów. 

| Opcja | Opis |
| --- | --- |
| Serviceindex | Określa indeks usługi v3 repozytorium, który ma być zaufany. To repozytorium ma obsługiwać zasób sygnatur repozytorium. Jeśli nie zostanie podany, polecenie będzie szukać źródła pakietu o tej samej `-Name` i pobrać z niego indeks usługi. |
| AllowUntrustedRoot | Określa, czy certyfikat zaufanego podpisującego ma być dozwolony w łańcuchu do niezaufanego certyfikatu głównego. |
| rzecz | Rozdzielana średnikami lista zaufanych właścicieli, aby bardziej ograniczyć zaufanie do repozytorium. |

## <a name="options-for-add-based-on-the-certificate-information"></a>Opcje dodawania na podstawie informacji o certyfikacie

```cli
nuget trusted-signers add -Name <name> [options]
```

_Uwaga_: Jeśli zaufany podpis o podanej nazwie już istnieje, element certyfikatu zostanie dodany do osoby podpisującej. W przeciwnym razie zaufany autor zostanie utworzony za pomocą elementu certyfikatu z informacji podanych w certyfikacie.

| Opcja | Opis |
| --- | --- |
| CertificateFingerprint | Określa odciski palca certyfikatu, z którym podpisane pakiety muszą być podpisane. Odcisk palca certyfikatu jest skrótem certyfikatu. Algorytm wyznaczania wartości skrótu używany do obliczania tego skrótu powinien być określany w opcji `FingerprintAlgorithm`. |
| FingerprintAlgorithm | Określa algorytm wyznaczania wartości skrótu używany do obliczania odcisku palca certyfikatu. Wartość domyślna to `SHA256`. Obsługiwane wartości to `SHA256`, `SHA384` i `SHA512` |
| AllowUntrustedRoot | Określa, czy certyfikat zaufanego podpisującego ma być dozwolony w łańcuchu do niezaufanego certyfikatu głównego. |

## <a name="nuget-trusted-signers-remove--name-name"></a>zaufane osoby podpisujące NuGet usuwają nazwę \<nazwy\>

Usuwa wszystkie zaufane osoby podpisujące zgodne z podaną nazwą.

## <a name="nuget-trusted-signers-sync--name-name"></a>Synchronizacja zaufanych nadawców NuGet — nazwa \<nazwa\>

Żąda najnowszej listy certyfikatów używanych w bieżącym repozytorium, aby zaktualizować listę istniejących certyfikatów w zaufanej rejestracji.

_Uwaga_: ten gest spowoduje usunięcie bieżącej listy certyfikatów i zamienienie ich na aktualną listę z repozytorium.

## <a name="options"></a>Opcje

| Opcja | Opis |
| --- | --- |
| ConfigFile | Plik konfiguracji NuGet, który ma zostać zastosowany. Jeśli nie zostanie określony, używany jest `%AppData%\NuGet\NuGet.Config` (Windows) lub `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).|
| ForceEnglishOutput | Wymusza uruchomienie NuGet. exe przy użyciu niezmiennej, opartej na języku angielskim kultury. |
| Pomoc | Wyświetla informacje pomocy dla polecenia. |
| Szczegółowość | Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *ciche*, *szczegółowe*. |

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
