---
title: Предупреждение SYSLIB0011
description: Сведения об устаревших элементах, которые приводят к появлению предупреждения во время компиляции SYSLIB0011.
ms.topic: reference
ms.date: 10/20/2020
ms.openlocfilehash: 36292cc5314e2b7677d705780880b7e25ae0dfb6
ms.sourcegitcommit: e301979e3049ce412d19b094c60ed95b316a8f8c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/16/2020
ms.locfileid: "97596361"
---
# <a name="syslib0011-binaryformatter-serialization-is-obsolete"></a>SYSLIB0011. Сериализация BinaryFormatter устарела

Из-за [уязвимостей системы безопасности](../../../standard/serialization/binaryformatter-security-guide.md#binaryformatter-security-vulnerabilities) в <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter>, следующие API являются устаревшими, начиная с версии .NET 5.0. При их использовании во время компиляции создается предупреждение `SYSLIB0011`.

- <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter.Serialize%2A?displayProperty=nameWithType>
- <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter.Deserialize%2A?displayProperty=nameWithType>
- <xref:System.Runtime.Serialization.Formatter.Serialize(System.IO.Stream,System.Object)?displayProperty=nameWithType>
- <xref:System.Runtime.Serialization.Formatter.Deserialize(System.IO.Stream)?displayProperty=nameWithType>
- <xref:System.Runtime.Serialization.IFormatter.Serialize(System.IO.Stream,System.Object)?displayProperty=nameWithType>
- <xref:System.Runtime.Serialization.IFormatter.Deserialize(System.IO.Stream)?displayProperty=nameWithType>

## <a name="workarounds"></a>Обходные пути

Рассмотрите возможность использования <xref:System.Text.Json.JsonSerializer> или <xref:System.Xml.Serialization.XmlSerializer> вместо <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter>.

Дополнительные сведения о рекомендуемых действиях см. в статье [Устранение ошибок, связанных с устареванием и отключением BinaryFormatter](https://aka.ms/binaryformatter).

[!INCLUDE [suppress-syslib-warning](../../../../includes/suppress-syslib-warning.md)]

## <a name="see-also"></a>См. также

- [Устранение ошибок, связанных с устареванием и отключением BinaryFormatter](https://aka.ms/binaryformatter)
- [Методы сериализации BinaryFormatter устарели и запрещены в приложениях ASP.NET](../core-libraries/5.0/binaryformatter-serialization-obsolete.md)
