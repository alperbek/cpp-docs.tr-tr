---
title: '&lt;ios &gt;'
ms.date: 11/04/2016
f1_keywords:
- <ios>
- ios/std::<ios>
helpviewer_keywords:
- ios header
ms.assetid: d3d4c161-2f37-4f04-93cc-0a2a89984a9c
ms.openlocfilehash: a322e517a4adb51879fc2a60f6c08f6561276de9
ms.sourcegitcommit: 590e488e51389066a4da4aa06d32d4c362c23393
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/21/2019
ms.locfileid: "72689501"
---
# <a name="ltiosgt"></a>&lt;ios &gt;

Birden çok tür ve temel olarak Iostreams işleminin işlevlerini tanımlar. Bu üst bilgi, genellikle başka bir ıostream üst bilgisi tarafından sizin için eklenmiştir; Bunu nadiren doğrudan dahil edersiniz.

## <a name="requirements"></a>Gereksinimler

**Üst bilgi**: \<ios >

**Ad alanı:** std

> [!NOTE]
> @No__t_0ios > kitaplığı `#include <iosfwd>` ifadesini kullanır.

## <a name="remarks"></a>Açıklamalar

Büyük bir işlev grubu, işleicilere sahiptir. @No__t_0ios > bildirildiği bir işleyici, [ios_base](../standard-library/ios-base-class.md)sınıfının bağımsız değişken nesnesinde depolanan değerleri değiştirir. Diğer düzenlemeler, [basic_istream](../standard-library/basic-istream-class.md) veya [basic_ostream](../standard-library/basic-ostream-class.md)sınıf şablonlarından birinin özelleştirmesi gibi bu sınıftan türetilmiş bir türün nesneleri tarafından denetlenen akışlar üzerinde eylemler gerçekleştirir. Örneğin, [noskipws](../standard-library/ios-functions.md#noskipws)(**Str**), bu türlerden biri olabilen nesne `str` `ios_base::skipws` biçim bayrağını temizler.

Ayrıca, `ios_base` türetilen sınıflar için sağlanan özel ekleme ve ayıklama işlemleri nedeniyle bir işleme bir çıkış akışına ekleyerek veya bir giriş akışından çıkartarak bir işleme çağırabilirsiniz. Örneğin:

```cpp
istr>> noskipws;
```

[noskipws](../standard-library/ios-functions.md#noskipws)(**ISTR**) öğesini çağırır.

## <a name="members"></a>Üyeler

### <a name="typedefs"></a>Tür tanımları

|||
|-|-|
|[işlemine](../standard-library/ios-typedefs.md#ios)|Eski ıostream kitaplığından iOS sınıfını destekler.|
|[streamoff](../standard-library/ios-typedefs.md#streamoff)|İç işlemleri destekler.|
|[streampos](../standard-library/ios-typedefs.md#streampos)|Arabellek işaretçisinin veya dosya işaretçisinin geçerli konumunu tutar.|
|[streamsize](../standard-library/ios-typedefs.md#streamsize)|Akışın boyutunu belirtir.|
|[wmorolar](../standard-library/ios-typedefs.md#wios)|Eski ıostream kitaplığından wios sınıfını destekler.|
|[wstreampos](../standard-library/ios-typedefs.md#wstreampos)|Arabellek işaretçisinin veya dosya işaretçisinin geçerli konumunu tutar.|

### <a name="manipulators"></a>Manipülatörleri

|||
|-|-|
|[boolalpha](../standard-library/ios-functions.md#boolalpha)|[Bool](../cpp/bool-cpp.md) türündeki değişkenlerin akışta **doğru** veya **yanlış** olarak göründüğünü belirtir.|
|[Dec](../standard-library/ios-functions.md#dec)|Tamsayı değişkenlerinin taban 10 gösteriminde göründüğünü belirtir.|
|[defaultfloat](../standard-library/ios-functions.md#ios_defaultfloat)|Bir `ios_base` nesnesinin bayraklarını, float değerleri için varsayılan bir görüntüleme biçimi kullanacak şekilde yapılandırır.|
|[Düzenle](../standard-library/ios-functions.md#fixed)|Sabit ondalık gösterimde bir kayan noktalı sayının görüntülendiğini belirtir.|
|[eşlenecek](../standard-library/ios-functions.md#hex)|Tamsayı değişkenlerinin temel 16 gösterimde göründüğünü belirtir.|
|[onaltıdan kayan](../standard-library/ios-functions.md#hexfloat)|
|[internal](../standard-library/ios-functions.md#internal)|Bir sayının işaretinin hizalı olarak sola ve sağa yaslanmasına neden olur.|
|[tarafta](../standard-library/ios-functions.md#left)|Çıktı genişliği, sol kenar boşluğu ile boşaltımın üzerinde görünmesini sağlayan metnin geniş olmasına neden olur.|
|[noboolalpha](../standard-library/ios-functions.md#noboolalpha)|[Bool](../cpp/bool-cpp.md) türündeki değişkenlerin akışta 1 veya 0 olarak göründüğünü belirtir.|
|[noshowbase](../standard-library/ios-functions.md#noshowbase)|Bir sayının gösterildiği notational temelini belirtir.|
|[noshowpoint](../standard-library/ios-functions.md#noshowpoint)|Kısmi bölümü sıfır olan kayan noktalı sayıların yalnızca tam sayı kısmını görüntüler.|
|[noshowpos](../standard-library/ios-functions.md#noshowpos)|Pozitif sayıların açıkça imzalanmamasını sağlar.|
|[noskipws](../standard-library/ios-functions.md#noskipws)|Giriş akışı tarafından boşlukların okunmasına neden olur.|
|[nounitbuf](../standard-library/ios-functions.md#nounitbuf)|Arabellek dolduğunda çıktının arabelleğe alınmasına ve işlenmesine neden olur.|
|[nouppercase](../standard-library/ios-functions.md#nouppercase)|Bilimsel gösterimdeki onaltılık basamakların ve üs harflerin küçük harf olarak göründüğünü belirtir.|
|[Oct](../standard-library/ios-functions.md#oct)|Tamsayı değişkenlerinin taban 8 gösteriminde göründüğünü belirtir.|
|[Right](../standard-library/ios-functions.md#right)|Çıktı genişliği doğru olmayan metnin akış temizlemesi durumunda sağ kenar boşluğu ile görünmesini sağlar.|
|[bilimsel](../standard-library/ios-functions.md#scientific)|, Kayan nokta numaralarının bilimsel gösterim kullanılarak görüntülenmesine neden olur.|
|[showbase](../standard-library/ios-functions.md#showbase)|Bir sayının gösterileceği notational tabanını gösterir.|
|[showpoint](../standard-library/ios-functions.md#showpoint)|Kesirli bölüm sıfır olduğunda bile ondalık noktanın sağ tarafındaki bir kayan nokta sayısı ve rakamların tam sayı kısmını görüntüler.|
|[showpos](../standard-library/ios-functions.md#showpos)|Pozitif sayıların açıkça imzalanmasına neden olur.|
|[skipws](../standard-library/ios-functions.md#skipws)|Giriş akışı tarafından okunmamasına neden olan boşluk.|
|[unitbuf](../standard-library/ios-functions.md#unitbuf)|Arabellek boş olmadığında çıktının işlenmesine neden olur.|
|[İngiliz](../standard-library/ios-functions.md#uppercase)|Bilimsel gösterimdeki onaltılık basamakların ve üs 'ın büyük harfle göründüğünü belirtir.|

### <a name="error-reporting"></a>Hata Raporlama

|||
|-|-|
|[io_errc](../standard-library/ios-functions.md#io_errc)||
|[is_error_code_enum](../standard-library/ios-functions.md#is_error_code_enum)||
|[iostream_category](../standard-library/ios-functions.md#iostream_category)||
|[make_error_code](../standard-library/ios-functions.md#make_error_code)||
|[make_error_condition](../standard-library/ios-functions.md#make_error_condition)||

### <a name="classes"></a>Sınıflar

|||
|-|-|
|[basic_ios](../standard-library/basic-ios-class.md)|Sınıf şablonu, şablon parametrelerine bağlı olan giriş akışları (sınıf şablonu [basic_istream](../standard-library/basic-istream-class.md)) ve çıkış akışları ( [basic_ostream](../standard-library/basic-ostream-class.md)sınıfı) için ortak depolama ve üye işlevlerini açıklar.|
|[fpos](../standard-library/fpos-class.md)|Sınıf şablonu, herhangi bir akışta rastgele bir dosya konumu göstergesini geri yüklemek için gereken tüm bilgileri depolayabilen bir nesneyi tanımlar.|
|[ios_base](../standard-library/ios-base-class.md)|Sınıfı, şablon parametrelerine bağlı olmayan hem giriş hem de çıkış akışları için ortak olan depolama ve üye işlevlerini açıklar.|

## <a name="see-also"></a>Ayrıca bkz.

[Üst bilgi dosyaları başvurusu](../standard-library/cpp-standard-library-header-files.md) \
[Standart kitaplıkta Iş parçacığı güvenliği \ C++ ](../standard-library/thread-safety-in-the-cpp-standard-library.md)
[iostream programlama](../standard-library/iostream-programming.md) \
[iostreams Kuralları](../standard-library/iostreams-conventions.md)
