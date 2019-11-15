---
title: Przestarzałe pakiety w nuget.org
description: Szczegółowy opis procesu wycofywania pakietów i sposobu wyświetlania tych informacji przez klientów
author: anangaur
ms.author: anangaur
ms.date: 09/23/2019
ms.topic: conceptual
ms.reviewer: karann-msft
ms.openlocfilehash: 70666ddf9cd7bdc448d29d4235e57bc91e2c003e
ms.sourcegitcommit: 60414a17af65237652c1de9926475a74856b91cc
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/14/2019
ms.locfileid: "74096884"
---
# <a name="deprecating-packages"></a>Przestarzałe pakiety

Możesz zastąpić pakiet, jeśli już nie przechowujesz pakietu lub chcesz zachęcić odbiorców pakietu do przejścia do innego pakietu. 

Wycofanie pakietu jest inne niż Wycofaj **listę** pakietów, jak wyjaśniono poniżej:
* **Nielistowanie** pakietu uniemożliwia jego odnajdywanie, ponieważ jest on ukryty w wynikach wyszukiwania. 
* **Wycofanie** pakietu pozwala istniejącym konsumentom pakietu sprawdzić, czy są one zainstalowane lub używane w projektach. Pozwala również znać przyczynę wycofania i inny zalecany pakiet określony przez użytkownika (Wydawca pakietu). Wycofanie pakietu nie powoduje odlistowania pakietu. 

Jako wydawca możesz wybrać zarówno opcję unlist, jak i przestarzałe pakiety.

## <a name="deprecation-workflow"></a>Przepływ pracy wycofania
1. Aby zastąpić pakiet, przejdź do obszaru **Zarządzanie pakietami** i wybierz pozycję **przestarzałe**:

    ![Przejdź do opcji przestarzały pakiet](media/deprecation-select-option.png)

2. Wybierz wersję, którą chcesz wycofać. Jeśli chcesz zrezygnować z całej wersji, wybierz opcję **Wybierz wszystkie wersje** .

    ![Wybierz wersje pakietu do wycofania](media/deprecation-select-version.png)

3. Wybierz przyczynę wycofania. Jeśli pakiet nie jest już obsługiwany, wybierz opcję **Starsza wersja** . Jeśli określona wersja ma krytyczny błąd, wybierz opcję **ma błędy krytyczne** . Z dowolnego powodu wybierz pozycję **inne**. Zawsze możesz określić alternatywny, zalecany pakiet (i wersja) oraz niestandardowy komunikat do właścicieli. 

    ![Wybieranie z przyczyn alternatywnego zalecenia pakietu i komunikatu niestandardowego](media/deprecation-save.png)

> [!Note]
> Komunikat niestandardowy jest wyświetlany tylko w witrynie nuget.org, ale nie z poziomu klientów. Obecnie klienci tacy jak `dotnet.exe` i Menedżer pakietów NuGet nie wyświetlają komunikatu niestandardowego.

## <a name="client-experience-for-deprecated-packages"></a>Środowisko klienta dla przestarzałych pakietów
Gdy pakiet jest przestarzały, jego konsumenci są powiadamiani o nich w następujący sposób (w zależności od używanego klienta).

### <a name="visual-studio"></a>Visual Studio 
*Dostępne począwszy od programu Visual Studio 2019 w wersji 16,3*

Program Visual Studio ostrzega o użyciu przestarzałego pakietu na karcie `Installed`. Spowoduje to wyświetlenie ostrzeżenia dotyczącego pakietu i jego informacji o zaniechaniu (w tym przyczyny jego wycofania oraz alternatywnego pakietu do użycia zamiast tego, jeśli istnieje).

   ![Przestarzałe pakiety na karcie zainstalowanej w programie Visual Studio Menedżer pakietów](media/deprecation-vs.png)

### <a name="dotnetexe"></a>dotnet. exe
*Dostępne począwszy od zestawu .NET SDK 3,0*

Jeśli używasz programu dotnet. exe, możesz uruchomić polecenie `dotnet list package --deprecated` w folderze rozwiązania lub projektu, aby uzyskać listę przestarzałych pakietów wraz z informacjami o zaniechaniu:

```
> dotnet list package --deprecated

The following sources were used:
   https://api.nuget.org/v3/index.json

Project `My.Test.Project` has the following deprecated packages
   [netcoreapp3.0]:
   Top-level Package      Resolved   Reason(s)   Alternative
   > My.Sample.Lib        6.0.0      Legacy      My.Awesome.Package

```
