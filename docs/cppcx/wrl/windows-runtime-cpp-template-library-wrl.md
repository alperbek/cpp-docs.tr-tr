---
title: Windows Çalışma Zamanı C++ Şablon Kitaplığı (WRL)
ms.date: 11/04/2016
ms.topic: reference
ms.assetid: b915afce-553b-44a7-b8dc-0ab601758eb0
ms.openlocfilehash: 5c1a4e7df424499f400dbd70d675956deef6bc5d
ms.sourcegitcommit: 5cecccba0a96c1b4ccea1f7a1cfd91f259cc5bde
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/01/2019
ms.locfileid: "58787132"
---
# <a name="windows-runtime-c-template-library-wrl"></a>Windows Çalışma Zamanı C++ Şablon Kitaplığı (WRL)

Windows çalışma zamanı C++ Şablon kitaplığı (WRL) yazıp Windows çalışma zamanı bileşenlerini kullanmanın alt düzey bir yolunu sağlayan bir şablon kitaplığıdır.

> [!NOTE]
> WRL artık yerini tarafından C + +/ WinRT, standart C ++ 17 dil projeksiyon Windows Runtime API'ları için. C + +/ WinRT, Windows 10 SDK sürüm 1803 ileriye doğru kullanılabilir. C + +/ WinRT tamamen üstbilgi dosyalarında uygulanan ve modern Windows API ile birinci sınıf erişim sağlayacak şekilde tasarlanmıştır.
>
> İle C + +/ WinRT, size hem kullanabilir ve Windows çalışma zamanı API'leri kullanarak tüm standartlara uyumlu C ++ 17 derleyici yazar. C + +/ WinRT genellikle daha iyi gerçekleştirir ve Windows çalışma zamanı için diğer bir dil seçeneği değerinden daha küçük ikili dosyaları üretir. Biz C + desteklemeye devam edecektir +/ CX ve WRL, ancak yüksek yeni uygulama C + kullanmanız +/ WinRT. Daha fazla bilgi için [C + +/ WinRT](https://docs.microsoft.com/windows/uwp/cpp-and-winrt-apis/index).

## <a name="benefits"></a>Yararları

Windows çalışma zamanı C++ Şablon Kitaplığı daha kolay uygulamanızı ve Bileşen Nesne Modeli (COM) bileşenlerini kullanmasını sağlar. Bu nesnelerin ömrünü yönetmek için başvuru sayımı ve bir işlemi başarılı veya başarısız olduğunu belirlemek için HRESULT değerleri test etme gibi temizlik teknikleri sunar. Başarıyla Windows çalışma zamanı C++ Şablon kitaplığı kullanmak için bu kuralları ve teknikleri dikkatle izlemeniz gerekir.

C + +/ CX, Windows çalışma zamanı bileşenlerini kullanmak için üst düzey, dile dayanan bir yoludur. Windows çalışma zamanı C++ Şablon Kitaplığı hem C + +/ CX, temizlik görevlerini adınıza otomatik olarak gerçekleştirerek Windows çalışma zamanı için kod yazma basitleştirin.

Windows çalışma zamanı C++ Şablon kitaplığı ve C + +/ CX farklı avantajları sunar. Windows çalışma zamanı C++ Şablon kitaplığı C + yerine kullanmak istemenize Bazı nedenlerle +/ CX:

- Windows çalışma zamanı C++ Şablon kitaplığı çok az soyutlama Windows çalışma zamanı uygulama ikili arabirimi (ABI üzerinden) ekler, size temel kodu daha iyi kontrol etme becerisinin oluşturabilir veya Windows çalışma zamanı API'leri.

- C + +/ CX COM HRESULT değerlerini özel durumlar olarak temsil eder. COM veya özel durumlar kullanmayan bir kullanan bir kod tabanına devraldıysanız, Windows çalışma zamanı C++ Şablon kitaplığı özel durumlar kullanmak durumunda olmadığınızdan dolayı Windows çalışma zamanı ile çalışmak için daha doğal bir yol olduğunu fark edebilirsiniz.

   > [!NOTE]
   > Windows çalışma zamanı C++ Şablon kitaplığı HRESULT değerleri kullanır ve özel durum oluşturmaz. Ayrıca, uygulama kodunuz bir özel durum oluşturduğunda nesnelerin düzgün şekilde yok edileceğini garanti etmeye yardımcı olmak için akıllı işaretçiler ve RAII deseni Windows çalışma zamanı C++ Şablon kitaplığı kullanır. Akıllı işaretçiler ve RAII hakkında daha fazla bilgi için bkz. [akıllı işaretçiler](../../cpp/smart-pointers-modern-cpp.md) ve [nesneleri kendi kaynakları (RAII)](../../cpp/objects-own-resources-raii.md).

