---
title: istreambuf_iterator Sınıfı
ms.date: 11/04/2016
f1_keywords:
- streambuf/std::istreambuf_iterator
- iterator/std::istreambuf_iterator::char_type
- iterator/std::istreambuf_iterator::int_type
- iterator/std::istreambuf_iterator::istream_type
- iterator/std::istreambuf_iterator::streambuf_type
- iterator/std::istreambuf_iterator::traits_type
- iterator/std::istreambuf_iterator::equal
helpviewer_keywords:
- std::istreambuf_iterator [C++]
- std::istreambuf_iterator [C++], char_type
- std::istreambuf_iterator [C++], int_type
- std::istreambuf_iterator [C++], istream_type
- std::istreambuf_iterator [C++], streambuf_type
- std::istreambuf_iterator [C++], traits_type
- std::istreambuf_iterator [C++], equal
ms.assetid: 39002da2-61a6-48a5-9d0c-5df8271f6038
ms.openlocfilehash: 80bca2160f2e60938e9d0c85557b11a273c23264
ms.sourcegitcommit: c123cc76bb2b6c5cde6f4c425ece420ac733bf70
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81363056"
---
# <a name="istreambuf_iterator-class"></a>istreambuf_iterator Sınıfı

Sınıf şablonu istreambuf_iterator, karakter öğelerini depoladığı bir nesne üzerinden erişen bir giriş akışı arabellesinden, `basic_streambuf` \< **CharType**, **Özellikler**> için tür işaretçisinden çıkaran bir giriş yineleme nesnesini açıklar.

## <a name="syntax"></a>Sözdizimi

```cpp
template <class CharType class Traits = char_traits <CharType>>
class istreambuf_iterator
: public iterator<input_iterator_tag, CharType, typename Traits ::off_type, CharType*, CharType&>
```

### <a name="parameters"></a>Parametreler

*Chartype*\
istreambuf_iterator için karakter türünü temsil eden tür.

*Özellik*\
istreambuf_iterator için karakter türünü temsil eden tür. Bu bağımsız değişken isteğe `char_traits` \< bağlıdır ve varsayılan değer *CharType>' dir.*

## <a name="remarks"></a>Açıklamalar

istreambuf_iterator sınıfının, bir giriş yineleyici için gereksinimleri karşılaması gerekir.

Sınıf istreambuf_iterator bir nesnesini null olmayan depolanmış bir işaretçiyle yaptıktan veya artıya çıkardıktan sonra, nesne etkili bir şekilde ilişkili giriş akışından *CharType* türübir nesneyi ayıklamayı ve depolamayı dener. Ayıklama, ancak nesne başvurusu kaldırılana veya kopyalanana kadar gecikebilir. Ayıklama işlemi başarısız olursa, nesne etkili bir şekilde depolanan işaretçinin yerini alır, böylece bir dizi sonu gösterge oluşturur.

### <a name="constructors"></a>Oluşturucular

