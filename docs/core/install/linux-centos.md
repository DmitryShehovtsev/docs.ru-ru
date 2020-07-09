---
title: Установка .NET Core в CentOS — .NET Core
description: Здесь приводятся различные способы установки пакета SDK для .NET Core и среды выполнения .NET Core в CentOS.
author: adegeo
ms.author: adegeo
ms.date: 06/04/2020
ms.openlocfilehash: 6b1bad3a6c967483bb683866de84c9e5077a336f
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/01/2020
ms.locfileid: "85619511"
---
# <a name="install-net-core-sdk-or-net-core-runtime-on-centos"></a><span data-ttu-id="708e5-103">Установка пакета SDK для .NET Core или среды выполнения .NET Core в CentOS</span><span class="sxs-lookup"><span data-stu-id="708e5-103">Install .NET Core SDK or .NET Core Runtime on CentOS</span></span>

<span data-ttu-id="708e5-104">.NET Core поддерживается в CentOS.</span><span class="sxs-lookup"><span data-stu-id="708e5-104">.NET Core is supported on CentOS.</span></span> <span data-ttu-id="708e5-105">В этой статье описано, как установить .NET Core в CentOS.</span><span class="sxs-lookup"><span data-stu-id="708e5-105">This article describes how to install .NET Core on CentOS.</span></span>

[!INCLUDE [linux-intro-sdk-vs-runtime](includes/linux-intro-sdk-vs-runtime.md)]

[!INCLUDE [linux-install-package-manager-x64-vs-arm](includes/linux-install-package-manager-x64-vs-arm.md)]

## <a name="supported-distributions"></a><span data-ttu-id="708e5-106">Поддерживаемые дистрибутивы</span><span class="sxs-lookup"><span data-stu-id="708e5-106">Supported distributions</span></span>

