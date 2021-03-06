---
title: Kod Sayfaları
ms.date: 11/04/2016
helpviewer_keywords:
- character sets [C++], code pages
- ANSI [C++], code pages
- system-default code page
- multibyte code pages [C++]
- localization [C++], code pages
- code pages [C++], types of
- locale code pages [C++]
ms.assetid: 4a26fc42-185a-4add-98bf-a7b314ae6186
ms.openlocfilehash: 13b31b7d7750158caf498d92db67fd3e61856c5c
ms.sourcegitcommit: 63784729604aaf526de21f6c6b62813882af930a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/17/2020
ms.locfileid: "79443506"
---
# <a name="code-pages"></a>Kod Sayfaları

*Kod sayfası* , sayılar, noktalama işaretleri ve diğer Glifler içerebilen bir karakter kümesidir. Farklı diller ve yerel ayarlar farklı kod sayfaları kullanabilir. Örneğin, ANSI kod sayfası 1252, Ingilizce ve çoğu Avrupa dilleri için kullanılır; OEM kod sayfası 932, Japonca Kanji için kullanılır.

Bir kod sayfası, tek baytlık değerlere veya çok baytlı değerlere karakter eşleştirmesi olarak bir tabloda gösterilebilir. Birçok kod sayfası, 0x00-0x7F aralığındaki karakterler için ASCII karakter kümesini paylaşır.

Microsoft çalışma zamanı kitaplığı aşağıdaki kod sayfası türlerini kullanır:

- Sistem varsayılan ANSI kod sayfası. Varsayılan olarak, başlangıçta çalışma zamanı sistemi, çok baytlı kod sayfasını işletim sisteminden alınan sistem varsayılan ANSI kod sayfasına otomatik olarak ayarlar. Çağrı:

    ```C
    setlocale ( LC_ALL, "" );
    ```

   Ayrıca yerel ayarı sistem varsayılan ANSI kod sayfasına ayarlar.

- Yerel ayar kodu sayfası. Çalışma zamanı yordamlarının bir dizi davranışı, yerel ayar kodu sayfasını içeren geçerli yerel ayara bağımlıdır. (Daha fazla bilgi için bkz. [yerel ayara bağımlı yordamlar](../c-runtime-library/locale.md).) Varsayılan olarak, Microsoft çalışma zamanı kitaplığındaki tüm yerel ayara bağımlı yordamlar, "C" yerel ayarına karşılık gelen kod sayfasını kullanır. Çalışma zamanında, kullanılan yerel ayar kodu sayfasını bir [setlocale](../c-runtime-library/reference/setlocale-wsetlocale.md)çağrısıyla değiştirebilir veya sorgulayabilirsiniz.

- Çok baytlı kod sayfası. Çalışma zamanı kitaplığındaki çok baytlı karakter yordamlarının çoğunun davranışı geçerli çok baytlı kod sayfası ayarına bağlıdır. Varsayılan olarak, bu yordamlar sistem varsayılan ANSI kod sayfasını kullanır. Çalışma zamanında çok baytlı kod sayfasını, sırasıyla [_getmbcp](../c-runtime-library/reference/getmbcp.md) ve [_setmbcp](../c-runtime-library/reference/setmbcp.md)ile sorgulayabilir ve değiştirebilirsiniz.

- "C" yerel ayarı ANSI tarafından, C programlarının geleneksel olarak yürütüldüğü yerel ayara karşılık gelecek şekilde tanımlanır. "C" yerel ayarı ("C" kod sayfası) için kod sayfası ASCII karakter kümesine karşılık gelir. Örneğin, "C" yerel ayarında, **ılower** yalnızca 0x61-0x7A değerleri için true döndürür. Başka bir yerel ayarda, **IsLower** , bu yerel ayar tarafından tanımlanan diğer değerler için de true döndürebilir.

## <a name="see-also"></a>Ayrıca bkz.

[Uluslararası duruma getirme](../c-runtime-library/internationalization.md)<br/>
[Kategoriye göre Evrensel C çalışma zamanı yordamları](../c-runtime-library/run-time-routines-by-category.md)<br/>
