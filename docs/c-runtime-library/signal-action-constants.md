---
title: sinyal Eylemi Sabitleri
ms.date: 11/04/2016
f1_keywords:
- SIG_IGN
- SIG_DFL
helpviewer_keywords:
- signal action constants
- SIG_IGN constant
- SIG_DFL constant
ms.assetid: c3cb4f15-d39e-4d9d-84f9-0d33e3eb5993
ms.openlocfilehash: 4ff79626d576a05744336d36f99caf95d9b9902d
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62267995"
---
# <a name="signal-action-constants"></a>sinyal Eylemi Sabitleri

Gerçekleştirilecek eylemi Kesme sinyali alındığında değerine bağlıdır `func`.

## <a name="syntax"></a>Sözdizimi

```
#include <signal.h>
```

## <a name="remarks"></a>Açıklamalar

`func` Bağımsız değişkeni bir işlev adresi veya aşağıda listelenen ve SİNYAL içinde tanımlı bildirim sabitleri biri olmalıdır. H

|||
|-|-|
| `SIG_DFL`  | Sistem varsayılan yanıt kullanır. Akış g/ç çağıran program kullanılıyorsa, çalışma zamanı kitaplığı tarafından oluşturulan arabellekler Temizlenen değil.  |
| `SIG_IGN`  | Kesme sinyali yok sayıyor. Bu değer için hiçbir zaman verilmelidir `SIGFPE`, kayan nokta işleminin durumunu sol beri tanımlanmamış.  |
| `SIG_SGE`  | Bir hata oluştu sinyal gösterir.  |
| `SIG_ACK`  | Bir bildirim alındı gösterir.  |
| `SIG_ERR`  | Bir dönüş türü sinyalinden belirten bir hata oluştu.  |

## <a name="see-also"></a>Ayrıca bkz.

[signal](../c-runtime-library/reference/signal.md)<br/>
[Global Sabitler](../c-runtime-library/global-constants.md)
