---
title: Yerel Masaüstü Uygulamaları Dağıtma (Visual C++)
ms.date: 05/11/2018
helpviewer_keywords:
- deploying applications [C++]
- application deployment [C++]
- Visual C++, application deployment
- application deployment [C++], about application deployment
- deploying applications [C++], about deploying applications
- distributing applications [C++]
ms.assetid: 37f1691e-d67c-41e4-926e-528a237a9bac
ms.topic: overview
ms.openlocfilehash: e9ae5db05c0835bb65a65cdccf58ab7f7d1b789f
ms.sourcegitcommit: 857fa6b530224fa6c18675138043aba9aa0619fb
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/24/2020
ms.locfileid: "80160196"
---
# <a name="deploying-native-desktop-applications-visual-c"></a>Yerel Masaüstü Uygulamaları Dağıtma (Visual C++)

Dağıtım, başka bilgisayarlara yüklenmek üzere tamamlanmış bir uygulamayı veya bileşeni dağıttığınız bir işlemdir. Dağıtım planlama, bir uygulamanın geliştirici bilgisayarında oluşturulması durumunda başlatılır. Dağıtım, uygulama yüklendiğinde ve kullanıcının bilgisayarında çalışmaya hazırsa sona erer.

Visual Studio, Windows uygulamalarını dağıtmak için farklı teknolojiler sağlar. Bunlara ClickOnce dağıtımı ve Windows Installer dağıtımı dahildir.

- ClickOnce, ortak dil çalışma zamanı C++ (CLR) (karışık, saf ve Doğrulanabilen Derlemeler) hedefleyen uygulamaları dağıtmak için kullanılabilir. Yönetilen bir uygulama dağıtmak için Windows Installer kullanabilseniz de, bildirim imzalama gibi .NET Framework güvenlik özelliklerinden yararlandığından ClickOnce kullanmanızı öneririz. ClickOnce yerel C++ uygulamaların dağıtımını desteklemez. Daha fazla bilgi için bkz. [Visual C++ uygulamaları için ClickOnce dağıtımı](clickonce-deployment-for-visual-cpp-applications.md).

- Windows Installer teknolojisi, CLR 'yi hedefleyen yerel C++ uygulamaları veya C++ uygulamaları dağıtmak için kullanılabilir.

Belgelerinin bu bölümündeki makaleler, yerel bir görsel C++ uygulamanın desteklenen bir hedef platform sağlayan herhangi bir bilgisayarda çalıştığını, bir yükleme paketine hangi dosyaların ekleneceğini ve uygulamanızın bağımlı olduğu bileşenleri yeniden dağıtmak için önerilen yolları ele alır.

## <a name="in-this-section"></a>Bu Bölümde

- [Visual C++ üzerinde Dağıtım](deployment-in-visual-cpp.md)

- [Dağıtım Kavramları](deployment-concepts.md)

- [Visual C++ Uygulaması Bağımlılıklarını Anlama](understanding-the-dependencies-of-a-visual-cpp-application.md)

- [Hangi DLL'lerin Yeniden Dağıtılacağını Belirleme](determining-which-dlls-to-redistribute.md)

- [Dağıtım Yöntemi Seçme](choosing-a-deployment-method.md)

- [Evrensel CRT dağıtımı](universal-crt-deployment.md).

- [Visual C++ Dosyalarını Yeniden Dağıtma](redistributing-visual-cpp-files.md)

- [Dağıtım Örnekleri](deployment-examples.md)

- [Web İstemcisi Uygulamalarını Yeniden Dağıtma](redistributing-web-client-applications.md)

- [Visual C++ Uygulamaları için ClickOnce Dağıtımı](clickonce-deployment-for-visual-cpp-applications.md)

- [Önceki çalışma C++ zamanı sürümünde/CLR uygulaması çalıştırma](running-a-cpp-clr-application-on-a-previous-runtime-version.md)

## <a name="related-sections"></a>İlgili Bölümler

- [C/C++ Yalıtılmış Uygulamaları ve Yan Yana Derlemeleri Oluşturma](../build/building-c-cpp-isolated-applications-and-side-by-side-assemblies.md)

- [Dağıtım](/dotnet/framework/deployment/index)

- [C/C++ Yalıtılmış Uygulamalar ve Yan Yana Derlemeler ile İlgili Sorunları Giderme](../build/troubleshooting-c-cpp-isolated-applications-and-side-by-side-assemblies.md)
