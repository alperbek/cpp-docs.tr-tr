---
title: Ad Alanları
ms.date: 11/04/2016
helpviewer_keywords:
- union keyword [C], tags
- enumeration tags
- structure tags
- names [C++], declared elements
- name spaces [C++]
- tags, structure tags
- union keyword [C]
ms.assetid: b4bda1d1-cb5e-4f60-ac2b-29af93d8a9a2
ms.openlocfilehash: 76ad9b797a4f192e8f22f8c040f5a308371a461b
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62325773"
---
# <a name="name-spaces"></a>Ad Alanları

Derleyici, farklı türlerde öğeler için kullanılan tanımlayıcılar arasında ayrım yapmak için "ad alanları" ayarlar. Her ad alanı içindeki adların, çakışmayı önlemek için benzersiz olması gerekir, ancak aynı ada sahip birden fazla ad alanında görünebilirler. Bu, öğelerin farklı ad alanlarında olması şartıyla, iki veya daha fazla farklı öğe için aynı tanımlayıcıyı kullanabileceğiniz anlamına gelir. Derleyici, programdaki tanımlayıcının sözdizimsel bağlamına göre başvuruları çözümleyebilir.

> [!NOTE]
> Ad alanının sınırlı C kavramının C++ "namespace" özelliği ile karıştırmayın. Daha fazla bilgi için bkz. C++ dil başvurusunda [ad alanları](../cpp/namespaces-cpp.md) .

Bu liste, C 'de kullanılan ad alanlarını açıklar.

Deyim etiketleri adlandırılmış deyim bir parçasıdır. İfade etiketlerinin tanımları her zaman iki nokta üst üste gelir, ancak **büyük/küçük harf** etiketlerinin bir parçası değildir. İfade etiketlerinin kullanımları her zaman hemen **Git**anahtar sözcüğünü izler. İfade etiketlerinin diğer adlardan veya diğer işlevlerdeki etiket adlarından farklı olması gerekmez.

Yapı, birleşim ve Numaralandırma etiketleri bu Etiketler yapı, birleşim ve numaralandırma türü Belirticilerinin bir parçasıdır ve varsa, her zaman ayrılmış sözcükler **struct**, **Union**veya **enum**' ı hemen izleyin. Etiket adları, aynı görünürlüğe sahip diğer tüm yapı, sabit listesi veya birleşim etiketlerinden farklı olmalıdır.

Yapılar veya birleşimler üye adları üyeleri her bir yapıyla ve birleşim türüyle ilişkili ad alanlarında ayrılır. Diğer bir deyişle, aynı tanımlayıcı aynı zamanda herhangi bir sayıda yapıya veya birleşimde bir bileşen adı olabilir. Bileşen adları tanımları, her zaman yapı veya birleşim türü belirticileri içinde gerçekleşir. Bileşen adlarının kullanımları her zaman üye seçim işleçlerini (**->** ve **.**) izler. Üyenin adı yapı veya birleşim içinde benzersiz olmalıdır, ancak farklı yapıların ve birleşimlerin üyelerinin adları veya yapının kendisi de dahil olmak üzere programdaki diğer adlardan farklı olması gerekmez.

Normal tanımlayıcılar, diğer tüm adlar değişkenleri, işlevleri (resmi parametreler ve yerel değişkenler dahil) ve numaralandırma sabitlerini içeren bir ad alanına girer. Tanımlayıcı adlarında iç içe görünürlük vardır, bu sayede bunları bloklar içinde yeniden tanımlayabilirsiniz.

Typedef adları typedef adları aynı kapsamda tanımlayıcı olarak kullanılamaz.

Örneğin, yapı etiketleri, yapı üyeleri ve değişken adları üç farklı ad alanı içinde olduğundan, bu örnekteki adlı `student` üç öğe çakışmaz. Her öğenin bağlamı, programdaki her oluşumun `student` doğru yorumlanmasını sağlar. (Yapılar hakkında bilgi için bkz. [Yapı bildirimleri](../c-language/structure-declarations.md).)

```C
struct student {
   char student[20];
   int class;
   int id;
   } student;
```

Struct `student` anahtar sözcüğünden sonra **struct** göründüğünde, derleyici onu bir yapı etiketi olarak tanır. Bir `student` üye seçim işlecinden (**->** veya **.**) sonra göründüğünde, ad yapı üyesine başvurur. Diğer bağlamlarda, `student` yapı değişkenine başvurur. Ancak, etiket adı alanını aşırı yüklemek, anlamı olumsuz bir şekilde gösterdiğinden bu yana önerilmez.

## <a name="see-also"></a>Ayrıca bkz.

[Program Yapısı](../c-language/program-structure.md)
