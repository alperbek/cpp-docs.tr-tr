---
title: Derleme Görevleri Dosyası Önişleme Yönergeleri
ms.date: 08/11/2019
f1_keywords:
- '!UNDEF'
- '!INCLUDE'
- '!IFNDEF'
- '!MESSAGE'
helpviewer_keywords:
- ERROR directive
- '!MESSAGE directive'
- IF directive
- '!UNDEF directive'
- IFDEF directive
- '!ELSEIF directive'
- '!IFDEF directive'
- '!IF directive'
- UNDEF directive
- '!CMDSWITCHES directive'
- ENDIF directive
- directives, makefile preprocessing
- INCLUDE directive
- IFNDEF directive
- preprocessing directives, makefiles
- '!IFNDEF directive'
- ELSEIFNDEF directive
- NMAKE program, expressions
- ELSEIF directive
- '!ERROR directive'
- '!ENDIF directive'
- MESSAGE directive
- '!INCLUDE directive'
- '!ELSEIFNDEF directive'
- CMDSWITCHES directive
- '!ELSEIFDEF directive'
- '!ELSE directive'
- NMAKE program, preprocessor directives
- makefiles, preprocessing directives
- ELSE directive
- ELSEIFDEF directive
ms.assetid: bcedeccb-d981-469d-b9e8-ab5d097fd8c2
ms.openlocfilehash: 1dd30c8e338343626d8a8cc3157d118e44f0ea18
ms.sourcegitcommit: 857fa6b530224fa6c18675138043aba9aa0619fb
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/24/2020
ms.locfileid: "80170494"
---
# <a name="makefile-preprocessing-directives"></a>Derleme Görevleri Dosyası Önişleme Yönergeleri

Ön işleme yönergeleri büyük/küçük harfe duyarlı değildir. İlk ünlem işareti (!) satırın başlangıcında görünmelidir. Girintileme için, ünlem işaretiyle sıfır veya daha fazla boşluk veya sekme görünebilir.

- {`+` &#124; `-`}*seçeneği* `!CMDSWITCHES`...

   Üzerinde listelenen her *seçeneği* kapatır veya kapatır. Boşluk veya sekmeler `+` veya `-` işlecinden önce gelmelidir; işleç ve [seçenek harfleri](running-nmake.md#nmake-options)arasında hiçbiri görünmeyebilir. Harfler büyük/küçük harfe duyarlı değildir ve eğik çizgi olmadan belirtilir (`/`). Bazı seçenekleri açıp diğerlerini devre dışı bırakmak için `!CMDSWITCHES`ayrı belirtimlerini kullanın.

   Derleme görevleri dosyası içinde yalnızca/D,/I,/N ve/S kullanılabilir. Tools. ini dosyasında/F,/HELP,/NOLOGO,/X ve/? dışında tüm seçeneklere izin verilir. Açıklama bloğunda belirtilen değişiklikler bir sonraki açıklama bloğuna kadar etkili olmaz. Bu yönerge **makeflags**'i güncelleştirir; **makeflags** belirtilmişse, değişiklikler özyineleme sırasında devralınır.

- `!ERROR` *metin*

   /K,/ı, `.IGNORE`, `!CMDSWITCHES`veya Dash (`-`) komut değiştiricisi kullanılırsa bile hata U1050 ve ardından durursa NMAKE içinde *metin* görüntüler. *Metinden* önce boşluklar veya sekmeler yok sayılır.

- `!MESSAGE` *metin*

   Standart çıktıya *metin* görüntüler. *Metinden* önce boşluklar veya sekmeler yok sayılır.

- `!INCLUDE` [`<`] *filename* [`>`]

   *Dosya adını* derleme görevleri dosyası olarak okur, ardından geçerli derleme görevleri dosyası ile devam eder. NMAKE, belirtilen veya geçerli dizinde önce *dosya adını* arar, ardından herhangi bir üst makefiles dizininde özyinelemeli olarak, *dosya adı* açılı ayraçlar (`< >`) tarafından **, dahil etme makrosu tarafından** BELIRTILEN dizinlerde, bu, başlangıçta dahil olan ortam değişkenine ayarlanır. `.SUFFIXES` ayarları, `.PRECIOUS`ve çıkarım kurallarının özyinelemeli makefiles 'a iletilmesi yararlı olur.

- `!IF` *constant_expression*

   *Constant_expression* sıfır dışında bir değere değerlendirilirse, `!IF` ve sonraki `!ELSE` veya `!ENDIF` arasındaki deyimleri işler.

- `!IFDEF` *makroadı*

   `!IFDEF` ve bir sonraki `!ELSE` veya *makroadı* tanımlanmışsa `!ENDIF` arasında deyimlerini işler. Null bir makronun tanımlanması kabul edilir.

- `!IFNDEF` *makroadı*

   `!IFNDEF` ve sonraki `!ELSE` ya da *makroadı* tanımlanmamışsa, `!ENDIF` deyimlerini işler.

- `!ELSE` [`IF` *constant_expression* &#124; `IFDEF` *makroadı* &#124; `IFNDEF` *makroadı*]

   Önceki `!IF`, `!IFDEF`veya `!IFNDEF` deyimi sıfıra değerlendirilirse, `!ELSE` ve sonraki `!ENDIF` arasındaki deyimleri işler. İsteğe bağlı anahtar sözcükler, ön işleme için daha fazla denetim sağlar.

- `!ELSEIF`

   İçin eş anlamlı `!ELSE IF`.

- `!ELSEIFDEF`

   İçin eş anlamlı `!ELSE IFDEF`.

- `!ELSEIFNDEF`

   İçin eş anlamlı `!ELSE IFNDEF`.

- `!ENDIF`

   `!IF`, `!IFDEF`veya `!IFNDEF` bloğunun sonunu işaretler. Aynı satırdaki `!ENDIF` sonra herhangi bir metin yok sayılır.

- `!UNDEF` *makroadı*

   *Makroadı*öğesini kaldır.

## <a name="see-also"></a>Ayrıca bkz.

- [Derleme Görevleri Dosyası Ön İşlemi](makefile-preprocessing.md)
