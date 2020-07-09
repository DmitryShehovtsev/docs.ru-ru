---
title: Установка .NET Core в Alpine — .NET Core
description: Здесь приводятся различные способы установки пакета SDK для .NET Core и среды выполнения .NET Core в Alpine.
author: adegeo
ms.author: adegeo
ms.date: 06/04/2020
ms.openlocfilehash: 0efe3bbacbe573b77eae8818ea29b5a3867e4570
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.contentlocale: ru-RU
ms.lasthandoff: 07/01/2020
ms.locfileid: "85619524"
---
# <a name="install-net-core-sdk-or-net-core-runtime-on-alpine"></a><span data-ttu-id="625f0-103">Установка пакета SDK для .NET Core или среды выполнения .NET Core в Alpine</span><span class="sxs-lookup"><span data-stu-id="625f0-103">Install .NET Core SDK or .NET Core Runtime on Alpine</span></span>

<span data-ttu-id="625f0-104">В этой статье описано, как установить .NET Core в Alpine.</span><span class="sxs-lookup"><span data-stu-id="625f0-104">This article describes how to install .NET Core on Alpine.</span></span> <span data-ttu-id="625f0-105">Если поддержка какой-либо версии Alpine прекращается, то .NET Core также перестает поддерживать ее.</span><span class="sxs-lookup"><span data-stu-id="625f0-105">When a Alpine version falls out of support, .NET Core is no longer supported with that version.</span></span> <span data-ttu-id="625f0-106">Но с помощью этих инструкций вы сможете запустить .NET Core даже в неподдерживаемых версиях.</span><span class="sxs-lookup"><span data-stu-id="625f0-106">However, these instructions may help you to get .NET Core running on those versions, even though it isn't supported.</span></span>

[!INCLUDE [linux-intro-sdk-vs-runtime](includes/linux-intro-sdk-vs-runtime.md)]

