---
title: 'Nasıl yapılır: Zamanlayıcı Örneğini Yönetme'
ms.date: 11/04/2016
helpviewer_keywords:
- managing a scheduler instance [Concurrency Runtime]
- scheduler instances, managing [Concurrency Runtime]
ms.assetid: 2cc804f0-5ff3-498b-97f1-a9f67a005448
ms.openlocfilehash: c7ec321eaf0960dc14b61bbd8fdc76b53a31f8c5
ms.sourcegitcommit: a8ef52ff4a4944a1a257bdaba1a3331607fb8d0f
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 02/11/2020
ms.locfileid: "77141722"
---
# <a name="how-to-manage-a-scheduler-instance"></a>Nasıl yapılır: Zamanlayıcı Örneğini Yönetme

Zamanlayıcı örnekleri, belirli zamanlama ilkelerini çeşitli iş yükleriyle ilişkilendirmenize olanak sağlar. Bu konu, bir Zamanlayıcı örneğinin nasıl oluşturulacağını ve yönetileceğini gösteren iki temel örnek içerir.

Örnekler varsayılan Zamanlayıcı ilkelerini kullanan zamanlayıcılar oluşturur. Özel bir ilke kullanan bir Zamanlayıcı oluşturan bir örnek için bkz. [nasıl yapılır: belirli Zamanlayıcı Ilkeleri belirtme](../../parallel/concrt/how-to-specify-specific-scheduler-policies.md).

## <a name="to-manage-a-scheduler-instance-in-your-application"></a>Uygulamanızda bir zamanlayıcı örneğini yönetmek için

1. Zamanlayıcı için kullanılacak ilke değerlerini içeren bir [concurrency:: SchedulerPolicy](../../parallel/concrt/reference/schedulerpolicy-class.md) nesnesi oluşturun.

1. Bir zamanlayıcı örneği oluşturmak için [concurrency:: CurrentScheduler:: Create](reference/currentscheduler-class.md#create) metodunu veya [concurrency:: Scheduler:: Create](reference/scheduler-class.md#create) metodunu çağırın.

   `Scheduler::Create` yöntemini kullanırsanız, zamanlayıcıyı geçerli bağlamla ilişkilendirmeniz gerektiğinde [concurrency:: Scheduler:: Attach](reference/scheduler-class.md#attach) metodunu çağırın.

1. Sinyalsiz, otomatik sıfırlama olay nesnesine bir tanıtıcı oluşturmak için [CreateEvent](/windows/win32/api/synchapi/nf-synchapi-createeventw) işlevini çağırın.

1. Yeni oluşturduğunuz olay nesnesine tanıtıcıyı [concurrency:: CurrentScheduler:: RegisterShutdownEvent](reference/currentscheduler-class.md#registershutdownevent) metoduna veya [concurrency:: Scheduler:: RegisterShutdownEvent](reference/scheduler-class.md#registershutdownevent) metoduna geçirin. Bu, Zamanlayıcı yok edildiğinde ayarlanacak olayı kaydeder.

1. Geçerli zamanlayıcının zamanlamasını istediğiniz görevleri gerçekleştirin.

1. Geçerli zamanlayıcıyı ayırmak ve önceki zamanlayıcıyı güncel olarak geri yüklemek için [concurrency:: CurrentScheduler::D etach](reference/currentscheduler-class.md#detach) yöntemini çağırın.

   `Scheduler::Create` yöntemini kullanırsanız, `Scheduler` nesnesinin başvuru sayısını azaltmak için [concurrency:: Scheduler:: Release](reference/scheduler-class.md#release) metodunu çağırın.

1. Zamanlayıcıyı, Scheduler 'ın kapatılmasını beklemek için olayı [WaitForSingleObject](/windows/win32/api/synchapi/nf-synchapi-waitforsingleobject) işlevine geçirin.

1. Olay nesnesine olan tanıtıcıyı kapatmak için [CloseHandle](/windows/win32/api/handleapi/nf-handleapi-closehandle) işlevini çağırın.

## <a name="example"></a>Örnek

Aşağıdaki kod, bir zamanlayıcı örneğini yönetmenin iki yolunu göstermektedir. Her örnek ilk olarak geçerli Scheduler 'ın benzersiz tanımlayıcısını yazdıran bir görevi gerçekleştirmek için varsayılan zamanlayıcıyı kullanır. Her örnek, aynı görevi yeniden gerçekleştirmek için bir zamanlayıcı örneği kullanır. Son olarak, her örnek varsayılan zamanlayıcıyı geçerli bir olarak geri yükler ve görevi bir kez daha gerçekleştirir.

İlk örnek, bir zamanlayıcı örneği oluşturmak ve bunu geçerli bağlamla ilişkilendirmek için [concurrency:: CurrentScheduler](../../parallel/concrt/reference/currentscheduler-class.md) sınıfını kullanır. İkinci örnek, aynı görevi gerçekleştirmek için [concurrency:: Scheduler](../../parallel/concrt/reference/scheduler-class.md) sınıfını kullanır. Genellikle, `CurrentScheduler` sınıfı geçerli Scheduler ile çalışmak için kullanılır. `Scheduler` sınıfını kullanan ikinci örnek, Scheduler 'ın geçerli bağlamla ne zaman ilişkilendirildiğini denetlemek istediğinizde veya belirli görevlerle ilgili zamanlayıcılar ilişkilendirmek istediğinizde yararlıdır.

[!code-cpp[concrt-scheduler-instance#1](../../parallel/concrt/codesnippet/cpp/how-to-manage-a-scheduler-instance_1.cpp)]

Bu örnek aşağıdaki çıktıyı üretir.

```Output
Using CurrentScheduler class...

Current scheduler id: 0
Creating and attaching scheduler...
Current scheduler id: 1
Detaching scheduler...
Current scheduler id: 0

Using Scheduler class...

Current scheduler id: 0
Creating scheduler...
Attaching scheduler...
Current scheduler id: 2
Detaching scheduler...
Current scheduler id: 0
```

## <a name="compiling-the-code"></a>Kod Derleniyor

Örnek kodu kopyalayın ve bir Visual Studio projesine yapıştırın veya `scheduler-instance.cpp` adlı bir dosyaya yapıştırın ve sonra bir Visual Studio komut Istemi penceresinde aşağıdaki komutu çalıştırın.

> **CL. exe/EHsc Scheduler-instance. cpp**

## <a name="see-also"></a>Ayrıca bkz.

[Zamanlayıcı Örnekleri](../../parallel/concrt/scheduler-instances.md)<br/>
[Nasıl yapılır: Belirli Zamanlayıcı İlkeleri Belirtme](../../parallel/concrt/how-to-specify-specific-scheduler-policies.md)
