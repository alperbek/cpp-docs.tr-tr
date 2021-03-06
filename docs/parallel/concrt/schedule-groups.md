---
title: Zamanlama Grupları
ms.date: 11/04/2016
helpviewer_keywords:
- schedule groups
ms.assetid: 03523572-5891-4d17-89ce-fa795605f28b
ms.openlocfilehash: 1765c10f4cf8fe499aed1a140d2bba1ecaaf2300
ms.sourcegitcommit: a8ef52ff4a4944a1a257bdaba1a3331607fb8d0f
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 02/11/2020
ms.locfileid: "77142305"
---
# <a name="schedule-groups"></a>Zamanlama Grupları

Bu belge, Eşzamanlılık Çalışma Zamanı zamanlama gruplarının rolünü açıklamaktadır. Bir *zamanlama grubu* , ilgili görevleri birlikte sıralar veya gruplar. Her Scheduler bir veya daha fazla zamanlama grubuna sahiptir. Görevler arasında yüksek düzeyde yere ihtiyacınız olduğunda, örneğin, bir ilgili görev grubu aynı işlemci düğümünde yürütmeyi avantajı olduğunda zamanlama gruplarını kullanın. Buna karşılık, uygulamanız belirli kalite gereksinimlerine sahip olduğunda Zamanlayıcı örnekleri kullanın, örneğin, bir görev kümesine ayrılan işlem kaynakları miktarını sınırlamak istediğinizde. Zamanlayıcı örnekleri hakkında daha fazla bilgi için bkz. [Zamanlayıcı örnekleri](../../parallel/concrt/scheduler-instances.md).

> [!TIP]
> Eşzamanlılık Çalışma Zamanı varsayılan bir Zamanlayıcı sağlar ve bu nedenle uygulamanızda bir tane oluşturmanız gerekmez. Görev Zamanlayıcı uygulamalarınızın performansını hassas bir şekilde ayarlamanıza yardımcı olduğundan, Eşzamanlılık Çalışma Zamanı yeni başladıysanız [paralel Desenler kitaplığı (PPL)](../../parallel/concrt/parallel-patterns-library-ppl.md) veya [zaman uyumsuz aracılar Kitaplığı](../../parallel/concrt/asynchronous-agents-library.md) ile başlamanız önerilir.

Her `Scheduler` nesnesinin her zamanlama düğümü için varsayılan bir zamanlama grubu vardır. Bir *zamanlama düğümü* , temeldeki sistem topolojisine eşlenir. Çalışma zamanı, her işlemci paketi veya Tekdüzen olmayan bellek mimarisi (NUMA) düğümü için bir zamanlama düğümü oluşturur ve bu sayı daha büyüktür. Bir görevi bir zamanlama grubuyla açıkça ilişkilendirmediyseniz Zamanlayıcı, görevin hangi gruba ekleneceğini seçer.

`SchedulingProtocol` Zamanlayıcı İlkesi, Scheduler 'ın her bir zamanlama grubundaki görevleri yürütme sırasını etkiler. `SchedulingProtocol` `EnhanceScheduleGroupLocality` olarak ayarlandığında (varsayılan olarak), Görev Zamanlayıcı geçerli görev tamamlandığında veya işbirliği yaptığı sırada üzerinde çalıştığı zamanlama grubundan sonraki görevi seçer. Görev Zamanlayıcı, geçerli zamanlama grubunu iş için bir sonraki kullanılabilir gruba geçmeden önce arar. Buna karşılık, `SchedulingProtocol` `EnhanceForwardProgress`olarak ayarlandığında, her görev tamamlandıktan veya her gerçekleştirildikten sonra Zamanlayıcı bir sonraki zamanlama grubuna gider. Bu ilkeleri karşılaştıran bir örnek için bkz. [nasıl yapılır: yürütme sırasını etkilemek Için zamanlama gruplarını kullanma](../../parallel/concrt/how-to-use-schedule-groups-to-influence-order-of-execution.md).

Çalışma zamanı, zamanlama gruplarını temsil etmek için [concurrency:: ScheduleGroup](../../parallel/concrt/reference/schedulegroup-class.md) sınıfını kullanır. `ScheduleGroup` nesnesi oluşturmak için [concurrency:: CurrentScheduler:: CreateScheduleGroup](reference/currentscheduler-class.md#createschedulegroup) veya [concurrency:: Scheduler:: CreateScheduleGroup](reference/scheduler-class.md#createschedulegroup) metodunu çağırın. Çalışma zamanı, `ScheduleGroup` nesnelerinin yaşam süresini denetlemek için bir başvuru sayma mekanizması kullanır, tıpkı `Scheduler` nesneleri gibi. Bir `ScheduleGroup` nesnesi oluşturduğunuzda, çalışma zamanı başvuru sayacını bir olarak ayarlar. [Concurrency:: ScheduleGroup:: Reference](reference/schedulegroup-class.md#reference) yöntemi başvuru sayacını bir tane artırır. [Concurrency:: ScheduleGroup:: Release](reference/schedulegroup-class.md#release) yöntemi başvuru sayacını bir tane azaltır.

Eşzamanlılık Çalışma Zamanı pek çok tür, bir nesneyi bir zamanlama grubuyla ilişkilendirmenizi sağlar. Örneğin, concurrency [:: Agent](../../parallel/concrt/reference/agent-class.md) sınıfı ve [concurrency:: unbounded_buffer](reference/unbounded-buffer-class.md), [concurrency:: JOIN](../../parallel/concrt/reference/join-class.md)ve concurrency::[timer](reference/timer-class.md)gibi ileti bloğu sınıfları, bir `ScheduleGroup` nesnesi alan oluşturucunun aşırı yüklenmiş sürümlerini sağlar. Çalışma zamanı, görevi zamanlamak için bu `ScheduleGroup` nesnesiyle ilişkili `Scheduler` nesnesini kullanır.

Hafif bir görevi zamanlamak için [concurrency:: ScheduleGroup:: ScheduleTask](reference/schedulegroup-class.md#scheduletask) yöntemini de kullanabilirsiniz. Hafif görevler hakkında daha fazla bilgi için bkz. [hafif görevler](../../parallel/concrt/lightweight-tasks.md).

## <a name="example"></a>Örnek

Görev yürütme sırasını denetlemek için zamanlama gruplarını kullanan bir örnek için bkz. [nasıl yapılır: yürütme sırasını etkilemek Için zamanlama gruplarını kullanma](../../parallel/concrt/how-to-use-schedule-groups-to-influence-order-of-execution.md).

## <a name="see-also"></a>Ayrıca bkz.

[Görev Zamanlayıcı](../../parallel/concrt/task-scheduler-concurrency-runtime.md)<br/>
[Zamanlayıcı Örnekleri](../../parallel/concrt/scheduler-instances.md)<br/>
[Nasıl yapılır: Yürütme Sırasını Etkilemek için Zamanlama Grupları Kullanma](../../parallel/concrt/how-to-use-schedule-groups-to-influence-order-of-execution.md)
