---
title: İşlev Şablonu Çağrılarının Aşırı Yük Çözümü
ms.date: 11/04/2016
helpviewer_keywords:
- function templates overload resolution
ms.assetid: a2918748-2cbb-4fc6-a176-e256f120bee4
ms.openlocfilehash: d96046c629e812e342ce86b850b6d52a57094997
ms.sourcegitcommit: 857fa6b530224fa6c18675138043aba9aa0619fb
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/24/2020
ms.locfileid: "80188447"
---
# <a name="overload-resolution-of-function-template-calls"></a>İşlev Şablonu Çağrılarının Aşırı Yük Çözümü

Bir işlev şablonu aynı adda şablon olmayan işlevleri aşırı yükleyebilir. Bu senaryoda, işlev çağrıları öncelikle, benzersiz bir özelleşmeye sahip işlev şablonunu örneklemek için şablon bağımsız değişken kesintisi kullanılarak çözümlenir. Şablon bağımsız değişkeni kesintisi başarısız olursa, diğer işlev aşırı yüklemeleri çağrıyı çözümlemek için kabul edilir. Aday kümesi olarak da bilinen bu diğer aşırı yüklemeler, şablon olmayan işlevleri ve diğer örneklenmiş işlev şablonlarını içerir. Şablon bağımsız değişkeni kesintisi başarılı olursa oluşturulan işlev, en iyi eşleşmeyi tespit etmek için diğer işlevlerle karşılaştırılır ve aşırı yükleme çözümlemesi kurallarını takip edin. Daha fazla bilgi için bkz. [Işlev aşırı yüklemesi](function-overloading.md).

## <a name="example"></a>Örnek

Şablon olmayan bir işlev, bir şablon işlevi ile eşit derecede iyi bir eşleşmedir, aşağıdaki örnekte `f(1, 1)` olduğu gibi şablon olmayan işlev seçilir (şablon bağımsız değişkenleri açıkça belirtilmediği sürece).

```cpp
// template_name_resolution9.cpp
// compile with: /EHsc
#include <iostream>
using namespace std;

void f(int, int) { cout << "f(int, int)" << endl; }
void f(char, char) { cout << "f(char, char)" << endl; }

template <class T1, class T2>
void f(T1, T2)
{
   cout << "void f(T1, T2)" << endl;
};

int main()
{
   f(1, 1);   // Equally good match; choose the nontemplate function.
   f('a', 1); // Chooses the template function.
   f<int, int>(2, 2);  // Template arguments explicitly specified.
}
```

```Output
f(int, int)
void f(T1, T2)
void f(T1, T2)
```

## <a name="example"></a>Örnek

Sonraki örnekte, şablon olmayan işlev bir dönüştürme gerektiriyorsa, tam olarak eşleşen şablon işlevinin tercih edildiği gösterilmektedir.

```cpp
// template_name_resolution10.cpp
// compile with: /EHsc
#include <iostream>
using namespace std;

void f(int, int) { cout << "f(int, int)" << endl; }

template <class T1, class T2>
void f(T1, T2)
{
   cout << "void f(T1, T2)" << endl;
};

int main()
{
   long l = 0;
   int i = 0;
   // Call the template function f(long, int) because f(int, int)
   // would require a conversion from long to int.
   f(l, i);
}
```

```Output
void f(T1, T2)
```

## <a name="see-also"></a>Ayrıca bkz.

[Ad çözümlemesi](../cpp/templates-and-name-resolution.md)<br/>
[typename](../cpp/typename.md)
