---
title: '&lt;vektör&gt; işlevleri'
ms.date: 11/04/2016
f1_keywords:
- vector/std::swap
ms.assetid: 6cdcf043-eef6-4330-83f0-4596fb9f968a
helpviewer_keywords:
- std::swap [vector]
ms.openlocfilehash: cdf67b3cb34546f5d0dfcd9a4f3bd96500c18af9
ms.sourcegitcommit: 3590dc146525807500c0477d6c9c17a4a8a2d658
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/16/2019
ms.locfileid: "68241033"
---
# <a name="ltvectorgt-functions"></a>&lt;vektör&gt; işlevleri

## <a name="swap"></a> değiştirme

İki vektör öğelerini birbiriyle değiştirir.

```cpp
template <class Type, class Allocator>
void swap(vector<Type, Allocator>& left, vector<Type, Allocator>& right);
```

### <a name="parameters"></a>Parametreler

*sağ*\
Değiştirilecek öğeleri sağlayan vektör veya öğeleri vektör öğelerle ilişkili vektör *sol*.

*Sol*\
Öğeleri vektör öğelerle ilişkili vektör *doğru*.

### <a name="remarks"></a>Açıklamalar

Özel üye işlevini yürütmek için kapsayıcı sınıfı vektör bir algoritma şablon işlevi olan `left`. [Vector::Swap](../standard-library/vector-class.md) *(doğru*). İşlev şablonlarının kısmi derleyici tarafından sıralanması, örnekleri şunlardır. Şablon işlevleri şablonu işlev çağrısı ile eşleşen benzersiz değil bir şekilde aşırı yüklendiğinde, derleyici en özel şablon işlevi sürümü seçin. Şablon işlevinin genel sürüm **şablon** \< **sınıfı T**> **void takas**( **T &** , **T &** ), algoritma sınıfı tarafından atama çalışır ve yavaş bir işlemdir. Her bir kapsayıcıdaki özelleştirilmiş bir sürüm olarak kapsayıcı sınıfı iç gösterimine ile çalışabilir daha hızlıdır.

### <a name="example"></a>Örnek

Üye işlevi kod örneğine bakın [vector::swap](../standard-library/vector-class.md) şablon sürümünü kullanan bir örnek için `swap`.
