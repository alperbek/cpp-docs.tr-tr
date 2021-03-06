---
title: /Gw (Genel Verileri En İyileştir)
ms.date: 11/04/2016
f1_keywords:
- /Gw
helpviewer_keywords:
- /Gw compiler option [C++]
- -Gw compiler option [C++]
ms.assetid: 6f90f4e9-5eb8-4c47-886e-631278a5a4a9
ms.openlocfilehash: 8afdb21defbbc8309b27749ab18a40f9555139e5
ms.sourcegitcommit: 28eae422049ac3381c6b1206664455dbb56cbfb6
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66450142"
---
# <a name="gw-optimize-global-data"></a>/Gw (Genel Verileri En İyileştir)

COMDAT bölümleri için en iyi duruma getirme genel veri paketi.

## <a name="syntax"></a>Sözdizimi

```
/Gw[-]
```

## <a name="remarks"></a>Açıklamalar

**/Gw** seçeneği COMDAT bölümleri tek tek Paket genel veri derleyicinin neden olur. Varsayılan olarak, **/Gw** kapalıdır ve açıkça etkinleştirilmesi gerekir. Açıkça devre dışı bırakmak için kullanın **/Gw-** . Her ikisi de **/Gw** ve [/GL](gl-whole-program-optimization.md) olan etkin bağlayıcı bütün program iyileştirmesi COMDAT bölümler arasında birden çok nesne dosyaları başvurulmayan genel verileri dışlamak için veya birleştirmek için karşılaştırılacak kullanır aynı salt okunur genel veriler. Bu, sonuçta elde edilen ikili yürütülebilir boyutunu önemli ölçüde azaltabilir.

Derleme ve ayrı ayrı bağlantı kullanabilirsiniz [/OPT: ref](opt-optimizations.md) bağlayıcı seçeneği ile derlenmiş nesne dosyaları başvurulmayan genel verilerde yürütülebilir dışlanacak **/Gw** seçeneği.

Ayrıca [/OPT: ICF](opt-optimizations.md) ve [/LTCG](ltcg-link-time-code-generation.md) herhangi aynı salt okunur genel verilerde birden çok nesne dosyaları ile derlenmiş çalıştırılabilir dosyada birleştirmek için bağlayıcı seçenekleri **/Gw** seçeneği.

Daha fazla bilgi için [/Gw derleyici anahtarı ile tanışın](https://devblogs.microsoft.com/cppblog/introducing-gw-compiler-switch/) üzerinde C++ ekibi blogu.

### <a name="to-set-this-compiler-option-in-the-visual-studio-development-environment"></a>Bu derleyici seçeneğini Visual Studio geliştirme ortamında ayarlamak için

1. Projenin açın **özellik sayfaları** iletişim kutusu. Ayrıntılar için bkz [Visual Studio'da ayarlayın C++ derleyicisi ve derleme özellikleri](../working-with-project-properties.md).

1. Seçin **C/C++** klasör.

1. Seçin **komut satırı** özellik sayfası.

1. Değiştirme **ek seçenekler** eklenecek özellik **/Gw** seçip **Tamam**.

### <a name="to-set-this-compiler-option-programmatically"></a>Bu derleyici seçeneğini program üzerinden ayarlamak için

- Bkz. <xref:Microsoft.VisualStudio.VCProjectEngine.VCCLCompilerTool.AdditionalOptions%2A>.

## <a name="see-also"></a>Ayrıca bkz.

[MSVC Derleyicisi Seçenekleri](compiler-options.md)<br/>
[MSVC Derleyicisi Komut Satırı Söz Dizimi](compiler-command-line-syntax.md)
