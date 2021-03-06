---
title: 'Nasıl yapılır: Bir .NET Koleksiyonundan STL/CLR Kapsayıcısına Dönüştürme'
ms.date: 11/04/2016
helpviewer_keywords:
- STL/CLR, converting from .NET collections
- STL/CLR Containers [STL/CLR]
ms.assetid: bb927c48-78e8-4150-bd0b-787c651f4a87
ms.openlocfilehash: 156b4162f742915939ebdfaec6a84d77afaad8cd
ms.sourcegitcommit: 573b36b52b0de7be5cae309d45b68ac7ecf9a6d8
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/10/2019
ms.locfileid: "74988282"
---
# <a name="how-to-convert-from-a-net-collection-to-a-stlclr-container"></a>Nasıl yapılır: Bir .NET Koleksiyonundan STL/CLR Kapsayıcısına Dönüştürme

Bu konu başlığında, .NET koleksiyonlarının eşdeğer STL/CLR kapsayıcılarına nasıl dönüştürüleceği gösterilmektedir. Örnek olarak, bir .NET <xref:System.Collections.Generic.List%601> STL/CLR [vektörüne](../dotnet/vector-stl-clr.md) nasıl dönüştüreceğiniz ve bir .net <xref:System.Collections.Generic.Dictionary%602> STL/CLR [eşlemesine](../dotnet/map-stl-clr.md)nasıl dönüştürüleceği gösterilmektedir, ancak yordam tüm koleksiyonlar ve kapsayıcılar için benzerdir.

### <a name="to-create-a-container-from-a-collection"></a>Bir koleksiyondan kapsayıcı oluşturmak için

1. Tüm bir koleksiyonu dönüştürmek için bir STL/CLR kapsayıcısı oluşturun ve koleksiyonu oluşturucuya geçirin.

   İlk örnekte bu yordam gösterilmektedir.

\- VEYA -

1. [Collection_adapter](../dotnet/collection-adapter-stl-clr.md) nesnesi oluşturarak genel bir STL/CLR kapsayıcısı oluşturun. Bu şablon sınıfı bir .NET koleksiyon arabirimini bağımsız değişken olarak alır. Desteklenen arabirimlerin doğrulanması için bkz. [collection_adapter (STL/CLR)](../dotnet/collection-adapter-stl-clr.md).

1. .NET koleksiyonunun içeriğini kapsayıcıya kopyalayın. Bu, STL/CLR [algoritması](../dotnet/algorithm-stl-clr.md)kullanılarak veya .net koleksiyonunun üzerine giderek ve her öğenin BIR kopyasını STL/CLR kapsayıcısına ekleyerek yapılabilir.

   İkinci örnekte bu yordam gösterilmektedir.

## <a name="example"></a>Örnek

Bu örnekte, genel <xref:System.Collections.Generic.List%601> oluşturacağız ve buna 5 öğe ekleyeceğiz. Sonra, bir <xref:System.Collections.Generic.IEnumerable%601> bağımsız değişken olarak alan oluşturucuyu kullanarak bir `vector` oluşturacağız.

```cpp
// cliext_convert_list_to_vector.cpp
// compile with: /clr

#include <cliext/adapter>
#include <cliext/algorithm>
#include <cliext/vector>

using namespace System;
using namespace System::Collections;
using namespace System::Collections::Generic;

int main(array<System::String ^> ^args)
{
    List<int> ^primeNumbersColl = gcnew List<int>();
    primeNumbersColl->Add(2);
    primeNumbersColl->Add(3);
    primeNumbersColl->Add(5);
    primeNumbersColl->Add(7);
    primeNumbersColl->Add(11);

    cliext::vector<int> ^primeNumbersCont =
        gcnew cliext::vector<int>(primeNumbersColl);

    Console::WriteLine("The contents of the cliext::vector are:");
    cliext::vector<int>::const_iterator it;
    for (it = primeNumbersCont->begin(); it != primeNumbersCont->end(); it++)
    {
        Console::WriteLine(*it);
    }
}
```

```Output
The contents of the cliext::vector are:
2
3
5
7
11
```

## <a name="example"></a>Örnek

Bu örnekte, genel <xref:System.Collections.Generic.Dictionary%602> oluşturacağız ve buna 5 öğe ekleyeceğiz. Daha sonra, <xref:System.Collections.Generic.Dictionary%602> basit bir STL/CLR kapsayıcısı olarak kaydırmak için bir `collection_adapter` oluşturacağız. Son olarak, bir `map` oluşturup <xref:System.Collections.Generic.Dictionary%602> içeriğini `map` `collection_adapter`üzerinde yineletireceğiz. Bu işlem sırasında, `make_pair` işlevini kullanarak yeni bir çift oluşturur ve yeni çifti doğrudan `map`içine ekler.

```cpp
// cliext_convert_dictionary_to_map.cpp
// compile with: /clr

#include <cliext/adapter>
#include <cliext/algorithm>
#include <cliext/map>

using namespace System;
using namespace System::Collections;
using namespace System::Collections::Generic;

int main(array<System::String ^> ^args)
{
    System::Collections::Generic::Dictionary<float, int> ^dict =
        gcnew System::Collections::Generic::Dictionary<float, int>();
    dict->Add(42.0, 42);
    dict->Add(13.0, 13);
    dict->Add(74.0, 74);
    dict->Add(22.0, 22);
    dict->Add(0.0, 0);

    cliext::collection_adapter<System::Collections::Generic::IDictionary<float, int>> dictAdapter(dict);
    cliext::map<float, int> aMap;
    for each (KeyValuePair<float, int> ^kvp in dictAdapter)
    {
        cliext::pair<float, int> aPair = cliext::make_pair(kvp->Key, kvp->Value);
        aMap.insert(aPair);
    }

    Console::WriteLine("The contents of the cliext::map are:");
    cliext::map<float, int>::const_iterator it;
    for (it = aMap.begin(); it != aMap.end(); it++)
    {
        Console::WriteLine("Key: {0:F} Value: {1}", it->first, it->second);
    }
}
```

```Output
The contents of the cliext::map are:
Key: 0.00 Value: 0
Key: 13.00 Value: 13
Key: 22.00 Value: 22
Key: 42.00 Value: 42
Key: 74.00 Value: 74
```

## <a name="see-also"></a>Ayrıca bkz.

[STL/CLR Kitaplık Başvurusu](../dotnet/stl-clr-library-reference.md)<br/>
[bağdaştırıcı (STL/CLR)](../dotnet/adapter-stl-clr.md)<br/>
[Nasıl yapılır: Bir STL/CLR Kapsayıcısından .NET Koleksiyonuna Dönüştürme](../dotnet/how-to-convert-from-a-stl-clr-container-to-a-dotnet-collection.md)
