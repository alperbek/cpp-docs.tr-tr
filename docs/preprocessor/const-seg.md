---
title: const_seg pragması
ms.date: 08/29/2019
f1_keywords:
- vc-pragma.const_seg
- const_seg_CPP
helpviewer_keywords:
- pragmas, const_seg
- const_seg pragma
ms.assetid: 1eb58ee2-fb0e-4a39-9621-699c8f5ef957
ms.openlocfilehash: 845583889eb922ba97d145eefe6bca280a83817b
ms.sourcegitcommit: 6e1c1822e7bcf3d2ef23eb8fac6465f88743facf
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/03/2019
ms.locfileid: "70220440"
---
# <a name="const_seg-pragma"></a>const_seg pragması

[Const](../cpp/const-cpp.md) değişkenlerinin nesne (. obj) dosyasında depolandığı bölümü (segmenti) belirtir.

## <a name="syntax"></a>Sözdizimi

> **#pragma const_seg (** ["*bölüm-adı*" [ **,** "*bölüm-sınıfı*"]] **)** \
> **#pragma const_seg (** { **Push** | **pop** } [ **,** *tanımlayıcı* ] [ **,** "*bölüm-adı*" [ **,** "*bölüm-sınıfı*"]] **)**

### <a name="parameters"></a>Parametreler

**hareketle**\
Seçim İç derleyici yığınına bir kayıt koyar. **Gönderim** bir *tanımlayıcıya* ve *bölüm adına*sahip olabilir.

**cağımız**\
Seçim İç derleyici yığınının en üstünden bir kaydı kaldırır. Bir **pop** bir *tanımlayıcıya* ve *bölüm adına*sahip olabilir. *Tanımlayıcıyı*kullanarak yalnızca bir **pop** komutu kullanarak birden çok kayıt ekleyebilirsiniz. *Bölüm adı* , pop sonrasında etkin const bölüm adı olur.

*Tanımlayıcısını*\
Seçim **Push**ile kullanıldığında, iç derleyici yığınındaki kayda bir ad atar. Pop ile kullanıldığında, *tanımlayıcı* kaldırılana kadar yönerge, iç yığının içinden **açılır**. İç yığında *tanımlayıcı* bulunmazsa hiçbir şey yapılmadı.

"*bölüm-adı*" \
Seçim Bir bölümün adı. **Pop**ile kullanıldığında, yığın çıkar ve *bölüm adı* etkin const bölüm adı olur.

"*bölüm-sınıfı*" \
Seçim Yoksayıldı, ancak sürüm 2,0 ' den önceki Microsoft C++ sürümleriyle uyumluluk için eklenmiştir.

## <a name="remarks"></a>Açıklamalar

Bir nesne dosyasındaki *bölüm* , bir birim olarak belleğe yüklenen adlandırılmış veri bloğudur. *Const bölümü* , sabit veri içeren bir bölümdür. Bu makalede, koşullar *segmenti* ve *bölümü* aynı anlama sahiptir.

**Const_seg** pragma yönergesi, derleyiciye çeviri biriminden tüm sabit veri öğelerini *bölüm adı*adlı bir const bölümüne koymasını söyler. **Const** değişkenlerinin `.rdata`nesne dosyasındaki varsayılan bölüm. Yapı değerleri gibi bazı **const** değişkenleri, kod akışına otomatik olarak satır içine alınır. Satır içi kod içinde `.rdata`görünmez. *Bölüm adı* parametresi olmayan bir **const_seg** pragma yönergesi, sonraki **const** veri öğelerinin bölüm adını olarak `.rdata`sıfırlar.

Bir `const_seg`içinde dinamik başlatma gerektiren bir nesne tanımlarsanız, sonuç tanımsız bir davranıştır.

Bölüm oluşturmak için kullanılmaması gereken adların bir listesi için, bkz. [/section](../build/reference/section-specify-section-attributes.md).

Başlatılmış veriler ([data_seg](../preprocessor/data-seg.md)), başlatılmamış veriler ([bss_seg](../preprocessor/bss-seg.md)) ve işlevler ([code_seg](../preprocessor/code-seg.md)) için de bölümler belirtebilirsiniz.

Dumpbin ' i kullanabilirsiniz [. ](../build/reference/dumpbin-command-line.md)Nesne dosyalarını görüntülemek IÇIN exe uygulaması. Desteklenen her hedef mimari için DUMPBIN sürümleri Visual Studio 'Ya dahildir.

## <a name="example"></a>Örnek

```cpp
// pragma_directive_const_seg.cpp
// compile with: /EHsc
#include <iostream>

const int i = 7;               // inlined, not stored in .rdata
const char sz1[]= "test1";     // stored in .rdata

#pragma const_seg(".my_data1")
const char sz2[]= "test2";     // stored in .my_data1

#pragma const_seg(push, stack1, ".my_data2")
const char sz3[]= "test3";     // stored in .my_data2

#pragma const_seg(pop, stack1) // pop stack1 from stack
const char sz4[]= "test4";     // stored in .my_data1

int main() {
    using namespace std;
   // const data must be referenced to be put in .obj
   cout << sz1 << endl;
   cout << sz2 << endl;
   cout << sz3 << endl;
   cout << sz4 << endl;
}
```

```Output
test1
test2
test3
test4
```

## <a name="see-also"></a>Ayrıca bkz.

[Pragma yönergeleri ve __pragma anahtar sözcüğü](../preprocessor/pragma-directives-and-the-pragma-keyword.md)
