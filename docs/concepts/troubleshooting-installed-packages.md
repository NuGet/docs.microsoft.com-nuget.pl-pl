---
title: Rozwiązywanie problemów z zainstalowanymi pakietami
description: Jak znaleźć źródło pakietu, które zostało użyte dla poszczególnych pakietów
author: JonDouglas
ms.author: jodou
ms.date: 03/26/2021
ms.topic: conceptual
ms.openlocfilehash: 22fb51ebb996c66e10b860f0158676fd2d9da295
ms.sourcegitcommit: c8bf16420f235fc3e42c08cd0d56359e91d490e5
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/14/2021
ms.locfileid: "107387572"
---
# <a name="troubleshooting-installed-packages"></a>Rozwiązywanie problemów z zainstalowanymi pakietami

Czasami może być konieczne zweryfikowanie źródła, z którego został zainstalowany określony pakiet. Oto kilka sposobów, które można sprawdzić.

> [!Note]
> Niektóre źródła pakietów obsługują koncepcję znaną jako źródła nadrzędne. Na przykład [Azure Artifacts nadrzędne źródła](/azure/devops/artifacts/concepts/upstream-sources). Klienci NuGet nie wiedzą, czy pakiet pochodzi ze źródła nadrzędnego. W związku z tym każde rejestrowanie źródła pakietu spowoduje, że zostanie wyświetlona lista skonfigurowanego źródła, a nie nadrzędnego źródła.

## <a name="nupkgmetadata-file-in-global-packages-folder"></a>`.nupkg.metadata` plik w folderze pakietów globalnych

Gdy pakiet jest wyodrębniony do *folderu global-packages,* jest `.nupkg.metadata` zapisywany plik. Począwszy od pakietu NuGet 5.9.0, pakiet NuGet doda źródło pakietu. Zobacz poniżej, aby zamapować wersje nuGet na Visual Studio zestawu SDK platformy .NET. Na przykład:

```json
{
  "version": 2,
  "contentHash": "bw3R9q8cVNhWXNpnvWb0OGP4HadS4zvClq+T1zf7AF+tLY1haZ2AvbHidQekf4PDv1T40c6brZeT/V0IBq7cEQ==",
  "source": "https://api.nuget.org/v3/index.json"
}
```

> [!Note]
> Jeśli folder *global-packages* zawiera pakiety wyodrębnione przed uaktualnieniem do nowszej wersji narzędzi z pakietem NuGet 5.9.0, plik będzie w wersji 1 i nie będzie zawierać źródła `.nupkg.metadata` pakietu. Możesz [wyczyścić folder *global-packages,*](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders) aby upewnić się, że wszystkie pakiety będą zawierać źródło pakietu.

> [!Tip]
> Program NuGet zapisuje `.nupkg.metadata` plik tylko w *folderze global-packages.* Projekty `packages.config` używające programu używają folderu pakietów rozwiązań, który nie tworzy `.nupkg.metadata` pliku.

## <a name="installed-package-log-message"></a>Komunikat dziennika zainstalowanego pakietu

Począwszy od pakietu NuGet 5.9.0, pakiet NuGet wyprowadza źródło pakietu w komunikacie przywracania informujący o zainstalowaniu pakietu. Na przykład:

```text
Installed Moq 4.16.1 from https://api.nuget.org/v3/index.json with content hash bw3R9q8cVNhWXNpnvWb0OGP4HadS4zvClq+T1zf7AF+tLY1haZ2AvbHidQekf4PDv1T40c6brZeT/V0IBq7cEQ==.
```

> [!Tip]
> Ten komunikat jest wyjściowy z normalnym/informacyjnym poziomem szczegółowości. Visual Studio i interfejsie wiersza polecenia mają domyślnie minimalną szczegółowość, więc ten `dotnet` komunikat nie będzie widoczny domyślnie. Narzędzia interfejsu wiersza polecenia i `msbuild` domyślnie mają normalną szczegółowość, więc ten `nuget` komunikat będzie domyślnie widoczny.

## <a name="http-log-message"></a>Komunikat dziennika HTTP

Jeśli pakiet nie jest dostępny lokalnie, w folderze *pakietów* globalnych, folderze rezerwowym lub lokalnym źródle plików nuGet pobierze go z dowolnego skonfigurowanego źródła pakietu za pośrednictwem protokołu HTTP. Żądania HTTP i odpowiedzi są rejestrowane na normalnym poziomie szczegółowości i powinno być widać tylko jedno żądanie i odpowiedź na wersję pakietu. Na przykład:

```text
info :   GET https://api.nuget.org/v3-flatcontainer/moq/index.json
info :   OK https://api.nuget.org/v3-flatcontainer/moq/index.json 56ms
info :   GET https://api.nuget.org/v3-flatcontainer/moq/4.16.1/moq.4.16.1.nupkg
info :   OK https://api.nuget.org/v3-flatcontainer/moq/4.16.1/moq.4.16.1.nupkg 3ms
```

Jeśli pliki zostały ostatnio pobrane, mogą zostać pobrane z pamięci podręcznej *http-cache programu* NuGet

```text
CACHE https://api.nuget.org/v3-flatcontainer/moq/index.json
CACHE https://api.nuget.org/v3-flatcontainer/moq/4.16.1/moq.4.16.1.nupkg
```

Format adresu URL może się różnić w przypadku różnych implementacji serwera HTTP NuGet oraz tego, czy implementuje on protokół HTTP NuGet v2, czy V3.

Jeśli masz zdefiniowanych wiele źródeł HTTP, zobaczysz wiele żądań do pliku każdego `nuget.config` `index.json` pakietu, po jednym dla każdego źródła. Jednak dla każdej wersji pakietu będzie dostępne tylko jedno `nupkg` pobranie.

## <a name="package-signature-log-message"></a>Komunikat dziennika sygnatury pakietu

Jeśli pobierany pakiet jest podpisany, pakiet NuGet zweryfikuje podpis i zweryfikuje następujący komunikat ze szczegółowymi informacjami:

```text
PackageSignatureVerificationLog: PackageIdentity: Moq.4.16.1 Source: https://api.nuget.org/v3/index.json PackageSignatureValidity: True
```

Ten komunikat będzie zgłaszany, czy pakiet został pobrany ze źródła pakietu HTTP, czy skopiowany ze źródła pakietu lokalnego. Nie będzie to dane wyjściowe, jeśli pakiet jest już dostępny w folderze *global-packages* lub folderze rezerwowym.

> [!Important]
> Ze względu na usunięcie zaufania narzędzia NuGet urzędu certyfikacji [VeriSign](https://github.com/dotnet/announcements/issues/180) wyłączono weryfikację podpisanych pakietów na niektórych platformach, w niektórych wersjach pakietu NuGet i zestawu .NET SDK. W związku z tym te same pakiety mogą zawierać dzienniki lub mogą brakować tych dzienników w zależności od platformy, na której jest uruchomione przywracanie, oraz wersji platformy .NET lub `PackageSignatureVerificationLog` nuGet, której używasz.

## <a name="nuget-version-map"></a>Mapa wersji programu NuGet

Następujące wersje pakietu NuGet mają istotne zmiany dotyczące rejestrowania źródła pakietu:

|Wersja nuGet|Visual Studio wersji|Wersja zestawu .NET SDK|
|---|---|---|
|NuGet 5.9.0|Visual Studio 2019 r. 16.9.0|.NET 5 SDK 5.0.200|
