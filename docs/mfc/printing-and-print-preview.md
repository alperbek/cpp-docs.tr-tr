---
title: Yazdırma ve Baskı Önizleme
ms.date: 11/04/2016
helpviewer_keywords:
- printing [MFC]
- previewing printing
- printing [MFC]
- print preview
- printing [MFC], print preview
ms.assetid: d15059cd-32de-4450-95f7-e73aece238f6
ms.openlocfilehash: 26ced8172a36d34883d6b65997bb3a81fdc3c319
ms.sourcegitcommit: c21b05042debc97d14875e019ee9d698691ffc0b
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/09/2020
ms.locfileid: "84625272"
---
# <a name="printing-and-print-preview"></a>Yazdırma ve Baskı Önizleme

MFC, [CView](reference/cview-class.md)sınıfı aracılığıyla programınızın belgeleri için yazdırma ve baskı önizlemeyi destekler. Temel yazdırma ve baskı önizleme için, Görünüm sınıfınızın [OnDraw](reference/cview-class.md#ondraw) üye işlevini, yine de yapmanız gereken geçersiz kılmanız yeterlidir. Bu işlev, ekranda görünüme, gerçek bir yazıcı için bir yazıcı cihazına veya ekran üzerinde yazıcınızı taklit eden bir cihaz bağlamına çizebilir.

Ayrıca, çok sayfalı belge yazdırmayı ve önizlemesini yönetmek, yazdırılmış belgelerinizi Sayfalandırmaya ve bunlara üstbilgiler ve altbilgiler eklemek için de kod ekleyebilirsiniz.

Bu makale ailesi, yazdırmanın Microsoft Foundation Class Kitaplığı (MFC) nasıl uygulandığını ve çerçevede yerleşik olarak bulunan yazdırma mimarisinden nasıl yararlanılacağını açıklamaktadır. Makaleler Ayrıca, MFC 'nin baskı önizleme işlevselliğinin kolay uygulanmasını nasıl desteklediğini ve bu işlevselliği nasıl kullanabileceğinizi ve değiştirebileceğini açıklar.

## <a name="what-do-you-want-to-know-more-about"></a>Hakkında daha fazla bilgi edinmek istiyorsunuz

- [Yazdırma](printing.md)

- [Baskı önizleme mimarisi](print-preview-architecture.md)

- [Örnek](../overview/visual-cpp-samples.md)

## <a name="see-also"></a>Ayrıca bkz.

[Kullanıcı arabirimi öğeleri](user-interface-elements-mfc.md)
