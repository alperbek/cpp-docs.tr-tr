---
title: 'Nasıl yapılır: -Clr kullanarak MFC ve ATL kodu derleme'
ms.custom: get-started-article
ms.date: 11/04/2016
helpviewer_keywords:
- MFC [C++], interoperability
- ATL [C++], interoperability
- mixed assemblies [C++], MFC code
- mixed assemblies [C++], ATL code
- /clr compiler option [C++], compiling ATL and MFC code
- interoperability [C++], /clr compiler option
- regular MFC DLLs [C++], /clr compiler option
- interop [C++], /clr compiler option
- extension DLLs [C++], /clr compiler option
ms.assetid: 12464bec-33a4-482c-880a-c078de7f6ea5
ms.openlocfilehash: 9a24e82787eb0fce8ff668843e73de9f2d05e1ad
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62379057"
---
# <a name="how-to-compile-mfc-and-atl-code-by-using-clr"></a>Nasıl yapılır: MFC ve ATL kodu kullanarak/CLR ile derleyin

Bu konu, ortak dil çalışma zamanını hedeflemek için mevcut MFC ve ATL programlarının nasıl yapılandırılabileceğini açıklar.

### <a name="to-compile-an-mfc-executable-or-regular-mfc-dll-by-using-clr"></a>/ CLR kullanarak MFC yürütülebilir veya Normal MFC DLL derlemek için

1. Projeye sağ **Çözüm Gezgini** ve ardından **özellikleri**.

1. İçinde **proje özellikleri** iletişim kutusunda, yanındaki düğümü genişletin **yapılandırma özellikleri** seçip **genel**. Sağ bölmede altında **Proje Varsayılanları**ayarlayın **ortak dil çalışma zamanı desteği** için **ortak dil çalışma zamanı desteği (/ clr)**.

   Emin olun aynı bölmede **MFC kullanımı** ayarlanır **MFC'yi bir ortak DLL'de**.

1. Altında **yapılandırma özellikleri**, yanındaki düğümü genişletin **C/C++** seçip **genel**. Emin olun **hata ayıklama bilgi biçimi** ayarlanır **Program veritabanı/zi** (değil **/zi**).

1. Seçin **kod oluşturma** düğümü. Ayarlama **en az yeniden derlemeyi etkinleştir** için **Hayır (/ Gm-)**. Ayrıca **temel çalışma zamanı denetimleri** için **varsayılan**.

1. Altında **yapılandırma özellikleri**seçin **C/C++** ardından **kod oluşturma**. Emin olun **çalışma zamanı kitaplığı** ayarlandığından **hata ayıklama çok iş parçacıklı DLL (/ MDd)** veya **çok iş parçacıklı DLL (/ MD)**.

1. Stdafx.h içinde şu satırı ekleyin.

    ```
    #using <System.Windows.Forms.dll>
    ```

### <a name="to-compile-an-mfc-extension-dll-by-using-clr"></a>Bir MFC uzantılı DLL/CLR'ı kullanarak derlemek için

1. "Bir MFC yürütülebilir veya Normal MFC DLL/CLR kullanarak derleme" adımları izleyin.

1. Altında **yapılandırma özellikleri**, yanındaki düğümü genişletin **C/C++** seçip **önceden derlenmiş üst bilgiler**. Ayarlama **önceden derlenmiş üst bilgi Oluştur/Kullan** için **önceden derlenmiş üst bilgiler kullanmayan**.

   Alternatif olarak, **Çözüm Gezgini**, Stdafx.cpp sağ tıklayın ve ardından **özellikleri**. Altında **yapılandırma özellikleri**, yanındaki düğümü genişletin **C/C++** seçip **genel**. Ayarlama **ortak dil çalışma zamanı desteği ile Derle** için **ortak dil çalışma zamanı desteği yok**.

1. DllMain ve her şeyi içeren bir dosya için buna çağrı **Çözüm Gezgini**, dosyaya sağ tıklayın ve ardından **özellikleri**. Altında **yapılandırma özellikleri**, yanındaki düğümü genişletin **C/C++** seçip **genel**. Sağ bölmede altında **Proje Varsayılanları**ayarlayın **ortak dil çalışma zamanı desteği ile Derle** için **ortak dil çalışma zamanı desteği yok**.

### <a name="to-compile-an-atl-executable-by-using-clr"></a>/ CLR'ı kullanarak bir ATL yürütülebilir dosya derlemek için

1. İçinde **Çözüm Gezgini**, projeye sağ tıklayın ve ardından **özellikleri**.

1. İçinde **proje özellikleri** iletişim kutusunda, yanındaki düğümü genişletin **yapılandırma özellikleri** seçip **genel**. Sağ bölmede altında **Proje Varsayılanları**ayarlayın **ortak dil çalışma zamanı desteği** için **ortak dil çalışma zamanı desteği (/ clr)**.

1. Altında **yapılandırma özellikleri**, yanındaki düğümü genişletin **C/C++** seçip **genel**. Emin olun **hata ayıklama bilgi biçimi** ayarlanır **Program veritabanı/zi** (değil **/zi**).

1. Seçin **kod oluşturma** düğümü. Ayarlama **en az yeniden derlemeyi etkinleştir** için **Hayır (/ Gm-)**. Ayrıca **temel çalışma zamanı denetimleri** için **varsayılan**.

1. Altında **yapılandırma özellikleri**seçin **C/C++** ardından **kod oluşturma**. Emin olun **çalışma zamanı kitaplığı** ayarlandığından **hata ayıklama çok iş parçacıklı DLL (/ MDd)** veya **çok iş parçacıklı DLL (/ MD)**.

1. Her MIDL tarafından oluşturulan dosya için (C dosyaları), dosyaya sağ **Çözüm Gezgini** ve ardından **özellikleri**. Altında **yapılandırma özellikleri**, yanındaki düğümü genişletin **C/C++** seçip **genel**. Ayarlama **ortak dil çalışma zamanı desteği ile Derle** için **ortak dil çalışma zamanı desteği yok**.

### <a name="to-compile-an-atl-dll-by-using-clr"></a>ATL DLL/CLR'ı kullanarak derlemek için

1. "Yürütülebilir bir ATL/CLR kullanarak derlemek için" bölümündeki adımları izleyin.

1. Altında **yapılandırma özellikleri**, yanındaki düğümü genişletin **C/C++** seçip **önceden derlenmiş üst bilgiler**. Ayarlama **önceden derlenmiş üst bilgi Oluştur/Kullan** için **önceden derlenmiş üst bilgiler kullanmayan**.

   Alternatif olarak, **Çözüm Gezgini**, Stdafx.cpp sağ tıklayın ve ardından **özellikleri**. Altında **yapılandırma özellikleri**, yanındaki düğümü genişletin **C/C++** seçip **genel**. Ayarlama **ortak dil çalışma zamanı desteği ile Derle** için **ortak dil çalışma zamanı desteği yok**.

1. DllMain ve her şeyi içeren bir dosya için buna çağrı **Çözüm Gezgini**, dosyaya sağ tıklayın ve ardından **özellikleri**. Altında **yapılandırma özellikleri**, yanındaki düğümü genişletin **C/C++** seçip **genel**. Sağ bölmede altında **Proje Varsayılanları**ayarlayın **ortak dil çalışma zamanı desteği ile Derle** için **ortak dil çalışma zamanı desteği yok**.

## <a name="see-also"></a>Ayrıca bkz.

[Karışık (Yerel ve Yönetilen) Derlemeler](../dotnet/mixed-native-and-managed-assemblies.md)
