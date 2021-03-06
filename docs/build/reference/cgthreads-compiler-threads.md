---
title: /CGTHREADS (Derleyici İş Parçacıkları)
ms.date: 11/04/2016
helpviewer_keywords:
- /CGTHREADS linker option
- -CGTHREADS linker option
- CGTHREADS linker option
ms.assetid: 4b52cfdb-3702-470b-9580-fabeb1417488
ms.openlocfilehash: b778802d3fffcaafc0cf01ac46ae85c4efbef95c
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62294674"
---
# <a name="cgthreads-compiler-threads"></a>/CGTHREADS (Derleyici İş Parçacıkları)

Bağlama sırasında kod oluşturma belirtildiği zaman iyileştirme ve kod oluşturma için kullanılacak cl.exe iş parçacığı sayısını ayarlar.

## <a name="syntax"></a>Sözdizimi

```
/CGTHREADS:[1-8]
```

## <a name="arguments"></a>Arguments

*Sayı*<br/>
Cl.exe kullanılacak aralığı 1-8 iş parçacığı sayısı.

## <a name="remarks"></a>Açıklamalar

**/Cgthreads** seçeneği paralel olarak cl.exe kullandığı iş parçacığı sayısı için derleme bağlama sırasında zaman iyileştirme ve kod üretimi aşamaları belirtir kod oluşturma ([/LTCG](ltcg-link-time-code-generation.md)) olan Belirtilen. Varsayılan olarak, dört iş parçacığı cl.exe kullanır gibi **/CGTHREADS:4** belirtildi. Daha fazla işlemci çekirdek varsa, daha büyük bir `number` değer oluşturma sürelerini geliştirebilir.

Paralellik derecesi birden çok düzeyi için bir derleme belirtilebilir. Msbuild.exe anahtar **/maxcpucount** paralel olarak çalıştırılabilir MSBuild işlem sayısını belirtir. [/MP (birden çok süreçle derleme)](mp-build-with-multiple-processes.md) derleyici bayrağı aynı anda kaynak dosyaları derleme cl.exe işlem sayısını belirtir. [/Cgthreads](cgthreads-code-generation-threads.md) derleyici seçeneği her cl.exe işlemi tarafından kullanılan iş parçacıklarının sayısını belirtir. İşlemci yalnızca işlemci çekirdeği olduğu gibi birçok iş parçacığı aynı anda çalıştırılabildiği için bu seçeneklerin tümü, daha büyük değerler aynı anda belirtmek kullanışlı değildir ve ters etki olabilir. Paralel olarak proje oluşturma hakkında daha fazla bilgi için bkz. [paralel birden çok proje oluşturma](/visualstudio/msbuild/building-multiple-projects-in-parallel-with-msbuild).

### <a name="to-set-this-linker-option-in-the-visual-studio-development-environment"></a>Visual Studio geliştirme ortamındaki bu bağlayıcı seçeneğini ayarlamak için

1. Projenin açın **özellik sayfaları** iletişim kutusu. Ayrıntılar için bkz [Visual Studio'da ayarlayın C++ derleyicisi ve derleme özellikleri](../working-with-project-properties.md).

1. Seçin **yapılandırma özellikleri**, **bağlayıcı** klasör.

1. Seçin **komut satırı** özellik sayfası.

1. Değiştirme **ek seçenekler** eklenecek özellik **/cgthreads:**`number`burada `number` 8 ile 1 arasında bir değer olan ve ardından **Tamam**.

### <a name="to-set-this-linker-option-programmatically"></a>Bu bağlayıcı seçeneğini program aracılığıyla ayarlamak için

- Bkz. <xref:Microsoft.VisualStudio.VCProjectEngine.VCLinkerTool.AdditionalOptions%2A>.

## <a name="see-also"></a>Ayrıca bkz.

[MSVC Bağlayıcı Seçenekleri](linker-options.md)<br/>
[MSVC bağlayıcı başvurusu](linking.md)
