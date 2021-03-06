---
title: /BASE (Temel Adres)
ms.date: 09/05/2018
f1_keywords:
- /base
- VC.Project.VCLinkerTool.BaseAddress
helpviewer_keywords:
- base addresses [C++]
- programs [C++], preventing relocation
- semicolon [C++], specifier
- -BASE linker option
- key address size
- environment variables [C++], LIB
- programs [C++], base address
- LIB environment variable
- BASE linker option
- DLLs [C++], linking
- /BASE linker option
- '@ symbol for base address'
- executable files [C++], base address
- at sign symbol for base address
ms.assetid: 00b9f6fe-0bd2-4772-a69c-7365eb199069
ms.openlocfilehash: dc6380903af0be2e6696ca3589813c249f71dd05
ms.sourcegitcommit: c6f8e6c2daec40ff4effd8ca99a7014a3b41ef33
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/24/2019
ms.locfileid: "64341019"
---
# <a name="base-base-address"></a>/BASE (Temel Adres)

Bir program için temel adresini belirtir.

## <a name="syntax"></a>Sözdizimi

> **/ BASE:**{*adresi*[**,**<em>boyutu</em>] | **\@** <em>filename</em>**,**<em>anahtar</em>}

## <a name="remarks"></a>Açıklamalar

> [!NOTE]
> Güvenlik nedenleriyle, Microsoft, kullanmanızı önerir [dynamıcbase](dynamicbase-use-address-space-layout-randomization.md) , yürütülebilir dosyalar için temel adresler belirtmek yerine seçeneği. Bu rastgele yükleme zamanında Windows'ın adres alanı düzenini (ASLR) rastgele özelliği temellendirilebilen bir yürütülebilir görüntü oluşturur. Dynamıcbase seçeneği varsayılan olarak açıktır.

/ Temel seçeneği, .exe veya DLL dosyasının varsayılan konumunu geçersiz kılma program için temel adres ayarlar. Bir .exe dosyası için varsayılan taban adresi 32-bit görüntüleri 0x400000 veya 64-bit görüntüleri 0x140000000 ' dir. Bir DLL için varsayılan taban 0x10000000 32-bit görüntüleri veya 64-bit görüntüleri 0x180000000 adresidir. İşletim rastgele adres alanı düzenini (ASLR) desteklemez veya taban seçeneği ayarlandığında sistemlerinde işletim sistemi programı, belirtilen veya varsayılan taban adresi yüklemek önce çalışır. Sistem, yeterli alan yok kullanılabilir değilse, programın yeniden yerleştirir. Yeniden konumlandırma önlemek için [/FIXED](fixed-fixed-base-address.md) seçeneği.

Bağlayıcı hata durumunda sorunları *adresi* 64 k katı değil. İsteğe bağlı olarak, program boyutunu belirtebilirsiniz; program, belirtilen boyutta sığdıramazsanız bağlayıcı bir uyarı verir.

Komut satırında temel adresini belirtmek için başka bir temel adres bir yanıt dosyası kullanarak yoludur. Temel adres bir yanıt dosyası temel adresler ve isteğe bağlı boyutları programınızı kullanacağınız tüm DLL'ler ve her bir temel adres için benzersiz bir metin anahtarı içeren bir metin dosyasıdır. Temel adres bir yanıt dosyası kullanarak belirtmek için kullanın bir at işareti (**\@**) yanıt dosya adından önce gelen *filename*, bir virgül tarafından izlenen sonra *anahtarı*dosyasında kullanılacak temel adres için değer. Bağlayıcı arar *filename* ya da belirtilen yolda veya hiçbir yol belirtilmezse LIB ortam değişkeninde belirtilen dizinlerde. Her satırda *filename* bir DLL temsil eder ve sözdizimi aşağıdaki gibidir:

> *anahtar* *adresi* [*boyutu*] **;** *açıklaması*

*Anahtar* alfasayısal karakterden oluşan bir dizedir ve büyük/küçük harfe duyarlı değildir. Bu genellikle bir DLL'nin adıdır, ancak olmaması. *Anahtarı* temel tarafından izlenen *adresi* C dili, onaltılık veya ondalık gösterim ve isteğe bağlı bir maksimum *boyutu*. Tüm üç bağımsız değişken, boşluk veya sekme tarafından ayrılır. Bağlayıcı, yalnızca bir uyarı verir belirtilen *boyutu* program tarafından gereken sanal adres alanı'dan küçük. A *yorum* noktalı virgül belirtilirse (**;**) ve aynı ya da ayrı bir satır üzerinde olabilir. Bağlayıcı satırın sonuna noktalı virgülden tüm metni yok sayar. Bu örnekte, böyle bir dosya parçası gösterilmiştir:

```
main   0x00010000    0x08000000    ; for PROJECT.exe
one    0x28000000    0x00100000    ; for DLLONE.DLL
two    0x28100000    0x00300000    ; for DLLTWO.DLL
```

Bu satırlar içeren dosyanın DLLS.txt çağrılırsa, bu bilgiler aşağıdaki örnekte komut geçerlidir:

```
link dlltwo.obj /dll /base:@dlls.txt,two
```

Temel adresi ayarlamak için başka bir yolu kullanmaktır *temel* bağımsız değişkeni olarak bir [adı](name-c-cpp.md) veya [Kitaplığı](library.md) deyimi. / Base ve [/dll](dll-build-a-dll.md) seçenekler birbirine eşit **Kitaplığı** deyimi.

### <a name="to-set-this-linker-option-in-the-visual-studio-development-environment"></a>Visual Studio geliştirme ortamındaki bu bağlayıcı seçeneğini ayarlamak için

1. Projenin açın **özellik sayfaları** iletişim kutusu. Ayrıntılar için bkz [Visual Studio'da ayarlayın C++ derleyicisi ve derleme özellikleri](../working-with-project-properties.md).

1. Seçin **yapılandırma özellikleri** > **bağlayıcı** > **Gelişmiş** özellik sayfası.

1. Değiştirme **temel adresi** özelliği.

### <a name="to-set-this-linker-option-programmatically"></a>Bu bağlayıcı seçeneğini program aracılığıyla ayarlamak için

- Bkz. <xref:Microsoft.VisualStudio.VCProjectEngine.VCLinkerTool.BaseAddress%2A>.

## <a name="see-also"></a>Ayrıca bkz.

[MSVC bağlayıcı başvurusu](linking.md)<br/>
[MSVC Bağlayıcı Seçenekleri](linker-options.md)
