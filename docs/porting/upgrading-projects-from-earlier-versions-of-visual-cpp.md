---
title: Projeleri C++ Visual Studio 'nun önceki sürümlerinden yükseltme
description: Microsoft C++ projelerini Visual Studio 'nun eski sürümlerinden yükseltme.
ms.date: 01/21/2020
helpviewer_keywords:
- 32-bit code porting
- upgrading Visual C++ applications, 32-bit code
ms.assetid: 18cdacaa-4742-43db-9e4c-2d9e73d8cc84
ms.openlocfilehash: bc9fb5628c1a628b91f306c346f2bbb1dea13de8
ms.sourcegitcommit: 7bea0420d0e476287641edeb33a9d5689a98cb98
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 02/17/2020
ms.locfileid: "77416117"
---
# <a name="upgrade-c-projects-from-earlier-versions-of-visual-studio"></a>Projeleri C++ Visual Studio 'nun önceki sürümlerinden yükseltme

Visual Studio 'nun önceki bir sürümünde oluşturulan bir projeyi yükseltmek için, projeyi Visual Studio 'nun en son sürümünde açmanız yeterlidir. Visual Studio, projeyi geçerli şemaya yükseltmek için teklifler sunar.

**Hayır**' ı seçerseniz, proje yükseltilmez. Visual Studio 2010 ve üzeri sürümlerde oluşturulan projeler için, projeyi Visual Studio 'nun daha yeni bir sürümünde kullanmaya devam edebilirsiniz. Daha eski araç takımını hedefleyecek şekilde, proje özelliklerinizi ayarlamanız yeterlidir. Visual Studio 'nun eski sürümünü bilgisayarınızda bırakırsanız, araç takımı daha sonraki sürümlerde kullanılabilir. Örneğin, projenizin Windows XP 'de çalışmaya devam etmesi gerekiyorsa, Visual Studio 2019 ' e yükseltebilirsiniz. Ardından, proje özelliklerinde araç takımını v141_xp veya daha önceki bir sürümü olarak belirtirsiniz. Daha fazla bilgi için bkz. [Eski projeler oluşturmak Için Visual Studio 'da yerel çoklu sürüm kullanımını kullanma](use-native-multi-targeting.md).

**Evet**' i seçerseniz, proje yerinde yükseltilir. Önceki sürüme geri dönüştürülemez. Yükseltme senaryolarında, mevcut proje ve çözüm dosyalarının yedek bir kopyasını oluşturmak iyi bir uygulamadır.

## <a name="upgrade-reports"></a>Yükseltme raporları

Bir projeyi yükselttiğinizde, bir yükseltme raporu alırsınız. Rapor aynı zamanda proje klasörünüze UpgradeLog. htm olarak kaydedilir. Yükseltme raporu, dönüştürme sırasında hangi sorunların bulunduğu hakkında bir Özet gösterir. Aşağıdakiler de dahil olmak üzere yapılan değişikliklerle ilgili bazı bilgileri listeler:

- Proje özellikleri.

- Dosyaları dahil et.

- Derleyicinin uyumluluk geliştirmeleri veya standart değişiklikler nedeniyle artık düzgün derlenmediği kod.

- Artık kullanılamayan Visual Studio veya Windows özelliklerine dayanan kod. Ya da, varsayılan Visual Studio yüklemesinde yer almayan veya üründen kaldırılmış olan dosyaları üstbilgi.

- Yeniden adlandırılan API 'Ler, değiştirilen işlev imzaları veya kullanım dışı işlevler gibi API 'lerde yapılan değişiklikler nedeniyle artık derlenmediği kod.

- Bir hata haline gelme gibi Tanılamadaki değişiklikler nedeniyle artık derlenmediği kod

- Özellikle/NODEFAULTLIB kullanıldığında değiştirilen kitaplıklar nedeniyle bağlayıcı hataları.

- Davranış değişiklikleri nedeniyle çalışma zamanı hataları veya beklenmedik sonuçlar.