- Ürününün amaç ve tasarımında, Windows çalışma zamanı C++ Şablon kitaplığı ilham Etkin Şablon kitaplığı (ATL tarafından), COM nesneleri programlamayı kolaylaştıran şablon tabanlı C++ sınıfları kümesi olduğu. Windows çalışma zamanı C++ Şablon kitaplığı, Windows çalışma zamanı kaydırmak için standart C++ kullandığından, daha kolay bağlantı noktası ve varolan birçok COM bileşeni ATL içinde Windows çalışma zamanı için yazılan etkileşim. Zaten ATL'yi biliyorsanız, Windows çalışma zamanı C++ Şablon kitaplığı programlama daha kolay olduğunu fark edebilirsiniz.

## <a name="getting-started"></a>Başlarken

Windows çalışma zamanı C++ Şablon kitaplığı ile hemen çalışmaya başlayabilirsiniz yardımcı olabilecek bazı kaynaklar aşağıda verilmiştir.

[Windows çalışma zamanı kitaplığı (WRL)](https://channel9.msdn.com/Events/Windows-Camp/Developing-Windows-8-Metro-style-apps-in-Cpp/The-Windows-Runtime-Library-WRL-)<br/>
Bu kanal 9 videosunda, Windows çalışma zamanı C++ Şablon Kitaplığı'nın nasıl yardımcı olduğu hakkında yazdığınız Evrensel Windows Platformu (UWP) uygulamaları ve yazar ve Windows çalışma zamanı bileşenlerini kullanma hakkında bilgi edinin.

[Nasıl yapılır: Bir Windows çalışma zamanı bileşenini etkinleştirme ve kullanma](how-to-activate-and-use-a-windows-runtime-component-using-wrl.md)<br/>
Windows çalışma zamanı C++ Şablon kitaplığı Windows çalışma zamanı başlatma, etkinleştirmek ve bir Windows çalışma zamanı bileşeni kullanmak için nasıl kullanılacağını gösterir.

[Nasıl yapılır: Zaman uyumsuz işlemleri tamamlama](how-to-complete-asynchronous-operations-using-wrl.md)<br/>
Windows çalışma zamanı C++ Şablon kitaplığı zaman uyumsuz işlemler başlatmak ve işlemler tamamlandığında iş gerçekleştirmek için nasıl kullanılacağını gösterir.

[Nasıl yapılır: Olayları işleme](how-to-handle-events-using-wrl.md)<br/>
Windows çalışma zamanı C++ Şablon kitaplığı abone olup bir Windows çalışma zamanı nesnesi olaylarını işlemek için nasıl kullanılacağını gösterir.

[İzlenecek yol: WRL ve Medya Altyapısı kullanarak UWP uygulaması oluşturma](walkthrough-creating-a-windows-store-app-using-wrl-and-media-foundation.md)<br/>
Kullanan bir UWP uygulaması oluşturmayı öğrenin [Microsoft Media Foundation](/windows/desktop/medfound/microsoft-media-foundation-sdk).

[Nasıl yapılır: Klasik COM bileşeni oluşturma](how-to-create-a-classic-com-component-using-wrl.md)<br/>
Temel bir COM bileşeni ve kaydetmek ve bir masaüstü uygulamasından COM bileşeni kullanmak için basit bir yol oluşturmak için Windows çalışma zamanı C++ Şablon kitaplığı kullanmayı gösterir.

[Nasıl yapılır: Doğrudan WRL Bileşenlerinin Örneğini Oluşturma](how-to-instantiate-wrl-components-directly.md)<br/>
Nasıl kullanacağınızı öğrenin [Microsoft::wrl:: Make](make-function.md) ve [Microsoft::WRL::Details::MakeAndInitialize](makeandinitialize-function.md) kendisini tanımlayan modülden bir bileşen örneği oluşturmak için işlevleri.

[Nasıl yapılır: Windows meta verilerinden .h dosyaları oluşturmak için winmdidl.exe ve midlrt.exe programını kullanma](use-winmdidl-and-midlrt-to-create-h-files-from-windows-metadata.md)<br/>
.Winmd meta verisinden bir IDL dosyası oluşturarak özel Windows Runtime bileşenlerinin wrl'den kullanma işlemi gösterilmektedir.

[İzlenecek yol: Görevleri ve XML HTTP İsteklerini Kullanarak Bağlanma](../../parallel/concrt/walkthrough-connecting-using-tasks-and-xml-http-requests.md)<br/>
Nasıl kullanılacağını gösterir [Ixmlhttprequest2](/windows/desktop/api/msxml6/nn-msxml6-ixmlhttprequest2) ve [Ixmlhttprequest2callback](/windows/desktop/api/msxml6/nn-msxml6-ixmlhttprequest2callback) bir UWP uygulamasında bir web hizmetine HTTP GET ve POST istekleri göndermek için görevleri ile birlikte arabirimleri.

[Bing Maps Trip Optimizer örneği](https://code.msdn.microsoft.com/Bing-Maps-trip-optimizer-c4e037f7)<br/>
Kullanan `HttpRequest` tanımlanan sınıfı [izlenecek yol: Bağlama kullanarak görevleri ve XML HTTP isteklerini](../../parallel/concrt/walkthrough-connecting-using-tasks-and-xml-http-requests.md) eksiksiz bir UWP uygulaması bağlamında.

[C++ örnek ile bir Windows çalışma zamanı DLL bileşeni oluşturma](https://code.msdn.microsoft.com/windowsapps/Creating-a-Windows-Runtime-6c399797)<br/>
Bir işlemde DLL bileşeni oluşturma ve C + tüketicilerimizin Windows çalışma zamanı C++ Şablon kitaplığı kullanma işlemini gösterir +/ CX, JavaScript ve C#.

[DirectX marble maze oyun örneği](https://code.msdn.microsoft.com/windowsapps/DirectX-Marble-Maze-Game-e4806345)<br/>
Windows çalışma zamanı C++ Şablon kitaplığı bağlamında, tam bir 3-b oyunda DirectX ve Media Foundation gibi COM bileşenlerinin kullanım ömrünü yönetmek için nasıl kullanılacağını gösterir.

[Masaüstü uygulama örneğinden kutlama bildirimleri gönderme](https://code.msdn.microsoft.com/windowsdesktop/Sending-toast-notifications-71e230a2)<br/>
Bir masaüstü uygulamasından kutlama bildirimleri ile iş için Windows çalışma zamanı C++ Şablon Kitaplığı nasıl yapılacağı açıklanır.

## <a name="windows-runtime-c-template-library-compared-to-atl"></a>Windows çalışma zamanı C++ Şablon kitaplığı ile ATL karşılaştırması

Küçük, hızlı COM nesneleri oluşturmak için kullanabileceğiniz Windows çalışma zamanı C++ Şablon kitaplığı Etkin Şablon kitaplığı (ATL) benzer. Windows çalışma zamanı C++ Şablon kitaplığı ve ATL Ayrıca, arabirimlerin açık kaydı modüllerdeki nesnelerin tanımı gibi kavramları paylaşın ve oluşturma nesnelerin Fabrikalar kullanılarak açık. İle çalışmakta güçlük çekmezsiniz biliyorsanız, Windows çalışma zamanı C++ Şablon kitaplığı ile rahat olabilir

Windows çalışma zamanı C++ Şablon kitaplığı UWP uygulamaları için gereken COM işlevini destekler. Bu nedenle, aşağıdakiler gibi COM özellikleri için doğrudan destek atlandığı için ATL farklıdır:

- Toplama

- kalıp uygulamalar

- çift arabirimler (`IDispatch`)

- Standart sabit listesi arabirimleri

- bağlantı noktaları

- Etiket arabirimleri

- OLE katıştırma

- ActiveX denetimleri

- COM+

## <a name="concepts"></a>Kavramlar

Windows çalışma zamanı C++ Şablon kitaplığı, bir temel kavramlar temsil eden türler sağlar. Aşağıdaki bölümler bu türleri açıklamaktadır.

### <a name="comptr"></a>ComPtr

[ComPtr](comptr-class.md) olduğu bir *akıllı işaretçi* şablon parametresi tarafından belirlenen arabirimi temsil eden tür. Kullanım `ComPtr` arabirimden türetilmiş bir nesnenin üyelerine erişebilen bir değişken bildirmek için. `ComPtr` otomatik olarak temel arabirim işaretçisi için bir başvuru sayısını tutar ve başvuru sayısı sıfıra gittiğinde arabirimi serbest bırakır.

### <a name="runtimeclass"></a>RuntimeClass

[RuntimeClass](runtimeclass-class.md) belirtilen arabirim kümesini devralan örneklenmiş bir sınıfı temsil eder. A `RuntimeClass` nesnesi bir birleşimini bir veya daha fazla Windows çalışma zamanı COM arabirimi ya da bir bileşene zayıf başvuru desteği sağlar.

### <a name="module"></a>Modül

[Modül](module-class.md) ilgili nesnelerin bir koleksiyonunu temsil eder. A `Module` nesnesi, nesneleri ve diğer uygulamaların bir nesne kullanmasını sağlayan kaydı oluşturan sınıf üreteçlerini yönetir.

### <a name="callback"></a>geri çağırma

[Geri çağırma](callback-function-wrl.md) işlevi, üye işlevi bir olay işleyicisi (bir geri arama yöntemi) olan bir nesne oluşturur. Kullanım `Callback` zaman uyumsuz işlemler yazmak için işlevi.

### <a name="eventsource"></a>EventSource

[EventSource](eventsource-class.md) yönetmek için kullanılan *temsilci* olay işleyicileri. Bir temsilci uygulamak ve kullanmak için Windows çalışma zamanı C++ Şablon kitaplığı kullanın `EventSource` eklemek, kaldırmak ve temsilci çağırma.

### <a name="asyncbase"></a>AsyncBase

[AsyncBase](asyncbase-class.md) Windows çalışma zamanı zaman uyumsuz programlama modelini temsil eden sanal yöntemleri sağlar. Başlat, Durdur veya zaman uyumsuz bir işlemin ilerleme durumunu denetlemek için özel bir sınıf oluşturmak için bu sınıftaki üyeleri geçersiz kılar.

### <a name="ftmbase"></a>FtmBase

[FtmBase](ftmbase-class.md) ücretsiz iş parçacıklı bir Sıralayıcı nesnesini temsil eder. `FtmBase` bir genel arabirim tablosu (GIT) oluşturur ve sıralama ve proxy nesnelerinin yönetimine yardım eder.

### <a name="weakref"></a>WeakRef

[WeakRef](weakref-class.md) temsil eden akıllı işaretçi türünde bir *zayıf başvuru*, erişilebilir olmayabilir veya bir nesne başvuruyor. A `WeakRef` yalnızca Windows çalışma zamanı tarafından hem klasik COM tarafından değil, nesne kullanılabilir

A `WeakRef` nesnesi genelde, varlığı harici bir iş parçacığı ya da uygulama tarafından denetlenen bir nesne temsil eder. Örneğin, bir `WeakRef` nesnesi, bir dosya nesnesine başvurabilir. Dosya açıldığında, `WeakRef` geçerlidir ve başvurulan dosyaya erişilebilir. Ancak dosya kapatıldığında `WeakRef` geçersiz ve dosyaya erişilemiyor.

## <a name="related-topics"></a>İlgili Konular

|||
|-|-|
|[Kategoriye göre başlıca API'ler](key-wrl-apis-by-category.md)|Birincil Windows çalışma zamanı C++ Şablon kitaplığı türleri, işlevlerini ve makrolarını vurgular.|
|[Başvuru](wrl-reference.md)|Windows çalışma zamanı C++ Şablon kitaplığı için başvuru bilgileri içerir.|
|[Hızlı Başvuru (Windows Runtime ve Visual C++)](../../cppcx/quick-reference-c-cx.md)|Kısaca açıklar C + +/ CX özellikleri, Windows çalışma zamanı desteği.|
|[Visual C++'ta Windows çalışma zamanı bileşenlerini kullanma](/windows/uwp/winrt-components/walkthrough-creating-a-basic-windows-runtime-component-in-cpp-and-calling-it-from-javascript-or-csharp)|Gösterilmektedir kullanmak C + +/ CX temel bir Windows çalışma zamanı bileşeni oluşturma.|