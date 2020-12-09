---
title: Критическое изменение. Элемент DataGridView больше не сбрасывает шрифты для настраиваемых стилей ячеек
description: Сведения о критическом изменении в .NET 5.0, где элемент DataGridView больше не сбрасывает шрифты стиля ячейки по умолчанию, чтобы они совпадали со шрифтом окружения, если шрифт стиля ячейки был настроен.
ms.date: 10/18/2020
ms.openlocfilehash: 708b12ba1305681f5c38eb605861d02e3b2c8eb1
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/24/2020
ms.locfileid: "95760284"
---
# <a name="datagridview-no-longer-resets-fonts-for-customized-cell-styles"></a><span data-ttu-id="f1673-103">Элемент DataGridView больше не сбрасывает шрифты для настраиваемых стилей ячеек</span><span class="sxs-lookup"><span data-stu-id="f1673-103">DataGridView no longer resets fonts for customized cell styles</span></span>

<span data-ttu-id="f1673-104">При изменении шрифта окружения <xref:System.Windows.Forms.DataGridViewElement.DataGridView> больше не выполняет сброс шрифтов стиля ячейки по умолчанию, чтобы они совпадали со шрифтом окружения, если шрифт стиля ячейки был настроен.</span><span class="sxs-lookup"><span data-stu-id="f1673-104">When the ambient font changes, <xref:System.Windows.Forms.DataGridViewElement.DataGridView> no longer resets default cell style fonts to match the ambient font if the cell style font has been customized.</span></span>

## <a name="change-description"></a><span data-ttu-id="f1673-105">Описание изменений</span><span class="sxs-lookup"><span data-stu-id="f1673-105">Change description</span></span>

<span data-ttu-id="f1673-106">В предыдущих версиях .NET при изменении шрифта окружения <xref:System.Windows.Forms.DataGridViewElement.DataGridView> сбрасывал и переопределял пользовательские шрифты в свойствах <xref:System.Windows.Forms.DataGridView.DefaultCellStyle>, <xref:System.Windows.Forms.DataGridView.ColumnHeadersDefaultCellStyle> и <xref:System.Windows.Forms.DataGridView.RowHeadersDefaultCellStyle>.</span><span class="sxs-lookup"><span data-stu-id="f1673-106">In previous .NET versions, if the ambient font changes, <xref:System.Windows.Forms.DataGridViewElement.DataGridView> resets and overrides user-defined fonts in the <xref:System.Windows.Forms.DataGridView.DefaultCellStyle>, <xref:System.Windows.Forms.DataGridView.ColumnHeadersDefaultCellStyle>, and <xref:System.Windows.Forms.DataGridView.RowHeadersDefaultCellStyle> properties.</span></span>

<span data-ttu-id="f1673-107">Начиная с .NET 5.0 при настройке параметров шрифтов в свойствах <xref:System.Windows.Forms.DataGridView.DefaultCellStyle>, <xref:System.Windows.Forms.DataGridView.ColumnHeadersDefaultCellStyle> или <xref:System.Windows.Forms.DataGridView.RowHeadersDefaultCellStyle> эти параметры сохраняются даже при изменении шрифта окружения.</span><span class="sxs-lookup"><span data-stu-id="f1673-107">Starting in .NET 5.0, if you configure font settings in the <xref:System.Windows.Forms.DataGridView.DefaultCellStyle>, <xref:System.Windows.Forms.DataGridView.ColumnHeadersDefaultCellStyle>, or <xref:System.Windows.Forms.DataGridView.RowHeadersDefaultCellStyle> properties, those settings are retained even when the ambient font changes.</span></span> <span data-ttu-id="f1673-108">Для всех свойств, для которых шрифт не был настроен, шрифт изменится в соответствии с параметрами шрифта окружения.</span><span class="sxs-lookup"><span data-stu-id="f1673-108">For any of these properties that you don't customize the font, the font will change to match the ambient font settings.</span></span>

