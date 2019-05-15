---
title: Interfejs wiersza polecenia NuGet źródeł, polecenie
description: Dokumentacja dotycząca nuget.exe źródeł, polecenie
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 94134b87f83e057d5d11a2722d9067fb76cc8e21
ms.sourcegitcommit: 4ea46498aee386b4f592b5ebba4af7f9092ac607
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/14/2019
ms.locfileid: "65610625"
---
# <a name="sources-command-nuget-cli"></a><span data-ttu-id="b51f6-103">sources command, polecenie (interfejs wiersza polecenia NuGet)</span><span class="sxs-lookup"><span data-stu-id="b51f6-103">sources command (NuGet CLI)</span></span>

<span data-ttu-id="b51f6-104">**Dotyczy:** zużycie pakietów, publikowania &bullet; **obsługiwane wersje:** wszystkie</span><span class="sxs-lookup"><span data-stu-id="b51f6-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="b51f6-105">Zarządza listę identyfikatorów źródeł znajduje się w pliku konfiguracji zakresu użytkownika lub określonego pliku konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="b51f6-105">Manages the list of sources located in the user scope configuration file or a specified configuration file.</span></span> <span data-ttu-id="b51f6-106">Plik konfiguracji zakresu użytkownika znajduje się w `%appdata%\NuGet\NuGet.Config` (Windows) i `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="b51f6-106">The user scope configuration file is located at `%appdata%\NuGet\NuGet.Config` (Windows) and `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).</span></span>

<span data-ttu-id="b51f6-107">Należy zauważyć, że adres URL źródła nuget.org `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="b51f6-107">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

## <a name="usage"></a><span data-ttu-id="b51f6-108">Użycie</span><span class="sxs-lookup"><span data-stu-id="b51f6-108">Usage</span></span>

```cli
nuget sources <operation> -Name <name> -Source <source>
```

<span data-ttu-id="b51f6-109">gdzie `<operation>` jest jednym z *listy, dodawanie, usuwanie, włączanie, wyłączanie,* lub *aktualizacji*, `<name>` jest nazwą źródła, a `<source>` jest adres URL źródła.</span><span class="sxs-lookup"><span data-stu-id="b51f6-109">where `<operation>` is one of *List, Add, Remove, Enable, Disable,* or *Update*, `<name>` is the name of the source, and `<source>` is the source's URL.</span></span> <span data-ttu-id="b51f6-110">Jednocześnie może działać na tylko jedno źródło.</span><span class="sxs-lookup"><span data-stu-id="b51f6-110">You can operate on only one source at a time.</span></span>

## <a name="options"></a><span data-ttu-id="b51f6-111">Opcje</span><span class="sxs-lookup"><span data-stu-id="b51f6-111">Options</span></span>

| <span data-ttu-id="b51f6-112">Opcja</span><span class="sxs-lookup"><span data-stu-id="b51f6-112">Option</span></span> | <span data-ttu-id="b51f6-113">Opis</span><span class="sxs-lookup"><span data-stu-id="b51f6-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b51f6-114">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="b51f6-114">ConfigFile</span></span> | <span data-ttu-id="b51f6-115">Plik konfiguracyjny NuGet do zastosowania.</span><span class="sxs-lookup"><span data-stu-id="b51f6-115">The NuGet configuration file to apply.</span></span> <span data-ttu-id="b51f6-116">Jeśli nie zostanie określony, `%AppData%\NuGet\NuGet.Config` (Windows) lub `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) jest używany.</span><span class="sxs-lookup"><span data-stu-id="b51f6-116">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="b51f6-117">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="b51f6-117">ForceEnglishOutput</span></span> | <span data-ttu-id="b51f6-118">*(3.5 +)* Wymusza nuget.exe przy użyciu opartego na język angielski, niezmienna kultura.</span><span class="sxs-lookup"><span data-stu-id="b51f6-118">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="b51f6-119">Format</span><span class="sxs-lookup"><span data-stu-id="b51f6-119">Format</span></span> | <span data-ttu-id="b51f6-120">Dotyczy `list` akcji i może być `Detailed` (ustawienie domyślne) lub `Short`.</span><span class="sxs-lookup"><span data-stu-id="b51f6-120">Applies to the `list` action and can be `Detailed` (the default) or `Short`.</span></span> |
| <span data-ttu-id="b51f6-121">Help</span><span class="sxs-lookup"><span data-stu-id="b51f6-121">Help</span></span> | <span data-ttu-id="b51f6-122">Wyświetla Pomoc dla polecenia.</span><span class="sxs-lookup"><span data-stu-id="b51f6-122">Displays help information for the command.</span></span> |
| <span data-ttu-id="b51f6-123">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="b51f6-123">NonInteractive</span></span> | <span data-ttu-id="b51f6-124">Wyłącza monity dotyczące danych wejściowych użytkownika lub potwierdzenia.</span><span class="sxs-lookup"><span data-stu-id="b51f6-124">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="b51f6-125">Hasło</span><span class="sxs-lookup"><span data-stu-id="b51f6-125">Password</span></span> | <span data-ttu-id="b51f6-126">Określa hasło do uwierzytelniania za pomocą źródła.</span><span class="sxs-lookup"><span data-stu-id="b51f6-126">Specifies the password for authenticating with the source.</span></span> |
| <span data-ttu-id="b51f6-127">StorePasswordInClearText</span><span class="sxs-lookup"><span data-stu-id="b51f6-127">StorePasswordInClearText</span></span> | <span data-ttu-id="b51f6-128">Wskazuje, aby zapisać hasło nieszyfrowane tekstu zamiast domyślnego zachowania przechowywania w postaci zaszyfrowanej.</span><span class="sxs-lookup"><span data-stu-id="b51f6-128">Indicates to store the password in unencrypted text instead of the default behavior of storing an encrypted form.</span></span> |
| <span data-ttu-id="b51f6-129">UserName</span><span class="sxs-lookup"><span data-stu-id="b51f6-129">UserName</span></span> | <span data-ttu-id="b51f6-130">Określa nazwę użytkownika do uwierzytelniania za pomocą źródła.</span><span class="sxs-lookup"><span data-stu-id="b51f6-130">Specifies the user name for authenticating with the source.</span></span> |
| <span data-ttu-id="b51f6-131">Verbosity</span><span class="sxs-lookup"><span data-stu-id="b51f6-131">Verbosity</span></span> | <span data-ttu-id="b51f6-132">Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *cichy*, *szczegółowe*.</span><span class="sxs-lookup"><span data-stu-id="b51f6-132">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

