---
title: İşaretçi Türlerine ve Türlerinden Dönüşümler
ms.date: 11/04/2016
helpviewer_keywords:
- pointers, converting
- conversions, pointer
- type casts, involving pointers
- void pointers
ms.assetid: 3facc56f-06d3-4570-b1a2-7d4927b83086
ms.openlocfilehash: 2d907dbcf4f826d364fb68ce65f7d44c6cfe97cd
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62312423"
---
# <a name="conversions-to-and-from-pointer-types"></a>İşaretçi Türlerine ve Türlerinden Dönüşümler

Bir değer türünün işaretçisi, farklı türden bir işaretçiye dönüştürülebilir. Ancak sonuç, depolanan farklı türlerin hizalama gereksinimleri ve boyutları nedeniyle tanımlanmamış olabilir. Bir nesnenin işaretçisi, türü daha az katı veya eşit derecede katı olan depolama hizalaması gerektiren bir nesnenin işaretçisine dönüştürülebilir ve değiştirilmeden geri alınabilir.

`void` işaretçisi, herhangi bir türden işaretçiye veya işaretçiden kısıtlama veya bilgi kaybı olmadan dönüştürülebilir. Sonuç yeniden orijinal türüne dönüştürülürse, orijinal işaretçi kurtarılır.

Bir işaretçi aynı türden, ancak farklı veya ek niteleyicileri olan başka bir işaretçiye dönüştürülürse, yeni işaretçi yeni niteleyici tarafından uygulanan kısıtlamalar dışında eskisiyle aynı olur.

İşaretçi değeri, integral değerine de dönüştürülebilir. Dönüştürme yolu, aşağıdaki kurallara göre işaretçinin boyutuna ve integral türünün boyutuna bağlıdır:

- İşaretçinin boyutu integral türünün boyutundan büyük veya buna eşitse, işaretçi dönüştürme işleminde işaretsiz bir değer gibi görev alır, ancak bu değer gibi kayan bir değere dönüştürülemez.

- İşaretçi integral türünden küçükse, işaretçi önce integral türüyle aynı boyuttan bir işaretçiye, ardından integral türüne dönüştürülür.

Bunun tersi olarak, aşağıdaki kurallara göre bir integral türü işaretçi türüne dönüştürülebilir:

- İntegral türü işaretçi türüyle aynı boyuttaysa, dönüştürme işlemi integral değerinin bir işaretçi (işaretsiz tamsayı) olarak değerlendirilmesine neden olur.

- İntegral türünün boyutu işaretçi türünün boyutundan farklıysa, integral türü önce, [Işaretli Integral türlerinden](../c-language/conversions-from-signed-integral-types.md) ve [Işaretsiz integral türlerden dönüşümden](../c-language/conversions-from-unsigned-integral-types.md)gelen tablolarda verilen dönüştürme yolları kullanılarak işaretçinin boyutuna dönüştürülür. Daha sonra bir işaretçi değeri olarak kabul edilir.

0 değerine sahip bir tamsayı sabiti ifadesi veya **void** <strong>\*</strong> türüne bir ifade dönüştürme türü tür atama, atamaya göre veya herhangi bir tür işaretçisine karşılaştırmaya göre dönüştürülebilir. Bu, aynı türden başka bir null işaretçisine eşit olan bir null işaretçisi oluşturur, ancak bu null işaretçisi bir işlevin veya nesnenin herhangi bir işaretçisine eşit değildir. 0 sabiti dışındaki tamsayılar işaretçi türüne dönüştürülebilir, ancak sonuç taşınabilir değildir.

## <a name="see-also"></a>Ayrıca bkz.

[Atama Dönüştürmeleri](../c-language/assignment-conversions.md)
