---
title: Tarih ve Saat Seçici Denetiminde Özel Biçim Dizeleri Kullanma
ms.date: 11/04/2016
helpviewer_keywords:
- CDateTimeCtrl class [MFC], display styles
- DateTimePicker control [MFC], display styles
- DateTimePicker control [MFC]
ms.assetid: 7d577f03-6ca0-4597-9093-50b78f304719
ms.openlocfilehash: 8da5ecaf473d6d3c35ddc1b95ac856ce8c12f163
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62411636"
---
# <a name="using-custom-format-strings-in-a-date-and-time-picker-control"></a>Tarih ve Saat Seçici Denetiminde Özel Biçim Dizeleri Kullanma

Varsayılan olarak, geçerli tarih ve saati görüntülemek için üç türleri (benzersiz stiline karşılık gelen her biçim) biçimlendirmek tarih ve Saat Seçici denetimleri sağlayın:

- **DTS_LONGDATEFORMAT** uzun biçimde, "Çarşamba, 3 Şubat 2000" gibi bir çıktı üretir tarihi görüntüler.

- **DTS_SHORTDATEFORMAT** "1/3/00" gibi bir çıktı üretir kısa biçimindeki tarihi görüntüler.

- **DTS_TIMEFORMAT** "-17:31:42" gibi bir çıktı üretir uzun biçimde süreyi görüntüler.

Ancak, bir özel biçim dizesi kullanarak tarih ve saati görünümünü özelleştirebilirsiniz. Bu özel bir dize, var olan biçim karakterleri, nonformat karakter veya her ikisinin bir birleşimi yapılır. Özel bir dize oluşturulduktan sonra bir çağrı yapmak [CDateTimeCtrl::SetFormat](../mfc/reference/cdatetimectrl-class.md#setformat) geçirme, özel bir dize. Tarih ve Saat Seçici denetimini daha sonra özel biçim dizesi kullanarak geçerli değeri görüntüler.

Aşağıdaki kod örneği (burada *m_dtPicker* olduğu `CDateTimeCtrl` nesnesi) bir olası çözümü göstermektedir:

[!code-cpp[NVC_MFCControlLadenDialog#7](../mfc/codesnippet/cpp/using-custom-format-strings-in-a-date-and-time-picker-control_1.cpp)]

Özel biçim dizelerine ek olarak, tarih ve Saat Seçici desteği de denetimleri [geri çağrı alanlarını](../mfc/using-callback-fields-in-a-date-and-time-picker-control.md).

## <a name="see-also"></a>Ayrıca bkz.

[CDateTimeCtrl Kullanma](../mfc/using-cdatetimectrl.md)<br/>
[Denetimler](../mfc/controls-mfc.md)
