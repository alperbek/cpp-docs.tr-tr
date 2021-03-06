---
title: /FA, /Fa (Listeleme Dosyası)
ms.date: 11/04/2016
f1_keywords:
- VC.Project.VCCLWCECompilerTool.AssemblerListingLocation
- VC.Project.VCCLCompilerTool.ConfigureASMListing
- VC.Project.VCCLWCECompilerTool.AssemblerOutput
- VC.Project.VCCLCompilerTool.AssemblerListingLocation
- /fa
- VC.Project.VCCLCompilerTool.AssemblerOutput
- VC.Project.VCCLCompilerTool.UseUnicodeForAssemblerListing
helpviewer_keywords:
- FA compiler option [C++]
- /FA compiler option [C++]
- -FA compiler option [C++]
- listing file type
- assembly-only listing
ms.assetid: c7507d0e-c69d-44f9-b8e2-d2c398697402
ms.openlocfilehash: b78704ea12365d9e10222d75c6807517f7cdb893
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62292841"
---
# <a name="fa-fa-listing-file"></a>/FA, /Fa (Listeleme Dosyası)

Derleme kodu içeren bir listeleme dosyası oluşturur.

## <a name="syntax"></a>Sözdizimi

> **/FA**[**c**\][**s**\][**u**] **/Fa**_yol adı_

## <a name="remarks"></a>Açıklamalar

**/FA** derleyici seçeneği, genellikle bir C veya C++ kaynak dosyasına karşılık gelen derleme her çeviri birimi için bir assembler listeleme dosyası oluşturur. Varsayılan olarak, yalnızca assembler ANSI kodlanmış listeleme dosyası dahildir. İsteğe bağlı **c**, **s**, ve **u** bağımsız değişkenleri **/FA** birlikte assembler çıkış denetimi, kod olup olmadığını makine ya da kaynak kodu Listeleme ve listenin UTF-8 kodlanmış olup olmadığı.

Varsayılan olarak, her listeleme dosyası kaynak dosyası olarak aynı temel adlı alır ve bir .asm uzantısına sahiptir. Makine kodu zaman dahil kullanarak **c** seçeneği, listeleme dosyası .cod uzantısı vardır. Adını ve uzantısını listeleme dosyası ve onu oluşturulduğu kullanarak dizini değiştirebilirsiniz **/Fa** seçeneği.

### <a name="fa-arguments"></a>/FA bağımsız değişkenleri

yok<br/>
Yalnızca Çevirici dil listesinde dahil edilir.

**c**<br/>
İsteğe bağlı. Makine kodu listesindeki içerir.

**s**<br/>
İsteğe bağlı. Kaynak kodu listesindeki içerir.

**u**<br/>
İsteğe bağlı. UTF-8 biçiminde listeleme dosyası kodlar ve bayt sırası işareti içerir. Varsayılan olarak, dosya ANSI kodlanır. Kullanım `u` herhangi bir sistemde doğru bir şekilde görüntüleyen bir listeleme dosyası oluşturmak için veya Unicode kullanıyorsanız, kaynak kodu dosyaları derleyici giriş olarak.

Her iki **s** ve **u** belirtilir ve dosya bir kaynak kodu UTF-8, ardından .asm dosyasına kod satırları düzgün görüntülenmeyebilir dışındaki bir Unicode kodlaması kullanır.

### <a name="fa-argument"></a>/FA bağımsız değişken

yok<br/>
Bir *kaynak*.asm dosyasına, her kaynak kodu dosyasında derleme için oluşturulur.

*Dosya adı*<br/>
Adlı bir listeleme dosyası *filename*.asm geçerli dizine yerleştirilir. Bu yalnızca bir tek bir kaynak kodu dosyasını derlerken geçerlidir.

*gt;filename.Extension*<br/>
Adlı bir listeleme dosyası *gt;filename.Extension* geçerli dizine yerleştirilir. Bu yalnızca bir tek bir kaynak kodu dosyasını derlerken geçerlidir.

*Dizin*__\\__<br/>
Bir *$source_file*.asm dosyasına oluşturulur ve belirtilen yerleştirilen *dizin* her kaynak kodu dosyasında derleme için. Gerekli eğik unutmayın. Yalnızca geçerli disk üzerindeki yollara izin verilir.

*Dizin*__\\__*dosya adı*<br/>
Adlı bir listeleme dosyası *filename*.asm yerleştirilir belirtilen *dizin*. Bu yalnızca bir tek bir kaynak kodu dosyasını derlerken geçerlidir.

*Dizin*__\\__*gt;filename.Extension*<br/>
Adlı bir listeleme dosyası *gt;filename.Extension* yerleştirilir belirtilen *dizin*. Bu yalnızca bir tek bir kaynak kodu dosyasını derlerken geçerlidir.

### <a name="to-set-this-compiler-option-in-the-visual-studio-development-environment"></a>Bu derleyici seçeneğini Visual Studio geliştirme ortamında ayarlamak için

1. Projenin açın **özellik sayfaları** iletişim kutusu. Ayrıntılar için bkz [Visual Studio'da ayarlayın C++ derleyicisi ve derleme özellikleri](../working-with-project-properties.md).

1. Seçin **yapılandırma özellikleri** > **C/C++** > **Çıkış dosyalarını** özellik sayfası.

1. Değiştirme **Assembler çıkışı** ayarlamak için özellik **/Fac** ve **/Fas** assembler, makine ve kaynak kodu için Seçenekler. Değiştirme **kullanım listeleme Assembler Unicode için** ayarlamak için özellik **/fau** ANSI ya da UTF-8 çıkışı için seçeneği. Değiştirme **ASM liste konumu** ayarlanacak **/Fa** dosya adını ve konumunu listeleme seçeneği.

Her ikisi de o ayarı unutmayın **Assembler çıkışı** ve **kullanım listeleme Assembler Unicode için** özellikleri açabilir [komut satırı uyarısı D9025](../../error-messages/tool-errors/command-line-warning-d9025.md). IDE'de bu seçenekleri birleştirmek için kullanın **ek seçenekler** alanındaki **komut satırı** özellik sayfasında bunun yerine.

### <a name="to-set-this-compiler-option-programmatically"></a>Bu derleyici seçeneğini program üzerinden ayarlamak için

- Bkz: <xref:Microsoft.VisualStudio.VCProjectEngine.VCCLCompilerTool.AssemblerListingLocation%2A> veya <xref:Microsoft.VisualStudio.VCProjectEngine.VCCLCompilerTool.AssemblerOutput%2A>. Belirtmek için **/fau**, bkz: <xref:Microsoft.VisualStudio.VCProjectEngine.VCCLCompilerTool.AdditionalOptions%2A>.

## <a name="example"></a>Örnek

Aşağıdaki komut satırını birleştirilmiş bir kaynak oluşturur ve makine kod listesi HELLO.cod çağrılır:

```cmd
CL /FAcs HELLO.CPP
```

## <a name="see-also"></a>Ayrıca bkz.

[Çıktı Dosyası (/F) Seçenekleri](output-file-f-options.md)<br/>
[MSVC Derleyicisi Seçenekleri](compiler-options.md)<br/>
[MSVC Derleyicisi Komut Satırı Söz Dizimi](compiler-command-line-syntax.md)<br/>
[Yol Adını Belirtme](specifying-the-pathname.md)
