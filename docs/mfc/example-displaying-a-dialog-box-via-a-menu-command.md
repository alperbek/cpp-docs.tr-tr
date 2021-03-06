---
title: 'Örnek: Bir İletişim Kutusunu Menü Komutu ile Görüntüleme'
ms.date: 09/07/2019
helpviewer_keywords:
- MFC dialog boxes [MFC], examples
- MFC dialog boxes [MFC], displaying
- modeless dialog boxes [MFC], displaying
- dialog boxes [MFC], MFC
- modal dialog boxes [MFC], displaying
- examples [MFC], dialog boxes
- menu items [MFC], examples
ms.assetid: e8692549-acd7-478f-9c5e-ba310ce8cccd
ms.openlocfilehash: 281fa77f4954691002268d1e597146a615264695
ms.sourcegitcommit: c21b05042debc97d14875e019ee9d698691ffc0b
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/09/2020
ms.locfileid: "84616032"
---
# <a name="example-displaying-a-dialog-box-via-a-menu-command"></a>Örnek: Bir İletişim Kutusunu Menü Komutu ile Görüntüleme

Bu konu aşağıdaki yordamları içerir:

- Bir menü komutu aracılığıyla kalıcı iletişim kutusu görüntüleyin.

- Bir menü komutu aracılığıyla kalıcı olmayan bir iletişim kutusu görüntüleyin.

Her iki örnek yordam de MFC uygulamalarına yöneliktir ve [MFC Uygulama Sihirbazı](reference/mfc-application-wizard.md)ile oluşturduğunuz bir uygulamada çalışır.

Yordamlar aşağıdaki adları ve değerleri kullanır:

|Öğe|Ad veya değer|
|----------|-------------------|
|Uygulama|DisplayDialog|
|Menü komutu|Görünüm menüsündeki test komutu; Komut KIMLIĞI = ID_VIEW_TEST|
|İletişim kutusu|Test iletişim kutusu; Class = CTestDialog; Üstbilgi dosyası = TestDialog. h; Değişken = TestDlg, ptestdlg|
|Komut işleyicisi|OnViewTest|

### <a name="to-display-a-modal-dialog-box"></a>Kalıcı iletişim kutusunu göstermek için

1. Menü komutunu oluşturun; bkz. [menü ve menü öğeleri oluşturma](../windows/creating-a-menu.md).

1. İletişim kutusunu oluşturun; bkz. [Iletişim kutusu düzenleyiciyi başlatma](../windows/creating-a-new-dialog-box.md).

1. İletişim kutusu için bir sınıf ekleyin. Daha fazla bilgi için bkz. [sınıf ekleme](../ide/adding-a-class-visual-cpp.md) .

1. **Sınıf görünümü**, belge sınıfını (CDisplayDialogDoc) seçin. **Özellikler** penceresinde **Olaylar** düğmesine tıklayın. Menü komutunun KIMLIĞINE (ID_VIEW_TEST) çift tıklayın. Ardından aşağı oka tıklayıp ** \<Add> OnViewTest**' i seçin.

   Bir MDI uygulamasının anaadına menü komutu eklediyseniz bunun yerine uygulama sınıfını (CDisplayDialogApp) seçin.

1. Var olan Include deyimlerden sonra CDisplayDialogDoc. cpp (veya CDisplayDialogApp. cpp) öğesine aşağıdaki Include deyimini ekleyin:

   ```cpp
   #include "TestDialog.h"
   ```

1. `OnViewTest`İşlevi uygulamak için aşağıdaki kodu ekleyin:

   ```cpp
   CTestDialog testdlg;
   testdlg.DoModal();
   ```

### <a name="to-display-a-modeless-dialog-box"></a>Kalıcı olmayan iletişim kutusu görüntüleme

1. 4. adımda görünüm sınıfını (CDisplayDialogView) seçin dışında, kalıcı bir iletişim kutusu görüntülemek için ilk dört adımı uygulayın.

1. DisplayDialogView. h öğesini Düzenle:

   - İlk Sınıf bildiriminden önceki iletişim kutusu sınıfını bildirin:

   ```cpp
   class CTestDialog;
   ```

   - Öznitelikler genel bölümünden sonra iletişim kutusuna bir işaretçi bildirin:

   ```cpp
   CTestDialog* m_pTestDlg;
   ```

1. DisplayDialogView. cpp öğesini Düzenle:

   - Mevcut Include deyimlerinin ardından aşağıdaki Include deyimini ekleyin:

   ```cpp
   #include "TestDialog.h"
   ```

   - Oluşturucuya aşağıdaki kodu ekleyin:

   ```cpp
   m_pTestDlg = NULL;
   ```

   - Yok ediciye aşağıdaki kodu ekleyin:

   ```cpp
   delete m_pTestDlg;
   ```

   - `OnViewTest`İşlevi uygulamak için aşağıdaki kodu ekleyin:

   ```cpp
   if (NULL == m_pTestDlg)
   {
      m_pTestDlg = new CTestDialog(this);
      m_pTestDlg->Create(CTestDialog::IDD, this);
   }
   m_pTestDlg->ShowWindow(SW_SHOW);
   ```

## <a name="see-also"></a>Ayrıca bkz.

[İletişim Kutuları](dialog-boxes.md)<br/>
[Kalıcı ve Kalıcı Olmayan İletişim Kutuları](modal-and-modeless-dialog-boxes.md)
