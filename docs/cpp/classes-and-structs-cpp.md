---
title: Sınıflar ve Yapılar (C++)
ms.date: 05/07/2019
helpviewer_keywords:
- C++, classes and structs
ms.assetid: 516dd496-13fb-4f17-845a-e9ca45437873
ms.openlocfilehash: 19d95c9519670db39f3ca467aff794233823d7ba
ms.sourcegitcommit: 857fa6b530224fa6c18675138043aba9aa0619fb
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/24/2020
ms.locfileid: "80180894"
---
# <a name="classes-and-structs-c"></a>Sınıflar ve Yapılar (C++)

Bu bölüm sınıfları C++ ve yapıları tanıtır. İki yapı, ' de varsayılan C++ erişilebilirliği genel olduğundan, ancak sınıflar varsayılan olarak Private olduğunda, ' de aynıdır.

Sınıflar ve yapılar, kendi türlerinizi tanımladığınız yapılardır. Sınıfların ve yapıların her ikisi de, türün durumunu ve davranışını açıklamanıza olanak sağlayan veri üyeleri ve üye işlevleri içerebilir.

Aşağıdaki konular dahil edilmiştir:

- [class](../cpp/class-cpp.md)

- [struct](../cpp/struct-cpp.md)

- [Sınıf Üyelerine Genel bakış](../cpp/class-member-overview.md)

- [Üye Erişim Denetimi](../cpp/member-access-control-cpp.md)

- [Devralma](../cpp/inheritance-cpp.md)

- [Statik Üyeler](../cpp/static-members-cpp.md)

- [Kullanıcı Tanımlı Tür Dönüşümleri](../cpp/user-defined-type-conversions-cpp.md)

- [Değişebilir veri üyeleri (kesilebilir tanımlayıcı)](../cpp/mutable-data-members-cpp.md)

- [İç İçe Geçmiş Sınıf Bildirimleri](../cpp/nested-class-declarations.md)

- [Anonim Sınıf Türleri](../cpp/anonymous-class-types.md)

- [Üye İşaretçileri](../cpp/pointers-to-members.md)

- [this İşaretçisi](../cpp/this-pointer.md)

- [C++ Bit Alanları](../cpp/cpp-bit-fields.md)

Üç sınıf türü yapı, sınıf ve birleşimdir. [Struct](../cpp/struct-cpp.md), [Class](../cpp/class-cpp.md)ve [Union](../cpp/unions.md) anahtar kelimeleri kullanılarak bildirilenler. Aşağıdaki tabloda, üç sınıf türü arasındaki farklılıklar gösterilmektedir.

Birleşimler hakkında daha fazla bilgi için bkz. [birleşimler](../cpp/unions.md). /CLI ve C++ C++/CX içindeki sınıflar ve yapılar hakkında daha fazla bilgi için bkz. [sınıflar ve yapılar](../extensions/classes-and-structs-cpp-component-extensions.md).

### <a name="access-control-and-constraints-of-structures-classes-and-unions"></a>Yapıların, sınıfların ve birleşimlerin Access Control ve kısıtlamaları

|Yapılar|Sınıflar|Birleşimler|
|----------------|-------------|------------|
|sınıf anahtarı **struct**|sınıf anahtarı **sınıf**|sınıf anahtarı **Union**|
|Varsayılan erişim geneldir|Varsayılan erişim özeldir|Varsayılan erişim geneldir|
|Kullanım kısıtlaması yok|Kullanım kısıtlaması yok|Tek seferde yalnızca bir üye kullanın|

## <a name="see-also"></a>Ayrıca bkz.

[C++ Dil Başvurusu](../cpp/cpp-language-reference.md)
