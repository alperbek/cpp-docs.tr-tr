---
title: /ALLOWBIND (DLL Bağlamayı Önle)
ms.date: 11/04/2016
f1_keywords:
- VC.Project.VCLinkerTool.PreventDLLBinding
- /allowbind
helpviewer_keywords:
- /ALLOWBIND linker option
- binding DLLs
- preventing DLL binding
- ALLOWBIND linker option
- -ALLOWBIND linker option
- DLLs [C++], preventing binding
ms.assetid: 30e37e24-12e4-407e-988a-39d357403598
ms.openlocfilehash: d963a7145ab2e8c8872dc21c485bdc8f877b0b76
ms.sourcegitcommit: fcb48824f9ca24b1f8bd37d647a4d592de1cc925
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/15/2019
ms.locfileid: "69493152"
---
# <a name="allowbind-prevent-dll-binding"></a>/ALLOWBIND (DLL Bağlamayı Önle)

```
/ALLOWBIND[:NO]
```

## <a name="remarks"></a>Açıklamalar

/ALLOWBIND: NO, DLL 'nin üst bilgisinde, görüntünün bağlı olmasına izin verilmediğini belirten bir bit belirler. Dijital olarak imzalanmışsa DLL 'nin bağlanmasını istemeyebilirsiniz (bağlama imzayı geçersiz kılar).

Mevcut bir DLL 'yi, EDITBIN yardımcı programının [/allowbind](allowbind.md) seçeneğiyle birlikte/allowbind işlevselliği için düzenleyebilirsiniz.

### <a name="to-set-this-linker-option-in-the-visual-studio-development-environment"></a>Visual Studio geliştirme ortamındaki bu bağlayıcı seçeneğini ayarlamak için

1. Projenin **Özellik sayfaları** iletişim kutusunu açın. Ayrıntılar için bkz. [Visual C++ Studio 'da derleyici ve derleme özelliklerini ayarlama](../working-with-project-properties.md).

1. **Yapılandırma özellikleri**, **bağlayıcı**ve **komut satırı**Seç ' i genişletin.

1. `/ALLOWBIND:NO` **Ek seçeneklere**girin.

### <a name="to-set-this-linker-option-programmatically"></a>Bu bağlayıcı seçeneğini program aracılığıyla ayarlamak için

- Bkz. <xref:Microsoft.VisualStudio.VCProjectEngine.VCCLCompilerTool.AdditionalOptions%2A>.

## <a name="see-also"></a>Ayrıca bkz.

[MSVC bağlayıcı başvurusu](linking.md)<br/>
[MSVC Bağlayıcı Seçenekleri](linker-options.md)<br/>
[BindImage işlevi](/windows/win32/api/imagehlp/nf-imagehlp-bindimage)<br/>
[BindImageEx işlevi](/windows/win32/api/imagehlp/nf-imagehlp-bindimageex)
