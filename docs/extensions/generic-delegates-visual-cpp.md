---
title: Genel Temsilciler (C++/CLI)
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- generic delegates
- delegates, generic [C++]
ms.assetid: 09d430b2-1aef-4fbc-87f9-9d7b8185d798
ms.openlocfilehash: 4c579d0c0ab39a2ddcadfd116bdfed8ba9da2863
ms.sourcegitcommit: 857fa6b530224fa6c18675138043aba9aa0619fb
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/24/2020
ms.locfileid: "80182038"
---
# <a name="generic-delegates-ccli"></a>Genel Temsilciler (C++/CLI)

Temsilcilerle genel tür parametreleri kullanabilirsiniz. Temsilciler hakkında daha fazla bilgi için bkz. [DelegateC++(/CLI C++ve/CX)](delegate-cpp-component-extensions.md).

## <a name="syntax"></a>Sözdizimi

```cpp
[attributes]
generic < [class | typename] type-parameter-identifiers>
[type-parameter-constraints-clauses]
[accessibility-modifiers] delegate result-type identifier
([formal-parameters]);
```

### <a name="parameters"></a>Parametreler

*özelliklerine*<br/>
Seçim Ek bildirime dayalı bilgiler. Öznitelikler ve öznitelik sınıfları hakkında daha fazla bilgi için bkz. öznitelikler.

*tür-parametre tanımlayıcıları*<br/>
Tür parametrelerine yönelik tanımlayıcıların virgülle ayrılmış listesi.

*tür-parametre-kısıtlamalar-yan tümceler*<br/>
[Genel tür parametrelerindeki (C++/CLI) kısıtlamalarda](constraints-on-generic-type-parameters-cpp-cli.md) belirtilen formu alır

*Erişilebilirlik-değiştiriciler*<br/>
Seçim Erişilebilirlik değiştiricileri (örn. **genel**, **özel**).

*Sonuç türü*<br/>
Temsilcinin dönüş türü.

*Tanımlayıcısını*<br/>
Temsilcinin adı.

*biçimsel-parametreler*<br/>
Seçim Temsilcinin parametre listesi.

## <a name="example"></a>Örnek

Temsilci türü parametreleri, temsilci nesnesinin oluşturulduğu noktada belirtilir. Hem temsilci hem de ile ilişkili Yöntem aynı imzaya sahip olmalıdır. Aşağıda genel temsilci bildirimine bir örnek verilmiştir.

```cpp
// generics_generic_delegate1.cpp
// compile with: /clr /c
generic <class ItemType>
delegate ItemType GenDelegate(ItemType p1, ItemType% p2);
```

## <a name="example"></a>Örnek

Aşağıdaki örnek şunu gösterir

- Aynı temsilci nesnesini farklı oluşturulmuş türlerle kullanamazsınız. Farklı türler için farklı temsilci nesneleri oluşturun.

- Genel bir temsilci, genel bir yöntemle ilişkilendirilebilir.

- Genel bir yöntem tür bağımsız değişkenleri belirtilmeden çağrıldığında, derleyici, çağrının tür bağımsız değişkenlerini çıkarmaya çalışır.

```cpp
// generics_generic_delegate2.cpp
// compile with: /clr
generic <class ItemType>
delegate ItemType GenDelegate(ItemType p1, ItemType% p2);

generic <class ItemType>
ref struct MyGenClass {
   ItemType MyMethod(ItemType i, ItemType % j) {
      return ItemType();
   }
};

ref struct MyClass {
   generic <class ItemType>
   static ItemType MyStaticMethod(ItemType i, ItemType % j) {
      return ItemType();
   }
};

int main() {
   MyGenClass<int> ^ myObj1 = gcnew MyGenClass<int>();
   MyGenClass<double> ^ myObj2 = gcnew MyGenClass<double>();
   GenDelegate<int>^ myDelegate1 =
      gcnew GenDelegate<int>(myObj1, &MyGenClass<int>::MyMethod);

   GenDelegate<double>^ myDelegate2 =
      gcnew GenDelegate<double>(myObj2, &MyGenClass<double>::MyMethod);

   GenDelegate<int>^ myDelegate =
      gcnew GenDelegate<int>(&MyClass::MyStaticMethod<int>);
}
```

## <a name="example"></a>Örnek

Aşağıdaki örnek, `GenDelegate<ItemType>`bir genel temsilci bildirir ve ardından onu `ItemType`tür parametresini kullanan `MyMethod` yöntemiyle ilişkilendirerek onu başlatır. Temsilcinin iki örneği (tamsayı ve çift) oluşturulup çağrılır.

```cpp
// generics_generic_delegate.cpp
// compile with: /clr
using namespace System;

// declare generic delegate
generic <typename ItemType>
delegate ItemType GenDelegate (ItemType p1, ItemType% p2);

// Declare a generic class:
generic <typename ItemType>
ref class MyGenClass {
public:
   ItemType MyMethod(ItemType p1, ItemType% p2) {
      p2 = p1;
      return p1;
    }
};

int main() {
   int i = 0, j = 0;
   double m = 0.0, n = 0.0;

   MyGenClass<int>^ myObj1 = gcnew MyGenClass<int>();
   MyGenClass<double>^ myObj2 = gcnew MyGenClass<double>();

   // Instantiate a delegate using int.
   GenDelegate<int>^ MyDelegate1 =
      gcnew GenDelegate<int>(myObj1, &MyGenClass<int>::MyMethod);

   // Invoke the integer delegate using MyMethod.
   i = MyDelegate1(123, j);

   Console::WriteLine(
      "Invoking the integer delegate: i = {0}, j = {1}", i, j);

   // Instantiate a delegate using double.
   GenDelegate<double>^ MyDelegate2 =
      gcnew GenDelegate<double>(myObj2, &MyGenClass<double>::MyMethod);

   // Invoke the integer delegate using MyMethod.
   m = MyDelegate2(0.123, n);

   Console::WriteLine(
      "Invoking the double delegate: m = {0}, n = {1}", m, n);
}
```

```Output
Invoking the integer delegate: i = 123, j = 123
Invoking the double delegate: m = 0.123, n = 0.123
```

## <a name="see-also"></a>Ayrıca bkz.

[Genel Türler](generics-cpp-component-extensions.md)