<span data-ttu-id="625f0-107">Установщиков для Alpine не существует.</span><span class="sxs-lookup"><span data-stu-id="625f0-107">There are no installers for Alpine.</span></span> <span data-ttu-id="625f0-108">Необходимо либо использовать [сценарий установки](#scripted-install), либо следовать инструкциям по [установке вручную](#manual-install).</span><span class="sxs-lookup"><span data-stu-id="625f0-108">You must either use the [install script](#scripted-install) or follow the [manual install](#manual-install) instructions.</span></span>

## <a name="supported-distributions"></a><span data-ttu-id="625f0-109">Поддерживаемые дистрибутивы</span><span class="sxs-lookup"><span data-stu-id="625f0-109">Supported distributions</span></span>

<span data-ttu-id="625f0-110">В приведенной ниже таблице содержится список поддерживаемых сейчас выпусков .NET Core и версий Alpine, в которых они поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="625f0-110">The following table is a list of currently supported .NET Core releases and the versions of Alpine they're supported on.</span></span> <span data-ttu-id="625f0-111">Эти версии поддерживаются до окончания поддержки версии [.NET Core](https://dotnet.microsoft.com/platform/support/policy/dotnet-core) либо до окончания жизненного цикла версии [Alpine](https://wiki.alpinelinux.org/wiki/Alpine_Linux:Releases).</span><span class="sxs-lookup"><span data-stu-id="625f0-111">These versions remain supported until either the version of [.NET Core reaches end-of-support](https://dotnet.microsoft.com/platform/support/policy/dotnet-core) or the version of [Alpine reaches end-of-life](https://wiki.alpinelinux.org/wiki/Alpine_Linux:Releases).</span></span>

- <span data-ttu-id="625f0-112">Значок ✔️ означает, что версия Alpine или .NET Core поддерживается.</span><span class="sxs-lookup"><span data-stu-id="625f0-112">A ✔️ indicates that the version of Alpine or .NET Core is still supported.</span></span>
- <span data-ttu-id="625f0-113">Значок ❌ означает, что версия Alpine или версия .NET Core в таком выпуске Alpine не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="625f0-113">A ❌ indicates that the version of Alpine or .NET Core isn't supported on that Alpine release.</span></span>
- <span data-ttu-id="625f0-114">Если значок ✔️ стоит как напротив версии Alpine, так и напротив версии .NET Core, это значит, что такое сочетание ОС и .NET поддерживается.</span><span class="sxs-lookup"><span data-stu-id="625f0-114">When both a version of Alpine and a version of .NET Core have ✔️, that OS and .NET combination are supported.</span></span>

| <span data-ttu-id="625f0-115">Alpine</span><span class="sxs-lookup"><span data-stu-id="625f0-115">Alpine</span></span>                   | <span data-ttu-id="625f0-116">.NET Core 2.1</span><span class="sxs-lookup"><span data-stu-id="625f0-116">.NET Core 2.1</span></span> | <span data-ttu-id="625f0-117">.NET Core 3.1</span><span class="sxs-lookup"><span data-stu-id="625f0-117">.NET Core 3.1</span></span> | <span data-ttu-id="625f0-118">Предварительная версия .NET 5</span><span class="sxs-lookup"><span data-stu-id="625f0-118">.NET 5 Preview</span></span> |
|--------------------------|---------------|---------------|----------------|
| <span data-ttu-id="625f0-119">✔️ 3.12</span><span class="sxs-lookup"><span data-stu-id="625f0-119">✔️ 3.12</span></span>  | <span data-ttu-id="625f0-120">✔️ 2.1</span><span class="sxs-lookup"><span data-stu-id="625f0-120">✔️ 2.1</span></span>        | <span data-ttu-id="625f0-121">✔️ 3.1</span><span class="sxs-lookup"><span data-stu-id="625f0-121">✔️ 3.1</span></span>        | <span data-ttu-id="625f0-122">✔️ 5.0 (предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="625f0-122">✔️ 5.0 Preview</span></span> |
| <span data-ttu-id="625f0-123">✔️ 3.11</span><span class="sxs-lookup"><span data-stu-id="625f0-123">✔️ 3.11</span></span>  | <span data-ttu-id="625f0-124">✔️ 2.1</span><span class="sxs-lookup"><span data-stu-id="625f0-124">✔️ 2.1</span></span>        | <span data-ttu-id="625f0-125">✔️ 3.1</span><span class="sxs-lookup"><span data-stu-id="625f0-125">✔️ 3.1</span></span>        | <span data-ttu-id="625f0-126">✔️ 5.0 (предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="625f0-126">✔️ 5.0 Preview</span></span> |
| <span data-ttu-id="625f0-127">✔️ 3.10</span><span class="sxs-lookup"><span data-stu-id="625f0-127">✔️ 3.10</span></span>  | <span data-ttu-id="625f0-128">✔️ 2.1</span><span class="sxs-lookup"><span data-stu-id="625f0-128">✔️ 2.1</span></span>        | <span data-ttu-id="625f0-129">✔️ 3.1</span><span class="sxs-lookup"><span data-stu-id="625f0-129">✔️ 3.1</span></span>        | <span data-ttu-id="625f0-130">✔️ 5.0 (предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="625f0-130">✔️ 5.0 Preview</span></span> |
| <span data-ttu-id="625f0-131">✔️ 3.9</span><span class="sxs-lookup"><span data-stu-id="625f0-131">✔️ 3.9</span></span>   | <span data-ttu-id="625f0-132">✔️ 2.1</span><span class="sxs-lookup"><span data-stu-id="625f0-132">✔️ 2.1</span></span>        | <span data-ttu-id="625f0-133">✔️ 3.1</span><span class="sxs-lookup"><span data-stu-id="625f0-133">✔️ 3.1</span></span>        | <span data-ttu-id="625f0-134">✔️ 5.0 (предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="625f0-134">✔️ 5.0 Preview</span></span> |
| <span data-ttu-id="625f0-135">❌ 3.8</span><span class="sxs-lookup"><span data-stu-id="625f0-135">❌ 3.8</span></span>   | <span data-ttu-id="625f0-136">✔️ 2.1</span><span class="sxs-lookup"><span data-stu-id="625f0-136">✔️ 2.1</span></span>        | <span data-ttu-id="625f0-137">❌ 3.1</span><span class="sxs-lookup"><span data-stu-id="625f0-137">❌ 3.1</span></span>        | <span data-ttu-id="625f0-138">❌ 5.0 (предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="625f0-138">❌ 5.0 Preview</span></span> |

<span data-ttu-id="625f0-139">Следующие версии .NET Core больше не поддерживаются,</span><span class="sxs-lookup"><span data-stu-id="625f0-139">The following versions of .NET Core are no longer supported.</span></span> <span data-ttu-id="625f0-140">(но остаются доступными для скачивания):</span><span class="sxs-lookup"><span data-stu-id="625f0-140">The downloads for these still remain published:</span></span>

- <span data-ttu-id="625f0-141">3.0</span><span class="sxs-lookup"><span data-stu-id="625f0-141">3.0</span></span>
- <span data-ttu-id="625f0-142">2.2</span><span class="sxs-lookup"><span data-stu-id="625f0-142">2.2</span></span>
- <span data-ttu-id="625f0-143">2.0</span><span class="sxs-lookup"><span data-stu-id="625f0-143">2.0</span></span>

## <a name="dependencies"></a><span data-ttu-id="625f0-144">Зависимости</span><span class="sxs-lookup"><span data-stu-id="625f0-144">Dependencies</span></span>

<span data-ttu-id="625f0-145">Для .NET Core в Alpine Linux необходимо установить следующие зависимости:</span><span class="sxs-lookup"><span data-stu-id="625f0-145">.NET Core on Alpine Linux requires the following dependencies installed:</span></span>

- <span data-ttu-id="625f0-146">icu-libs</span><span class="sxs-lookup"><span data-stu-id="625f0-146">icu-libs</span></span>
- <span data-ttu-id="625f0-147">krb5-libs</span><span class="sxs-lookup"><span data-stu-id="625f0-147">krb5-libs</span></span>
- <span data-ttu-id="625f0-148">libgcc</span><span class="sxs-lookup"><span data-stu-id="625f0-148">libgcc</span></span>
- <span data-ttu-id="625f0-149">libintl</span><span class="sxs-lookup"><span data-stu-id="625f0-149">libintl</span></span>
- <span data-ttu-id="625f0-150">libssl 1.1 (Alpine версии 3.9 или более поздней)</span><span class="sxs-lookup"><span data-stu-id="625f0-150">libssl1.1 (Alpine v3.9 or greater)</span></span>
- <span data-ttu-id="625f0-151">libssl1.0 (Alpine версии 3.8 или более ранней)</span><span class="sxs-lookup"><span data-stu-id="625f0-151">libssl1.0 (Alpine v3.8 or lower)</span></span>
- <span data-ttu-id="625f0-152">libstdc++</span><span class="sxs-lookup"><span data-stu-id="625f0-152">libstdc++</span></span>
- <span data-ttu-id="625f0-153">zlib</span><span class="sxs-lookup"><span data-stu-id="625f0-153">zlib</span></span>

## <a name="scripted-install"></a><span data-ttu-id="625f0-154">Установка с помощью сценария</span><span class="sxs-lookup"><span data-stu-id="625f0-154">Scripted install</span></span>

[!INCLUDE [linux-install-scripted](includes/linux-install-scripted.md)]

## <a name="manual-install"></a><span data-ttu-id="625f0-155">Установка вручную</span><span class="sxs-lookup"><span data-stu-id="625f0-155">Manual install</span></span>

[!INCLUDE [linux-install-manual](includes/linux-install-manual.md)]

## <a name="next-steps"></a><span data-ttu-id="625f0-156">Следующие шаги</span><span class="sxs-lookup"><span data-stu-id="625f0-156">Next steps</span></span>

- [<span data-ttu-id="625f0-157">Учебник. Создание консольного приложения с помощью пакета SDK для .NET Core в Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="625f0-157">Tutorial: Create a console application with .NET Core SDK using Visual Studio Code</span></span>](../tutorials/with-visual-studio-code.md)