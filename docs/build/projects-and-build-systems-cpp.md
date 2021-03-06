---
title: Visual Studio 'da C/C++ projeleri ve derleme sistemleri
ms.description: Use Visual Studio to compile and build C++ projects for Windows, ARM or Linux based on any project system.
ms.date: 07/17/2019
helpviewer_keywords:
- builds [C++]
- C++ projects, building
- projects [C++], building
- builds [C++], options
- C++, build options
ms.assetid: fa6ed4ff-334a-4d99-b5e2-a1f83d2b3008
ms.topic: overview
ms.openlocfilehash: 3d82ac4569e06a4472047a79da60032ad2db43ca
ms.sourcegitcommit: 8e285a766523e653aeeb34d412dc6f615ef7b17b
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/21/2020
ms.locfileid: "80078468"
---
# <a name="cc-projects-and-build-systems-in-visual-studio"></a>Visual Studio 'da C/C++ projeleri ve derleme sistemleri

Visual Studio 'Yu, bu kodu Visual Studio projesine dönüştürmek veya MSVC araç kümesi ile derlemek zorunda kalmadan tam IntelliSense desteğiyle herhangi bir C++ kod tabanını düzenlemek, derlemek ve derlemek için kullanabilirsiniz. Örneğin, Visual Studio 'da bir platformlar arası CMake projesini bir Windows makinesinde düzenleyebilir ve ardından uzak bir Linux makinesinde g + + kullanarak Linux için derleyebilirsiniz.

## <a name="c-compilation"></a>C++ derlemesi

Bir C++ programı *oluşturmak* için, kaynak kodu bir veya daha fazla dosyadan derleyip sonra bu dosyaları yürütülebilir bir dosyaya (. exe), dinamik yükleme kitaplığı (. dll) veya statik kitaplık (. lib) ile bağlantılandırın.

Temel C++ derlemesi üç ana adımdan oluşur:

- C++ Önişlemci, her kaynak dosyadaki tüm #directives ve Makro tanımlarını dönüştürür. Bu bir *çeviri birimi*oluşturur.
- C++ derleyicisi her bir çeviri birimini, her bir derleyici seçeneğinin ayarlandığı nesne dosyalarına (. obj) derler.
- *Bağlayıcı* , nesne dosyalarını, ayarlanmış bağlayıcı seçeneklerini uygulayarak tek bir yürütülebilirde birleştirir.

## <a name="the-msvc-toolset"></a>MSVC araç takımı

Microsoft C++ derleyicisi, bağlayıcı, standart kitaplıklar ve ilgili yardımcı programlar, MSVC derleyici araç takımını (araç zinciri veya "derleme araçları" olarak da bilinir) oluşturur. Bunlar Visual Studio 'Ya dahildir. Ayrıca, araç takımını [Visual Studio 2019 indirme konumu Için derleme araçları](https://visualstudio.microsoft.com/downloads/#build-tools-for-visual-studio-2019)' ndan ücretsiz bir paket olarak indirebilir ve kullanabilirsiniz.

MSVC derleyicisini (CL. exe) doğrudan komut satırından çağırarak basit programlar oluşturabilirsiniz. Aşağıdaki komut, tek bir kaynak kod dosyasını kabul eder ve *Hello.* exe adlı bir yürütülebilir dosya oluşturmak için CL. exe ' yi çağırır:

```cmd
cl /EHsc hello.cpp
```

Burada derleyicinin (CL. exe), son çıktı dosyasını oluşturmak için C++ Önişlemci ve bağlayıcı için otomatik olarak çağırdığını unutmayın.  Daha fazla bilgi için, bkz. [komut satırı üzerinde oluşturma](building-on-the-command-line.md).

## <a name="build-systems-and-projects"></a>Yapı sistemleri ve projeler

Çoğu gerçek dünyada, birden çok yapılandırma (örneğin, hata ayıklama vs. sürüm), birden çok platform (x86, x64, ARM, vb.), özel derleme adımları ve hatta belirli bir sırada derlenmesi gereken birden çok yürütülebilir dosya için birden çok kaynak dosyası derleme karmaşıklıklarını yönetmek üzere bir tür *derleme sistemi* kullanır. Bir yapı yapılandırma dosyasında ayarları yaparsınız ve derleme sistemi bu dosyayı derleyicinin çağrılmadan önce girdi olarak kabul eder. Yürütülebilir dosya oluşturmak için gereken kaynak kodu dosyaları ve yapı yapılandırma dosyaları kümesi *Proje*olarak adlandırılır.

Aşağıdaki listede Visual Studio projeleri için çeşitli seçenekler gösterilmektedir-C++:

- Visual Studio IDE 'yi kullanarak Visual Studio projesi oluşturun ve özellik sayfalarını kullanarak yapılandırın. Visual Studio projeleri, Windows üzerinde çalışan programlar oluşturur. Genel bakış için bkz. Visual Studio belgelerinde [derleme ve oluşturma](/visualstudio/ide/compiling-and-building-in-visual-studio) .

