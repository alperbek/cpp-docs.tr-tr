---
title: Eşzamanlılık Çalışma Zamanında Özel Durum İşleme
ms.date: 11/04/2016
helpviewer_keywords:
- lightweight tasks, exception handling [Concurrency Runtime]
- exception handling [Concurrency Runtime]
- structured task groups, exception handling [Concurrency Runtime]
- agents, exception handling [Concurrency Runtime]
- task groups, exception handling [Concurrency Runtime]
ms.assetid: 4d1494fb-3089-4f4b-8cfb-712aa67d7a7a
ms.openlocfilehash: 4c7fee363da023b9252471a35aaecd262a55f17c
ms.sourcegitcommit: 7ecd91d8ce18088a956917cdaf3a3565bd128510
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/16/2020
ms.locfileid: "79422250"
---
# <a name="exception-handling-in-the-concurrency-runtime"></a>Eşzamanlılık Çalışma Zamanında Özel Durum İşleme

Eşzamanlılık Çalışma Zamanı birçok hata C++ türüyle iletişim kurmak için özel durum işlemeyi kullanır. Bu hatalar, çalışma zamanının geçersiz kullanımını, kaynak alma hatası gibi çalışma zamanı hatalarını ve görevlere ve görev gruplarına sağladığınız çalışma işlevlerinde oluşan hataları içerir. Bir görev veya görev grubu bir özel durum oluşturduğunda, çalışma zamanı bu özel durumu barındırır ve görevin veya görev grubunun bitmesini bekleyen bağlamına göre sıralar. Hafif görevler ve aracılar gibi bileşenler için çalışma zamanı sizin için özel durumları yönetmez. Bu durumlarda, kendi özel durum işleme mekanizmanızı uygulamanız gerekir. Bu konu, çalışma zamanının görevler, görev grupları, hafif görevler ve zaman uyumsuz aracılar tarafından oluşturulan özel durumları nasıl işlediğini ve uygulamalarınızda özel durumlara nasıl yanıt verileceğini açıklar.

## <a name="key-points"></a>Önemli Noktalar

- Bir görev veya görev grubu bir özel durum oluşturduğunda, çalışma zamanı bu özel durumu barındırır ve görevin veya görev grubunun bitmesini bekleyen bağlamına göre sıralar.

