---
title: Kullanıcı Arabirimi Nesneleri ile İlişkili İleti Türleri
ms.date: 11/04/2016
f1_keywords:
- vc.codewiz.uiobject.msgs
helpviewer_keywords:
- message types and user interface objects [MFC]
ms.assetid: 681ee1a7-f6e6-4ea0-9fc6-1fb53a35516e
ms.openlocfilehash: 37638d12c65986d40e7df9f0fbfdef4b8207e418
ms.sourcegitcommit: 65ed563a8a1d4d90f872a2a6edcb086f84ec9f77
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/06/2019
ms.locfileid: "66741570"
---
# <a name="message-types-associated-with-user-interface-objects"></a>Kullanıcı Arabirimi Nesneleri ile İlişkili İleti Türleri

Aşağıdaki tabloda, birlikte çalıştığınız nesne türlerini ve bunlarla ilişkili ileti türleri gösterilmektedir.

### <a name="user-interface-objects-and-associated-messages"></a>Kullanıcı arabirimi nesneleri ve ilişkili iletileri

|Nesne Kimliği|İletiler|
|---------------|--------------|
|Sınıf adı, kapsayan pencereye temsil eden|Windows iletileri uygun şekilde bir [CWnd](../../mfc/reference/cwnd-class.md)-türetilmiş sınıf: bir iletişim kutusu, penceresi, alt penceresi, MDI alt penceresi veya en üstteki çerçeve penceresi.|
|Menü veya Hızlandırıcı tanımlayıcısı|-KOMUT iletisi (program işlevi çalıştırılır).<br />-UPDATE_COMMAND_UI iletisi (dinamik olarak güncelleştirir. menü öğesi).|
|Denetim Kimliği|Seçili denetim türü için denetimi bildirim iletileri.|

## <a name="see-also"></a>Ayrıca bkz.

[İletileri İşlevlere Eşleme](../../mfc/reference/mapping-messages-to-functions.md)<br/>
[Kod Sihirbazlarıyla İşlevsellik Ekleme](../../ide/adding-functionality-with-code-wizards-cpp.md)<br/>
[Sınıf ekleme](../../ide/adding-a-class-visual-cpp.md)<br/>
[Üye işlevi ekleme](../../ide/adding-a-member-function-visual-cpp.md)<br/>
[Üye değişkeni ekleme](../../ide/adding-a-member-variable-visual-cpp.md)<br/>
[Bir sanal işlevi geçersiz kılma](../../ide/overriding-a-virtual-function-visual-cpp.md)<br/>
[MFC ileti işleyicisi](../../mfc/reference/adding-an-mfc-message-handler.md)<br/>
[Sınıf yapısında gezinme](../../ide/navigate-code-cpp.md)
