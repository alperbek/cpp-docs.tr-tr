---
title: Derleyici hatası C2666
ms.date: 11/04/2016
f1_keywords:
- C2666
helpviewer_keywords:
- C2666
ms.assetid: 78364d15-c6eb-439a-9088-e04a0176692b
ms.openlocfilehash: ca779269d573e3e5d270fccad6afe6220083fa42
ms.sourcegitcommit: 16fa847794b60bf40c67d20f74751a67fccb602e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/03/2019
ms.locfileid: "74755999"
---
# <a name="compiler-error-c2666"></a>Derleyici hatası C2666

' tanımlayıcı ': numara aşırı yüklemeleri benzer Dönüştürmelere sahip

Aşırı yüklenmiş bir işlev veya işleç belirsiz.   Biçimsel parametre listeleri, derleyicinin belirsizlik çözümlemesi için çok benzer olabilir.  Bu hatayı çözmek için bir veya daha fazla gerçek parametreyi açıkça atayın.

Aşağıdaki örnek C2666 oluşturur:

```cpp
// C2666.cpp
struct complex {
   complex(double);
};

void h(int,complex);
void h(double, double);

int main() {
   h(3,4);   // C2666
}
```

Bu hata, Visual Studio .NET 2003 için yapılan derleyici uygunluk işinin sonucu olarak da oluşturulabilir:

- işaretçi türlerine ikili işleçler ve Kullanıcı tanımlı dönüştürmeler

- niteleme dönüştürmesi, kimlik dönüşümleriyle aynı değil

\<, >, \<= ve > = ikili işleçleri için, geçirilen bir parametre, parametrenin türü işlenenin türüne dönüştürmek üzere Kullanıcı tanımlı bir dönüştürme işleci tanımlıyorsa artık örtük olarak işlenen türüne dönüştürülür. Belirsizlik için artık olası bir sorun var.

Visual Studio .NET 2003 ve Visual Studio .NET sürümlerinde geçerli olan kod için C++, işlev sözdizimini kullanarak sınıf işlecini açıkça çağırın.

## <a name="example"></a>Örnek

```cpp
// C2666b.cpp
#include <string.h>
#include <stdio.h>

struct T
{
    T( const T& copy )
    {
        m_str = copy.m_str;
    }

    T( const char* str )
    {
        int iSize = (strlen( str )+ 1);
        m_str = new char[ iSize ];
        if (m_str)
            strcpy_s( m_str, iSize, str );
    }

    bool operator<( const T& RHS )
    {
        return m_str < RHS.m_str;
    }

    operator char*() const
    {
        return m_str;
    }

    char* m_str;
};

int main()
{
    T str1( "ABCD" );
    const char* str2 = "DEFG";

    // Error - Ambiguous call to operator<()
    // Trying to convert str1 to char* and then call
    // operator<( const char*, const char* )?
    //  OR
    // trying to convert str2 to T and then call
    // T::operator<( const T& )?

    if( str1 < str2 )   // C2666

    if ( str1.operator < ( str2 ) )   // Treat str2 as type T
        printf_s("str1.operator < ( str2 )\n");

    if ( str1.operator char*() < str2 )   // Treat str1 as type char*
        printf_s("str1.operator char*() < str2\n");
}
```

## <a name="example"></a>Örnek

Aşağıdaki örnek C2666 oluşturur

```cpp
// C2666c.cpp
// compile with: /c

enum E
{
    E_A,   E_B
};

class A
{
    int h(const E e) const {return 0; }
    int h(const int i) { return 1; }
    // Uncomment the following line to resolve.
    // int h(const E e) { return 0; }

    void Test()
    {
        h(E_A);   // C2666
        h((const int) E_A);
        h((int) E_A);
    }
};
```
