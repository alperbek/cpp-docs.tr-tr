---
title: discrete_distribution Sınıfı
ms.date: 11/04/2016
f1_keywords:
- random/std::discrete_distribution
- random/std::discrete_distribution::reset
- random/std::discrete_distribution::probabilities
- random/std::discrete_distribution::param
- random/std::discrete_distribution::min
- random/std::discrete_distribution::max
- random/std::discrete_distribution::operator()
- random/std::discrete_distribution::param_type
- random/std::discrete_distribution::param_type::probabilities
- random/std::discrete_distribution::param_type::operator==
- random/std::discrete_distribution::param_type::operator!=
helpviewer_keywords:
- std::discrete_distribution [C++]
- std::discrete_distribution [C++], reset
- std::discrete_distribution [C++], probabilities
- std::discrete_distribution [C++], param
- std::discrete_distribution [C++], min
- std::discrete_distribution [C++], max
- std::discrete_distribution [C++], param_type
- std::discrete_distribution [C++], param_type
ms.assetid: 8c8ba8f8-c06f-4f07-b354-f53950142fcf
ms.openlocfilehash: 83d69df399d556025d0f7d4a8ccd714ff43a76ec
ms.sourcegitcommit: c123cc76bb2b6c5cde6f4c425ece420ac733bf70
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81368767"
---
# <a name="discrete_distribution-class"></a>discrete_distribution Sınıfı

Her aralıkta tek düze olasılık içeren tek düze genişlik aralıkları olan ayrı bir tamsayı dağılımı oluşturur.

## <a name="syntax"></a>Sözdizimi

```cpp
template<class IntType = int>
class discrete_distribution
   {
public:
   // types
   typedef IntType result_type;
   struct param_type;

   // constructor and reset functions
   discrete_distribution();
   template <class InputIterator>
   discrete_distribution(InputIterator firstW, InputIterator lastW);
   discrete_distribution(initializer_list<double> weightlist);
   template <class UnaryOperation>
   discrete_distribution(size_t count, double xmin, double xmax, UnaryOperation funcweight);
   explicit discrete_distribution(const param_type& parm);
   void reset();

   // generating functions
   template <class URNG>
   result_type operator()(URNG& gen);
   template <class URNG>
   result_type operator()(URNG& gen, const param_type& parm);

   // property functions
   vector<double> probabilities() const;
   param_type param() const;
   void param(const param_type& parm);
   result_type min() const;
   result_type max() const;
   };
```

### <a name="parameters"></a>Parametreler

*IntType*\
**İnt**varsayılan olarak, tümsedo sonuç türü. Olası türler için [ \<rasgele>](../standard-library/random.md)bakın.

## <a name="remarks"></a>Açıklamalar

