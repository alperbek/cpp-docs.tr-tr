---
title: Genel MBCS Programlama Önerileri
ms.date: 11/04/2016
helpviewer_keywords:
- MBCS [C++], dialog box fonts
- MS Shell Dlg
- MBCS [C++], programming
- dialog boxes [C++], fonts
ms.assetid: 7b541235-f3e5-4af0-b2c2-a0112cd5fbfb
ms.openlocfilehash: 887387220105614eb3257f008ec601a6fc0adc18
ms.sourcegitcommit: fcb48824f9ca24b1f8bd37d647a4d592de1cc925
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/15/2019
ms.locfileid: "69491180"
---
# <a name="general-mbcs-programming-advice"></a>Genel MBCS Programlama Önerileri

Aşağıdaki ipuçlarını kullanın:

- Esneklik için, mümkün olduğunda `_tcschr` ve `_tcscpy` gibi çalışma zamanı makrolarını kullanın. Daha fazla bilgi için, bkz. [Tchar. h 'de Genel metin eşlemeleri](../text/generic-text-mappings-in-tchar-h.md).

- Geçerli kod sayfasıyla ilgili bilgi almak `_getmbcp` için C çalışma zamanı işlevini kullanın.

- Dize kaynaklarını yeniden kullanmayın. Hedef dile bağlı olarak, belirli bir dize çevrildiğinde farklı anlamına sahip olabilir. Örneğin, uygulamanın ana menüsündeki "dosya" bir iletişim kutusunda "dosya" dizesinden farklı şekilde çevrilebilir. Aynı ada sahip birden fazla dize kullanmanız gerekiyorsa, her biri için farklı dize kimlikleri kullanın.

- Uygulamanızın MBCS özellikli bir işletim sisteminde çalışıp çalışmadığını öğrenmek isteyebilirsiniz. Bunu yapmak için program başlangıcında bir bayrak ayarlayın; API çağrılarına güvenmeyin.

- İletişim kutularını tasarlarken, MBCS çevirisi için statik metin denetimlerinin sonunda yaklaşık% 30 ek alana izin verin.

- Bazı yazı tipleri tüm sistemlerde kullanılamadığından uygulamanız için yazı tipi seçerken dikkatli olun.

- İletişim kutuları için yazı tipi seçerken MS Sans Serif veya Helvetica yerine [MS Shell Dlg](/windows/win32/Intl/using-ms-shell-dlg-and-ms-shell-dlg-2) kullanın. MS Shell Dlg, iletişim kutusu oluşturmadan önce sistem tarafından doğru yazı tipiyle değiştirilmiştir. MS Shell Dlg kullanımı, işletim sistemindeki bu yazı tipiyle başa çıkmak için tüm değişikliklerin otomatik olarak kullanılabilmesini sağlar. (MFC, MS Shell Dlg 'i Windows 95, Windows 98 ve Windows NT 4 ' te DEFAULT_GUI_FONT veya sistem yazı tipiyle değiştirir çünkü bu sistemler MS Shell Dlg 'i doğru şekilde işlemez.)

- Uygulamanızı tasarlarken hangi dizelerin yerelleştirilebileceğini belirleyin. Şüpheniz varsa, belirli bir dizenin yerelleştirileceğini varsayın. Bu nedenle, bu tür olmayan yerelleştirilebilecek dizeleri karışmayın.

## <a name="see-also"></a>Ayrıca bkz.

[MBCS Programlama İpuçları](../text/mbcs-programming-tips.md)<br/>
[İşaretçileri Artırma ve Azaltma](../text/incrementing-and-decrementing-pointers.md)
