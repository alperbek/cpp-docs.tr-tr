---
title: OLE'deki İletişim Kutuları
ms.date: 11/04/2016
helpviewer_keywords:
- MFC dialog boxes [MFC], OLE dialog boxes
- OLE dialog boxes
- dialog boxes
- OLE dialog boxes [MFC], about OLE dialog boxes
- dialog boxes [MFC], about dialog boxes
- dialog boxes [MFC], OLE
- Insert object
ms.assetid: 73c41eb8-738a-4d02-9212-d3395bb09a3a
ms.openlocfilehash: b59ba16e6e68df2a539232636e8fe710750e3214
ms.sourcegitcommit: c21b05042debc97d14875e019ee9d698691ffc0b
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/09/2020
ms.locfileid: "84616905"
---
# <a name="dialog-boxes-in-ole"></a>OLE'deki İletişim Kutuları

Bir Kullanıcı OLE özellikli bir uygulama çalıştırdığında, uygulamanın işlemi yürütmek için kullanıcıdan bilgi ihtiyacı olduğu durumlar vardır. MFC OLE sınıfları, gerekli bilgileri toplamak için bir dizi iletişim kutusu sağlar. Bu konu, OLE iletişim kutuları ve bu iletişim kutularını göstermek için gereken sınıflar tarafından işlenen görevleri listeler. OLE iletişim kutuları ve davranışlarını özelleştirmek için kullanılan yapılar hakkında ayrıntılar için bkz. [MFC başvurusu](mfc-desktop-applications.md).

*Nesne Ekle*<br/>
Bu iletişim kutusu, kullanıcının yeni oluşturulan veya varolan nesneleri bileşik belgeye eklemesini sağlar. Ayrıca, kullanıcının öğeyi bir simge olarak görüntülemeyi seçmesini ve simgeyi değiştir komut düğmesini kullanmasını sağlar. Kullanıcı düzenleme menüsünden Nesne Ekle ' i seçtiğinde bu iletişim kutusunu görüntüleyin. Bu iletişim kutusunu göstermek için [Cotaınsertdialog](reference/coleinsertdialog-class.md) sınıfını kullanın. MDI uygulamasını kendi içine ekleyemeyeceğinize unutmayın. Bir SDI uygulaması olmadığı müddetçe kapsayıcı/sunucu olan bir uygulama kendi kendine eklenemez.

*Özel Yapıştır*<br/>
Bu iletişim kutusu, kullanıcının bileşik bir belgeye veri yapıştırırken kullanılan biçimi denetlemesine olanak tanır. Kullanıcı, verilerin biçimini seçebilir, verilerin eklenip eklenmeyeceğini veya bağlantısının yapılıp yapılmayacağını ve bir simge olarak görüntülenip görüntülenmeyeceğini seçebilir. Kullanıcı düzenleme menüsünden Özel Yapıştır ' i seçtiğinde bu iletişim kutusunu görüntüleyin. Bu iletişim kutusunu göstermek için [COlePasteSpecialDialog](reference/colepastespecialdialog-class.md) sınıfını kullanın.

*Simgeyi Değiştir*<br/>
Bu iletişim kutusu, kullanıcının bağlantılı veya katıştırılmış öğeyi göstermek için hangi simgenin görüntüleneceğini seçmesine olanak sağlar. Kullanıcı düzenleme menüsünden Değiştir simgesini seçtiğinde veya Özel Yapıştır veya Dönüştür iletişim kutularında Simgeyi Değiştir düğmesini seçtiğinde bu iletişim kutusunu görüntüleyin. Ayrıca, Kullanıcı nesne Ekle iletişim kutusunu açtığında ve simge olarak göster ' i seçtiğinde bu gösterimi de görüntülenir. Bu iletişim kutusunu göstermek için [Cotachangeicondialog](reference/colechangeicondialog-class.md) sınıfını kullanın.

*Dönüştür*<br/>
Bu iletişim kutusu, kullanıcının katıştırılmış veya bağlantılı bir öğenin türünü değiştirmesine izin verir. Örneğin, bileşik bir belgede bir meta dosyası katıştırdıysanız ve daha sonra gömülü meta dosyayı değiştirmek için başka bir uygulama kullanmak istiyorsanız, Dönüştür iletişim kutusunu kullanabilirsiniz. Bu iletişim kutusu genellikle düzenleme menüsünde *öğe türü* nesne ' ye tıklanarak ve ardından basamaklı menüsünde Dönüştür ' e tıklayarak görüntülenir. Bu iletişim kutusunu göstermek için [Cotaconvertdialog](reference/coleconvertdialog-class.md) sınıfını kullanın. Örnek olarak, MFC OLE örnek [Oclient](../overview/visual-cpp-samples.md)' ı çalıştırın.

*Bağlantıları Düzenle veya bağlantıları güncelleştir*<br/>
Bağlantıları Düzenle iletişim kutusu, kullanıcının bağlantılı nesnenin kaynağıyla ilgili bilgileri değiştirmesine izin verir. Bağlantıları güncelleştir iletişim kutusu, geçerli iletişim kutusundaki tüm bağlantılı öğelerin kaynaklarını doğrular ve gerekirse bağlantıları Düzenle iletişim kutusunu görüntüler. Kullanıcı düzenleme menüsünden bağlantıları seçtiğinde bağlantıları Düzenle iletişim kutusunu görüntüleyin. Güncelleştirme bağlantıları iletişim kutusu genellikle bileşik belge ilk kez açıldığında görüntülenir. Hangi iletişim kutusuna göstermek istediğinize bağlı olarak [Cotalinksdialog](reference/colelinksdialog-class.md) veya [copaupdatedialog](reference/coleupdatedialog-class.md) sınıfını kullanın.

*Sunucu meşgul veya sunucu yanıt vermiyor*<br/>
Kullanıcı bir öğeyi etkinleştirmeye çalıştığında ve genellikle sunucu başka bir kullanıcı veya görev tarafından kullanıldığından, sunucu meşgul iletişim kutusu görüntülenir. Sunucu, etkinleştirme isteğine hiç yanıt vermezse sunucu yanıt vermiyor iletişim kutusu görüntülenir. Bu iletişim kutuları, `COleMessageFilter` OLE arabiriminin bir uygulamasına göre aracılığıyla görüntülenir `IMessageFilter` ve Kullanıcı etkinleştirme isteğini yeniden denemesinin denenmeyeceğine karar verebilir. Bu iletişim kutusunu göstermek için [Cotabusi iletişim](reference/colebusydialog-class.md) sınıfını kullanın.

## <a name="see-also"></a>Ayrıca bkz.

[İletişim Kutuları](dialog-boxes.md)<br/>
[MFC’de İletişim Kutularıyla çalışma](life-cycle-of-a-dialog-box.md)<br/>
[OLE](ole-in-mfc.md)
