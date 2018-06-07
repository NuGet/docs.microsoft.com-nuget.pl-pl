---
title: Polecenie źródeł NuGet interfejsu wiersza polecenia
description: Dokumentacja dotycząca nuget.exe źródeł polecenia
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 7c416d92c11328ecb020154981b0ddcc5ba9c5e8
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818350"
---
# <a name="sources-command-nuget-cli"></a><span data-ttu-id="ec2bf-103">sources command, polecenie (interfejs wiersza polecenia NuGet)</span><span class="sxs-lookup"><span data-stu-id="ec2bf-103">sources command (NuGet CLI)</span></span>

<span data-ttu-id="ec2bf-104">**Dotyczy:** zużycie pakietu, publikowanie &bullet; **obsługiwane wersje:** wszystkie</span><span class="sxs-lookup"><span data-stu-id="ec2bf-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="ec2bf-105">Zarządza listy źródeł znajduje się w pliku konfiguracji zakresu użytkownika lub pliku konfiguracyjnym.</span><span class="sxs-lookup"><span data-stu-id="ec2bf-105">Manages the list of sources located in the user scope configuration file or a specified configuration file.</span></span> <span data-ttu-id="ec2bf-106">Plik konfiguracji zakresu użytkownika znajduje się w `%appdata%\NuGet\NuGet.Config` (system Windows) i `~/.nuget/NuGet/NuGet.Config` (system Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="ec2bf-106">The user scope configuration file is located at `%appdata%\NuGet\NuGet.Config` (Windows) and `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).</span></span>