## <a name="reason-for-change"></a><span data-ttu-id="f1673-109">Причина изменения</span><span class="sxs-lookup"><span data-stu-id="f1673-109">Reason for change</span></span>

<span data-ttu-id="f1673-110">При [изменении шрифта по умолчанию в .NET Core 3.0](../../winforms.md#default-control-font-changed-to-segoe-ui-9-pt) параметры шрифтов по умолчанию для различных стилей ячеек также изменяются.</span><span class="sxs-lookup"><span data-stu-id="f1673-110">With the [change of the default font in .NET Core 3.0](../../winforms.md#default-control-font-changed-to-segoe-ui-9-pt), the default font settings for the various cell styles also changed.</span></span> <span data-ttu-id="f1673-111">Такое поведение нежелательно для приложений, которые используют пользовательский стиль в своих элементах управления <xref:System.Windows.Forms.DataGridViewElement.DataGridView>, и затрудняет их перенос с .NET Framework на .NET 5.0.</span><span class="sxs-lookup"><span data-stu-id="f1673-111">This behavior is undesirable for apps that rely on custom styling in their <xref:System.Windows.Forms.DataGridViewElement.DataGridView> controls, and impeded the migration of these apps from .NET Framework to .NET 5.0.</span></span>

## <a name="version-introduced"></a><span data-ttu-id="f1673-112">Представленная версия</span><span class="sxs-lookup"><span data-stu-id="f1673-112">Version introduced</span></span>

<span data-ttu-id="f1673-113">.NET 5.0</span><span class="sxs-lookup"><span data-stu-id="f1673-113">.NET 5.0</span></span>

## <a name="recommended-action"></a><span data-ttu-id="f1673-114">Рекомендованное действие</span><span class="sxs-lookup"><span data-stu-id="f1673-114">Recommended action</span></span>

<span data-ttu-id="f1673-115">Никаких действий выполнять не требуется.</span><span class="sxs-lookup"><span data-stu-id="f1673-115">No action is required on your part.</span></span> <span data-ttu-id="f1673-116">Однако если вы настроили шрифт в свойствах <xref:System.Windows.Forms.DataGridView.DefaultCellStyle>, <xref:System.Windows.Forms.DataGridView.ColumnHeadersDefaultCellStyle> или <xref:System.Windows.Forms.DataGridView.RowHeadersDefaultCellStyle> и хотите, чтобы шрифт совпадал со шрифтом окружения, установите параметр <xref:System.Windows.Forms.DataGridViewCellStyle.Font?displayProperty=nameWithType> в значение `null` для каждого свойства.</span><span class="sxs-lookup"><span data-stu-id="f1673-116">However, if you've customized the font in the <xref:System.Windows.Forms.DataGridView.DefaultCellStyle>, <xref:System.Windows.Forms.DataGridView.ColumnHeadersDefaultCellStyle>, or <xref:System.Windows.Forms.DataGridView.RowHeadersDefaultCellStyle> properties and want the font to match the ambient font, set <xref:System.Windows.Forms.DataGridViewCellStyle.Font?displayProperty=nameWithType> to `null` for each property.</span></span>

## <a name="affected-apis"></a><span data-ttu-id="f1673-117">Затронутые API</span><span class="sxs-lookup"><span data-stu-id="f1673-117">Affected APIs</span></span>

- <xref:System.Windows.Forms.DataGridView.DefaultCellStyle?displayProperty=fullName>
- <xref:System.Windows.Forms.DataGridView.ColumnHeadersDefaultCellStyle?displayProperty=fullName>
- <xref:System.Windows.Forms.DataGridView.RowHeadersDefaultCellStyle?displayProperty=fullName>

<!--

### Affected APIs

- `P:System.Windows.Forms.DataGridView.DefaultCellStyle`
- `P:System.Windows.Forms.DataGridView.ColumnHeadersDefaultCellStyle`
- `P:System.Windows.Forms.DataGridView.RowHeadersDefaultCellStyle`

### Category

- Windows Forms

-->