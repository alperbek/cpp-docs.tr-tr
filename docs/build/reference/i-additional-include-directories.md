---
title: /I (ek içeren dizinler)
ms.date: 11/04/2016
f1_keywords:
- VC.Project.VCCLWCECompilerTool.AdditionalIncludeDirectories
- VC.Project.VCCLCompilerTool.AdditionalIncludeDirectories
- /I
- VC.Project.VCNMakeTool.IncludeSearchPath
helpviewer_keywords:
- /I compiler option [C++]
- Additional Include Directories compiler option
- I compiler option [C++]
- -I compiler option [C++]
- set include directories
- include directories, compiler option [C++]
ms.assetid: 3e9add2a-5ed8-4d15-ad79-5b411e313a49
ms.openlocfilehash: 6ec8b15e77fec5214013c484e617904ed29e8197
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62270148"
---
# <a name="i-additional-include-directories"></a>/I (ek içeren dizinler)

Bir dizin dahil etme dosyaları için Aranan dizinleri listesine ekler.

## <a name="syntax"></a>Sözdizimi

> **/I**[]*dizini*

### <a name="arguments"></a>Arguments

*Dizin*<br/>
Dizinleri listesine eklenecek dizine dahil etme dosyaları için Aranan.

## <a name="remarks"></a>Açıklamalar

Birden fazla dizin eklemek için bu seçeneği birden çok kez kullanın. Yalnızca belirlenen içerme dosyasına bulunana kadar dizinlerde arama yapılır.

Bu seçeneği ile kullanabilirsiniz ([/X (Ignore Standard INCLUDE Paths)](x-ignore-standard-include-paths.md)) seçeneği.

Derleyici, dizinleri şu sırayla arar:

1. Kullanılarak belirtilen bir [#include yönergesi](../../preprocessor/hash-include-directive-c-cpp.md) çift tırnak formunda, onu önce yerel dizinleri arar. İçeren dosyayla aynı dizinde arama başlar **#include** deyimi. Bu dosyayı bulmak başarısız olursa, arama dizinleri şu anda açık açılış ters sırada dosyaları içerir. Arama üst dizininde başlar dosyasını dahil edin ve yukarı doğru devam ederek dosyaları herhangi iki üst dizinleri içerir.

1. Kullanılarak belirtilen bir **#include** yönergesinde açılı ayraç form veya yerel dizin araması başarısız olursa, bunu kullanarak belirtilen dizinleri arar **/I** CL bunları karşılaştığında sırada seçeneği komut satırına.

1. Belirtilen dizinleri **INCLUDE** ortam değişkeni.

### <a name="to-set-this-compiler-option-in-the-visual-studio-development-environment"></a>Bu derleyici seçeneğini Visual Studio geliştirme ortamında ayarlamak için

1. Projenin açın **özellik sayfaları** iletişim kutusu. Ayrıntılar için bkz [Visual Studio'da ayarlayın C++ derleyicisi ve derleme özellikleri](../working-with-project-properties.md).

1. Seçin **yapılandırma özellikleri** > **C/C++** > **genel** özellik sayfası.

1. Değiştirme **ek içerik dizinleri** özelliği.

### <a name="to-set-this-compiler-option-programmatically"></a>Bu derleyici seçeneğini program üzerinden ayarlamak için

- Bkz. <xref:Microsoft.VisualStudio.VCProjectEngine.VCCLCompilerTool.AdditionalIncludeDirectories%2A>.

## <a name="example"></a>Örnek

Aşağıdaki komutu şu sırayla MAIN.c tarafından talep edilen dahil edilme dosyalarını arar: İlk olarak, çift tırnak kullanılarak belirtilen, yerel dosyaları aranır. Ardından, arama içinde \INCLUDE dizini sonra \MY\INCLUDE dizinde devam eder ve son dizinler için Include ortam değişkeni atanmış.

```
CL /I \INCLUDE /I\MY\INCLUDE MAIN.C
```

## <a name="see-also"></a>Ayrıca bkz.

[MSVC Derleyicisi Seçenekleri](compiler-options.md)<br/>
[MSVC Derleyicisi Komut Satırı Söz Dizimi](compiler-command-line-syntax.md)
