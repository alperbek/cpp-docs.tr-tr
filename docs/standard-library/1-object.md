---
title: _1 Nesnesi
ms.date: 11/04/2016
f1_keywords:
- _1
- std::_1
- functional/std::_1
helpviewer_keywords:
- _1 object
ms.assetid: 30c3c480-ff31-4708-94be-7d0d65f243c9
ms.openlocfilehash: 8fdb53ea03031f2bf1634a105275c72263ee20e3
ms.sourcegitcommit: c21b05042debc97d14875e019ee9d698691ffc0b
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/09/2020
ms.locfileid: "84620922"
---
# <a name="_1-object"></a>_1 Nesnesi

Değiştirilebilen bağımsız değişkenler için yer tutucular.

## <a name="syntax"></a>Söz dizimi

```cpp
namespace placeholders {
    extern unspecified _1, _2, ... _M
} // namespace placeholders (within std)
```

## <a name="remarks"></a>Açıklamalar

Nesneler, `_1, _2, ... _M` [bağlama](functional-functions.md#bind)tarafından döndürülen bir nesne için bir işlev çağrısında sırasıyla birinci, ikinci,..., MTH bağımsız değişkenini tasartutuculardır. `_N`Bağlama ifadesi değerlendirildiğinde nth bağımsız değişkeninin nereye ekleneceğini belirtmek için kullanırsınız.

Bu uygulamada, değeri 20 ' `M` dir.

## <a name="example"></a>Örnek

```cpp
// std__functional_placeholder.cpp
// compile with: /EHsc
#include <functional>
#include <algorithm>
#include <iostream>

using namespace std::placeholders;

void square(double x)
    {
    std::cout << x << "^2 == " << x * x << std::endl;
    }

void product(double x, double y)
    {
    std::cout << x << "*" << y << " == " << x * y << std::endl;
    }

int main()
    {
    double arg[] = {1, 2, 3};

    std::for_each(&arg[0], &arg[3], square);
    std::cout << std::endl;

    std::for_each(&arg[0], &arg[3], std::bind(product, _1, 2));
    std::cout << std::endl;

    std::for_each(&arg[0], &arg[3], std::bind(square, _1));

    return (0);
    }
```

```Output
1^2 == 1
2^2 == 4
3^2 == 9

1*2 == 2
2*2 == 4
3*2 == 6

1^2 == 1
2^2 == 4
3^2 == 9
```
