---
title: ActiveX Denetimleri Oluşturmak için İşlem Dizisi
ms.date: 11/04/2016
helpviewer_keywords:
- MFC ActiveX controls [MFC], creating
- ActiveX controls [MFC], creating
- sequence [MFC], for creating ActiveX controls
- OLE controls [MFC], MFC
- sequence [MFC]
ms.assetid: 7d868c53-a0af-4ef6-a89c-e1c03c583a53
ms.openlocfilehash: 020c044cc0b3b96df102a5ab6625c945f1033f67
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62308439"
---
# <a name="sequence-of-operations-for-creating-activex-controls"></a>ActiveX Denetimleri Oluşturmak için İşlem Dizisi

Aşağıdaki tabloda, rol ve framework'ün rol (önceki adıyla OLE denetimleri da bilinir) ActiveX denetimleri oluşturmak gösterir.

### <a name="creating-activex-controls"></a>ActiveX denetimleri oluşturma

|Görev|Bunu|Framework yok|
|----------|------------|------------------------|
|Bir ActiveX denetim çerçevesi oluşturun.|Denetim oluşturmak için MFC ActiveX Denetim Sihirbazı'nı çalıştırın. Seçenekleri sayfalarında istediğiniz seçenekleri belirtin. Seçenekler, proje, lisanslama, sınıflara ve hakkında kutusu yöntemi denetimin adını ve türünü içerir.|MFC ActiveX Denetim Sihirbazı'nı temel işlevlerini uygulama, Denetim ve özellik sayfası veya sayfaları için kaynak dosyaları dahil olmak üzere, bir ActiveX denetimi için dosyaları oluşturur; bir kaynak dosyası; bir proje dosyası; ve diğer tüm uyarlanmış, belirtime uygun.|
|Kendi kod satırını eklemeden ne Denetim ve ActiveX Denetim Sihirbazı'nı teklif bakın.|ActiveX denetimi oluşturun ve Internet Explorer ile test veya [TSTCON örnek](../overview/visual-cpp-samples.md).|Çalışan denetimi yeniden boyutlandırılabilir ve taşınabilir özelliğine sahiptir. Ayrıca bir **hakkında kutusu** çağrılabilir (seçilmişse) yöntemi.|
|Denetimin yöntemleri ve özellikleri uygulayın.|Denetimin özel yöntemleri ve özellikleri denetimin verilere açık bir arabirim sağlayacağı şekilde üye işlevleri ekleyerek uygulayın. Veri yapıları basılı tutun ve olay işleyicileri, karar verirken olaylarını başlatmak için kullanmak için üye değişkenleri ekleyin.|Framework zaten bir harita denetimin olayları, özellikleri ve yöntemleri nasıl özellikleri ve yöntemleri uygulandığı üzerinde odaklanabilirsiniz bırakarak desteklemek için tanımlanır. Varsayılan özellik sayfası görüntülenebilir ve varsayılan hakkında kutusu yöntemi sağlanır.|
|Denetimin özellik sayfa veya sayfaları oluşturun.|Görsel olarak denetimin özellik sayfası arabirimini düzenlemek için Visual C++ kaynak düzenleyicileri kullanın:<br /><br />-Ek özellik sayfaları oluşturun.<br />-Oluşturma ve bit eşlemler, simgeler ve İmleçler düzenleyin.<br /><br /> Özellik sayfaları iletişim kutusu Düzenleyicisi'nde de test edebilirsiniz.|MFC Uygulama Sihirbazı tarafından oluşturulan varsayılan kaynak dosyası, ihtiyacınız olan kaynakları çoğunu sağlar. Visual C++ mevcut kaynakları düzenlemek ve yeni kaynakları kolayca ve görsel olarak eklemenize olanak tanır.|
|Denetim olaylarını, yöntemlerini ve özelliklerini test edin.|Denetimi yeniden oluşturun ve test İşleyicileriniz düzgün çalışması için Test kapsayıcısını kullanın.|Denetimin yöntemlerini çağırabilir ve Test kapsayıcı veya özellik sayfasında arabirimi aracılığıyla özelliklerini düzenleme. Ayrıca, Test kapsayıcısı denetiminden harekete geçirilen olayları izlemek ve denetimin kapsayıcı tarafından alınan bildirimler için kullanın.|

## <a name="see-also"></a>Ayrıca bkz.

[Framework'te Derleme](../mfc/building-on-the-framework.md)<br/>
[MFC Uygulamaları Oluşturmak için İşlem Dizisi](../mfc/sequence-of-operations-for-building-mfc-applications.md)<br/>
[OLE Uygulamaları Oluşturmak için İşlem Dizisi](../mfc/sequence-of-operations-for-creating-ole-applications.md)<br/>
[Veritabanı Uygulamaları Oluşturmak için İşlem Dizisi](../mfc/sequence-of-operations-for-creating-database-applications.md)