> [!Note]
> <span data-ttu-id="b51f6-133">Upewnij się, że dodanie hasła źródeł, w tym samym kontekście użytkownika, ponieważ nuget.exe jest później używany do uzyskiwania dostępu do źródła pakietu.</span><span class="sxs-lookup"><span data-stu-id="b51f6-133">Make sure to add the sources' password under the same user context as the nuget.exe is later used to access the package source.</span></span> <span data-ttu-id="b51f6-134">Hasło będzie przechowywany zaszyfrowany w pliku konfiguracji, a odszyfrować je mogą tylko w tym samym kontekście użytkownika, ponieważ został on zaszyfrowany.</span><span class="sxs-lookup"><span data-stu-id="b51f6-134">The password will be stored encrypted in the config file and can only be decrypted in the same user context as it was encrypted.</span></span> <span data-ttu-id="b51f6-135">Dlatego na przykład używając serwera kompilacji do przywracania pakietów NuGet, które hasło musi być szyfrowana przy użyciu tego samego użytkownika Windows, na którym będzie uruchamiana zadanie serwera kompilacji.</span><span class="sxs-lookup"><span data-stu-id="b51f6-135">So for example when you use a build server to restore NuGet packages the password must be encrypted with the same Windows user under which  the build server task will run.</span></span>

<span data-ttu-id="b51f6-136">Zobacz też [zmiennych środowiskowych](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="b51f6-136">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="b51f6-137">Przykłady</span><span class="sxs-lookup"><span data-stu-id="b51f6-137">Examples</span></span>

```cli
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget sources Enable -Name "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
