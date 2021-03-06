---
title: /DELAYSIGN (Derlemeyi Kısmen İmzala)
ms.date: 11/04/2016
f1_keywords:
- /delaysign
- VC.Project.VCLinkerTool.DelaySign
helpviewer_keywords:
- /DELAYSIGN linker option
- DELAYSIGN linker option
- -DELAYSIGN linker option
ms.assetid: 15244d30-3ecb-492f-a408-ffe81f38de20
ms.openlocfilehash: 65585b856627ad9fda5a8f8bfad6ad81fef0f81c
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62293842"
---
# <a name="delaysign-partially-sign-an-assembly"></a>/DELAYSIGN (Derlemeyi Kısmen İmzala)

```
/DELAYSIGN[:NO]
```

## <a name="arguments"></a>Arguments

**YOK**<br/>
Derleme olmayan kısmen imzalanması gerektiğini belirtir.

## <a name="remarks"></a>Açıklamalar

Kullanım **/delaysign** yalnızca derleme içinde ortak anahtar yerleştirmek istiyorsanız. Varsayılan değer **delaysıgn: No**.

**/Delaysign** seçeneği ile birlikte kullanılmadığı sürece hiçbir etkiye sahiptir [/keyfile](keyfile-specify-key-or-key-pair-to-sign-an-assembly.md) veya [/keycontainer](keycontainer-specify-a-key-container-to-sign-an-assembly.md).

Tam imzalı bir derleme istediğinizde; derleyici bildirimi (derleme meta verileri) içeren ve karmayı özel anahtarla imzalar dosyayı karma hale getirir. Elde edilen dijital imza, bildirimi içeren dosyada depolanır. Bir derlemeyi gecikmeli imzalanmış olduğunda, bağlayıcı işlem değil ve daha sonra imzanın eklenmesi için dosyada depolamak imzaya ancak ayırır.

Örneğin, kullanarak **/delaysign** derlemeyi genel önbellek üzerine koymasına olanak sağlar. Test edildikten sonra özel anahtarı derlemeye koyarak derlemenin tam olarak oturum açabilirsiniz.

Bkz: [tanımlayıcı ad derlemeleri (derleme imzalama) (C++/CLI)](../../dotnet/strong-name-assemblies-assembly-signing-cpp-cli.md) ve [derlemeyi imzalamayı geciktirme](/dotnet/framework/app-domains/delay-sign-assembly) derleme imzalama hakkında daha fazla bilgi.

Bütünleştirilmiş kod oluşturmayı etkileyen diğer bağlayıcı seçenekleri şunlardır:

- [/ ASSEMBLYDEBUG](assemblydebug-add-debuggableattribute.md)

- [/ ASSEMBLYLINKRESOURCE](assemblylinkresource-link-to-dotnet-framework-resource.md)

- [/ ASSEMBLYMODULE](assemblymodule-add-a-msil-module-to-the-assembly.md)

- [/ ASSEMBLYRESOURCE](assemblyresource-embed-a-managed-resource.md)

- [/ NOASSEMBLY](noassembly-create-a-msil-module.md)

### <a name="to-set-this-linker-option-in-the-visual-studio-development-environment"></a>Visual Studio geliştirme ortamındaki bu bağlayıcı seçeneğini ayarlamak için

1. Projenin açın **özellik sayfaları** iletişim kutusu. Ayrıntılar için bkz [Visual Studio'da ayarlayın C++ derleyicisi ve derleme özellikleri](../working-with-project-properties.md).

1. Tıklayın **bağlayıcı** klasör.

1. Tıklayın **komut satırı** özellik sayfası.

1. Seçeneğini yazın **ek seçenekler** kutusu.

### <a name="to-set-this-linker-option-programmatically"></a>Bu bağlayıcı seçeneğini program aracılığıyla ayarlamak için

- Bkz. <xref:Microsoft.VisualStudio.VCProjectEngine.VCLinkerTool.AdditionalOptions%2A>.

## <a name="see-also"></a>Ayrıca bkz.

[MSVC bağlayıcı başvurusu](linking.md)<br/>
[MSVC Bağlayıcı Seçenekleri](linker-options.md)
