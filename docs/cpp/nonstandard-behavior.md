---
title: Standart Dışı Davranış
ms.date: 05/06/2019
helpviewer_keywords:
- compatibility and compliance, nonstandard behavior
- Microsoft-specific, compiler behavior
- nonstandard behavior, compliance and compatibility
ms.assetid: a57dea27-dc79-4f64-8a83-017e84841773
ms.openlocfilehash: d3bb4ca843833cfe9e027f694f25c989895487bb
ms.sourcegitcommit: 857fa6b530224fa6c18675138043aba9aa0619fb
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/24/2020
ms.locfileid: "80161041"
---
# <a name="nonstandard-behavior"></a>Standart Dışı Davranış

Aşağıdaki bölümlerde, Microsoft uygulamasının C++ , C++ standart ile uyumlu olmadığı yerlerden bazıları listelenmektedir. Aşağıda verilen bölüm numaraları C++ 11 standartındaki (ISO/IEC 14882:2011(E)) bölüm numaralarına başvurur.

C++ Standart içinde tanımlananlardan farklı derleyici limitleri listesi [derleyici sınırları](../cpp/compiler-limits.md)içinde verilmiştir.

## <a name="covariant-return-types"></a>Birlikte Değişken Dönüş Türleri

Sanal işlevde bağımsız değişkenlerin bir değişken sayısı olduğunda, sanal taban sınıfları birlikte değişken dönüş türleri olarak desteklenmez. Bu, ISO C++ belirtimi 10.3 bölümü, paragraf 7 ile uyumlu değildir. Aşağıdaki örnek derlenmiyor, derleyici hatası [C2688](../error-messages/compiler-errors-2/compiler-error-c2688.md)

```cpp
// CovariantReturn.cpp
class A
{
   virtual A* f(int c, ...);   // remove ...
};

class B : virtual A
{
   B* f(int c, ...);   // C2688 remove ...
};
```

## <a name="binding-nondependent-names-in-templates"></a>Şablonlarda Bağımlı Olmayan Adları Bağlama

Microsoft C++ derleyicisi, başlangıçta bir şablonu ayrıştırırken bağımlı olmayan adları bağlamayı desteklememektedir. Bu, C++ ISO belirtiminin 14.6.3 bölümü ile uyumlu değildir. Bu, şablonun görülmesinden sonra (ancak şablon örneği oluşturulmadan önce) aşırı yüklerin bildirilmesine neden olabilir.

```cpp
#include <iostream>
using namespace std;

namespace N {
   void f(int) { cout << "f(int)" << endl;}
}

template <class T> void g(T) {
    N::f('a');   // calls f(char), should call f(int)
}

namespace N {
    void f(char) { cout << "f(char)" << endl;}
}

int main() {
    g('c');
}
// Output: f(char)
```

## <a name="function-exception-specifiers"></a>İşlev Özel Durum Belirleyicileri.

`throw()` dışındaki işlev özel durum belirticileri ayrıştırıldı, ancak kullanılmaz. Bu, ISO C++ belirtiminin 15.4 bölümü ile uyumlu değildir. Örneğin:

```cpp
void f() throw(int); // parsed but not used
void g() throw();    // parsed and used
```

Özel durum belirtimleri hakkında daha fazla bilgi için bkz. [özel durum belirtimleri](../cpp/exception-specifications-throw-cpp.md).

## <a name="char_traitseof"></a>char_traits::eof()

Standart C++ [char_traits:: EOF](../standard-library/char-traits-struct.md#eof) , geçerli bir `char_type` değerine karşılık gelmiyor olmalıdır. Microsoft C++ derleyicisi **char**türü için bu kısıtlamayı uygular, ancak **wchar_t**türü için kullanmaz. Bu, C++ ISO belirtiminin 12.1.1 bölümündeki Tablo 62'deki gereksinimlerle uyumlu değildir. Aşağıdaki örnek bunu gösterir.

```cpp
#include <iostream>

int main()
{
    using namespace std;

    char_traits<char>::int_type int2 = char_traits<char>::eof();
    cout << "The eof marker for char_traits<char> is: " << int2 << endl;

    char_traits<wchar_t>::int_type int3 = char_traits<wchar_t>::eof();
    cout << "The eof marker for char_traits<wchar_t> is: " << int3 << endl;
}
```

## <a name="storage-location-of-objects"></a>Nesnelerin Depolama Konumu

C++ standardı (bölüm 1.8 paragraph 6) tam C++ nesnelerinin benzersiz konumlara sahip olmasını gerektirir. Ancak Microsoft C++ile, veri üyesi olmayan türlerin nesne ömrü için diğer türlerle bir depolama konumunu paylaşacağı durumlar vardır.
