---
title: Çıkarsama Kurallarında Öncelik
ms.date: 11/04/2016
helpviewer_keywords:
- inference rules in NMAKE
- rules, inference
- precedence, inference rule
ms.assetid: 69e3dc02-0815-4c3a-b02b-1cb85fceaf24
ms.openlocfilehash: ca24134fd1829ad3d97ca67b8c30aae3af4109ee
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62319687"
---
# <a name="precedence-in-inference-rules"></a>Çıkarsama Kurallarında Öncelik

NMAKE çıkarım kuralı birden çok kez tanımlanmış, en yüksek öncelikli tanımı kullanır. Aşağıdaki liste, en yüksek öncelikten en düşüğe sırasını gösterir:

1. Derleme görevleri dosyasında tanımlanan bir çıkarma kuralı; sonraki tanımları önceliğe sahip olur.

1. Tools.ini içinde tanımlanan bir çıkarma kuralı; sonraki tanımları önceliğe sahip olur.

1. Bir önceden tanımlanmış çıkarım kuralı.

## <a name="see-also"></a>Ayrıca bkz.

[Çıkarım Kuralları](inference-rules.md)
