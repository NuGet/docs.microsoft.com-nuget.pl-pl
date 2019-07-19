---
title: Polecenie źródeł interfejsu wiersza polecenia NuGet
description: Dokumentacja polecenia NuGet. exe sources
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 94134b87f83e057d5d11a2722d9067fb76cc8e21
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/18/2019
ms.locfileid: "68328283"
---
# <a name="sources-command-nuget-cli"></a><span data-ttu-id="c1024-103">sources command, polecenie (interfejs wiersza polecenia NuGet)</span><span class="sxs-lookup"><span data-stu-id="c1024-103">sources command (NuGet CLI)</span></span>

<span data-ttu-id="c1024-104">**Dotyczy:** użycie pakietu, publikowanie &bullet; **obsługiwanych wersji:** wszystkie</span><span class="sxs-lookup"><span data-stu-id="c1024-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="c1024-105">Zarządza listą źródeł znajdujących się w pliku konfiguracyjnym zakresu użytkownika lub w określonym pliku konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="c1024-105">Manages the list of sources located in the user scope configuration file or a specified configuration file.</span></span> <span data-ttu-id="c1024-106">Plik konfiguracji zakresu użytkownika znajduje się w lokalizacji `%appdata%\NuGet\NuGet.Config` (Windows) i `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="c1024-106">The user scope configuration file is located at `%appdata%\NuGet\NuGet.Config` (Windows) and `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).</span></span>

<span data-ttu-id="c1024-107">Należy pamiętać, że źródłowy adres URL dla `https://api.nuget.org/v3/index.json`NuGet.org to.</span><span class="sxs-lookup"><span data-stu-id="c1024-107">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

## <a name="usage"></a><span data-ttu-id="c1024-108">Użycie</span><span class="sxs-lookup"><span data-stu-id="c1024-108">Usage</span></span>

```cli
nuget sources <operation> -Name <name> -Source <source>
```

<span data-ttu-id="c1024-109">gdzie `<operation>` to jeden z elementów *list, Add, Remove, Enable, Disable* lub *Update*, `<name>` jest nazwą źródła i `<source>` jest adresem URL źródła.</span><span class="sxs-lookup"><span data-stu-id="c1024-109">where `<operation>` is one of *List, Add, Remove, Enable, Disable,* or *Update*, `<name>` is the name of the source, and `<source>` is the source's URL.</span></span> <span data-ttu-id="c1024-110">Jednocześnie można wykonywać tylko jedno źródło.</span><span class="sxs-lookup"><span data-stu-id="c1024-110">You can operate on only one source at a time.</span></span>

## <a name="options"></a><span data-ttu-id="c1024-111">Opcje</span><span class="sxs-lookup"><span data-stu-id="c1024-111">Options</span></span>