- Mümkün olduğunda, her [concurrency:: task:: Get](reference/task-class.md#get) ve [concurrency:: task:](reference/task-class.md#wait) : ' a yönelik her çağrıyı, kurtarabileceğiniz hataları işlemek için bir `try`/`catch` bloğu ile bekleyin. Bir görev bir özel durum oluşturursa ve bu özel durum görev, devamlılık veya ana uygulama tarafından yakalanmadığında çalışma zamanı uygulamayı sonlandırır.

- Görev tabanlı devamlılık her zaman çalışır; öncül görevin başarıyla tamamlanıp tamamlanmadığını, bir özel durum mi oluşturulduğunu veya iptal edildiğini değil. Öncül görevi oluşturursa veya iptal ederse, değer tabanlı devamlılık çalışmaz.

- Görev tabanlı devamlılıklar her zaman çalıştığı için, devamlılık zincirinizin sonuna görev tabanlı devamlılık eklenip eklenmeyeceğini göz önünde bulundurun. Bu, kodunuzun tüm özel durumları görme garantisi sağlanmasına yardımcı olabilir.

- [Concurrency:: task:: Get](reference/task-class.md#get) ' i çağırdığınızda ve bu görev iptal edildiğinde, çalışma zamanı [eşzamanlılık:: task_canceled](../../parallel/concrt/reference/task-canceled-class.md) oluşturur.

- Çalışma zamanı, hafif görevler ve aracılar için özel durumları yönetmez.

## <a name="top"></a>Bu belgede

- [Görevler ve devamlılıklar](#tasks)

- [Görev grupları ve paralel algoritmalar](#task_groups)

- [Çalışma zamanı tarafından oluşturulan özel durumlar](#runtime)

- [Birden çok özel durum](#multiple)

- [İptal](#cancellation)

- [Basit Görevler](#lwts)

- [Zaman Uyumsuz Aracılar](#agents)

## <a name="tasks"></a>Görevler ve devamlılıklar

Bu bölüm, çalışma zamanının [concurrency:: Task](../../parallel/concrt/reference/task-class.md) nesneleri ve devamlılıkları tarafından oluşturulan özel durumları nasıl işlediğini açıklar. Görev ve devamlılık modeli hakkında daha fazla bilgi için bkz. [Görev Paralelliği](../../parallel/concrt/task-parallelism-concurrency-runtime.md).

Bir `task` nesnesine geçirdiğiniz bir çalışma işlevinin gövdesinde bir özel durum oluşturduğunuzda, çalışma zamanı bu özel durumu depolar ve bunu [concurrency:: task:: Get](reference/task-class.md#get) veya [concurrency:: Task](reference/task-class.md#wait):: wait öğesine çağıran bağlamına göre oluşturur. [Paralellik belge görevi](../../parallel/concrt/task-parallelism-concurrency-runtime.md) , görev tabanlı ve değer tabanlı devamlılıkları açıklar, ancak özetlemek gerekirse, değer tabanlı devamlılık, `T` türünde bir parametre alır ve görev tabanlı devamlılık, `task<T>`türünde bir parametre alır. Oluşturan bir görevde bir veya daha fazla değer tabanlı devamlılık varsa, bu devamlılıklar çalıştırılmak üzere zamanlanmamış. Aşağıdaki örnek bu davranışı göstermektedir:

[!code-cpp[concrt-eh-task#1](../../parallel/concrt/codesnippet/cpp/exception-handling-in-the-concurrency-runtime_1.cpp)]

Görev tabanlı devamlılık, öncül görev tarafından oluşturulan tüm özel durumları işlemenizi sağlar. Görev tabanlı devamlılık her zaman çalışır; görevin başarıyla tamamlanıp tamamlanmadığını, bir özel durum mi oluşturulduğunu veya iptal edildiğini değil. Bir görev bir özel durum oluşturduğunda, görev tabanlı devamlılıkları çalıştırılmak üzere zamanlanır. Aşağıdaki örnek her zaman oluşturan bir görevi gösterir. Görev iki devamlılığa sahiptir; biri değer tabanlıdır ve diğeri görev tabanlıdır. Görev tabanlı özel durum her zaman çalışır ve bu nedenle, öncül görev tarafından oluşturulan özel durumu yakalayabilir. Örnek her iki devamlılık için de bekleyeceğinden, `task::get` veya `task::wait` çağrıldığında görev özel durumu her zaman oluşturulduğu için özel durum yeniden oluşturulur.

[!code-cpp[concrt-eh-continuations#1](../../parallel/concrt/codesnippet/cpp/exception-handling-in-the-concurrency-runtime_2.cpp)]

İşleyebileceksiniz özel durumları yakalamak için görev tabanlı devamlılıkları kullanmanızı öneririz. Görev tabanlı devamlılıklar her zaman çalıştığı için, devamlılık zincirinizin sonuna görev tabanlı devamlılık eklenip eklenmeyeceğini göz önünde bulundurun. Bu, kodunuzun tüm özel durumları görme garantisi sağlanmasına yardımcı olabilir. Aşağıdaki örnekte, temel değer tabanlı devamlılık zinciri gösterilmektedir. Zincirdeki üçüncü görev atar ve bu nedenle, bunu izleyen değer tabanlı devamlılıklar çalıştırılmaz. Ancak, son devamlılık görev tabanlıdır ve bu nedenle her zaman çalışır. Bu son devamlılık, üçüncü görev tarafından oluşturulan özel durumu işler.

Kullanabileceğiniz en özel durumları yakalanmasını öneririz. Yakalayabilmeniz için özel özel durumlar yoksa, bu son görev tabanlı devamlılığın atlayabilirsiniz. Herhangi bir özel durum işlenmemiş olarak kalır ve uygulamayı sonlandırabilirler.

[!code-cpp[concrt-eh-task-chain#1](../../parallel/concrt/codesnippet/cpp/exception-handling-in-the-concurrency-runtime_3.cpp)]

> [!TIP]
> Bir özel durumu görev tamamlama olayı ile ilişkilendirmek için [concurrency:: task_completion_event:: set_exception](../../parallel/concrt/reference/task-completion-event-class.md) yöntemini kullanabilirsiniz. [Paralellik belge görevi](../../parallel/concrt/task-parallelism-concurrency-runtime.md) , [concurrency:: task_completion_event](../../parallel/concrt/reference/task-completion-event-class.md) sınıfını daha ayrıntılı olarak açıklar.

[concurrency:: task_canceled](../../parallel/concrt/reference/task-canceled-class.md) `task`ilişkili önemli bir çalışma zamanı özel durum türüdür. Çalışma zamanı, `task::get` çağırdığınızda ve bu görev iptal edildiğinde `task_canceled` oluşturur. (Buna karşılık, `task::wait` [task_status döndürür:: iptal edildi](reference/concurrency-namespace-enums.md#task_group_status) ve throw.) Bu özel durumu, görev tabanlı devamlılık veya `task::get`çağırdığınızda yakalayabilir ve işleyebilirsiniz. Görev iptali hakkında daha fazla bilgi için bkz. [PPL 'de iptal](cancellation-in-the-ppl.md).

> [!CAUTION]
> Kodınızdan hiçbir `task_canceled` oluşturun. Bunun yerine [concurrency:: cancel_current_task](reference/concurrency-namespace-functions.md#cancel_current_task) çağrısı yapın.

Bir görev bir özel durum oluşturursa ve bu özel durum görev, devamlılık veya ana uygulama tarafından yakalanmadığında çalışma zamanı uygulamayı sonlandırır. Uygulamanız kilitlenirse, Visual Studio 'Yu C++ özel durumlar oluştuğunda kesilecek şekilde yapılandırabilirsiniz. İşlenmeyen özel durumun konumunu tanıladıktan sonra, işlemek için görev tabanlı devamlılık kullanın.

Bu belgedeki [çalışma zamanı tarafından oluşturulan bölüm özel durumları](#runtime) , çalışma zamanı özel durumlarıyla daha ayrıntılı olarak nasıl çalışılacağını açıklar.

[[Üst](#top)]

## <a name="task_groups"></a>Görev grupları ve paralel algoritmalar

Bu bölüm, çalışma zamanının görev grupları tarafından oluşturulan özel durumları nasıl işlediğini açıklar. Bu bölüm aynı zamanda [eşzamanlılık::p arallel_for](reference/concurrency-namespace-functions.md#parallel_for)gibi paralel algoritmalar için de geçerlidir çünkü bu algoritmalar görev grupları üzerinde oluşturur.

> [!CAUTION]
> Özel durumların bağımlı görevlerle ilgili etkileri anladığınızdan emin olun. Görevler veya paralel algoritmalarda özel durum işlemenin nasıl kullanılacağına ilişkin önerilen uygulamalar için, paralel Desenler kitaplığı konusundaki En Iyi Yöntemler konusunun [iptal ve özel durum Işlemenin nesne yok etme işlemini nasıl etkilediğini anlama](../../parallel/concrt/best-practices-in-the-parallel-patterns-library.md#object-destruction) bölümüne bakın.

Görev grupları hakkında daha fazla bilgi için bkz. [Görev Paralelliği](../../parallel/concrt/task-parallelism-concurrency-runtime.md). Paralel algoritmalar hakkında daha fazla bilgi için bkz. [paralel algoritmalar](../../parallel/concrt/parallel-algorithms.md).

[Concurrency:: task_group](reference/task-group-class.md) veya [concurrency:: structured_task_group](../../parallel/concrt/reference/structured-task-group-class.md) nesnesine geçirdiğiniz bir çalışma işlevinin gövdesinde bir özel durum oluşturduğunuzda, çalışma zamanı bu özel durumu depolar ve bunu [eşzamanlılık:: task_group:](reference/task-group-class.md#wait): wait, eşzamanlılık:: [structured_task_group:: wait](reference/structured-task-group-class.md#wait) [, concurrency:](reference/task-group-class.md#run_and_wait): task_group:: run_and_wait veya [concurrency](reference/structured-task-group-class.md#run_and_wait):: structured_task_group:: run_and_wait öğesini çağıran içeriğe göre oluşturur. Çalışma zamanı, görev grubundaki (alt görev grupları dahil) tüm etkin görevleri de durduruyor ve henüz başlatılmamış tüm görevleri atar.

Aşağıdaki örnek, bir özel durum oluşturan bir çalışma işlevinin temel yapısını gösterir. Örnek, iki `point` nesnesinin değerlerini paralel olarak yazdırmak için bir `task_group` nesnesi kullanır. `print_point` Work işlevi, bir `point` nesnesinin değerlerini konsola yazdırır. Giriş değeri `NULL`, çalışma işlevi bir özel durum oluşturur. Çalışma zamanı bu özel durumu depolar ve `task_group::wait`çağıran bağlamına göre sıralar.

[!code-cpp[concrt-eh-task-group#1](../../parallel/concrt/codesnippet/cpp/exception-handling-in-the-concurrency-runtime_4.cpp)]

Bu örnek aşağıdaki çıktıyı üretir.

```Output
X = 15, Y = 30Caught exception: point is NULL.
```

Bir görev grubunda özel durum işlemeyi kullanan tüm bir örnek için bkz. [nasıl yapılır: paralel bir döngüden ayırmak Için özel durum Işlemeyi kullanma](../../parallel/concrt/how-to-use-exception-handling-to-break-from-a-parallel-loop.md).

[[Üst](#top)]

## <a name="runtime"></a>Çalışma zamanı tarafından oluşturulan özel durumlar

Bir özel durum, çalışma zamanına yapılan çağrıdan kaynaklanabilir. [Concurrency:: task_canceled](../../parallel/concrt/reference/task-canceled-class.md) ve [concurrency:: operation_timed_out](../../parallel/concrt/reference/operation-timed-out-class.md)dışında çok sayıda özel durum türü, bir programlama hatası gösterir. Bu hatalar genellikle kurtarılamaz olur ve bu nedenle uygulama kodu tarafından yakalanmamalıdır veya işlenmemelidir. Programlama hatalarını tanılamanıza gerek duyduğunuzda yalnızca uygulama kodunuzda kurtarılamaz hataları yakalamanızı veya işlemenizi öneririz. Ancak, çalışma zamanı tarafından tanımlanan özel durum türlerini anlamak programlama hatalarını tanılamanıza yardımcı olabilir.

Özel durum işleme mekanizması, çalışma zamanı tarafından iş işlevleri tarafından oluşturulan özel durumlar olarak oluşturulan özel durumlar için aynıdır. Örneğin, [concurrency:: Receive](reference/concurrency-namespace-functions.md#receive) işlevi, belirtilen dönemde bir ileti almadığınızda `operation_timed_out` oluşturur. `receive`, bir görev grubuna geçirdiğiniz bir iş işlevinde bir özel durum oluşturursa, çalışma zamanı bu özel durumu depolar ve `task_group::wait`, `structured_task_group::wait`, `task_group::run_and_wait`veya `structured_task_group::run_and_wait`çağıran bağlamına göre sıralar.

Aşağıdaki örnek, paralel olarak iki görevi çalıştırmak için [eşzamanlılık::p arallel_invoke](reference/concurrency-namespace-functions.md#parallel_invoke) algoritmasını kullanır. İlk görev beş saniye bekler ve ileti arabelleğine bir ileti gönderir. İkinci görev, aynı ileti arabelleğinden bir ileti almak için üç saniye beklemek üzere `receive` işlevini kullanır. `receive` işlevi, zaman diliminde iletiyi almadıysanız `operation_timed_out` oluşturur.

[!code-cpp[concrt-eh-time-out#1](../../parallel/concrt/codesnippet/cpp/exception-handling-in-the-concurrency-runtime_5.cpp)]

Bu örnek aşağıdaki çıktıyı üretir.

```Output
The operation timed out.
```

Uygulamanızı olağan dışı sonlandırmasını engellemek için, kodunuzun çalışma zamanına çağrı yaparken özel durumları işlediğinden emin olun. Ayrıca, örneğin bir üçüncü taraf kitaplığı olan Eşzamanlılık Çalışma Zamanı kullanan dış koda çağrı yaparken özel durumları işleyin.

[[Üst](#top)]

## <a name="multiple"></a>Birden çok özel durum

Bir görev veya paralel algoritma birden çok özel durum alırsa, çalışma zamanı bu özel durumların yalnızca birini çağıran bağlama göre sıralarar. Çalışma zamanı, hangi özel durumun sıraladığında garanti etmez.

Aşağıdaki örnek, sayıları konsola yazdırmak için `parallel_for` algoritmasını kullanır. Giriş değeri, bazı minimum değerden küçük veya en büyük değerden fazlaysa bir özel durum oluşturur. Bu örnekte, birden çok çalışma işlevi bir özel durum oluşturabilir.

[!code-cpp[concrt-eh-multiple#1](../../parallel/concrt/codesnippet/cpp/exception-handling-in-the-concurrency-runtime_6.cpp)]

Aşağıda bu örnek için örnek çıktı gösterilmektedir.

```Output
8293104567Caught exception: -5: the value is less than the minimum.
```

[[Üst](#top)]

## <a name="cancellation"></a>Kin

Tüm özel durumlar bir hata göstermiyor. Örneğin, bir arama algoritması, sonucu bulduğunda ilişkili görevini durdurmak için özel durum işlemeyi kullanabilir. Kodunuzda iptal mekanizmalarının nasıl kullanılacağı hakkında daha fazla bilgi için bkz. [PPL 'de iptal](../../parallel/concrt/cancellation-in-the-ppl.md).

[[Üst](#top)]

## <a name="lwts"></a>Hafif görevler

Hafif görev, doğrudan bir [eşzamanlılık:: Scheduler](../../parallel/concrt/reference/scheduler-class.md) nesnesinden zamanladığınız bir görevdir. Hafif görevler sıradan görevlerden daha az yük taşır. Ancak çalışma zamanı, hafif görevler tarafından oluşturulan özel durumları yakalamaz. Bunun yerine, özel durum işlenmemiş özel durum işleyicisi tarafından yakalanır, varsayılan olarak işlemi sonlandırır. Bu nedenle, uygulamanızda uygun bir hata işleme mekanizması kullanın. Hafif görevler hakkında daha fazla bilgi için bkz. [Görev Zamanlayıcı](../../parallel/concrt/task-scheduler-concurrency-runtime.md).

[[Üst](#top)]

## <a name="agents"></a>Zaman uyumsuz aracılar

Hafif görevler gibi, çalışma zamanı, zaman uyumsuz aracılar tarafından oluşturulan özel durumları yönetmez.

Aşağıdaki örnek, [concurrency:: Agent](../../parallel/concrt/reference/agent-class.md)' den türetilen bir sınıftaki özel durumları işlemenin bir yolunu gösterir. Bu örnek `points_agent` sınıfını tanımlar. `points_agent::run` yöntemi, ileti arabelleğindeki `point` nesneleri okur ve bunları konsola yazdırır. `run` yöntemi bir `NULL` işaretçisi alırsa bir özel durum oluşturur.

`run` yöntemi, tüm işleri bir `try`-`catch` bloğunda çevreler. `catch` bloğu özel durumu bir ileti arabelleğine depolar. Uygulama, aracı bittikten sonra, aracının bu arabellekten okurken bir hatayla karşılaşıp karşılaşmadığını denetler.

[!code-cpp[concrt-eh-agents#1](../../parallel/concrt/codesnippet/cpp/exception-handling-in-the-concurrency-runtime_7.cpp)]

Bu örnek aşağıdaki çıktıyı üretir.

```Output
X: 10 Y: 20
X: 20 Y: 30
error occurred in agent: point must not be NULL
the status of the agent is: done
```

`try`-`catch` bloğu `while` döngüsünün dışında olduğundan, aracı ilk hatayla karşılaştığında işlemi sonlandırır. `try`-`catch` bloğu `while` döngüsünün içindeyse, bir hata oluştuktan sonra aracı devam eder.

Bu örnek özel durumları bir ileti arabelleğinde depolar, böylece başka bir bileşen, çalıştığı şekilde aracıyı hatalara karşı izleyebilir. Bu örnek, hatayı depolamak için bir [concurrency:: single_assignment](../../parallel/concrt/reference/single-assignment-class.md) nesnesi kullanır. Bir aracının birden çok özel durumu işlediği durumda, `single_assignment` sınıfı yalnızca kendisine geçirilen ilk iletiyi depolar. Yalnızca son özel durumu depolamak için [concurrency:: overwrite_buffer](../../parallel/concrt/reference/overwrite-buffer-class.md) sınıfını kullanın. Tüm özel durumları depolamak için [concurrency:: unbounded_buffer](reference/unbounded-buffer-class.md) sınıfını kullanın. Bu ileti blokları hakkında daha fazla bilgi için bkz. [zaman uyumsuz Ileti blokları](../../parallel/concrt/asynchronous-message-blocks.md).

Zaman uyumsuz aracılar hakkında daha fazla bilgi için bkz. [zaman uyumsuz aracılar](../../parallel/concrt/asynchronous-agents.md).

[[Üst](#top)]

## <a name="summary"></a>Özetleme

[[Üst](#top)]

## <a name="see-also"></a>Ayrıca bkz.

[Eşzamanlılık Çalışma Zamanı](../../parallel/concrt/concurrency-runtime.md)<br/>
[Görev Paralelliği](../../parallel/concrt/task-parallelism-concurrency-runtime.md)<br/>
[Paralel Algoritmalar](../../parallel/concrt/parallel-algorithms.md)<br/>
[PPL'de İptal](cancellation-in-the-ppl.md)<br/>
[Görev Zamanlayıcı](../../parallel/concrt/task-scheduler-concurrency-runtime.md)<br/>
[Zaman Uyumsuz Aracılar](../../parallel/concrt/asynchronous-agents.md)
