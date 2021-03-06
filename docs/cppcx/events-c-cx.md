---
title: Olaylar (C++/CX)
description: Windows Çalışma Zamanı için/CX C++kullanarak olay işleyicileri oluşturma ve kullanma.
ms.date: 02/03/2020
ms.assetid: 31c8e08a-00ad-40f9-8f7e-124864aaad58
ms.openlocfilehash: b40f71b183561b52047c1f7316def3d895465d2a
ms.sourcegitcommit: 44eeb065c3148d0484de791080a3f963109744fc
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/18/2020
ms.locfileid: "79509382"
---
# <a name="events-ccx"></a>Olaylar (C++/CX)

Bir Windows Çalışma Zamanı türü, olayları bildirebilir (yani, yayımlayabilir) ve aynı bileşendeki veya diğer bileşenlerde bulunan istemci kodu, olay *işleyicileri* adlı yöntemleri olayla ilişkilendirerek, bu olaylara abone olabilir. Birden çok olay işleyicisi tek bir olayla ilişkilendirilebilir. Yayımlama nesnesi olayı harekete geçirirse, tüm olay işleyicilerinin çağrılmasına neden olur. Bu şekilde, abone olan bir sınıf, yayımcı olayı harekete geçirirse uygun olan herhangi bir özel eylemi gerçekleştirebilir. Bir olay, tüm olay işleyicilerinin olaya abone olmak için sahip olması gereken imzayı belirten bir temsilci türü içerir.

## <a name="consuming-events-in-windows-components"></a>Windows bileşenlerinde olayları kullanma

Windows Çalışma Zamanı birçok bileşeni olayları kullanıma sunar. Örneğin, algılayıcı yeni bir sütun değeri bildirdiğinde bir açık algılayıcı nesnesi ReadingChanged olayını tetikluyor. Programınızda bir Lightalgılayıcı nesnesi kullandığınızda, ReadingChanged olayı tetiklendiğinde çağrılacak yöntemi tanımlayabilirsiniz. Yöntemi, yapmak istediğiniz her şeyi yapabilir; Tek gereksinim, imzası çağrılan temsilcinin imzasıyla aynı olmalıdır. Bir temsilci olay işleyicisi oluşturma ve bir olaya abone olma hakkında daha fazla bilgi için bkz. [Temsilciler](../cppcx/delegates-c-cx.md).

## <a name="creating-custom-events"></a>Özel olaylar oluşturma

### <a name="declaration"></a>Bildirim

Bir başvuru sınıfında veya arabirimde bir olay bildirebilirsiniz ve ortak, iç (ortak/özel), genel korumalı, korunan, özel korumalı veya özel erişilebilirlik olabilir. Bir olayı bildirdiğinizde, derleyici dahili olarak iki erişimci yöntemi sunan bir nesne oluşturur: Ekle ve Kaldır. Abone nesneleri olay işleyicilerini kaydederken, olay nesnesi bunları bir koleksiyonda depolar. Bir olay harekete geçirildiğinde, olay nesnesi kendi listesindeki tüm işleyicileri sırayla çağırır. Aşağıdaki örnekte olduğu gibi önemsiz bir olay da örtük bir yedekleme deposuna ve örtük `add` ve `remove` erişimci yöntemlerine sahiptir. Ayrıca, bir özellik üzerinde özel `get` ve `set` erişimcileri belirtebileceğiniz şekilde kendi erişimclerinizi de belirtebilirsiniz.  Uygulama sınıfı, önemsiz bir olayda olay abone listesinde el ile geçiş yapılamaz.

Aşağıdaki örnek, bir olayın nasıl bildirilemeyeceğini ve tetikleneceği gösterilmektedir. Olayın bir temsilci türü olduğuna ve "^" simgesi kullanılarak bildirildiğine dikkat edin.