| <span data-ttu-id="c1024-112">Opcja</span><span class="sxs-lookup"><span data-stu-id="c1024-112">Option</span></span> | <span data-ttu-id="c1024-113">Opis</span><span class="sxs-lookup"><span data-stu-id="c1024-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c1024-114">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="c1024-114">ConfigFile</span></span> | <span data-ttu-id="c1024-115">Plik konfiguracji NuGet, który ma zostać zastosowany.</span><span class="sxs-lookup"><span data-stu-id="c1024-115">The NuGet configuration file to apply.</span></span> <span data-ttu-id="c1024-116">Jeśli nie zostanie określony `%AppData%\NuGet\NuGet.Config` , używany jest system `~/.nuget/NuGet/NuGet.Config` (Windows) lub (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="c1024-116">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="c1024-117">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="c1024-117">ForceEnglishOutput</span></span> | <span data-ttu-id="c1024-118">*(3.5 +)* Wymusza nuget.exe przy użyciu opartego na język angielski, niezmienna kultura.</span><span class="sxs-lookup"><span data-stu-id="c1024-118">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="c1024-119">Format</span><span class="sxs-lookup"><span data-stu-id="c1024-119">Format</span></span> | <span data-ttu-id="c1024-120">Dotyczy akcji i może być `Detailed` (wartość domyślna) lub `Short`. `list`</span><span class="sxs-lookup"><span data-stu-id="c1024-120">Applies to the `list` action and can be `Detailed` (the default) or `Short`.</span></span> |
| <span data-ttu-id="c1024-121">Help</span><span class="sxs-lookup"><span data-stu-id="c1024-121">Help</span></span> | <span data-ttu-id="c1024-122">Wyświetla informacje pomocy dla polecenia.</span><span class="sxs-lookup"><span data-stu-id="c1024-122">Displays help information for the command.</span></span> |
| <span data-ttu-id="c1024-123">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="c1024-123">NonInteractive</span></span> | <span data-ttu-id="c1024-124">Pomija monity o dane wejściowe lub potwierdzone przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="c1024-124">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="c1024-125">Hasło</span><span class="sxs-lookup"><span data-stu-id="c1024-125">Password</span></span> | <span data-ttu-id="c1024-126">Określa hasło do uwierzytelniania ze źródłem.</span><span class="sxs-lookup"><span data-stu-id="c1024-126">Specifies the password for authenticating with the source.</span></span> |
| <span data-ttu-id="c1024-127">StorePasswordInClearText</span><span class="sxs-lookup"><span data-stu-id="c1024-127">StorePasswordInClearText</span></span> | <span data-ttu-id="c1024-128">Wskazuje, że hasło ma być przechowywane w niezaszyfrowanym tekście zamiast w domyślnym zachowaniu zaszyfrowanego formularza.</span><span class="sxs-lookup"><span data-stu-id="c1024-128">Indicates to store the password in unencrypted text instead of the default behavior of storing an encrypted form.</span></span> |
| <span data-ttu-id="c1024-129">UserName</span><span class="sxs-lookup"><span data-stu-id="c1024-129">UserName</span></span> | <span data-ttu-id="c1024-130">Określa nazwę użytkownika do uwierzytelniania ze źródłem.</span><span class="sxs-lookup"><span data-stu-id="c1024-130">Specifies the user name for authenticating with the source.</span></span> |
| <span data-ttu-id="c1024-131">Verbosity</span><span class="sxs-lookup"><span data-stu-id="c1024-131">Verbosity</span></span> | <span data-ttu-id="c1024-132">Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *ciche*, *szczegółowe*.</span><span class="sxs-lookup"><span data-stu-id="c1024-132">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

> [!Note]
> <span data-ttu-id="c1024-133">Pamiętaj o dodaniu hasła źródeł w tym samym kontekście użytkownika, co plik NuGet. exe jest później używany do uzyskiwania dostępu do źródła pakietu.</span><span class="sxs-lookup"><span data-stu-id="c1024-133">Make sure to add the sources' password under the same user context as the nuget.exe is later used to access the package source.</span></span> <span data-ttu-id="c1024-134">Hasło będzie przechowywane w pliku konfiguracyjnym i może zostać odszyfrowane tylko w tym samym kontekście użytkownika, w którym został zaszyfrowany.</span><span class="sxs-lookup"><span data-stu-id="c1024-134">The password will be stored encrypted in the config file and can only be decrypted in the same user context as it was encrypted.</span></span> <span data-ttu-id="c1024-135">Na przykład w przypadku przywracania pakietów NuGet przy użyciu serwera kompilacji hasło musi być szyfrowane za pomocą tego samego użytkownika systemu Windows, w którym zostanie uruchomione zadanie serwera kompilacji.</span><span class="sxs-lookup"><span data-stu-id="c1024-135">So for example when you use a build server to restore NuGet packages the password must be encrypted with the same Windows user under which  the build server task will run.</span></span>

<span data-ttu-id="c1024-136">Zobacz również [zmienne środowiskowe](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="c1024-136">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="c1024-137">Przykłady</span><span class="sxs-lookup"><span data-stu-id="c1024-137">Examples</span></span>

```cli
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget sources Enable -Name "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