Bu örnekleme dağılımı, her aralıkta tek düze olasılık ile tek düze genişlik aralıkları vardır. Diğer örnekleme dağılımları hakkında bilgi için [piecewise_linear_distribution Sınıf](../standard-library/piecewise-linear-distribution-class.md) ve piecewise_constant_distribution [Sınıfı'na](../standard-library/piecewise-constant-distribution-class.md)bakın.

Bireysel üyeler le ilgili makalelere aşağıdaki tablo bağlantıları:

|||
|-|-|
|[discrete_distribution](#discrete_distribution)|`discrete_distribution::param`|
|`discrete_distribution::operator()`|[param_type](#param_type)|

Özellik işlevi, `vector<double> probabilities()` oluşturulan her bir arastıcının tek tek olasılıklarını döndürür.

Dağıtım sınıfları ve üyeleri hakkında daha fazla bilgi için [ \<rastgele>](../standard-library/random.md)bakın.

## <a name="example"></a>Örnek

```cpp
// compile with: /EHsc /W4
#include <random>
#include <iostream>
#include <iomanip>
#include <string>
#include <map>

using namespace std;

void test(const int s) {

    // uncomment to use a non-deterministic generator
    // random_device rd;
    // mt19937 gen(rd());
    mt19937 gen(1701);

    discrete_distribution<> distr({ 1, 2, 3, 4, 5 });

    cout << endl;
    cout << "min() == " << distr.min() << endl;
    cout << "max() == " << distr.max() << endl;
    cout << "probabilities (value: probability):" << endl;
    vector<double> p = distr.probabilities();
    int counter = 0;
    for (const auto& n : p) {
        cout << fixed << setw(11) << counter << ": " << setw(14) << setprecision(10) << n << endl;
        ++counter;
    }
    cout << endl;

    // generate the distribution as a histogram
    map<int, int> histogram;
    for (int i = 0; i < s; ++i) {
        ++histogram[distr(gen)];
    }

    // print results
    cout << "Distribution for " << s << " samples:" << endl;
    for (const auto& elem : histogram) {
        cout << setw(5) << elem.first << ' ' << string(elem.second, ':') << endl;
    }
    cout << endl;
}

int main()
{
    int samples = 100;

    cout << "Use CTRL-Z to bypass data entry and run using default values." << endl;
    cout << "Enter an integer value for the sample count: ";
    cin >> samples;

    test(samples);
}
```

```Output
Use CTRL-Z to bypass data entry and run using default values.
Enter an integer value for the sample count: 100
min() == 0
max() == 4
probabilities (value: probability):
          0:   0.0666666667
          1:   0.1333333333
          2:   0.2000000000
          3:   0.2666666667
          4:   0.3333333333

Distribution for 100 samples:
    0 :::
    1 ::::::::::::::
    2 ::::::::::::::::::
    3 :::::::::::::::::::::::::::::
    4 ::::::::::::::::::::::::::::::::::::
```

## <a name="requirements"></a>Gereksinimler

**Üstbilgi:** \<rastgele>

**Ad alanı:** std

## <a name="discrete_distributiondiscrete_distribution"></a><a name="discrete_distribution"></a>discrete_distribution::discrete_distribution

Dağıtımı kurar.

```cpp
// default constructor
discrete_distribution();

// construct using a range of weights, [firstW, lastW)
template <class InputIterator>
discrete_distribution(InputIterator firstW, InputIterator lastW);

// construct using an initializer list for range of weights
discrete_distribution(initializer_list<double> weightlist);

// construct using unary operation function
template <class UnaryOperation>
discrete_distribution(size_t count, double low, double high, UnaryOperation weightfunc);

// construct from an existing param_type structure
explicit discrete_distribution(const param_type& parm);
```

### <a name="parameters"></a>Parametreler

*ilkW*\
Dağıtım oluşturmak için listedeki ilk yineleyici.

*lastW*\
Dağıtım oluşturmak için listedeki son yineleyici (yinelemeciler sonu için boş bir öğe kullandığından dahil değildir).

*ağırlık listesi*\
[Dağıtımın](../cpp/initializers.md) initializer_list.

*Sayısı*\
Dağıtım aralığındaki eleman sayısı. Eğer, `count==0`varsayılan oluşturucuya eşdeğer (her zaman sıfır üretir).

*Düşük*\
Dağıtım aralığındaki en düşük değer.

*Yüksek*\
Dağıtım aralığındaki en yüksek değer.

*weightfunc*\
Dağılım için olasılık işlevini temsil eden nesne. Hem parametre hem de iade değeri **çift**e dönüştürülebilir olmalıdır.

*parm*\
Dağılımı `param_type` oluşturmak için kullanılan yapı.

### <a name="remarks"></a>Açıklamalar

Varsayılan oluşturucu, depolanan olasılık değeri 1 değeri olan bir öğeye sahip bir nesne inşa eder. Bu, her zaman sıfır üreten bir dağıtımla sonuçlanır.

*parametreleri firstW* ve *lastW* olan yineleyici aralığı oluşturucu, aralık sırası [*firstW*, *lastW]* üzerinden yineleyicilerden alınan ağırlık değerlerini kullanarak bir dağıtım nesnesi kurar.

*Ağırlık listesi* parametresi olan baş harf listesi oluşturucu, başharf listesi *ağırlık listesinden*ağırlıkları olan bir dağıtım nesnesi inşa eder.

*Sayı*, *düşük,* *yüksek*ve *weightfunc* parametreleri olan yapıcı, bu kurallara göre başharfle başlatınır bir dağıtım nesnesi inşa eder:

- 1 < *sayısı,* **n** = 1 ve bu nedenle varsayılan oluşturucu eşdeğer, her zaman sıfır üreten.
- 0 > *sayılsa,* **n** = *sayısı*. Sağlanan **d** = (*yüksek* - *düşük*) / **n** sıfırdan büyüktür, **d** düzgün `weight[k] = weightfunc(x)`alt aralıkları kullanılarak, her ağırlık aşağıdaki gibi atanır: , **x** = *düşük* + **k** * **d** + **d** / 2, **k** = 0 için, ..., **n** - 1.

Parm parametresi olan yapı oluşturucu, depolanan parametre yapısı olarak *parm* kullanarak bir dağıtım nesnesi inşa eder. *parm* `param_type`

## <a name="discrete_distributionparam_type"></a><a name="param_type"></a>discrete_distribution::param_type

Dağıtımın tüm parametrelerini depolar.

```cpp
struct param_type {
   typedef discrete_distribution<result_type> distribution_type;
   param_type();

   // construct using a range of weights, [firstW, lastW)
   template <class InputIterator>
   param_type(InputIterator firstW, InputIterator lastW);

   // construct using an initializer list for range of weights
   param_type(initializer_list<double> weightlist);

   // construct using unary operation function
   template <class UnaryOperation>
   param_type(size_t count, double low, double high, UnaryOperation weightfunc);

   std::vector<double> probabilities() const;

   bool operator==(const param_type& right) const;
   bool operator!=(const param_type& right) const;
   };
```

### <a name="parameters"></a>Parametreler

*ilkW*\
Dağıtım oluşturmak için listedeki ilk yineleyici.

*lastW*\
Dağıtım oluşturmak için listedeki son yineleyici (yinelemeciler sonu için boş bir öğe kullandığından dahil değildir).

*ağırlık listesi*\
[Dağıtımın](../cpp/initializers.md) initializer_list.

*Sayısı*\
Dağıtım aralığındaki eleman sayısı. *Sayım* 0 ise, bu varsayılan oluşturucuya eşdeğerdir (her zaman sıfır oluşturur).

*Düşük*\
Dağıtım aralığındaki en düşük değer.

*Yüksek*\
Dağıtım aralığındaki en yüksek değer.

*weightfunc*\
Dağılım için olasılık işlevini temsil eden nesne. Hem parametre hem de iade değeri **çift**e dönüştürülebilir olmalıdır.

*Doğru*\
Bununla `param_type` karşılaştırılacak nesne.

### <a name="remarks"></a>Açıklamalar

Bu parametre paketi, `operator()` iade değerini oluşturmak için geçirilebilir.

## <a name="see-also"></a>Ayrıca bkz.

[\<rastgele>](../standard-library/random.md)
