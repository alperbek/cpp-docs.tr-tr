---
title: Dll 'LerC++(/CX)
ms.date: 02/06/2018
ms.assetid: 5b8bcc57-64dd-4c54-9f24-26a25bd5dddd
ms.openlocfilehash: 4db0ed4f11f03c65c440c7b654653347da1d4536
ms.sourcegitcommit: 180f63704f6ddd07a4172a93b179cf0733fd952d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/06/2019
ms.locfileid: "70740266"
---
# <a name="dlls-ccx"></a>Dll 'LerC++(/CX)

Visual Studio 'Yu, standart bir Win32 DLL veya Evrensel Windows Platformu (UWP) uygulamaları tarafından tüketilen bir Windows Çalışma Zamanı Component DLL oluşturmak için kullanabilirsiniz. Visual Studio 'dan önceki bir sürümü kullanılarak oluşturulmuş standart bir DLL veya Visual Studio 2012 ' C++ den önceki Microsoft DERLEYICISI, UWP uygulamasında düzgün yüklenmeyebilir ve Microsoft Store uygulama doğrulama testini geçemeyebilir.

## <a name="windows-runtime-component-dlls"></a>Windows Çalışma Zamanı bileşen DLL 'Leri

Neredeyse tüm durumlarda, UWP uygulamasında kullanmak üzere bir DLL oluşturmak istediğinizde, bu adın proje şablonunu kullanarak bir Windows Çalışma Zamanı bileşeni olarak oluşturun. Ortak veya özel Windows Çalışma Zamanı türlerine sahip dll 'Ler için Windows Çalışma Zamanı bileşen projesi oluşturabilirsiniz. Windows Çalışma Zamanı bileşene, Windows Çalışma Zamanı uyumlu herhangi bir dilde yazılan uygulamalardan erişilebilir. Varsayılan olarak, bir Windows Çalışma Zamanı bileşen projesi için derleyici ayarları **/ZW** anahtarını kullanır. Bir. winmd dosyası, kök ad alanıyla aynı ada sahip olmalıdır. Örneğin, A. B. C. MyClass adlı bir sınıf, yalnızca bir. winmd veya A. B. winmd veya A. B. C. winmd adında bir meta veri dosyasında tanımlanmışsa oluşturulabilir. DLL 'nin adı. winmd dosya adıyla eşleşmek için gerekli değildir.

Daha fazla bilgi için bkz. [içinde C++Windows çalışma zamanı bileşenleri oluşturma ](/windows/uwp/winrt-components/creating-windows-runtime-components-in-cpp).

### <a name="to-reference-a-third-party-windows-runtime-component-binary-in-your-project"></a>Projenizdeki bir üçüncü taraf Windows Çalışma Zamanı bileşen ikilisini başvurmak için

1. DLL 'yi kullanacak proje için kısayol menüsünü açın ve ardından **Özellikler**' i seçin. **Ortak özellikler** sayfasında, **Yeni Başvuru Ekle** düğmesini seçin.

1. Bir Windows Çalışma Zamanı bileşeni, meta verileri içeren bir DLL dosyasından ve. winmd dosyasından oluşur. Genellikle, bu dosyalar aynı klasörde bulunur. **Başvuru Ekle** iletişim kutusunun sol **bölmesinde, e-bul düğmesini SEÇIN** ve ardından dll ve. winmd dosyasının konumuna gidin. Daha fazla bilgi için bkz. [Uzantı SDK 'ları](/visualstudio/extensibility/creating-a-software-development-kit#extension-sdks).

## <a name="standard-dlls"></a>Standart DLL 'Ler

Ortak Windows Çalışma Zamanı türlerini tüketmeyen veya üreten C++ ve bir UWP uygulamasından tüketen kod için standart bir DLL oluşturabilirsiniz. Visual Studio 'nun bu sürümünde derlemek için mevcut bir DLL 'yi geçirmek istediğinizde, ancak kodu bir Windows Çalışma Zamanı bileşen projesine dönüştürmeyeceğiniz zaman dinamik bağlantı kitaplığı (DLL) proje türünü kullanın. Aşağıdaki adımları kullandığınızda, DLL. appx paketinde uygulamanızın yürütülebilir dosyası ile birlikte dağıtılır.

### <a name="to-create-a-standard-dll-in-visual-studio"></a>Visual Studio 'da Standart DLL oluşturmak için

1. Menü çubuğunda **Dosya**, **Yeni**, **Proje**' yi seçin ve ardından **dinamik bağlantı kitaplığı (dll)** şablonunu seçin.

1. Proje için bir ad girin ve **Tamam** düğmesini seçin.

1. Kodu ekleyin. Dışarı aktarmayı düşündüğünüz işlevler `__declspec(dllexport)` için kullandığınızdan emin olun — Örneğin,`__declspec(dllexport) Add(int I, in j);`

1. UWP `#include winapifamily.h` uygulamaları için Windows SDK üst bilgi dosyasını dahil etmek ve makroyu `WINAPI_FAMILY=WINAPI_PARTITION_APP`ayarlamak için ekleyin.

### <a name="to-reference-a-standard-dll-project-from-the-same-solution"></a>Aynı çözümden standart bir DLL projesine başvurmak için

1. DLL 'yi kullanacak proje için kısayol menüsünü açın ve ardından **Özellikler**' i seçin. **Ortak özellikler** sayfasında, **Yeni Başvuru Ekle** düğmesini seçin.

1. Sol bölmede **çözüm**' ü seçin ve sağ bölmedeki ilgili onay kutusunu seçin.

1. Kaynak kodu dosyalarınızda, gereken şekilde dll üstbilgi `#include` dosyası için bir ifade ekleyin.

### <a name="to-reference-a-standard-dll-binary"></a>Standart bir DLL ikiliye başvurmak için

1. DLL dosyasını,. lib dosyasını ve üst bilgi dosyasını kopyalayın ve bu dosyaları bilinen bir konuma (örneğin, geçerli proje klasörünüzde) yapıştırın.

1. DLL 'yi kullanacak proje için kısayol menüsünü açın ve ardından **Özellikler**' i seçin. **Yapılandırma özellikleri**, **bağlayıcı**, **giriş** sayfasında,. lib dosyasını bir bağımlılık olarak ekleyin.

1. Kaynak kodu dosyalarınızda, gereken şekilde dll üstbilgi `#include` dosyası için bir ifade ekleyin.

### <a name="to-migrate-an-existing-win32-dll-for-uwp-app-compatibility"></a>UWP uygulama uyumluluğu için mevcut bir Win32 DLL 'yi geçirmek için

1. DLL (Evrensel Windows) türünde bir proje oluşturun ve var olan kaynak kodunuzu buna ekleyin.

1. UWP `#include winapifamily.h` uygulamaları için Windows SDK üst bilgi dosyasını dahil etmek ve makroyu `WINAPI_FAMILY=WINAPI_PARTITION_APP`ayarlamak için ekleyin.

1. Kaynak kodu dosyalarınızda, gereken şekilde dll üstbilgi `#include` dosyası için bir ifade ekleyin.