[!code-cpp[cx_events#01](../cppcx/codesnippet/CPP/cx_events/class1.h#01)]

### <a name="usage"></a>Kullanım

Aşağıdaki örnek, abone olan bir sınıfın olaya abone olmak için `+=` işlecini nasıl kullandığını gösterir ve olay tetiklendiğinde çağrılacak olay işleyicisini sağlar. Belirtilen işlevin, `EventTest` ad alanındaki Yayımcı tarafında tanımlanan temsilcinin imzasıyla eşleştiğinden emin olun.

[!code-cpp[cx_events#02](../cppcx/codesnippet/CPP/eventsupportinvs/eventclientclass.h#02)]

> [!WARNING]
> Genel olarak, döngüsel başvuruların oluşmaması için harika bir işlem yapmadığınız müddetçe, bir olay işleyicisi olarak bir lambda yerine adlandırılmış bir işlevin kullanılması daha iyidir. Adlandırılmış bir işlev, zayıf başvuruya göre "This" işaretçisini yakalar, ancak bir lambda bunu güçlü başvuruya göre yakalar ve döngüsel bir başvuru oluşturur. Daha fazla bilgi için bkz. [zayıf başvurular ve ayırma döngüleriC++(/CX)](../cppcx/weak-references-and-breaking-cycles-c-cx.md).

### <a name="custom-add-and-remove-methods"></a>Özel ekleme ve kaldırma yöntemleri

Dahili olarak, bir olayda Add yöntemi, Remove yöntemi ve bir Raise yöntemi vardır. İstemci kodu bir olaya abone olduğunda, Add yöntemi çağrılır ve geçirilen temsilci olayın çağırma listesine eklenir. Yayımlama sınıfı olayını çağırır, Raise () yönteminin çağrılmasına ve listedeki her temsilcinin sırayla çağrılmasına neden olur. Abone, olayın kaldırma yönteminin çağrılmasına neden olan temsilci listesinden kendisini kaldırabilir. Derleyici kodunuzda tanımlamadıysanız bu yöntemlerin varsayılan sürümlerini sağlar; Bunlar önemsiz olaylar olarak bilinir. Çoğu durumda, gereken tek şey basit bir olaydır.

Aboneler ekleme veya kaldırmaya yanıt olarak özel mantık gerçekleştirmeniz gerekiyorsa, bir olay için özel Ekle, kaldır ve Yükselt yöntemlerini belirtebilirsiniz. Örneğin, yalnızca olay raporlama için gerekli olan pahalı bir nesneniz varsa, bir istemci olaya gerçekten abone olana kadar nesnenin oluşturulmasını erteleyebilirsiniz.

Sonraki örnek, bir olaya özel ekleme, kaldırma ve oluşturma yöntemlerinin nasıl ekleneceğini gösterir:

[!code-cpp[cx_events#03](../cppcx/codesnippet/CPP/cx_events/class1.h#03)]

## <a name="removing-an-event-handler-from-the-subscriber-side"></a>Abone tarafında bir olay işleyicisini kaldırma

Nadir durumlarda, daha önce abone olduğunuz bir olay için bir olay işleyicisini kaldırmak isteyebilirsiniz. Örneğin, başka bir olay işleyicisiyle değiştirmek isteyebilirsiniz veya onu tarafından tutulan bazı kaynakları silmek isteyebilirsiniz. Bir işleyiciyi kaldırmak için `+=` işlemden döndürülen EventRegistrationToken 'ı depolamanız gerekir. Daha sonra bir olay işleyicisini kaldırmak için belirteçteki `-=` işlecini kullanabilirsiniz.  Ancak, özgün işleyici kaldırıldıktan sonra bile hala çağrılabilir. Örneğin, olay kaynağı işleyicilerin bir listesini aldığında ve bunları çağırmaya başladığında bir yarış durumu oluşabilir. Bu durumda bir olay işleyicisi kaldırılırsa, listenin tarihi eski olur. Bu nedenle, bir olay işleyicisini kaldırmak istiyorsanız üye bayrağı oluşturun. Olay kaldırılırsa bu ayarı ayarlayın ve ardından olay işleyicisinde bayrağı işaretleyin ve ayarlandıysa hemen geri dönün. Sonraki örnekte temel desenler gösterilmektedir.

[!code-cpp[cx_events#04](../cppcx/codesnippet/CPP/eventsupportinvs/eventclientclass.h#04)]

### <a name="remarks"></a>Açıklamalar

Birden çok işleyici aynı olayla ilişkili olabilir. Olay kaynağı, aynı iş parçacığından tüm olay işleyicileriyle ardışık olarak çağrı yapılır. Bir olay alıcısı olay işleyicisi yöntemi içinde engelliyorsa, olay kaynağının bu olay için diğer olay işleyicilerini yürütmesini engeller.

Olay kaynağının olay sıralarından olay işleyicilerini çağırdıkları sıra garanti edilmez ve çağrı çağrısından farklı olabilir.

## <a name="see-also"></a>Ayrıca bkz.

[Tür Sistemi](../cppcx/type-system-c-cx.md)<br/>
[Temsilciler](../cppcx/delegates-c-cx.md)<br/>
[C++/CX Dil Başvurusu](../cppcx/visual-c-language-reference-c-cx.md)<br/>
[Ad Alanları Başvurusu](../cppcx/namespaces-reference-c-cx.md)
