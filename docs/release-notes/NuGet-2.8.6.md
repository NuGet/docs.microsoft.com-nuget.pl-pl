---
title: Informacje o wersji narzędzia NuGet 2.8.6
description: Informacje o wersji programu NuGet 2.8.6, w tym znane problemy, poprawki błędów, dodane funkcje i DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: ea291bdf7a5b6cc3ac3bde526030e517db4632d7
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776697"
---
# <a name="nuget-286-release-notes"></a><span data-ttu-id="b471f-103">Informacje o wersji narzędzia NuGet 2.8.6</span><span class="sxs-lookup"><span data-stu-id="b471f-103">NuGet 2.8.6 Release Notes</span></span>

<span data-ttu-id="b471f-104">Informacje o wersji narzędzia [NuGet 2.8.5](../release-notes/nuget-2.8.5.md)  |  [Informacje o wersji narzędzia NuGet 2.8.7](../release-notes/nuget-2.8.7.md)</span><span class="sxs-lookup"><span data-stu-id="b471f-104">[NuGet 2.8.5 Release Notes](../release-notes/nuget-2.8.5.md) | [NuGet 2.8.7 Release Notes](../release-notes/nuget-2.8.7.md)</span></span>

<span data-ttu-id="b471f-105">Pakiet NuGet 2.8.6 został wydany 20 lipca 2015 jako drobna aktualizacja naszego 2.8.5 VSIX z niektórymi skierowanymi poprawkami i ulepszeniami dotyczącymi pakietów, które mogą być dostarczane z obsługą systemu Windows 10 platformy UWP Development model.</span><span class="sxs-lookup"><span data-stu-id="b471f-105">NuGet 2.8.6 was released July 20, 2015 as a minor update to our 2.8.5 VSIX with some targeted fixes and improvements to support packages that may be delivered with support for the Windows 10 UWP development model.</span></span>

<span data-ttu-id="b471f-106">Ta wersja rozszerzenia Menedżera pakietów NuGet zapewnia obsługę tylko Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="b471f-106">This version of the NuGet package manager extension provides support for Visual Studio 2013 only.</span></span>

<span data-ttu-id="b471f-107">W tej wersji okno dialogowe Menedżera pakietów NuGet obsługiwało Dodawanie do:</span><span class="sxs-lookup"><span data-stu-id="b471f-107">In this release, the NuGet Package Manager dialog had support added for:</span></span>

* <span data-ttu-id="b471f-108">Wprowadzono moniker platformy docelowej UAP do obsługi programowania aplikacji systemu Windows 10.</span><span class="sxs-lookup"><span data-stu-id="b471f-108">Introduced the UAP Target Framework Moniker to support Windows 10 Application Development.</span></span>
* <span data-ttu-id="b471f-109">Punkty końcowe protokołu NuGet w wersji 3</span><span class="sxs-lookup"><span data-stu-id="b471f-109">NuGet protocol version 3 endpoints</span></span>
* <span data-ttu-id="b471f-110">Obsługa [Nuget.Config](../consume-packages/configuring-nuget-behavior.md) atrybutu protocolVersion w źródłach repozytorium.</span><span class="sxs-lookup"><span data-stu-id="b471f-110">Support for [Nuget.Config](../consume-packages/configuring-nuget-behavior.md) protocolVersion attribute on repository sources.</span></span> <span data-ttu-id="b471f-111">Wartość domyślna to "2"</span><span class="sxs-lookup"><span data-stu-id="b471f-111">Default value is "2"</span></span>
* <span data-ttu-id="b471f-112">Powracanie do zdalnego repozytorium, jeśli wymagana wersja pakietu nie jest dostępna w lokalnej pamięci podręcznej</span><span class="sxs-lookup"><span data-stu-id="b471f-112">Falling back to remote repository if a required package version is not available in the local cache</span></span>