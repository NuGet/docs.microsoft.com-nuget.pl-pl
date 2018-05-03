---
title: Informacje o wersji 1.6 NuGet
description: Informacje o wersji dla tym znanych problemów, poprawki, dodatkowe funkcje i dcr NuGet w wersji 1.6.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 0345e180893a56302385d27792c4e15ba5d96989
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/26/2018
---
 # <a name="nuget-16-release-notes"></a>Informacje o wersji 1.6 NuGet

[Informacje o wersji NuGet w wersji 1.5](../release-notes/nuget-1.5.md) | [NuGet 1.7 informacje o wersji](../release-notes/nuget-1.7.md)

NuGet w wersji 1.6 został wydany 13 grudnia 2011.

## <a name="known-installation-issue"></a>Znane problem
Jeśli korzystasz z VS 2010 z dodatkiem SP1, możesz napotkać błąd instalacji podczas próby uaktualnienia NuGet, jeśli masz starszą wersję zainstalowane.

Obejście jest po prostu odinstalować NuGet, a następnie zainstaluj go z galerii rozszerzeń programu VS.  Zobacz [ http://support.microsoft.com/kb/2581019 ](http://support.microsoft.com/kb/2581019) Aby uzyskać więcej informacji.

Uwaga: Jeśli program Visual Studio nie pozwalają na odinstalować rozszerzenia (przycisk Odinstaluj jest wyłączony), następnie prawdopodobnie konieczne ponowne uruchomienie programu Visual Studio za pomocą polecenia "Uruchom jako Administrator".

## <a name="features"></a>Funkcje

### <a name="support-for-semantic-versioning-and-prerelease-packages"></a>Obsługa Wersjonowania semantycznego i pakiety wersji wstępnej
NuGet 1.6 wprowadzono obsługę Wersjonowania semantycznego (programu SemVer). Aby uzyskać więcej informacji o używaniu go programu SemVer, przeczytaj [dokumentacji Versioning](../create-packages/prerelease-packages.md).

### <a name="using-nuget-without-checking-in-packages-package-restore"></a>Bez sprawdzania w pakietach (Przywracanie pakietu) przy użyciu narzędzia NuGet
NuGet w wersji 1.6 ma teraz obsługę aparatów przepływu pracy, w których NuGet nie zostaną dodane do kontroli źródła pakietów, ale zamiast tego są przywracane podczas kompilacji Brak. Aby uzyskać więcej informacji, przeczytaj [za pomocą NuGet bez zatwierdzania pakietów do kontroli źródła](../consume-packages/packages-and-source-control.md) tematu.

### <a name="item-templates-that-install-nuget-packages"></a>Szablony elementów, które zainstalować pakietów NuGet
Korzystając z pracy do obsługi wstępnie zainstalowane pakiet NuGet do szablony projektu Visual Studio, NuGet w wersji 1.6 również dodaje obsługę szablony elementów Visual Studio. Szablony elementów może mieć skojarzone pakiety NuGet, które są instalowane przy szablonu w wywołaniu.

Aby uzyskać więcej informacji na temat zmiany szablonu projektu/elementu można zainstalować pakietów NuGet, przeczytaj [pakietów w szablony Visual Studio](../visual-studio-extensibility/visual-studio-templates.md) tematu.

### <a name="support-for-disabling-package-sources"></a>Obsługa wyłączenie źródła pakietów
Jeśli skonfigurowano wiele źródeł pakietów, NuGet będzie wyglądać w każdej z nich pakietów podczas instalowania pakietu i jego zależności. Źródło pakietu, który nie działa dla jakiegoś powodu może poważnie wolno dół NuGet.

Przed NuGet w wersji 1.6 można usunąć źródła pakietów, ale następnie należy pamiętać, że szczegółowe informacje, gdy chcesz dodać ją ponownie.

NuGet w wersji 1.6 umożliwia zaznaczenie pola wyboru źródła pakietów, aby ją wyłączyć, ale zachować ją wokół.

![Wyłączanie pakietu](./media/package-source-with-disabled-source.png)

## <a name="bug-fixes"></a>Poprawki błędów
NuGet w wersji 1.6 było łącznie 106 stałej elementów roboczych. 95 tych zostały sklasyfikowane jako usterki i 10 tych były funkcji.

Pełną listę prac elementów usunięto w wersji NuGet w wersji 1.6, sprawdź widok [NuGet Tracker problem w tej wersji](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.6&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).
