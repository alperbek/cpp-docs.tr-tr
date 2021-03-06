---
title: Öznitelikler (C++/CX)
ms.date: 12/30/2016
ms.assetid: 4438e03c-4de3-433d-abcc-31aa863bc0e0
ms.openlocfilehash: b9e645de021e8618d1dc15a7d58dbbe5998e6fbc
ms.sourcegitcommit: 89d9e1cb08fa872483d1cde98bc2a7c870e505e9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/22/2020
ms.locfileid: "82032388"
---
# <a name="attributes-ccx"></a>Öznitelikler (C++/CX)

Öznitelik, meta veri oluşturmada belirli davranışları belirtmek için Windows Runtime türleri ve yöntemlerine kare ayraçlar halinde hazırlanabilen özel bir ref sınıfı türüdür. C++/CX kodunda yaygın olarak kullanılan birkaç önceden tanımlanmış öznitelikler-örneğin, [Windows::Foundation::Metadata::WebHostHidden—](/uwp/api/windows.foundation.metadata.webhosthiddenattribute)yaygın olarak kullanılır. Bu örnek, özniteliğin bir sınıfa nasıl uygulandığını gösterir:

[!code-cpp[cx_attributes#01](../cppcx/codesnippet/CPP/cx_attributes/class1.h#01)]

## <a name="custom-attributes"></a>Özel öznitelikler

Özel öznitelikleri de tanımlayabilirsiniz. Özel öznitelikler, bu Windows Runtime kurallarına uygun olmalıdır:

- Özel öznitelikler yalnızca ortak alanlar içerebilir.

- Öznitelik bir sınıfa uygulandığında özel öznitelik alanları başharfe bilebilir.

- Bir alan bu türlerden biri olabilir:

  - int32 (int)

  - uint32 (imzasız int)

  - bool

  - Platform::String^

  - Windows::Foundation::HResult

  - Platform::Tip^

  - public enum sınıfı (kullanıcı tanımlı enumları içerir)

Sonraki örnek, özel bir özniteliği nasıl tanımlayıp kullandığınızda nasıl başharflere verilebildiğini gösterir.

[!code-cpp[cx_attributes#02](../cppcx/codesnippet/CPP/cx_attributes/class1.h#02)]

## <a name="see-also"></a>Ayrıca bkz.

[Tür Sistemi (C++/CX)](../cppcx/type-system-c-cx.md)<br/>
[C++/CX Dil Başvurusu](../cppcx/visual-c-language-reference-c-cx.md)<br/>
[Ad Alanları Başvurusu](../cppcx/namespaces-reference-c-cx.md)
