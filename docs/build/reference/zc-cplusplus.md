---
title: '/ ZC: __cplusplus (güncelleştirilmiş __cplusplus makrosu etkinleştir)'
ms.date: 05/16/2019
f1_keywords:
- /Zc:__cplusplus
helpviewer_keywords:
- -Zc:__cplusplus compiler option (C++)
- __cplusplus macro (C++)
ms.openlocfilehash: 43392438eabc7cc7f6decb1349d112a0ce5bd0f5
ms.sourcegitcommit: a10c9390413978d36b8096b684d5ed4cf1553bc8
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/17/2019
ms.locfileid: "65837546"
---
# <a name="zccplusplus-enable-updated-cplusplus-macro"></a>/ ZC: __cplusplus (güncelleştirilmiş __cplusplus makrosu etkinleştir)

**/ZC: __cplusplus** derleyici seçeneğini etkinleştirir  **\_ \_cplusplus** için güncelleştirilmiş bir değeri bildirmek için önişlemci makrosu son C++ dil standartları destekler. Varsayılan olarak, Visual Studio her zaman değeri "199711 L" için döndürür  **\_ \_cplusplus** önişlemci makrosu.

## <a name="syntax"></a>Sözdizimi

> **/Zc:__cplusplus**[**-**]

## <a name="remarks"></a>Açıklamalar

 **\_ \_Cplusplus** önişlemci makrosu belirli bir C++ standart sürümü için rapor desteklemek için yaygın olarak kullanılır. Varolan kodu çok sayıda göründüğünden "199711 L" eşleşen bu makronun değeri bağımlı, açıkça kullanarak katılımı sürece derleyici makrosunun değeri değişmez **/ZC: __cplusplus** derleyici seçeneği. **/ZC: __cplusplus** seçeneği, Visual Studio 2017 sürüm 15.7'den itibaren kullanılabilmektedir ve varsayılan olarak kapalıdır. Visual Studio ve varsayılan olarak, önceki sürümlerde veya **/Zc:__cplusplus-** belirtilirse, Visual Studio döndürür "199711 L" değeri için  **\_ \_cplusplus** Önişlemci makrosu. [/ Permissive-](permissive-standards-conformance.md) seçeneği sağlamaz **/ZC: __cplusplus**.

Zaman **/ZC: __cplusplus** seçeneği etkin olduğunda, bildirilen değer  **\_ \_cplusplus** makrosu bağlıdır [/Std](std-specify-language-standard-version.md) sürüm anahtarı ayar. Bu tabloda, makro için olası değerler gösterilir:

|/ ZC: __cplusplus anahtarı|/Std:c++ anahtarı|__cplusplus value|
|-|-|-|
Zc:__cplusplus|/ Std: c ++ 14 (varsayılan)|201402 M
Zc:__cplusplus|/std:c++17|201703 M
Zc:__cplusplus|/std:c++latest|201704 M
Zc:__cplusplus-(devre dışı)|Herhangi bir değer|199711 M
Belirtilmemiş.|Herhangi bir değer|199711 M

Derleyici C ++ 98, C ++ 03 veya C ++ 11 standartlar anahtarları desteklemez.

Daha ayrıntılı için algılama derleyici araç takımı yapılan değişikliklerin [_MSC_VER](../../preprocessor/predefined-macros.md) önceden tanımlanmış makro. Her araç takımı güncelleştirme Visual Studio 2017 ve sonraki sürümler için yerleşik bu makronun değeri artırılır. [_MSVC_LANG](../../preprocessor/predefined-macros.md) önceden tanımlanmış makro raporları standart sürümü olup olmadığını **/ZC: __cplusplus** seçeneği etkin veya devre dışı. Zaman **/ZC: __cplusplus** etkinleştirildiğinde `__cplusplus == _MSVC_LANG`.

### <a name="to-set-this-compiler-option-in-visual-studio"></a>Bu derleyici seçeneğini Visual Studio'da ayarlamak için

1. Projenin açın **özellik sayfaları** iletişim kutusu. Ayrıntılar için bkz [Visual Studio'da ayarlayın C++ derleyicisi ve derleme özellikleri](../working-with-project-properties.md).

1. Seçin **yapılandırma özellikleri** > **C/C++** > **komut satırı** özellik sayfası.

1. Ekleme **/ZC: __cplusplus** veya **/Zc:__cplusplus-** için **ek seçenekler:** bölmesi.

## <a name="see-also"></a>Ayrıca bkz.

- [/Zc (Uyumluluk)](zc-conformance.md)
- [/ Std (belirtin dil standart sürümünü)](std-specify-language-standard-version.md)
- [Önceden tanımlanmış makrolar](../../preprocessor/predefined-macros.md)