- Araçlarda sunulan hatalar. Bir sorun bulursanız, normal destek kanallarınız aracılığıyla veya C++ [Visual Studio C++ geliştirici topluluğu](https://developercommunity.visualstudio.com/spaces/62/index.html) sayfasını kullanarak görsel ekibe bildirin.

Bazı Yükseltilen projeler ve çözümler değişiklik yapılmadan başarıyla oluşturulabilir. Ancak, çoğu proje muhtemelen proje ayarlarında ve kaynak kodunuzda değişiklik yapılmasını gerektirir. Bu sorunları düzeltmek için tek bir doğru yol yoktur, ancak aşamalı bir yaklaşım kullanmanızı öneririz. Başlamadan önce, çok sayıda yaygın hata hakkında daha fazla bilgi için [olası yükseltme sorunlarının genel bakışını](../porting/overview-of-potential-upgrade-issues-visual-cpp.md) inceleyin.

1. Platform araç takımı, C++ dil standardı ve Windows SDK sürümü (varsa) tercih edilen sürümlere ayarlayın. (**Proje** > **özellikleri** > **yapılandırma özellikleri** > **genel**)

1. Birçok hata varsa, bunları düzelttikten sonra bazı seçenekleri geçici olarak kapatabilirsiniz. [/Permissive-](../build/reference/permissive-standards-conformance.md) seçeneğini devre dışı bırakmak için, **Proje** > **özellikleri** > **yapılandırma özellikleri** > **C/C++**  > **dil**' i kullanın. [Kod Analizi](/cpp/code-quality/code-analysis-for-c-cpp-overview) seçeneğini kapatmak Için, **proje** > **özellikleri** > **yapılandırma özellikleri** > **Kod Analizi**' ni kullanın.

1. Tüm bağımlılıkların mevcut olduğundan ve içerme yollarının veya kitaplık konumlarının doğru olduğundan emin olun. (**Proje** > **özellikleri** > **yapılandırma özellikleri** > **VC + + dizinleri**)

1. Artık mevcut olmayan API başvuruları nedeniyle oluşan hataları tespit edin ve onarın.

1. Derlemeyi engelleyen kalan hataları giderin. Yaygın hatalara yönelik düzeltmeler için [olası yükseltme sorunlarından genel bakış](../porting/overview-of-potential-upgrade-issues-visual-cpp.md) bölümüne bakın.

1. **/Permissive-** yeniden açın ve daha önce MSVC içinde derlenen uyumsuz kodun neden olduğu yeni hataları düzeltin.

1. Artık kabul edilebilir olarak kabul edilen olası sorunları veya geçmiş kodlama düzenlerini belirlemek için kod analizini etkinleştirin. Kod Analizi birçok hatayı işaretleyemdeyse, bazı uyarıları kapatarak öncelikle en önemli öneme sahip olursunuz. IDE, bazı sorun türleri için hızlı düzeltmelerde yardımcı olabilir.

1. Kodu modernize etmek için diğer fırsatları göz önünde bulundurun. Örneğin, özel veri yapılarını ve algoritmaları C++ standart kitaplıktan olanlarla veya açık kaynak kitaplığı 'nı arttırma ile değiştirin. Standart özellikleri kullanarak başkalarının kodu bakımını daha kolay hale getirir. Bu kodun iyi bir şekilde sınanmış ve Standartlar Komitesi ve daha geniş C++ topluluk üzerinde birçok uzman tarafından incelendiğinden emin olabilirsiniz.

Onarma sırasında hatalar için Stack Overflow veya [ C++ geliştirici topluluğu](https://developercommunity.visualstudio.com/spaces/62/index.html)üzerinde bir soruyu aramayı veya göndermeyi deneyin.

## <a name="in-this-section"></a>Bu bölümde

[Olası yükseltme sorunlarına genel bakış](overview-of-potential-upgrade-issues-visual-cpp.md)\
[Kodunuzu UNIVERSAL CRT\ yükseltin](upgrade-your-code-to-the-universal-crt.md)
[WINVER ve _WIN32_WINNT\ güncelleştirme](modifying-winver-and-win32-winnt.md)
[Kitaplık iç yapıları üzerinde bağımlılıklarınızı onarın](fix-your-dependencies-on-library-internals.md)\
[Kayan nokta geçiş sorunları](floating-point-migration-issues.md)\
[Visual Studio 2019 'de kullanım dışı Özellikler\ C++ ](features-deprecated-in-visual-studio.md)
[VCBuild ve MSBuild\ karşılaştırması](build-system-changes.md)
[Bağlantı noktası 3. taraf kitaplıkları](porting-third-party-libraries.md)

## <a name="see-also"></a>Ayrıca bkz.

Visual [Studio 'Daki görsele C++ yönelik](../overview/what-s-new-for-visual-cpp-in-visual-studio.md) yenilikler\
[Görsel C++ değişiklik geçmişi 2003-2015](../porting/visual-cpp-change-history-2003-2015.md)\
[Standart olmayan davranış](../cpp/nonstandard-behavior.md)\
[Bağlantı noktası veri uygulamaları](../data/data-access-programming-mfc-atl.md)
