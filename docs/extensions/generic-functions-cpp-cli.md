---
title: Genel İşlevler (C++/CLI)
ms.date: 10/12/2018
ms.topic: reference
helpviewer_keywords:
- functions [C++], generic
- generic methods
- generics [C++], functions
- methods [C++], generic
- generic functions
ms.assetid: 8e409364-58f9-4360-b486-e7d555e0c218
ms.openlocfilehash: a4a1702c8b9902f5265a8a5f92316d7c82751609
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62349571"
---
# <a name="generic-functions-ccli"></a>Genel İşlevler (C++/CLI)

Genel bir işlev tür parametreleri ile bildirilen bir işlevdir. Gerçek türler, çağrıldığında, tür parametreleri yerine kullanılır.

## <a name="all-platforms"></a>Tüm Platformlar

### <a name="remarks"></a>Açıklamalar

Bu özellik, tüm platformlar için geçerli değildir.

## <a name="windows-runtime"></a>Windows Çalışma Zamanı

### <a name="remarks"></a>Açıklamalar

Bu özellik, Windows çalışma zamanı'nda desteklenmiyor.

### <a name="requirements"></a>Gereksinimler

Derleyici seçeneği: `/ZW`

## <a name="common-language-runtime"></a>Ortak Dil Çalışma Zamanı

Genel bir işlev tür parametreleri ile bildirilen bir işlevdir. Gerçek türler, çağrıldığında, tür parametreleri yerine kullanılır.

### <a name="syntax"></a>Sözdizimi

```cpp
[attributes] [modifiers]
return-type identifier<type-parameter identifier(s)>
[type-parameter-constraints clauses]

([formal-parameters])
{function-body}
```

### <a name="parameters"></a>Parametreler

*Öznitelikleri*<br/>
(İsteğe bağlı) Ek bildirim temelli bilgiler. Öznitelikleri öznitelikleri ve öznitelik sınıfları hakkında daha fazla bilgi için bkz.

*Değiştiriciler*<br/>
(İsteğe bağlı) Statik gibi işlevine yönelik bir değiştirici.  **Sanal** sanal yöntem genel olamaz bu yana izin verilmez.

*dönüş türü*<br/>
Yöntem tarafından döndürülen tür. Dönüş türü void ise, dönüş değeri gereklidir.

*tanımlayıcı*<br/>
İşlev adı.

*tür-parametresi tanımlayıcıları*<br/>
Tanımlayıcıları virgülle ayrılmış listesi.

*Resmi-Parametreler*<br/>
(İsteğe bağlı) Parametre listesi.

*tür parametresi kısıtlamaları tümceleri*<br/>
Bu tür bağımsız değişkenleri kullanılan türler üzerindeki kısıtlamaları belirtir ve belirtilen biçimi alır [genel tür parametrelerindeki kısıtlamalar (C++/CLI)](constraints-on-generic-type-parameters-cpp-cli.md).

*işlev gövdesi*<br/>
Tür parametresi tanımlayıcılarına yönlendirebiliriz Yöntemin gövdesi.

### <a name="remarks"></a>Açıklamalar

Genel tür parametresi ile bildirilen işlevlerle genel işlevlerdir. Bunlar, bir sınıf veya yapı veya tek başına işlevleri yöntemleri olabilir. Tek bir genel bildirimi, genel tür parametresi için farklı bir gerçek tür değiştirmedeki yalnızca farklı işlevler ailesini örtük olarak bildiriyor.

Genel tür parametreleri ile bir sınıf veya yapı Oluşturucu bildirilemez.

Çağrıldığında, genel tür parametresi geçerli bir tür tarafından değiştirilir. Gerçek tür açıkça bir şablonu işlev çağrısı için benzer bir sözdizimi kullanarak açılı köşeli ayraçlar içindeki belirtilebilir. Tür parametreleri çağrılırsa, derleyici işlev çağrısında belirtilen parametreler gerçek türünden türetme dener. Kullanılan parametreler hedeflenen tür bağımsız değişkeni anlaşılamıyor, derleyici bir hata rapor eder.

### <a name="requirements"></a>Gereksinimler

Derleyici seçeneği: `/clr`

### <a name="examples"></a>Örnekler

Aşağıdaki kod örneği, genel bir işlev gösterir.

```cpp
// generics_generic_function_1.cpp
// compile with: /clr
generic <typename ItemType>
void G(int i) {}

ref struct A {
   generic <typename ItemType>
   void G(ItemType) {}

   generic <typename ItemType>
   static void H(int i) {}
};

int main() {
   A myObject;

   // generic function call
   myObject.G<int>(10);

   // generic function call with type parameters deduced
   myObject.G(10);

   // static generic function call
   A::H<int>(10);

   // global generic function call
   G<int>(10);
}
```

Genel İşlevler, imza veya parametre, üzerinde bir işlev türü parametre sayısı bazında aşırı yüklenebilir. Ayrıca, bazı tür parametrelerinde işlevleri farklı olduğu sürece genel işlevleri ile genel olmayan işlevler aynı ada sahip aşırı yüklenebilir. Örneğin, aşağıdaki işlevleri aşırı yüklenebilir:

```cpp
// generics_generic_function_2.cpp
// compile with: /clr /c
ref struct MyClass {
   void MyMythod(int i) {}

   generic <class T>
   void MyMythod(int i) {}

   generic <class T, class V>
   void MyMythod(int i) {}
};
```

Aşağıdaki örnek, bir dizideki ilk öğeyi bulmak için genel bir işlev kullanır. Bunu bildirir `MyClass`, taban sınıfından devralan `MyBaseClass`. `MyClass` Genel bir işlev içeriyor `MyFunction`, başka bir genel işlev çağrıları `MyBaseClassFunction`, temel sınıf içerisinde. İçinde `main`, alan genel işlevin `MyFunction`, farklı tür bağımsız değişkeni kullanılarak çağrılır.

```cpp
// generics_generic_function_3.cpp
// compile with: /clr
using namespace System;

ref class MyBaseClass {
protected:
   generic <class ItemType>
   ItemType MyBaseClassFunction(ItemType item) {
      return item;
   }
};

ref class MyClass: public MyBaseClass {
public:
   generic <class ItemType>
   ItemType MyFunction(ItemType item) {
      return MyBaseClass::MyBaseClassFunction<ItemType>(item);
   }
};

int main() {
   MyClass^ myObj = gcnew MyClass();

   // Call MyFunction using an int.
   Console::WriteLine("My function returned an int: {0}",
                           myObj->MyFunction<int>(2003));

   // Call MyFunction using a string.
   Console::WriteLine("My function returned a string: {0}",
   myObj->MyFunction<String^>("Hello generic functions!"));
}
```

```Output
My function returned an int: 2003
My function returned a string: Hello generic functions!
```

## <a name="see-also"></a>Ayrıca bkz.

[.NET ve UWP İçin Bileşen Uzantıları](component-extensions-for-runtime-platforms.md)<br/>
[Genel Türler](generics-cpp-component-extensions.md)
