---
title: inline_recursion pragması
ms.date: 08/29/2019
f1_keywords:
- inline_recursion_CPP
- vc-pragma.inline_recursion
helpviewer_keywords:
- pragmas, inline_recursion
- inline_recursion pragma
ms.assetid: cfef5791-63b7-45ac-9574-623747b9b9c9
ms.openlocfilehash: 0169e06e8e47f7b0a7b3f73e809ddc988bcf1e95
ms.sourcegitcommit: 6e1c1822e7bcf3d2ef23eb8fac6465f88743facf
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/03/2019
ms.locfileid: "70220956"
---
# <a name="inline_recursion-pragma"></a>inline_recursion pragması

Doğrudan veya birbirini dışlayan özyinelemeli işlev çağrılarının satır içi genişletmesini denetler.

## <a name="syntax"></a>Sözdizimi

> **#pragma inline_recursion (** [{ | **off** }] **)**

## <a name="remarks"></a>Açıklamalar

[Satır içi](../cpp/inline-functions-cpp.md) ve [__inline](../cpp/inline-functions-cpp.md) olarak işaretlenen işlevleri veya derleyicinin `/Ob2` seçenek altında otomatik olarak genişledikleri işlevleri denetlemek için bu pragmayı kullanın. Bu pragma kullanımı, 1 veya 2 ' nin [/ob](../build/reference/ob-inline-function-expansion.md) derleyici seçeneği ayarını gerektirir. **İnline_recursion** için varsayılan durum kapalı ' dır. Bu pragma, pragma görüntülendikten sonra ilk işlev çağrısında etkili olur ve işlevin tanımını etkilemez.

**İnline_recursion** pragma özyinelemeli işlevlerin nasıl genişletildiğini denetler. **İnline_recursion** kapalıysa ve bir satır içi işlev kendisini doğrudan ya da dolaylı olarak çağırırsa, işlev yalnızca bir kez genişletilir. **İnline_recursion** açık ise, işlev, [inline_depth](../preprocessor/inline-depth.md) pragması, `inline_depth` pragma tarafından tanımlanan Özyinelemeli işlevler için varsayılan değer veya bir kapasite sınırı olan değer kümesine ulaşana kadar birden çok kez genişletilir.

## <a name="see-also"></a>Ayrıca bkz.

[Pragma yönergeleri ve __pragma anahtar sözcüğü](../preprocessor/pragma-directives-and-the-pragma-keyword.md)\
[inline_depth](../preprocessor/inline-depth.md)\
[/Ob (Satır İçi İşlev Genişletmesi)](../build/reference/ob-inline-function-expansion.md)
