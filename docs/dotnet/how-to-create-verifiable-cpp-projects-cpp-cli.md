---
title: 'Nasıl yapılır: Doğrulanabilen oluşturma C++ projeleri (C++/CLI)'
ms.date: 11/04/2016
helpviewer_keywords:
- verifiable assemblies [C++], creating
- conversions, C++ projects
- Visual Studio C++ projects
ms.assetid: 4ef2cc1a-e3e5-4d67-8d8d-9c614f8ec5d3
ms.openlocfilehash: 0784e6f202750e846c75434eef62a12dab3952f1
ms.sourcegitcommit: 7d64c5f226f925642a25e07498567df8bebb00d4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/08/2019
ms.locfileid: "65448114"
---
# <a name="how-to-create-verifiable-c-projects-ccli"></a>Nasıl yapılır: doğrulanabilir oluşturma C++ projeleri (C++/CLI)

Visual C++ uygulama sihirbazları doğrulanabilir projeleri oluşturabilirsiniz.

> [!IMPORTANT]
> Visual Studio 2015 kullanım dışı ve Visual Studio 2017'yi desteklemez **/CLR: pure** ve **/CLR: safe** doğrulanabilir projeleri oluşturma. Doğrulanabilen kod gerekiyorsa, C# kodunuzda Çevir öneririz.

Ancak, Microsoft daha eski bir sürümünü kullanıyorsanız C++ destekleyen derleyici araç takımı **/CLR: pure** ve **/CLR: safe**, projeleri doğrulanabilir dönüştürülebilir. Bu konuda, proje özelliklerini ve Visual Studio dönüştürmek için proje kaynak dosyalarında değişiklik açıklar C++ doğrulanabilir uygulamalar oluşturmak için proje.

## <a name="compiler-and-linker-settings"></a>Derleyici ve bağlayıcı ayarları

Varsayılan olarak, .NET projeleri, / CLR derleyici bayrağını kullanın ve hedef x86 donanım bağlayıcıya yapılandırın. Doğrulanabilir kod için/CLR: safe bayrağı kullanmanız gerekir ve yerel makine yönergelerine yerine MSIL oluşturma konusunda talimat vermelisiniz.

### <a name="to-change-the-compiler-and-linker-settings"></a>Derleyici ve bağlayıcı ayarları değiştirmek için

1. ' % S'proje özelliği sayfasında görüntüler. Daha fazla bilgi için [derleyici ayarlayın ve derleme özellikleri](../build/working-with-project-properties.md).

1. Üzerinde **genel** altındaki **yapılandırma özellikleri** , düğüm kümesi **ortak dil çalışma zamanı desteği** özelliğini **Güvenli MSIL Ortak dil Çalışma zamanı desteği (/ CLR: safe)**.

1. Üzerinde **Gelişmiş** altındaki **bağlayıcı** , düğüm kümesi **CLR imaj türü** özelliğini **Güvenli IL imajını zorla (/ CLRIMAGETYPE: safe)**.

## <a name="removing-native-data-types"></a>Yerel veri türlerini kaldırma

Yerel veri türleri doğrulanabilir olduğundan, aslında kullanılmazlar bile yerel türler içeren tüm üst bilgi dosyaları kaldırmanız gerekir.

> [!NOTE]
> Aşağıdaki yordam Windows Forms uygulaması (.NET) ve konsol uygulaması (.NET) projeler için geçerlidir.

### <a name="to-remove-references-to-native-data-types"></a>Yerel veri türleri başvuruları kaldırmak için

1. Stdafx.h dosyadaki her şeyi açıklama.

## <a name="configuring-an-entry-point"></a>Bir giriş noktası yapılandırma

C çalışma zamanı kitaplıkları (CRT) doğrulanabilir uygulamaları kullanamazsınız çünkü ana işlevi standart giriş noktası olarak çağırmak için CRT üzerinde bağımlı olamaz. Başka bir deyişle, açıkça için bağlayıcı başlangıçta çağrılacak işlevin adını sağlamanız gerekir. (Bu durumda, Main() main() veya _tmain() yerine bir CRT olmayan giriş noktasını belirtmek için kullanılan, ancak giriş noktası açıkça belirtilmesi gerektiğinden, bu rastgele bir addır.)

> [!NOTE]
> Aşağıdaki yordamlar, konsol uygulaması (.NET) projeler için geçerlidir.

#### <a name="to-configure-an-entry-point"></a>Bir giriş noktası yapılandırmak için

1. _Tmain() Main() projenin ana .cpp dosyası ile değiştirin.

1. ' % S'proje özelliği sayfasında görüntüler. Daha fazla bilgi için [derleyici ayarlayın ve derleme özellikleri](../build/working-with-project-properties.md).

1. Üzerinde **Gelişmiş** altındaki **bağlayıcı** düğümünü girin `Main` olarak **giriş noktası** özellik değeri.

## <a name="see-also"></a>Ayrıca bkz.

- [Saf ve Doğrulanabilen Kod (C++/CLI)](../dotnet/pure-and-verifiable-code-cpp-cli.md)
