---
title: MFC Uygulaması Oluşturma
ms.date: 08/28/2019
helpviewer_keywords:
- applications [MFC]
- MFC, creating applications
- MFC applications
ms.assetid: b8b8aa08-9c49-404c-8078-b42079ac18f0
ms.openlocfilehash: f0d0287c9914bbefc2c5659e5f5d4386ab566c1a
ms.sourcegitcommit: 857fa6b530224fa6c18675138043aba9aa0619fb
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/24/2020
ms.locfileid: "80215143"
---
# <a name="creating-an-mfc-application"></a>MFC Uygulaması Oluşturma

MFC uygulaması, Microsoft Foundation Class (MFC) kitaplığı 'nı temel alan Windows için yürütülebilir bir uygulamadır. MFC yürütülebilir dosyaları genellikle beş türe ayrılır: standart Windows uygulamaları, iletişim kutuları, form tabanlı uygulamalar, Gezgin stili uygulamalar ve Web tarayıcı stili uygulamalar. Daha fazla bilgi için bkz.

- [Windows uygulamaları yazmak için sınıfları kullanma](../../mfc/using-the-classes-to-write-applications-for-windows.md)

- [İletişim Kutuları Oluşturma ve Görüntüleme](../../mfc/creating-and-displaying-dialog-boxes.md)

- [Form Tabanlı MFC Uygulaması Oluşturma](../../mfc/reference/creating-a-forms-based-mfc-application.md)

- [Dosya Gezgini Stilinde MFC Uygulaması Oluşturma](../../mfc/reference/creating-a-file-explorer-style-mfc-application.md)

- [Web Tarayıcısı Stilinde MFC Uygulaması Oluşturma](../../mfc/reference/creating-a-web-browser-style-mfc-application.md)

MFC Uygulama Sihirbazı, sihirbazda belirlediğiniz seçeneklere bağlı olarak, bu tür uygulamalardan herhangi biri için uygun sınıfları ve dosyaları oluşturur.

MFC uygulaması oluşturmanın en kolay yolu MFC Uygulama Sihirbazı 'Nı kullanmaktır (Visual Studio 2019 ' de**MFC Uygulama Projesi** ). MFC konsol uygulaması (MFC kitaplıklarını kullanan ancak konsol penceresinde çalışan bir komut satırı programı) oluşturmak için, Windows Masaüstü Sihirbazı 'Nı kullanın ve **konsol uygulaması** ve **MFC üstbilgileri** seçeneklerini belirleyin.

::: moniker range=">=vs-2019"

## <a name="to-create-an-mfc-forms-or-dialog-based-application"></a>MFC formları veya iletişim kutusu tabanlı uygulama oluşturmak için

1. Ana menüden **dosya** > **Yeni** > **Proje**' yi seçin.
1. Arama kutusuna "MFC" yazın ve ardından sonuç listesinden **MFC uygulaması** ' nı seçin.
1. Gerekirse Varsayılanları değiştirin ve ardından **Oluştur** ' a basarak **MFC Uygulama sihirbazını**açın.
1. Yapılandırma değerlerini gereken şekilde değiştirip **son**' a basın.

Daha fazla bilgi için bkz. [form tabanlı MFC uygulaması oluşturma](creating-a-forms-based-mfc-application.md).

![MFC Uygulama Sihirbazı](media/mfc-app-wizard.png)

## <a name="to-create-an-mfc-console-application"></a>MFC konsol uygulaması oluşturmak için

MFC konsol uygulaması MFC kitaplıklarını kullanan ancak konsol penceresinde çalıştırılan bir komut satırı programıdır.

1. Ana menüden **dosya** > **Yeni** > **Proje**' yi seçin.
1. Arama kutusuna "Masaüstü" yazın ve ardından sonuç listesinden **Windows Masaüstü Sihirbazı** ' nı seçin.
1. Proje adını gereken şekilde değiştirin ve ardından **İleri** ' ye basarak **Windows Masaüstü Sihirbazı 'nı**açın.
1. **MFC üstbilgileri** kutusunu işaretleyin ve diğer değerleri gerektiği gibi ayarlayıp **son**' a basın.

![MFC Uygulama Sihirbazı](media/windows-desktop-wizard.png)

::: moniker-end

