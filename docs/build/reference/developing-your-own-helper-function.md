---
title: Kendi Yardımcı İşlevinizi Geliştirme
ms.date: 11/04/2016
helpviewer_keywords:
- helper functions
ms.assetid: a845429d-68b1-4e14-aa88-f3f5343bd490
ms.openlocfilehash: 73b4a8180345dd6f7dc26f4243f6e63eda80e4af
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62293803"
---
# <a name="developing-your-own-helper-function"></a>Kendi Yardımcı İşlevinizi Geliştirme

DLL içeri aktarmaları ve adlarına göre belirli işleme yapmak için yordamının kendi sürüm sağlamak isteyebilirsiniz. Bunu yapmanın iki yöntemi vardır: büyük olasılıkla sağlanan kodu, göre kendi kodlama veya yalnızca daha önce ayrıntılı bildirim kancaları kullanarak sağlanan sürüm takma.

## <a name="code-your-own"></a>Kendi kod

Temelde girilen kod bir kılavuz olarak yeni bir tane için kullanabileceğiniz bu yana oldukça basittir. Elbette, çağırma kurallarına uyması gerekir ve bağlayıcı tarafından oluşturulan dönüştürücülerine döndürürse, doğru işlev işaretçisi döndürmelidir. Bir kez kodunuzda tarayıcınızdaki alma çağrısı dışında veya çağrı karşılamak için istediğiniz yapabilirsiniz.

## <a name="use-the-start-processing-notification-hook"></a>Bildirim kanca işleme Başlat

Büyük olasılıkla yalnızca yeni bir bildirim dliStartProcessing üzerinde varsayılan yardımcı olarak aynı değerleri alır bildirim kullanıcı tarafından sağlanan bir kanca işlevini işaretçiye sağlamak kolay olacaktır. Bu noktada, başarılı bir geri döndürme varsayılan Yardımcısı için diğer tüm varsayılan yardımcı işleme atlama gibi kanca işlevini temelde yeni yardımcı işlevini dönüşebilir.

## <a name="see-also"></a>Ayrıca bkz.

[Gecikmeli Yüklenen DLL'ler için Bağlayıcı Desteği](linker-support-for-delay-loaded-dlls.md)
