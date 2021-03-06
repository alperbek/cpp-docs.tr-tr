---
title: /cgthreads (Kod Oluşturma İş Parçacıkları)
ms.date: 11/04/2016
f1_keywords:
- /cgthreads
helpviewer_keywords:
- /cgthreads compiler option (C++)
- -cgthreads compiler option (C++)
- cgthreads compiler option (C++)
- cgthreads
ms.assetid: 64bc768c-6caa-4baf-9dea-7cfa1ffb01c2
ms.openlocfilehash: df353eb255c731478863ed6088cafa1cc38053fb
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62294700"
---
# <a name="cgthreads-code-generation-threads"></a>/cgthreads (Kod Oluşturma İş Parçacıkları)

En iyi duruma getirme ve kod oluşturma için kullanılacak cl.exe iş parçacığı sayısını ayarlar.

## <a name="syntax"></a>Sözdizimi

```
/cgthreads[1-8]
```

## <a name="arguments"></a>Arguments

*Sayı*<br/>
Cl.exe kullanılacak aralığı 1-8 iş parçacığı sayısı.

## <a name="remarks"></a>Açıklamalar

**/Cgthreads** seçeneği, iş parçacıkları cl.exe sayısı kullanır paralel olarak kod ve iyileştirme için derleme aşamaları nesil belirtir. Arasında boşluk olabilir fark **/cgthreads** ve `number` bağımsız değişken. Varsayılan olarak, dört iş parçacığı cl.exe kullanır gibi **/cgthreads4** belirtildi. Daha fazla işlemci çekirdek varsa, daha büyük bir `number` değer oluşturma sürelerini geliştirebilir. İle birlikte kullanıldığında bu seçenek özellikle yararlıdır [/GL (bütün Program iyileştirmesi)](gl-whole-program-optimization.md).

Paralellik derecesi birden çok düzeyi için bir derleme belirtilebilir. Msbuild.exe anahtar **/maxcpucount** paralel olarak çalıştırılabilir MSBuild işlem sayısını belirtir. [/MP (birden çok süreçle derleme)](mp-build-with-multiple-processes.md) derleyici bayrağı aynı anda kaynak dosyaları derleme cl.exe işlem sayısını belirtir. **/Cgthreads** seçeneği her cl.exe işlemi tarafından kullanılan iş parçacıklarının sayısını belirtir. İşlemci yalnızca işlemci çekirdeği olduğu gibi birçok iş parçacığı aynı anda çalıştırılabildiği için bu seçeneklerin tümü, daha büyük değerler aynı anda belirtmek kullanışlı değildir ve ters etki olabilir. Paralel olarak proje oluşturma hakkında daha fazla bilgi için bkz. [paralel birden çok proje oluşturma](/visualstudio/msbuild/building-multiple-projects-in-parallel-with-msbuild).

### <a name="to-set-this-compiler-option-in-the-visual-studio-development-environment"></a>Bu derleyici seçeneğini Visual Studio geliştirme ortamında ayarlamak için

1. Projenin açın **özellik sayfaları** iletişim kutusu. Ayrıntılar için bkz [Visual Studio'da ayarlayın C++ derleyicisi ve derleme özellikleri](../working-with-project-properties.md).

1. Seçin **yapılandırma özellikleri**, **C/C++** klasör.

1. Seçin **komut satırı** özellik sayfası.

1. Değiştirme **ek seçenekler** eklenecek özellik **/cgthreads**`N`burada `N` 8 ile 1 arasında bir değer olan ve ardından **Tamam**.

### <a name="to-set-this-compiler-option-programmatically"></a>Bu derleyici seçeneğini program üzerinden ayarlamak için

- Bkz. <xref:Microsoft.VisualStudio.VCProjectEngine.VCCLCompilerTool.AdditionalOptions%2A>.

## <a name="see-also"></a>Ayrıca bkz.

[MSVC Derleyicisi Seçenekleri](compiler-options.md)<br/>
[MSVC Derleyicisi Komut Satırı Söz Dizimi](compiler-command-line-syntax.md)
