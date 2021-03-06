---
title: Formdaki Verileri Görüntüleme ve Düzenleme
ms.date: 11/04/2016
helpviewer_keywords:
- forms [C++], displaying data
- displaying data [C++], forms
- ODBC [C++], forms
- record views [C++], displaying data
- data [MFC]
- data [MFC], displaying in a form
ms.assetid: c56185c4-12cb-40b1-b499-02b29ea83e3a
ms.openlocfilehash: 6b663fabd0c87d9a2773e6f5a2796bcc8f57ce29
ms.sourcegitcommit: 857fa6b530224fa6c18675138043aba9aa0619fb
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/24/2020
ms.locfileid: "80213258"
---
# <a name="displaying-and-manipulating-data-in-a-form"></a>Formdaki Verileri Görüntüleme ve Düzenleme

Birçok veri erişimi uygulaması verileri seçer ve formdaki alanlarda görüntüler. [CRecordView](../../mfc/reference/crecordview-class.md) veritabanı sınıfı, size doğrudan bir kayıt kümesi nesnesine bağlı bir [CFormView](../../mfc/reference/cformview-class.md) nesnesi sağlar. Kayıt görünümü, geçerli kaydın alanlarının değerlerini kayıt kümesinden form denetimlerine taşımak ve güncelleştirilmiş bilgileri kayıt kümesine geri taşımak için [iletişim kutusu veri değişimi 'ni (DDX)](../../mfc/dialog-data-exchange-and-validation.md) kullanır. Kayıt kümesi sırasıyla, veri kaynağındaki bir tablodaki verileri alan veri üyeleri ve karşılık gelen sütunlar arasında taşımak için kayıt alanı değişimi (RFX) kullanır.

Görünüm sınıfını ve ilişkili kayıt kümesi sınıfını birlikte oluşturmak için MFC Uygulama Sihirbazı 'Nı veya **sınıf ekleme** ( [MFC ODBC Tüketicisi Ekleme](../../mfc/reference/adding-an-mfc-odbc-consumer.md)bölümünde açıklandığı gibi).

Belgeyi kapattığınızda kayıt görünümü ve kayıt kümesi yok edilir. Kayıt görünümleri hakkında daha fazla bilgi için bkz. [Kayıt görünümleri](../../data/record-views-mfc-data-access.md). RFX hakkında daha fazla bilgi için bkz. [kayıt alanı değişimi (RFX)](../../data/odbc/record-field-exchange-rfx.md).

## <a name="see-also"></a>Ayrıca bkz.

[ODBC ve MFC](../../data/odbc/odbc-and-mfc.md)