|Oluşturucu|Açıklama|
|-|-|
|[istreambuf_iterator](#istreambuf_iterator)|Giriş akışındaki karakterleri okumak için başharflere alınan bir `istreambuf_iterator` oluşturma.|

### <a name="typedefs"></a>Tür tanımları

|Tür adı|Açıklama|
|-|-|
|[Char_type](#char_type)|`ostreambuf_iterator`Karakter türünü sağlayan bir tür.|
|[Int_type](#int_type)|Bir tamsayı türü sağlayan bir `istreambuf_iterator`tür.|
|[istream_type](#istream_type)|Akış türünü sağlayan bir `istream_iterator`tür.|
|[streambuf_type](#streambuf_type)|Akış türünü sağlayan bir `istreambuf_iterator`tür.|
|[traits_type](../standard-library/istream-iterator-class.md#traits_type)|`istream_iterator`Karakter özellikleri türünü sağlayan bir tür.|

### <a name="member-functions"></a>Üye işlevler

|Üye fonksiyonu|Açıklama|
|-|-|
|[Eşit](#equal)|İki giriş akışı önbelleği yineleyicisi arasındaki eşitliği sınar.|

### <a name="operators"></a>İşleçler

|İşleç|Açıklama|
|-|-|
|[işleç*](#op_star)|Başvuru kaldırma işleci akıştaki sonraki karakteri döndürür.|
|[işleç++](#op_add_add)|Giriş akışındaki sonraki öğeyi döndürür ya da artırmadan önce nesneyi kopyalar ve kopyayı döndürür.|
|[operatör->](#op_arrow)|Varsa, bir üyenin değerini döndürür.|

## <a name="requirements"></a>Gereksinimler

**Üstbilgi:** \<yineleyici>

**Ad alanı:** std

## <a name="istreambuf_iteratorchar_type"></a><a name="char_type"></a>istreambuf_iterator::char_type

`ostreambuf_iterator`Karakter türünü sağlayan bir tür.

```cpp
typedef CharType char_type;
```

### <a name="remarks"></a>Açıklamalar

Tür, şablon parametresi *CharType*ile eş anlamlıdır.

### <a name="example"></a>Örnek

```cpp
// istreambuf_iterator_char_type.cpp
// compile with: /EHsc
#include <iterator>
#include <vector>
#include <iostream>
#include <algorithm>

int main( )
{
   using namespace std;

   typedef istreambuf_iterator<char>::char_type CHT1;
   typedef istreambuf_iterator<char>::traits_type CHTR1;

   cout << "(Try the example: 'So many dots to be done'\n"
        << " then an Enter key to insert into the output,\n"
        << " & use a ctrl-Z Enter key combination to exit): ";

   // istreambuf_iterator for input stream
   istreambuf_iterator< CHT1, CHTR1> charInBuf ( cin );
   ostreambuf_iterator<char> charOut ( cout );

   // Used in conjunction with replace_copy algorithm
   // to insert into output stream and replace spaces
   // with dot-separators
   replace_copy ( charInBuf , istreambuf_iterator<char>( ),
        charOut , ' ' , '.' );
}
```

## <a name="istreambuf_iteratorequal"></a><a name="equal"></a>istreambuf_iterator::eşit

İki giriş akışı arabellek yineleyicisi arasında eşdeğerlik testleri.

```cpp
bool equal(const istreambuf_iterator<CharType, Traits>& right) const;
```

### <a name="parameters"></a>Parametreler

*Doğru*\
Eşitliği kontrol etmek için hangi yineleyici.

### <a name="return-value"></a>Dönüş Değeri

**her** ikisi `istreambuf_iterator`de akış sonu yineleyicileri yse veya akış sonu yineleyici değilse; aksi takdirde **yanlış**.

### <a name="remarks"></a>Açıklamalar

Bir aralık geçerli `istreambuf_iterator` konuma ve akış sonu yineleyicisine göre tanımlanır, ancak tüm non-end-of akış yineleyicileri `equal` üye işlev altında eşdeğer olduğundan, s `istreambuf_iterator`kullanarak herhangi bir alt aralığı tanımlamak mümkün değildir. Ve `==` `!=` operatörler aynı anlambilime sahiptir.

### <a name="example"></a>Örnek

```cpp
// istreambuf_iterator_equal.cpp
// compile with: /EHsc
#include <iterator>
#include <iostream>

int main( )
{
   using namespace std;

   cout << "(Try the example: 'Hello world!'\n"
        << " then an Enter key to insert into the output,\n"
        << " & use a ctrl-Z Enter key combination to exit): ";

   istreambuf_iterator<char> charReadIn1 ( cin );
   istreambuf_iterator<char> charReadIn2 ( cin );

   bool b1 = charReadIn1.equal ( charReadIn2 );

   if (b1)
      cout << "The iterators are equal." << endl;
   else
      cout << "The iterators are not equal." << endl;
}
```

## <a name="istreambuf_iteratorint_type"></a><a name="int_type"></a>istreambuf_iterator:int_type

Bir tamsayı türü sağlayan bir `istreambuf_iterator`tür.

```cpp
typedef typename traits_type::int_type int_type;
```

### <a name="remarks"></a>Açıklamalar

Türü için `Traits::int_type`eşanlamlıdır.

### <a name="example"></a>Örnek

```cpp
// istreambuf_iterator_int_type.cpp
// compile with: /EHsc
#include <iterator>
#include <iostream>

int main( )
{
   using namespace std;
   istreambuf_iterator<char>::int_type inttype1 = 100;
   cout << "The inttype1 = " << inttype1 << "." << endl;
}
/* Output:
The inttype1 = 100.
*/
```

## <a name="istreambuf_iteratoristream_type"></a><a name="istream_type"></a>istreambuf_iterator:istream_type

Akış türünü sağlayan bir `istreambuf_iterator`tür.

```cpp
typedef basic_istream<CharType, Traits> istream_type;
```

### <a name="remarks"></a>Açıklamalar

Türü `basic_istream` \< **CharType**için eşanlamlıdır , **Özellikler**>.

### <a name="example"></a>Örnek

Nasıl [istreambuf_iterator](#istreambuf_iterator) bildirilir ve kullanılacağına `istream_type`ilgili bir örnek için istreambuf_iterator bakın.

## <a name="istreambuf_iteratoristreambuf_iterator"></a><a name="istreambuf_iterator"></a>istreambuf_iterator::istreambuf_iterator

Giriş akışındaki karakterleri okumak için başharfe çevrilmiş bir istreambuf_iterator kurar.

```cpp
istreambuf_iterator(streambuf_type* strbuf = 0) throw();
istreambuf_iterator(istream_type& _Istr) throw();
```

### <a name="parameters"></a>Parametreler

*strbuf*\
Bağlanan giriş akışı arabelleği. `istreambuf_iterator`

*_Istr*\
Bağlanan `istreambuf_iterator` giriş akışı.

### <a name="remarks"></a>Açıklamalar

İlk oluşturucu, giriş akışı arabellek işaretçisini *strbuf*ile başharfe çevirer. İkinci oluşturucu, giriş akışı arabellek işaretçisini *_Istr.* `rdbuf`, ve daha sonra sonunda ayıklamak ve `CharType`türünde bir nesne depolamak için çalışır.

### <a name="example"></a>Örnek

```cpp
// istreambuf_iterator_istreambuf_iterator.cpp
// compile with: /EHsc
#include <iterator>
#include <vector>
#include <algorithm>
#include <iostream>

int main( )
{
   using namespace std;

   // Following declarations will not compile:
   istreambuf_iterator<char>::istream_type &istrm = cin;
   istreambuf_iterator<char>::streambuf_type *strmbf = cin.rdbuf( );

   cout << "(Try the example: 'Oh what a world!'\n"
      << " then an Enter key to insert into the output,\n"
      << " & use a ctrl-Z Enter key combination to exit): ";
   istreambuf_iterator<char> charReadIn ( cin );
   ostreambuf_iterator<char> charOut ( cout );

   // Used in conjunction with replace_copy algorithm
   // to insert into output stream and replace spaces
   // with hyphen-separators
   replace_copy ( charReadIn , istreambuf_iterator<char>( ),
      charOut , ' ' , '-' );
}
```

## <a name="istreambuf_iteratoroperator"></a><a name="op_star"></a>istreambuf_iterator::operatör*

Başvuru kaldırma işleci akıştaki sonraki karakteri döndürür.

```cpp
CharType operator*() const;
```

### <a name="return-value"></a>Dönüş Değeri

Akıştaki bir sonraki karakter.

### <a name="example"></a>Örnek

```cpp
// istreambuf_iterator_operator_deref.cpp
// compile with: /EHsc
#include <iterator>
#include <iostream>

int main( )
{
   using namespace std;

   cout << "Type string of characters & enter to output it,\n"
      << " with stream buffer iterators,(try: 'I'll be back.')\n"
      << " repeat as many times as desired,\n"
      << " then keystroke ctrl-Z Enter to exit program: ";
   istreambuf_iterator<char> inpos ( cin );
   istreambuf_iterator<char> endpos;
   ostreambuf_iterator<char> outpos ( cout );
   while ( inpos != endpos )
   {
*outpos = *inpos;   //Put value of outpos equal to inpos
      ++inpos;
      ++outpos;
   }
}
```

## <a name="istreambuf_iteratoroperator"></a><a name="op_add_add"></a>istreambuf_iterator::operator++

Giriş akışındaki sonraki öğeyi döndürür ya da artırmadan önce nesneyi kopyalar ve kopyayı döndürür.

```cpp
istreambuf_iterator<CharType, Traits>& operator++();
istreambuf_iterator<CharType, Traits> operator++(int);
```

### <a name="return-value"></a>Dönüş Değeri

Bir `istreambuf_iterator` başvuru veya `istreambuf_iterator`bir.

### <a name="remarks"></a>Açıklamalar

İlk işleç sonunda ilişkili giriş akışından `CharType` bir tür nesnesini ayıklamayı ve depolamayı dener. İkinci işleç nesnenin bir kopyasını yapar, nesneyi artımlar ve sonra kopyayı döndürür.

### <a name="example"></a>Örnek

```cpp
// istreambuf_iterator_operator_incr.cpp
// compile with: /EHsc
#include <iterator>
#include <iostream>

int main( )
{
   using namespace std;

   cout << "Type string of characters & enter to output it,\n"
      << " with stream buffer iterators,(try: 'I'll be back.')\n"
      << " repeat as many times as desired,\n"
      << " then keystroke ctrl-Z Enter to exit program: ";
   istreambuf_iterator<char> inpos ( cin );
   istreambuf_iterator<char> endpos;
   ostreambuf_iterator<char> outpos ( cout );
   while ( inpos != endpos )
   {
*outpos = *inpos;
      ++inpos;   //Increment istreambuf_iterator
      ++outpos;
   }
}
```

## <a name="istreambuf_iteratoroperator-gt"></a><a name="op_arrow"></a>istreambuf_iterator::operatör-&gt;

Varsa, bir üyenin değerini döndürür.

```cpp
const Elem* operator->() const;
```

### <a name="return-value"></a>Dönüş Değeri

Operatör ** & \* \*bunu**döndürür.

## <a name="istreambuf_iteratorstreambuf_type"></a><a name="streambuf_type"></a>istreambuf_iterator:streambuf_type

istreambuf_iterator akış türünü sağlayan bir tür.

```cpp
typedef basic_streambuf<CharType, Traits> streambuf_type;
```

### <a name="remarks"></a>Açıklamalar

Türü `basic_streambuf` \< **CharType**için eşanlamlıdır , **Özellikler**>.

### <a name="example"></a>Örnek

Nasıl [istreambuf_iterator](#istreambuf_iterator) bildirilir ve kullanılacağına `istreambuf_type`ilgili bir örnek için istreambuf_iterator bakın.

## <a name="istreambuf_iteratortraits_type"></a><a name="traits_type"></a>istreambuf_iterator:traits_type

`istream_iterator`Karakter özellikleri türünü sağlayan bir tür.

```cpp
typedef Traits traits_type;
```

### <a name="remarks"></a>Açıklamalar

Tür, şablon parametresi *Özellikleri*ile eş anlamlıdır.

### <a name="example"></a>Örnek

```cpp
// istreambuf_iterator_traits_type.cpp
// compile with: /EHsc
#include <iterator>
#include <vector>
#include <iostream>
#include <algorithm>

int main( )
{
   using namespace std;

   typedef istreambuf_iterator<char>::char_type CHT1;
   typedef istreambuf_iterator<char>::traits_type CHTR1;

   cout << "(Try the example: 'So many dots to be done'\n"
        << " then an Enter key to insert into the output,\n"
        << " & use a ctrl-Z Enter key combination to exit): ";

   // istreambuf_iterator for input stream
   istreambuf_iterator< CHT1, CHTR1> charInBuf ( cin );
   ostreambuf_iterator<char> charOut ( cout );

   // Used in conjunction with replace_copy algorithm
   // to insert into output stream and replace spaces
   // with dot-separators
   replace_copy ( charInBuf , istreambuf_iterator<char>( ),
        charOut , ' ' , '.' );
}
```

## <a name="see-also"></a>Ayrıca bkz.

[iterator Yapıt](../standard-library/iterator-struct.md)\
[\<iterator>](../standard-library/iterator.md)\
[C++ Standart Kitaplığında İş Parçacığı Güvenliği](../standard-library/thread-safety-in-the-cpp-standard-library.md)\
[C++ Standart Kütüphane Başvurusu](../standard-library/cpp-standard-library-reference.md)
