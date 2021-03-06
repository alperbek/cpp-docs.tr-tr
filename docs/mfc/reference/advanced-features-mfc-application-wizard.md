---
title: Gelişmiş Özellikler, MFC Uygulama Sihirbazı
ms.date: 11/04/2016
f1_keywords:
- vc.appwiz.mfc.exe.advanced
helpviewer_keywords:
- MFC Application Wizard, advanced features
ms.assetid: 8a6681c5-6576-4b12-841a-6862beee76fa
ms.openlocfilehash: dc2b745bf97dff65a3612c29745c9d0e455a347d
ms.sourcegitcommit: fcb48824f9ca24b1f8bd37d647a4d592de1cc925
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/15/2019
ms.locfileid: "69507802"
---
# <a name="advanced-features-mfc-application-wizard"></a>Gelişmiş Özellikler, MFC Uygulama Sihirbazı

Bu başlıkta; uygulamanıza yönelik, Yardım, yazdırma desteği vb. gibi ek özelliklerin seçenekleri listelenmiştir. Her bölümde, bu gelişmiş özelliklere yönelik ek destek belirtin.

- **Bağlama duyarlı Yardım (HTML)**

   Bağlam duyarlı yardım için F1 ve yardım menüsü kullanılarak veya iletişim kutusunda bir **Yardım** düğmesine tıklayarak kullanabileceğiniz bir dizi yardım dosyası oluşturur. Yardım desteği yardım derleyicisi gerektirir. Yardım derleyicisini yüklemediyseniz, Kur'u yeniden çalıştırarak yükleyebilirsiniz.

   Bkz [. HTML Yardımı: Daha fazla bilgi için programlarınız](../../mfc/html-help-context-sensitive-help-for-your-programs.md) ve yardım dosyalarınız için bağlama duyarlı Yardım [(HTML Yardımı)](../../build/reference/help-files-html-help.md) .

- **Yazdırma ve baskı önizleme**

   MFC kitaplığından [CView sınıfındaki](../../mfc/reference/cview-class.md) üye işlevlerini çağırarak yazdırma, yazdırma Kurulumu ve baskı önizleme komutlarını işleyecek kodu üretir. Ayrıca, sihirbaz, bu işlevlerin komutlarını uygulamanın menüsüne ekler. Yazdırma desteği yalnızca sihirbazın [uygulama türü, MFC Uygulama Sihirbazı](../../mfc/reference/application-type-mfc-application-wizard.md) sayfasında **belge/görünüm mimarisi desteğini** belirten uygulamalar için kullanılabilir. Varsayılan olarak, belge/görünüm uygulamaları yazdırma desteğine sahiptir.

- **Otomatikleştirme**

   Uygulamanın başka bir uygulamada yerleştirilen nesneleri işleyebileceğini belirtir ya da uygulamayı otomasyon istemcilerine açık hale getirir.

- **ActiveX denetimleri**

   ActiveX denetimlerini (varsayılan) destekler. Bu seçeneği seçmezseniz ve daha sonra projenize ActiveX denetimleri eklemek istiyorsanız, uygulamanızın [CWinApp:: InitInstance](../../mfc/reference/cwinapp-class.md#initinstance) üye Işlevindeki [AfxEnableControlContainer](ole-initialization.md#afxenablecontrolcontainer) öğesine bir çağrı eklemeniz gerekir.

- **MAPI (mesajlaşma API 'SI)**

   Uygulamanın e-posta iletilerini oluşturabileceğini, kullanabileceğini, aktarabileceğini ve depolayabileceğini belirtir.

- **Windows Yuvaları**

   TCP/IP ağları üzerinden iletişim kuran uygulamaları yazmak için kullanabileceğiniz Windows yuvalarını destekler.

- **Etkin Erişilebilirlik**

   , Erişilebilirlik istemcileriyle daha iyi etkileşim sağlamak üzere Kullanıcı arabirimini özelleştirmek için kullanabileceğiniz [CWnd](../../mfc/reference/cwnd-class.md)ile türetilmiş sınıflar Için [ıerişilebilen](/windows/win32/api/oleacc/nn-oleacc-iaccessible) destek ekler.

- **Ortak denetim bildirimi**

   Varsayılan olarak etkindir. Microsoft Windows XP ve daha yeni işletim sistemleri ile birlikte gelen, Ortak Denetim DLL'sini etkinleştirmek üzere bir uygulama bildirimi oluşturur.

   Ortak Denetim DLL 6 sürümü, varolan uygulamalarınızın kullandığı Ortak Denetimlerin önceki sürümünü otomatik olarak güncelleştirmez. Ortak Denetim DLL 6 sürümünü kullanmak için, uygulamanızı DLL'yi yüklemeye yönlendiren bir uygulama bildirimi oluşturmanız gerekir. Bu Ortak Denetim DLL Windows XP temalarını da destekler.

   Bir uygulama bildirimi, diğer DLL'leri ve uygulamanızın ihtiyaç duyduğu sürümleri de belirtebilir. Uygulama bildirimleri hakkında daha fazla bilgi için, bkz. Windows SDK [Yalıtılmış uygulamalar ve yan yana derlemeler](/windows/win32/SbsCs/isolated-applications-and-side-by-side-assemblies-portal) .

- **Yeniden başlatma yöneticisini destekle**

   [Windows yeniden başlatma Yöneticisi](/windows/win32/RstMgr/using-restart-manager)için destek ekler. Bu videoda, MFC 'den yeniden başlatma Yöneticisi 'nin nasıl kullanılacağı gösterilmektedir: [Nasıl yapılır: Yeni yeniden başlatma Yöneticisini](/previous-versions/visualstudio/visual-studio-2010/dd831853(v%3dvs.100))kullanın.

- **Gelişmiş çerçeve bölmeleri**

   |Seçenek|Açıklama|
   |------------|-----------------|
   |**Gezgin yerleştirme bölmesi**|Ana çerçeve penceresinin solundaki Visual Studio **Çözüm Gezgini** benzer bir yerleştirme bölmesi oluşturur.|
   |**Çıkış yerleştirme çerçevesi**|Ana çerçeve penceresi altında bulunan Visual Studio **çıktı** bölmesine benzer bir yerleştirme bölmesi oluşturur.|
   |**Özellikler yerleştirme bölmesi**|Ana çerçeve penceresinin sağında yer alan Visual Studio **Özellikler** bölmesine benzer bir yerleştirme bölmesi oluşturur.|
   |**Gezinti Bölmesi**|Outlook gezinti çubuğuna benzer ve ana çerçeve penceresinin sol tarafında bulunan bir yerleştirme bölmesi oluşturur.|
   |**Başlık çubuğu**|Ana çerçeve penceresinin üzerinde, Office stili bir başlık çubuğu oluşturur.|

- **Son kullanılan dosya listesindeki dosyaların sayısı**

   En son kullanılan listesinde listelenen dosyaların sayısını belirtir. Varsayılan sayı 4'tür.

## <a name="see-also"></a>Ayrıca bkz.

[MFC Uygulama Sihirbazı](../../mfc/reference/mfc-application-wizard.md)
