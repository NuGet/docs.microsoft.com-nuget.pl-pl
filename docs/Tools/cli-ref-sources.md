---
title: Polecenie źródła interfejsu wiersza polecenia NuGet | Dokumentacja firmy Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Dokumentacja dotycząca nuget.exe źródeł polecenia
keywords: nuget źródeł odwołania, źródłem polecenia
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 5fb34654dc294de34cf0e15f784240884dc1e3d1
ms.sourcegitcommit: ecb598c790d4154366bc92757ec7db1a51c34faf
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/03/2018
---
# <a name="sources-command-nuget-cli"></a><span data-ttu-id="64453-104">polecenie źródeł (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="64453-104">sources command (NuGet CLI)</span></span>

<span data-ttu-id="64453-105">**Dotyczy:** zużycie pakietu, publikowanie &bullet; **obsługiwane wersje:** wszystkie</span><span class="sxs-lookup"><span data-stu-id="64453-105">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="64453-106">Zarządza listy źródeł znajduje się w pliku konfiguracji zakresu użytkownika lub pliku konfiguracyjnym.</span><span class="sxs-lookup"><span data-stu-id="64453-106">Manages the list of sources located in the user scope configuration file or a specified configuration file.</span></span> <span data-ttu-id="64453-107">Plik konfiguracji zakresu użytkownika znajduje się w `%appdata%\NuGet\NuGet.Config` (system Windows) i `~/.nuget/NuGet/NuGet.Config` (system Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="64453-107">The user scope configuration file is located at `%appdata%\NuGet\NuGet.Config` (Windows) and `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).</span></span>

<span data-ttu-id="64453-108">Należy zauważyć, że adres URL źródła dla nuget.org `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="64453-108">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

## <a name="usage"></a><span data-ttu-id="64453-109">Użycie</span><span class="sxs-lookup"><span data-stu-id="64453-109">Usage</span></span>

```cli
nuget sources <operation> -Name <name> -Source <source>
```

<span data-ttu-id="64453-110">gdzie `<operation>` jest jednym z *listy, dodawanie, usuwanie, włączanie i wyłączanie,* lub *aktualizacji*, `<name>` to nazwa źródła i `<source>` jest adres URL źródła.</span><span class="sxs-lookup"><span data-stu-id="64453-110">where `<operation>` is one of *List, Add, Remove, Enable, Disable,* or *Update*, `<name>` is the name of the source, and `<source>` is the source's URL.</span></span>

## <a name="options"></a><span data-ttu-id="64453-111">Opcje</span><span class="sxs-lookup"><span data-stu-id="64453-111">Options</span></span>

| <span data-ttu-id="64453-112">Opcja</span><span class="sxs-lookup"><span data-stu-id="64453-112">Option</span></span> | <span data-ttu-id="64453-113">Opis</span><span class="sxs-lookup"><span data-stu-id="64453-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="64453-114">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="64453-114">ConfigFile</span></span> | <span data-ttu-id="64453-115">Plik konfiguracyjny NuGet do zastosowania.</span><span class="sxs-lookup"><span data-stu-id="64453-115">The NuGet configuration file to apply.</span></span> <span data-ttu-id="64453-116">Jeśli nie zostanie określony, `%AppData%\NuGet\NuGet.Config` (system Windows) lub `~/.nuget/NuGet/NuGet.Config` (system Mac/Linux) jest używany.</span><span class="sxs-lookup"><span data-stu-id="64453-116">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="64453-117">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="64453-117">ForceEnglishOutput</span></span> | <span data-ttu-id="64453-118">*(3.5 +)* Wymusza nuget.exe przy użyciu opartego na język angielski, niezmienna kultura.</span><span class="sxs-lookup"><span data-stu-id="64453-118">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="64453-119">Format</span><span class="sxs-lookup"><span data-stu-id="64453-119">Format</span></span> | <span data-ttu-id="64453-120">Dotyczy `list` akcji i może być `Detailed` (ustawienie domyślne) lub `Short`.</span><span class="sxs-lookup"><span data-stu-id="64453-120">Applies to the `list` action and can be `Detailed` (the default) or `Short`.</span></span> |
| <span data-ttu-id="64453-121">Pomoc</span><span class="sxs-lookup"><span data-stu-id="64453-121">Help</span></span> | <span data-ttu-id="64453-122">Wyświetla Pomoc dla polecenia.</span><span class="sxs-lookup"><span data-stu-id="64453-122">Displays help information for the command.</span></span> |
| <span data-ttu-id="64453-123">Nieinterakcyjne</span><span class="sxs-lookup"><span data-stu-id="64453-123">NonInteractive</span></span> | <span data-ttu-id="64453-124">Pomija wyświetla monit o dane wejściowe użytkownika lub potwierdzeń.</span><span class="sxs-lookup"><span data-stu-id="64453-124">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="64453-125">Hasło</span><span class="sxs-lookup"><span data-stu-id="64453-125">Password</span></span> | <span data-ttu-id="64453-126">Określa hasło do uwierzytelniania w źródle.</span><span class="sxs-lookup"><span data-stu-id="64453-126">Specifies the password for authenticating with the source.</span></span> |
| <span data-ttu-id="64453-127">StorePasswordInClearText</span><span class="sxs-lookup"><span data-stu-id="64453-127">StorePasswordInClearText</span></span> | <span data-ttu-id="64453-128">Wskazuje, aby zapisać hasło w tekście niezaszyfrowane zamiast domyślnego zachowania przechowywania zaszyfrowane.</span><span class="sxs-lookup"><span data-stu-id="64453-128">Indicates to store the password in unencrypted text instead of the default behavior of storing an encrypted form.</span></span> |
| <span data-ttu-id="64453-129">UserName</span><span class="sxs-lookup"><span data-stu-id="64453-129">UserName</span></span> | <span data-ttu-id="64453-130">Określa nazwę użytkownika do uwierzytelniania w źródle.</span><span class="sxs-lookup"><span data-stu-id="64453-130">Specifies the user name for authenticating with the source.</span></span> |
| <span data-ttu-id="64453-131">Szczegółowość</span><span class="sxs-lookup"><span data-stu-id="64453-131">Verbosity</span></span> | <span data-ttu-id="64453-132">Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *quiet*, *szczegółowe*.</span><span class="sxs-lookup"><span data-stu-id="64453-132">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

> [!Note]
> <span data-ttu-id="64453-133">Upewnij się, że dodanie hasła źródeł w tym samym kontekście użytkownika, ponieważ nuget.exe jest później używany do uzyskiwania dostępu do źródła pakietu.</span><span class="sxs-lookup"><span data-stu-id="64453-133">Make sure to add the sources' password under the same user context as the nuget.exe is later used to access the package source.</span></span> <span data-ttu-id="64453-134">Hasło będzie przechowywany zaszyfrowany w pliku konfiguracji i mogły być odszyfrowane tylko w kontekście tego samego użytkownika, ponieważ został on zaszyfrowany.</span><span class="sxs-lookup"><span data-stu-id="64453-134">The password will be stored encrypted in the config file and can only be decrypted in the same user context as it was encrypted.</span></span> <span data-ttu-id="64453-135">Tak na przykład jeśli używasz serwera kompilacji do przywracania pakietów NuGet, które muszą być szyfrowane hasło z tego samego użytkownika systemu Windows, uruchamiania zadań serwera kompilacji.</span><span class="sxs-lookup"><span data-stu-id="64453-135">So for example when you use a build server to restore NuGet packages the password must be encrypted with the same Windows user under which  the build server task will run.</span></span>

<span data-ttu-id="64453-136">Zobacz też [zmienne środowiskowe](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="64453-136">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="64453-137">Przykłady</span><span class="sxs-lookup"><span data-stu-id="64453-137">Examples</span></span>

```cli
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget source Enable -Name "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
