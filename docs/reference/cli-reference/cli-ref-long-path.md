---
title: Obsługa długiej ścieżki interfejsu wiersza polecenia NuGet
description: Dokumentacja obsługi długich ścieżek NuGet. exe
author: zhili1208
ms.author: lzhi
ms.date: 07/12/2018
ms.topic: reference
ms.openlocfilehash: 9b5a97d963eab7fbbde4aefae1c9b1a8bfcdeb11
ms.sourcegitcommit: 415c70d7014545c1f65271a2debf8c3c1c5eb688
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/06/2020
ms.locfileid: "77036958"
---
# <a name="long-path-support-nuget-cli"></a><span data-ttu-id="6a2f0-103">Obsługa długich ścieżek (interfejs wiersza polecenia NuGet)</span><span class="sxs-lookup"><span data-stu-id="6a2f0-103">Long Path Support (NuGet CLI)</span></span>

<span data-ttu-id="6a2f0-104">**Dotyczy:** wszystkie &bullet; **obsługiwane wersje:** 4.8 +</span><span class="sxs-lookup"><span data-stu-id="6a2f0-104">**Applies to:** all &bullet; **Supported versions:** 4.8+</span></span>

<span data-ttu-id="6a2f0-105">NuGet. exe 4,8 i nowsze obsługują długie ścieżki dla plików i katalogów dla scenariuszy, takich jak pakowanie, przywracanie, Instalowanie i większość innych scenariuszy, które wymagają ścieżek plików.</span><span class="sxs-lookup"><span data-stu-id="6a2f0-105">NuGet.exe 4.8 and later support long paths for files and directories for scenarios like Pack, Restore, Install, and most other scenarios that need file paths.</span></span>

## <a name="required-operating-system"></a><span data-ttu-id="6a2f0-106">Wymagany system operacyjny</span><span class="sxs-lookup"><span data-stu-id="6a2f0-106">Required Operating System</span></span>

-   <span data-ttu-id="6a2f0-107">Windows 10 (wersja 1607 lub nowsza)</span><span class="sxs-lookup"><span data-stu-id="6a2f0-107">Windows 10 (version 1607 or later)</span></span>
-   <span data-ttu-id="6a2f0-108">Windows 10 (wydanie z lipca 2015 lub wersja 1511) w przypadku uaktualnienia .NET Framework do wersji 4.6.2 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="6a2f0-108">Windows 10 (July 2015 release or version 1511) if you upgrade .NET Framework to versions 4.6.2 or later.</span></span>
-   <span data-ttu-id="6a2f0-109">Windows Server 2016 (wszystkie wersje)</span><span class="sxs-lookup"><span data-stu-id="6a2f0-109">Windows Server 2016 (all versions)</span></span>

## <a name="enable-win32-long-paths-group-policy"></a><span data-ttu-id="6a2f0-110">Włącz "długie ścieżki Win32" zasady grupy</span><span class="sxs-lookup"><span data-stu-id="6a2f0-110">Enable "Win32 Long Paths" Group Policy</span></span>

<span data-ttu-id="6a2f0-111">Należy włączyć obsługę długich ścieżek w tych systemach przez ustawienie zasad grupy.</span><span class="sxs-lookup"><span data-stu-id="6a2f0-111">One needs to enable long path support on those systems by setting a group policy.</span></span>

<span data-ttu-id="6a2f0-112">Kroki:</span><span class="sxs-lookup"><span data-stu-id="6a2f0-112">Steps:</span></span>
1. <span data-ttu-id="6a2f0-113">Uruchom **zasady grupy Edytor** -wpisz "Edytuj zasady grupy" na Start paska wyszukiwania lub uruchom polecenie "gpedit. msc" z polecenia Run (Windows-R).</span><span class="sxs-lookup"><span data-stu-id="6a2f0-113">Launch **Group Policy Editor** - Type "Edit group policy" in the Start search bar or Run "gpedit.msc" from the Run command (Windows-R).</span></span>
2. <span data-ttu-id="6a2f0-114">W **Edytor lokalnych zasad grupy**Włącz ustawienie "zasady komputera lokalnego/Konfiguracja komputera/Szablony administracyjne/wszystkie ustawienia/Włącz długie ścieżki Win32".</span><span class="sxs-lookup"><span data-stu-id="6a2f0-114">In the **Local Group Policy Editor**, enable "Local Computer Policy/Computer Configuration/Administrative Templates/All Settings/Enable Win32 long paths".</span></span>

![Zasady dotyczące długiej ścieżki](media/LongPathPolicy.png)


> [!Note]
> <span data-ttu-id="6a2f0-116">Włączanie obsługi długich ścieżek przez inne narzędzia NuGet</span><span class="sxs-lookup"><span data-stu-id="6a2f0-116">Enabling Other NuGet Tools to Support Long Paths</span></span>
>
> -   <span data-ttu-id="6a2f0-117">Interfejs wiersza polecenia dotnet obsługuje długie ścieżki niezależnie od systemu operacyjnego lub wersji.</span><span class="sxs-lookup"><span data-stu-id="6a2f0-117">Dotnet CLI supports long paths regardless of the operating system or version.</span></span>
> -   <span data-ttu-id="6a2f0-118">Program Visual Studio lub `msbuild -t:restore` nie obsługuje jeszcze długich ścieżek.</span><span class="sxs-lookup"><span data-stu-id="6a2f0-118">Visual Studio or `msbuild -t:restore` does not yet support long paths.</span></span>
> -   <span data-ttu-id="6a2f0-119">Oprogramowanie, które korzysta z bibliotek NuGet do wykonywania przywracania i innych poleceń, będzie obsługiwało długie ścieżki w tych samych systemach, w których działa program NuGet. exe, jeśli również ustawili `longPathAware` w ich manifeście systemu Windows i skonfiguruj `UseLegacyPathHandling` do `false` za pomocą pliku App. config [Zobacz więcej informacji](https://blogs.msdn.microsoft.com/jeremykuhne/2016/07/30/net-4-6-2-and-long-paths-on-windows-10/)</span><span class="sxs-lookup"><span data-stu-id="6a2f0-119">Software that uses NuGet Libraries to execute restore and other commands, will support long paths on the same systems that NuGet.exe works on, if they also set `longPathAware` in their windows manifest and configure `UseLegacyPathHandling` to `false` via App.Config [See more information](https://blogs.msdn.microsoft.com/jeremykuhne/2016/07/30/net-4-6-2-and-long-paths-on-windows-10/)</span></span>

