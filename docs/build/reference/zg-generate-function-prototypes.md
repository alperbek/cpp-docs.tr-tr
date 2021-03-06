---
title: /Zg (İşlev Prototipleri Üret)
ms.date: 11/04/2016
f1_keywords:
- /zg
helpviewer_keywords:
- Zg compiler option [C++]
- /Zg compiler option [C++]
- function prototypes, generate function prototypes compiler option
- -Zg compiler option [C++]
- generate function prototypes compiler option
ms.assetid: c8df1b46-24ff-46f2-8356-e0a144b21dd2
ms.openlocfilehash: 591460b78a461aa2e33f873b79d6dcec0277f99f
ms.sourcegitcommit: 7d64c5f226f925642a25e07498567df8bebb00d4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/08/2019
ms.locfileid: "65446203"
---
# <a name="zg-generate-function-prototypes"></a>/Zg (İşlev Prototipleri Üret)

Kaldırıldı. Kaynak dosyada tanımlanan her işlev için bir işlev prototipi oluşturur, ancak kaynak dosyanın derleme yapmaz.

## <a name="syntax"></a>Sözdizimi

```
/Zg
```

## <a name="remarks"></a>Açıklamalar

Bu derleyici seçeneği artık kullanılabilir. Bu, Visual Studio 2015'te kaldırıldı. Bu sayfa için Visual Studio'nun eski sürümlerini kullanıcılarına kalır.

İşlev prototipi işlev dönüş türü ve bağımsız değişken türü listesi içerir. Bağımsız değişken türü listesi işlevin biçimsel parametreler türlerinden oluşturulur. Kaynak dosyada zaten mevcut herhangi bir işlev prototipleri göz ardı edilir.

Prototipleri listesini standart çıktıya yazılır. Bu liste, gerçek bağımsız değişkenler ve bir işlevin biçimsel parametreler uyumlu olduğunu doğrulamak yararlı bulabilirsiniz. Standart çıkışı bir dosyaya yeniden yönlendirerek listesini kaydedebilirsiniz. Kullanabileceğiniz sonra **#include** işlev prototipleri listesi kaynak dosyanıza bir parçası yapmak için. Bunun yapılması, derleyicinin tür bağımsız değişkeni denetimi gerçekleştirmek neden olur.

Kullanırsanız **/Zg** seçeneği ve programınızı yapısı, enum veya birleşim türü (veya gibi türler için işaretçiler) sahip biçimsel parametre içeriyor, her yapı, enum veya birleşim türü bildirimini (name) bir etiketi olması gerekir. Aşağıdaki örnekte etiket adı olan `MyStruct`.

```C
// Zg_compiler_option.c
// compile with: /Zg
typedef struct MyStruct { int i; } T2;
void f2(T2 * t) {}
```

**/Zg** seçeneği, Visual Studio 2005'te kullanım dışı bırakıldı ve Visual Studio 2015'te kaldırılmıştır. MSVC derleyicisi, eski C stili kod desteğini kaldırmıştır. Kullanım dışı derleyici seçeneklerinin bir listesi için bkz. **kullanım dışı ve derleyici seçenekleri kaldırıldı** içinde [kategoriye göre listelenmiş derleyici seçenekleri](compiler-options-listed-by-category.md).

### <a name="to-set-this-compiler-option-in-the-visual-studio-development-environment"></a>Bu derleyici seçeneğini Visual Studio geliştirme ortamında ayarlamak için

1. Projenin açın **özellik sayfaları** iletişim kutusu. Ayrıntılar için bkz [Visual Studio'da ayarlayın C++ derleyicisi ve derleme özellikleri](../working-with-project-properties.md).

1. Tıklayın **C/C++** klasör.

1. Tıklayın **komut satırı** özellik sayfası.

1. Derleyici seçeneğini yazın **ek seçenekler** kutusu.

### <a name="to-set-this-compiler-option-programmatically"></a>Bu derleyici seçeneğini program üzerinden ayarlamak için

- Bkz. <xref:Microsoft.VisualStudio.VCProjectEngine.VCCLCompilerTool.AdditionalOptions%2A>.

## <a name="see-also"></a>Ayrıca bkz.

[MSVC Derleyicisi Seçenekleri](compiler-options.md)<br/>
[MSVC Derleyicisi Komut Satırı Söz Dizimi](compiler-command-line-syntax.md)