<span data-ttu-id="708e5-107">В приведенной ниже таблице содержится список поддерживаемых сейчас выпусков .NET Core в CentOS 7 и CentOS 8.</span><span class="sxs-lookup"><span data-stu-id="708e5-107">The following table is a list of currently supported .NET Core releases on both CentOS 7 and CentOS 8.</span></span> <span data-ttu-id="708e5-108">Эти версии поддерживаются до того же времени, что и версия [.NET Core](https://dotnet.microsoft.com/platform/support/policy/dotnet-core) или CentOS.</span><span class="sxs-lookup"><span data-stu-id="708e5-108">These versions remain supported until either the version of [.NET Core reaches end-of-support](https://dotnet.microsoft.com/platform/support/policy/dotnet-core) or the version of CentOS is no longer supported.</span></span>

- <span data-ttu-id="708e5-109">Значок ✔️ означает, что версия CentOS или .NET Core поддерживается.</span><span class="sxs-lookup"><span data-stu-id="708e5-109">A ✔️ indicates that the version of CentOS or .NET Core is still supported.</span></span>
- <span data-ttu-id="708e5-110">Значок ❌ означает, что версия CentOS или версия .NET Core в таком выпуске CentOS не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="708e5-110">A ❌ indicates that the version of CentOS or .NET Core isn't supported on that CentOS release.</span></span>
- <span data-ttu-id="708e5-111">Если значок ✔️ стоит как напротив версии CentOS, так и напротив версии .NET Core, это значит, что такое сочетание ОС и .NET поддерживается.</span><span class="sxs-lookup"><span data-stu-id="708e5-111">When both a version of CentOS and a version of .NET Core have ✔️, that OS and .NET combination are supported.</span></span>

| <span data-ttu-id="708e5-112">CentOS</span><span class="sxs-lookup"><span data-stu-id="708e5-112">CentOS</span></span>                   | <span data-ttu-id="708e5-113">.NET Core 2.1</span><span class="sxs-lookup"><span data-stu-id="708e5-113">.NET Core 2.1</span></span> | <span data-ttu-id="708e5-114">.NET Core 3.1</span><span class="sxs-lookup"><span data-stu-id="708e5-114">.NET Core 3.1</span></span> | <span data-ttu-id="708e5-115">Предварительная версия .NET 5 (только установка вручную)</span><span class="sxs-lookup"><span data-stu-id="708e5-115">.NET 5 Preview (manual install only)</span></span> |
|--------------------------|---------------|---------------|----------------|
| <span data-ttu-id="708e5-116">✔️ [8](#centos-8-)</span><span class="sxs-lookup"><span data-stu-id="708e5-116">✔️ [8](#centos-8-)</span></span> | <span data-ttu-id="708e5-117">✔️ 2.1</span><span class="sxs-lookup"><span data-stu-id="708e5-117">✔️ 2.1</span></span>        | <span data-ttu-id="708e5-118">✔️ 3.1</span><span class="sxs-lookup"><span data-stu-id="708e5-118">✔️ 3.1</span></span>        | <span data-ttu-id="708e5-119">✔️ 5.0 (предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="708e5-119">✔️ 5.0 Preview</span></span> |
| <span data-ttu-id="708e5-120">✔️ [7](#centos-7-)</span><span class="sxs-lookup"><span data-stu-id="708e5-120">✔️ [7](#centos-7-)</span></span> | <span data-ttu-id="708e5-121">✔️ 2.1</span><span class="sxs-lookup"><span data-stu-id="708e5-121">✔️ 2.1</span></span>        | <span data-ttu-id="708e5-122">✔️ 3.1</span><span class="sxs-lookup"><span data-stu-id="708e5-122">✔️ 3.1</span></span>        | <span data-ttu-id="708e5-123">✔️ 5.0 (предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="708e5-123">✔️ 5.0 Preview</span></span> |

<span data-ttu-id="708e5-124">Следующие версии .NET Core больше не поддерживаются</span><span class="sxs-lookup"><span data-stu-id="708e5-124">The following versions of .NET Core are no longer supported.</span></span> <span data-ttu-id="708e5-125">(но остаются доступными для скачивания):</span><span class="sxs-lookup"><span data-stu-id="708e5-125">The downloads for these still remain published:</span></span>

- <span data-ttu-id="708e5-126">3.0</span><span class="sxs-lookup"><span data-stu-id="708e5-126">3.0</span></span>
- <span data-ttu-id="708e5-127">2.2</span><span class="sxs-lookup"><span data-stu-id="708e5-127">2.2</span></span>
- <span data-ttu-id="708e5-128">2.0</span><span class="sxs-lookup"><span data-stu-id="708e5-128">2.0</span></span>

[!INCLUDE [linux-install-package-manager-x64-vs-arm](includes/linux-install-package-manager-x64-vs-arm.md)]

## <a name="how-to-install-other-versions"></a><span data-ttu-id="708e5-129">Установка других версий</span><span class="sxs-lookup"><span data-stu-id="708e5-129">How to install other versions</span></span>

[!INCLUDE [package-manager-switcher](./includes/package-manager-heading-hack-pkgname.md)]

## <a name="centos-8-"></a><span data-ttu-id="708e5-130">CentOS 8 ✔️</span><span class="sxs-lookup"><span data-stu-id="708e5-130">CentOS 8 ✔️</span></span>

<span data-ttu-id="708e5-131">.NET Core 3.1 предоставляется в репозиториях пакетов по умолчанию для CentOS 8.</span><span class="sxs-lookup"><span data-stu-id="708e5-131">.NET Core 3.1 is available in the default package repositories for CentOS 8.</span></span>

[!INCLUDE [linux-dnf-install-31](includes/linux-install-31-dnf.md)]

## <a name="centos-7-"></a><span data-ttu-id="708e5-132">CentOS 7 ✔️</span><span class="sxs-lookup"><span data-stu-id="708e5-132">CentOS 7 ✔️</span></span>

[!INCLUDE [linux-prep-intro-generic](includes/linux-prep-intro-generic.md)]

```bash
sudo rpm -Uvh https://packages.microsoft.com/config/centos/7/packages-microsoft-prod.rpm
```

[!INCLUDE [linux-yum-install-31](includes/linux-install-31-yum.md)]

## <a name="troubleshoot-the-package-manager"></a><span data-ttu-id="708e5-133">Устранение неполадок диспетчера пакетов</span><span class="sxs-lookup"><span data-stu-id="708e5-133">Troubleshoot the package manager</span></span>

<span data-ttu-id="708e5-134">В этом разделе описаны распространенные ошибки, которые могут возникнуть при использовании диспетчера пакетов для установки .NET Core.</span><span class="sxs-lookup"><span data-stu-id="708e5-134">This section provides information on common errors you may get while using the package manager to install .NET Core.</span></span>

### <a name="failed-to-fetch"></a><span data-ttu-id="708e5-135">Ошибка получения</span><span class="sxs-lookup"><span data-stu-id="708e5-135">Failed to fetch</span></span>

[!INCLUDE [package-manager-failed-to-fetch-rpm](includes/package-manager-failed-to-fetch-rpm.md)]

## <a name="snap"></a><span data-ttu-id="708e5-136">Snap-пакеты</span><span class="sxs-lookup"><span data-stu-id="708e5-136">Snap</span></span>

[!INCLUDE [linux-install-snap](includes/linux-install-snap.md)]

## <a name="dependencies"></a><span data-ttu-id="708e5-137">Зависимости</span><span class="sxs-lookup"><span data-stu-id="708e5-137">Dependencies</span></span>

[!INCLUDE [linux-rpm-install-dependencies](includes/linux-rpm-install-dependencies.md)]

## <a name="scripted-install"></a><span data-ttu-id="708e5-138">Установка с помощью скрипта</span><span class="sxs-lookup"><span data-stu-id="708e5-138">Scripted install</span></span>

[!INCLUDE [linux-install-scripted](includes/linux-install-scripted.md)]

## <a name="manual-install"></a><span data-ttu-id="708e5-139">Установка вручную</span><span class="sxs-lookup"><span data-stu-id="708e5-139">Manual install</span></span>

[!INCLUDE [linux-install-manual](includes/linux-install-manual.md)]

## <a name="next-steps"></a><span data-ttu-id="708e5-140">Следующие шаги</span><span class="sxs-lookup"><span data-stu-id="708e5-140">Next steps</span></span>

- [<span data-ttu-id="708e5-141">Учебник. Создание консольного приложения с помощью пакета SDK для .NET Core в Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="708e5-141">Tutorial: Create a console application with .NET Core SDK using Visual Studio Code</span></span>](../tutorials/with-visual-studio-code.md)