- CMakeLists. txt dosyasını içeren bir klasör açın. CMake desteği Visual Studio ile tümleşiktir. CMake dosyalarını dilediğiniz şekilde değiştirmeden düzenlemek, test etmek ve hatalarını ayıklamak için IDE 'yi kullanabilirsiniz. Bu, farklı düzenleyiciler kullanıyor olabilecek diğer kullanıcılarla aynı CMake projesinde çalışmanıza olanak sağlar. CMake, platformlar arası geliştirme için önerilen yaklaşımdır. Daha fazla bilgi için bkz. [CMake projeleri](cmake-projects-in-visual-studio.md).

- Proje dosyası olmayan, kaynak dosyalarının gevşek bir klasörünü açın. Visual Studio, dosyaları derlemek için buluşsal yöntemler kullanır. Bu, küçük Konsol uygulamalarını derlemek ve çalıştırmak için kolay bir yoldur. Daha fazla bilgi için bkz. [klasör projelerini açma](open-folder-projects-cpp.md).

- derleme görevleri dosyası veya başka bir yapı sistemi yapılandırma dosyası içeren bir klasörü açın. Visual Studio 'Yu, JSON dosyalarını klasöre ekleyerek herhangi bir rastgele derleme komutunu çağırmak üzere yapılandırabilirsiniz. Daha fazla bilgi için bkz. [klasör projelerini açma](open-folder-projects-cpp.md).

- Visual Studio 'da bir Windows derleme görevleri dosyası açın. Daha fazla bilgi için bkz. [NMAKE Başvurusu](reference/nmake-reference.md).

## <a name="msbuild-from-the-command-line"></a>Komut satırından MSBuild

Komut satırı seçenekleriyle birlikte bir. vcxproj dosyası geçirerek, komut satırından MSBuild 'i çağırabilirsiniz. Bu yaklaşım MSBuild 'in iyi bir şekilde anlaşılmasına gerek duyar ve yalnızca kesinlikle gerekli olduğunda önerilir. Daha fazla bilgi için bkz. [MSBuild](msbuild-visual-cpp.md).

## <a name="in-this-section"></a>Bu Bölümde

[Visual Studio projeleri](creating-and-managing-visual-cpp-projects.md) Visual Studio 'da kendi yerel yapı sistemini (MSBuild) kullanarak C++ projeleri oluşturma, yapılandırma ve derleme.

[CMake projeleri](cmake-projects-in-visual-studio.md) Visual Studio 'da CMake projelerini kodlama, derleme ve dağıtma.

[Klasör projelerini aç](open-folder-projects-cpp.md) Visual Studio 'Yu kullanarak, herhangi bir rastgele derleme sistemine veya hiçbir derleme sistemine göre C++ projelerini nasıl kod, derlemek ve dağıtacağınızı öğrenin. Asla.

[Yayın yapıları](release-builds.md) Son kullanıcılara dağıtım için iyileştirilmiş yayın derlemeleri oluşturma ve sorunlarını giderme.

[Komut satırından MSVC araç takımını kullanma](building-on-the-command-line.md)<br/>
Visual Studio IDE kullanmak yerine C/C++ derleyicisinin ve doğrudan komut satırından derleme araçlarının nasıl kullanılacağını açıklar.

[Visual Studio 'Da dll 'Leri derleme](dlls-in-visual-cpp.md) Visual Studio 'da C/C++ dll 'Leri (paylaşılan kitaplıklar) oluşturma, hata ayıklama ve dağıtma.

[Izlenecek yol: statik kitaplık oluşturma ve kullanma](walkthrough-creating-and-using-a-static-library-cpp.md) . Lib ikili dosyası oluşturma.

[C/C++ yalıtılmış uygulamaları ve yan yana derlemeler oluşturma](building-c-cpp-isolated-applications-and-side-by-side-assemblies.md) Yalıtılmış uygulamaların ve yan yana derlemelerin fikrini temel alarak Windows Masaüstü uygulamaları için dağıtım modelini açıklar.

[64 bit, x64 hedefleri Için C++ projelerini yapılandırma](configuring-programs-for-64-bit-visual-cpp.md) MSVC derleme araçlarıyla 64 bitlik x64 donanımını hedefleme.

[ARM İşlemcileri Için C++ projelerini yapılandırma](configuring-programs-for-arm-processors-visual-cpp.md) ARM donanımını hedeflemek için MSVC derleme araçlarını kullanma.

[Kodunuzu iyileştirme](optimizing-your-code.md) Programın Kılavuzlu iyileştirmeler dahil çeşitli yollarla kodunuzu en iyi duruma getirme.

[WINDOWS XP Için programları yapılandırma](configuring-programs-for-windows-xp.md) Windows XP 'yi MSVC derleme araçlarıyla hedefleme.

[C/C++ Oluşturma Başvurusu](reference/c-cpp-building-reference.md)<br/>
C++, derleyici ve bağlayıcı seçenekleri ve çeşitli yapı araçları ile program oluşturma hakkında başvuru makalelerine bağlantılar sağlar.