<span data-ttu-id="ec2bf-107">Należy zauważyć, że adres URL źródła dla nuget.org `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="ec2bf-107">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

## <a name="usage"></a><span data-ttu-id="ec2bf-108">Użycie</span><span class="sxs-lookup"><span data-stu-id="ec2bf-108">Usage</span></span>

```cli
nuget sources <operation> -Name <name> -Source <source>
```

<span data-ttu-id="ec2bf-109">gdzie `<operation>` jest jednym z *listy, dodawanie, usuwanie, włączanie i wyłączanie,* lub *aktualizacji*, `<name>` to nazwa źródła i `<source>` jest adres URL źródła.</span><span class="sxs-lookup"><span data-stu-id="ec2bf-109">where `<operation>` is one of *List, Add, Remove, Enable, Disable,* or *Update*, `<name>` is the name of the source, and `<source>` is the source's URL.</span></span>

## <a name="options"></a><span data-ttu-id="ec2bf-110">Opcje</span><span class="sxs-lookup"><span data-stu-id="ec2bf-110">Options</span></span>

| <span data-ttu-id="ec2bf-111">Opcja</span><span class="sxs-lookup"><span data-stu-id="ec2bf-111">Option</span></span> | <span data-ttu-id="ec2bf-112">Opis</span><span class="sxs-lookup"><span data-stu-id="ec2bf-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ec2bf-113">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="ec2bf-113">ConfigFile</span></span> | <span data-ttu-id="ec2bf-114">Plik konfiguracyjny NuGet do zastosowania.</span><span class="sxs-lookup"><span data-stu-id="ec2bf-114">The NuGet configuration file to apply.</span></span> <span data-ttu-id="ec2bf-115">Jeśli nie zostanie określony, `%AppData%\NuGet\NuGet.Config` (system Windows) lub `~/.nuget/NuGet/NuGet.Config` (system Mac/Linux) jest używany.</span><span class="sxs-lookup"><span data-stu-id="ec2bf-115">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="ec2bf-116">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="ec2bf-116">ForceEnglishOutput</span></span> | <span data-ttu-id="ec2bf-117">*(3.5 +)* Wymusza nuget.exe przy użyciu opartego na język angielski, niezmienna kultura.</span><span class="sxs-lookup"><span data-stu-id="ec2bf-117">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="ec2bf-118">Format</span><span class="sxs-lookup"><span data-stu-id="ec2bf-118">Format</span></span> | <span data-ttu-id="ec2bf-119">Dotyczy `list` akcji i może być `Detailed` (ustawienie domyślne) lub `Short`.</span><span class="sxs-lookup"><span data-stu-id="ec2bf-119">Applies to the `list` action and can be `Detailed` (the default) or `Short`.</span></span> |
| <span data-ttu-id="ec2bf-120">Pomoc</span><span class="sxs-lookup"><span data-stu-id="ec2bf-120">Help</span></span> | <span data-ttu-id="ec2bf-121">Wyświetla Pomoc dla polecenia.</span><span class="sxs-lookup"><span data-stu-id="ec2bf-121">Displays help information for the command.</span></span> |
| <span data-ttu-id="ec2bf-122">Nieinterakcyjne</span><span class="sxs-lookup"><span data-stu-id="ec2bf-122">NonInteractive</span></span> | <span data-ttu-id="ec2bf-123">Pomija wyświetla monit o dane wejściowe użytkownika lub potwierdzeń.</span><span class="sxs-lookup"><span data-stu-id="ec2bf-123">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="ec2bf-124">Hasło</span><span class="sxs-lookup"><span data-stu-id="ec2bf-124">Password</span></span> | <span data-ttu-id="ec2bf-125">Określa hasło do uwierzytelniania w źródle.</span><span class="sxs-lookup"><span data-stu-id="ec2bf-125">Specifies the password for authenticating with the source.</span></span> |
| <span data-ttu-id="ec2bf-126">StorePasswordInClearText</span><span class="sxs-lookup"><span data-stu-id="ec2bf-126">StorePasswordInClearText</span></span> | <span data-ttu-id="ec2bf-127">Wskazuje, aby zapisać hasło w tekście niezaszyfrowane zamiast domyślnego zachowania przechowywania zaszyfrowane.</span><span class="sxs-lookup"><span data-stu-id="ec2bf-127">Indicates to store the password in unencrypted text instead of the default behavior of storing an encrypted form.</span></span> |
| <span data-ttu-id="ec2bf-128">UserName</span><span class="sxs-lookup"><span data-stu-id="ec2bf-128">UserName</span></span> | <span data-ttu-id="ec2bf-129">Określa nazwę użytkownika do uwierzytelniania w źródle.</span><span class="sxs-lookup"><span data-stu-id="ec2bf-129">Specifies the user name for authenticating with the source.</span></span> |
| <span data-ttu-id="ec2bf-130">Szczegółowość</span><span class="sxs-lookup"><span data-stu-id="ec2bf-130">Verbosity</span></span> | <span data-ttu-id="ec2bf-131">Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *quiet*, *szczegółowe*.</span><span class="sxs-lookup"><span data-stu-id="ec2bf-131">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

> [!Note]
> <span data-ttu-id="ec2bf-132">Upewnij się, że dodanie hasła źródeł w tym samym kontekście użytkownika, ponieważ nuget.exe jest później używany do uzyskiwania dostępu do źródła pakietu.</span><span class="sxs-lookup"><span data-stu-id="ec2bf-132">Make sure to add the sources' password under the same user context as the nuget.exe is later used to access the package source.</span></span> <span data-ttu-id="ec2bf-133">Hasło będzie przechowywany zaszyfrowany w pliku konfiguracji i mogły być odszyfrowane tylko w kontekście tego samego użytkownika, ponieważ został on zaszyfrowany.</span><span class="sxs-lookup"><span data-stu-id="ec2bf-133">The password will be stored encrypted in the config file and can only be decrypted in the same user context as it was encrypted.</span></span> <span data-ttu-id="ec2bf-134">Tak na przykład jeśli używasz serwera kompilacji do przywracania pakietów NuGet, które muszą być szyfrowane hasło z tego samego użytkownika systemu Windows, uruchamiania zadań serwera kompilacji.</span><span class="sxs-lookup"><span data-stu-id="ec2bf-134">So for example when you use a build server to restore NuGet packages the password must be encrypted with the same Windows user under which  the build server task will run.</span></span>

<span data-ttu-id="ec2bf-135">Zobacz też [zmienne środowiskowe](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="ec2bf-135">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="ec2bf-136">Przykłady</span><span class="sxs-lookup"><span data-stu-id="ec2bf-136">Examples</span></span>

```cli
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget source Enable -Name "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
