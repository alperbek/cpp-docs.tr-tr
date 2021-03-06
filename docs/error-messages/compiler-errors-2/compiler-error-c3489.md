---
title: Derleyici hatası C3489
ms.date: 11/04/2016
f1_keywords:
- C3489
helpviewer_keywords:
- C3489
ms.assetid: 47b58d69-459d-4499-abc7-5f0b9303d773
ms.openlocfilehash: 67eaa9806dff96783f391c46c890b34e1ceef5a3
ms.sourcegitcommit: 16fa847794b60bf40c67d20f74751a67fccb602e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/03/2019
ms.locfileid: "74738420"
---
# <a name="compiler-error-c3489"></a>Derleyici hatası C3489

varsayılan yakalama modu değere göre olduğunda ' var ' gereklidir

Bir lambda ifadesinin varsayılan yakalama modunun değere göre olduğunu belirttiğinizde, bir değişkeni değere göre bu ifadenin yakalama yan tümcesine geçiremezsiniz.

### <a name="to-correct-this-error"></a>Bu hatayı düzeltmek için

- Değişkeni, yakalama yan tümcesine açıkça geçirmeyin veya

- Varsayılan yakalama modu olarak değere göre belirtmeyin veya

- Varsayılan yakalama modu olarak başvuruya göre belirtin veya

- Değişkeni yakalama yan tümcesine başvuruya göre geçirin. (Bu durum lambda ifadesinin davranışını değiştirebilir.)

## <a name="example"></a>Örnek

Aşağıdaki örnek, varsayılan modu değere göre olan bir lambda ifadesinin yakalama yan tümcesinde değere göre görünen C3489 değişken `n` üretir:

```cpp
// C3489a.cpp

int main()
{
   int n = 5;
   [=, n]() { return n; } (); // C3489
}
```

## <a name="example"></a>Örnek

Aşağıdaki örnekte, C3489 için dört olası çözüm gösterilmektedir:

```cpp
// C3489b.cpp

int main()
{
   int n = 5;

   // Possible resolution 1:
   // Do not explicitly pass n to the capture clause.
   [=]() { return n; } ();

   // Possible resolution 2:
   // Do not specify by-value as the default capture mode.
   [n]() { return n; } ();

   // Possible resolution 3:
   // Specify by-reference as the default capture mode.
   [&, n]() { return n; } ();

   // Possible resolution 4:
   // Pass n by reference to the capture clause.
   [&n]() { return n; } ();
}
```

## <a name="see-also"></a>Ayrıca bkz.

[Lambda İfadeleri](../../cpp/lambda-expressions-in-cpp.md)
