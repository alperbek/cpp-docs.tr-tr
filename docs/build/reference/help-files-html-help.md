---
title: Yardım Dosyaları (HTML Yardım)
ms.date: 11/04/2016
helpviewer_keywords:
- file types [C++], HTML Help files
ms.assetid: d30a1b1b-318f-4a78-8b60-93da53a224a8
ms.openlocfilehash: 2b856defdac51c978aa07cd13ef8df153c9c3f5f
ms.sourcegitcommit: fc1de63a39f7fcbfe2234e3f372b5e1c6a286087
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/15/2019
ms.locfileid: "65707016"
---
# <a name="help-files-html-help"></a>Yardım Dosyaları (HTML Yardım)

Yardım desteği HTML Yardımı türünü seçerek uygulamanıza eklediğinizde, aşağıdaki dosyalar oluşturulur **bağlama duyarlı Yardım** onay kutusunu ve sonra seçerek **HTML Yardımı biçimi** içinde[Gelişmiş Özellikler](../../mfc/reference/advanced-features-mfc-application-wizard.md) MFC Uygulama Sihirbazı sayfası.

|Dosya adı|Dizin konumu|Çözüm Gezgini konumu|Açıklama|
|---------------|------------------------|--------------------------------|-----------------|
|*PROJNAME*.hhp|*PROJNAME*\hlp|HTML Yardım dosyaları|Yardım proje dosyası. Bu Yardım dosyaları bir .hxs dosyasına veya .chm dosyasını derlemek için gereken verileri içerir.|
|*PROJNAME*.hhk|*PROJNAME*\hlp|HTML Yardım dosyaları|Yardım konuları dizinini içerir.|
|*PROJNAME*.hhc|*PROJNAME*\hlp|HTML Yardım dosyaları|Yardım projenin içeriğini.|
|Makehtmlhelp.bat|*PROJNAME*|Kaynak dosyaları|Proje derlendiğinde Yardım Projeyi derlemek için sistem tarafından kullanılır.|
|Afxcore.htm|*PROJNAME*\hlp|HTML Yardım konuları|Standart MFC komutlarını ve ekran nesneleri için standart Yardım konularını içerir. Kendi Yardım konuları, bu dosyaya ekleyin.|
|Afxprint.htm|*PROJNAME*\hlp|HTML Yardım konuları|Yazdırma komutlar için Yardım konularını içerir.|
|*.jpg; \*.gif|*PROJNAME*\hlp\Images|Kaynak Dosyalar|Görüntüler farklı oluşturulmuş Yardım dosyası konuları içerir.|

## <a name="see-also"></a>Ayrıca bkz.

[Oluşturulan türleri için Visual Studio dosya C++ projeleri](file-types-created-for-visual-cpp-projects.md)