::: moniker range="=vs-2017"

## <a name="to-create-an-mfc-forms-or-dialog-based-application"></a>MFC formları veya iletişim kutusu tabanlı uygulama oluşturmak için

1. Ana menüden **dosya** > **Yeni** > **Proje**' yi seçin.
1. **Yüklü** Şablonlar altında **Visual C++**  > **MFC/ATL**' yi seçin. Bunları görmüyorsanız, eklemek için Visual Studio Yükleyicisi kullanın.
1. Orta bölmeden **MFC uygulaması** ' nı seçin.
1. Yapılandırma değerlerini gereken şekilde değiştirip **son**' a basın.

Daha fazla bilgi için bkz. [form tabanlı MFC uygulaması oluşturma](creating-a-forms-based-mfc-application.md).

![MFC Uygulama Sihirbazı](media/mfc-app-wizard.png)

## <a name="to-create-an-mfc-console-application"></a>MFC konsol uygulaması oluşturmak için

MFC konsol uygulaması MFC kitaplıklarını kullanan ancak konsol penceresinde çalıştırılan bir komut satırı programıdır.

1. Ana menüden **dosya** > **Yeni** > **Proje**' yi seçin.
1. **Yüklü** Şablonlar altında, **Windows Masaüstü**> **görsel C++**  ' i seçin.
1. Orta bölmeden **Windows Masaüstü Sihirbazı** ' nı seçin.
1. Proje adını gereken şekilde değiştirin ve sonra **Windows Masaüstü Sihirbazı 'nı**açmak için **Tamam** ' a basın.
1. **MFC üstbilgileri** kutusunu işaretleyin ve diğer değerleri gerektiği gibi ayarlayıp **son**' a basın.

![MFC Uygulama Sihirbazı](media/windows-desktop-wizard-2017.png)

::: moniker-end

::: moniker range="=vs-2015"

## <a name="to-create-an-mfc-forms-or-dialog-based-application"></a>MFC formları veya iletişim kutusu tabanlı uygulama oluşturmak için

1. Ana menüden **dosya** > **Yeni** > **Proje**' yi seçin.
1. **Yüklü** Şablonlar altında **Visual C++**  > **MFC**' yi seçin.
1. Orta bölmeden **MFC uygulaması** ' nı seçin.
1. **İleri** ' ye tıklayarak **MFC Uygulama Sihirbazı 'nı**başlatın.

Daha fazla bilgi için bkz. [form tabanlı MFC uygulaması oluşturma](creating-a-forms-based-mfc-application.md).

![MFC Uygulama Sihirbazı](media/mfc-app-wizard-2015.png)

## <a name="to-create-an-mfc-console-application"></a>MFC konsol uygulaması oluşturmak için

MFC konsol uygulaması MFC kitaplıklarını kullanan ancak konsol penceresinde çalıştırılan bir komut satırı programıdır.

1. Ana menüden **dosya** > **Yeni** > **Proje**' yi seçin.
1. **Yüklü** Şablonlar altında, **Visual C++**  > **Win32**öğesini seçin.
1. Orta bölmeden **Win32 konsol uygulaması** ' nı seçin.
1. Proje adını gereken şekilde değiştirip **Tamam**' a basın.
1. Sihirbazın ikinci sayfasında, **MFC için ortak üst bilgileri ekle** kutusunu işaretleyin ve diğer değerleri gerektiği gibi ayarlayıp **son**' a basın.

::: moniker-end

Projeniz oluşturulduktan sonra, **Çözüm Gezgini**oluşturulan dosyaları görüntüleyebilirsiniz. Sihirbazın projeniz için oluşturduğu dosyalar hakkında daha fazla bilgi için, proje tarafından oluşturulan ReadMe. txt dosyasına bakın. Dosya türleri hakkında daha fazla bilgi için bkz. [Visual Studio C++ projeleri Için oluşturulan dosya türleri](../../build/reference/file-types-created-for-visual-cpp-projects.md).

## <a name="see-also"></a>Ayrıca bkz.

[Kod Sihirbazlarıyla İşlevsellik Ekleme](../../ide/adding-functionality-with-code-wizards-cpp.md)<br/>
[Özellik Sayfaları](../../build/reference/property-pages-visual-cpp.md)
