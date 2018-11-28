---
title: Obsługa długich ścieżek interfejs wiersza polecenia NuGet
description: Dokumentacja dotycząca pomocy technicznej z długą ścieżką nuget.exe
author: zhili1208
ms.author: lzhi
ms.date: 07/12/2018
ms.topic: reference
ms.openlocfilehash: 42b5b7d863d22d7aad99a65700ca11bcc2861db1
ms.sourcegitcommit: 0c5a49ec6e0254a4e7a9d8bca7daeefb853c433a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/28/2018
ms.locfileid: "52453497"
---
# <a name="long-path-support-nuget-cli"></a><span data-ttu-id="ffed4-103">Obsługa długich ścieżek (interfejs wiersza polecenia NuGet)</span><span class="sxs-lookup"><span data-stu-id="ffed4-103">Long Path Support (NuGet CLI)</span></span>

<span data-ttu-id="ffed4-104">**Dotyczy:** wszystkich &bullet; **obsługiwane wersje:** 4.8 +</span><span class="sxs-lookup"><span data-stu-id="ffed4-104">**Applies to:** all &bullet; **Supported versions:** 4.8+</span></span>

<span data-ttu-id="ffed4-105">NuGet.exe pomocy technicznej lub nowszy 4,8 długich ścieżek plików i katalogów w scenariuszach, takich jak pakiet, przywracanie, instalacji i większości scenariuszy, które wymagają ścieżki do plików.</span><span class="sxs-lookup"><span data-stu-id="ffed4-105">NuGet.exe 4.8 and later support long paths for files and directories for scenarios like Pack, Restore, Install, and most other scenarios that need file paths.</span></span>

## <a name="required-operating-system"></a><span data-ttu-id="ffed4-106">Wymagany System operacyjny</span><span class="sxs-lookup"><span data-stu-id="ffed4-106">Required Operating System</span></span>

-   <span data-ttu-id="ffed4-107">Windows 10 (wersja 1607 lub nowszej)</span><span class="sxs-lookup"><span data-stu-id="ffed4-107">Windows 10 (version 1607 or later)</span></span>
-   <span data-ttu-id="ffed4-108">Windows 10 (lipiec 2015 r. lub używana wersja 1511) .NET Framework w przypadku uaktualnienia do wersji 4.6.2 lub nowszy.</span><span class="sxs-lookup"><span data-stu-id="ffed4-108">Windows 10 (July 2015 release or version 1511) if you upgrade .NET Framework to versions 4.6.2 or later.</span></span>
-   <span data-ttu-id="ffed4-109">System Windows Server 2016 (wszystkie wersje)</span><span class="sxs-lookup"><span data-stu-id="ffed4-109">Windows Server 2016 (all versions)</span></span>

## <a name="enable-win32-long-paths-group-policy"></a><span data-ttu-id="ffed4-110">Włączanie zasad grupy "Długich ścieżek systemu Win32"</span><span class="sxs-lookup"><span data-stu-id="ffed4-110">Enable "Win32 Long Paths" Group Policy</span></span>

<span data-ttu-id="ffed4-111">Należy włączyć obsługę długich ścieżek w tych systemach przez ustawienie zasad grupy.</span><span class="sxs-lookup"><span data-stu-id="ffed4-111">One needs to enable long path support on those systems by setting a group policy.</span></span>

<span data-ttu-id="ffed4-112">Kroki:</span><span class="sxs-lookup"><span data-stu-id="ffed4-112">Steps:</span></span>
1. <span data-ttu-id="ffed4-113">Uruchom **Edytor zasad grupy** — wpisz "Edytuj zasady grupy" na pasku wyszukiwania rozpoczęcia lub uruchomić "gpedit.msc" z polecenia Uruchom (Windows-R).</span><span class="sxs-lookup"><span data-stu-id="ffed4-113">Launch **Group Policy Editor** - Type "Edit group policy" in the Start search bar or Run "gpedit.msc" from the Run command (Windows-R).</span></span>
2. <span data-ttu-id="ffed4-114">W **Edytora lokalnych zasad grupy**, włącz "lokalnego komputera zasad i komputera Konfiguracja/administracyjne szablony/wszystkich długich ścieżek ustawienia/Włącz Win32".</span><span class="sxs-lookup"><span data-stu-id="ffed4-114">In the **Local Group Policy Editor**, enable "Local Computer Policy/Computer Configuration/Administrative Templates/All Settings/Enable Win32 long paths".</span></span>

![Zasady długie ścieżki](media/LongPathPolicy.png)


> [!Note]
> <span data-ttu-id="ffed4-116">Inne narzędzia NuGet, do obsługi długich ścieżek</span><span class="sxs-lookup"><span data-stu-id="ffed4-116">Enabling Other NuGet Tools to Support Long Paths</span></span>
>
> -   <span data-ttu-id="ffed4-117">Interfejsu wiersza polecenia DotNet obsługuje długich ścieżek niezależnie od systemu operacyjnego i wersji.</span><span class="sxs-lookup"><span data-stu-id="ffed4-117">Dotnet CLI supports long paths regardless of the operating system or version.</span></span>
> -   <span data-ttu-id="ffed4-118">Visual Studio lub program msbuild - t: restore nie obsługuje długich ścieżek.</span><span class="sxs-lookup"><span data-stu-id="ffed4-118">Visual Studio or msbuild -t:restore does not yet support long paths.</span></span>
> -   <span data-ttu-id="ffed4-119">Oprogramowanie, które korzysta z bibliotek usługi NuGet do wykonania przywracania i innych poleceń będzie obsługiwać długich ścieżek na tych samych systemach NuGet.exe działające w, również ustawić longPathAware w ich systemie windows manifestu i skonfigurować UseLegacyPathHandling na wartość false, za pomocą pliku App.Config [ Zobacz więcej informacji](https://blogs.msdn.microsoft.com/jeremykuhne/2016/07/30/net-4-6-2-and-long-paths-on-windows-10/)</span><span class="sxs-lookup"><span data-stu-id="ffed4-119">Software that uses NuGet Libraries to execute restore and other commands, will support long paths on the same systems that NuGet.exe works on, if they also set longPathAware in their windows manifest and configure UseLegacyPathHandling to false via App.Config [See more information](https://blogs.msdn.microsoft.com/jeremykuhne/2016/07/30/net-4-6-2-and-long-paths-on-windows-10/)</span></span>

