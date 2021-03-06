---
title: condition_variable Sınıfı
ms.date: 11/04/2016
f1_keywords:
- condition_variable/std::condition
- condition_variable/std::condition_variable::condition_variable
- condition_variable/std::condition_variable::native_handle
- condition_variable/std::condition_variable::notify_all
- condition_variable/std::condition_variable::notify_one
- condition_variable/std::condition_variable::wait
- condition_variable/std::condition_variable::wait_for
- condition_variable/std::condition_variable::wait_until
ms.assetid: 80b1295c-b73d-4d46-b664-6e183f2eec1b
helpviewer_keywords:
- std::condition
- std::condition_variable::condition_variable
- std::condition_variable::native_handle
- std::condition_variable::notify_all
- std::condition_variable::notify_one
- std::condition_variable::wait
- std::condition_variable::wait_for
- std::condition_variable::wait_until
ms.openlocfilehash: 999e236433ec4f3f2f52abb06855004a89169fa6
ms.sourcegitcommit: 7ecd91d8ce18088a956917cdaf3a3565bd128510
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/16/2020
ms.locfileid: "79421886"
---
# <a name="condition_variable-class"></a>condition_variable Sınıfı

`unique_lock<mutex>`türünde bir `mutex` olduğunda bir olayı beklemek için `condition_variable` sınıfını kullanın. Bu türün nesneleri [condition_variable_any < unique_lock\<mutex > >](../standard-library/condition-variable-any-class.md)türündeki nesnelerden daha iyi performansa sahip olabilir.

## <a name="syntax"></a>Sözdizimi

```cpp
class condition_variable;
```

## <a name="members"></a>Üyeler

### <a name="constructors"></a>Oluşturucular

|||
|-|-|
|[condition_variable](#condition_variable)|`condition_variable` nesnesi oluşturur.|

### <a name="functions"></a>İşlevler

|||
|-|-|
|[native_handle](#native_handle)|Condition_variable tanıtıcıyı temsil eden uygulamaya özel türü döndürür.|
|[notify_all](#notify_all)|`condition_variable` nesnesi bekleyen tüm iş parçacıklarının engellemesini kaldırır.|
|[notify_one](#notify_one)|`condition_variable` nesnesi bekleyen iş parçacıklarından birini engeller.|
|[bekleneceğini](#wait)|Bir iş parçacığını engeller.|
|[wait_for](#wait_for)|Bir iş parçacığını engeller ve sonra iş parçacığı bloklarından sonra bir zaman aralığı ayarlar.|
|[wait_until](#wait_until)|Bir iş parçacığını engeller ve iş parçacığı bloklarından en fazla bir zaman noktası ayarlar.|

## <a name="condition_variable"></a>condition_variable

`condition_variable` nesnesi oluşturur.

```cpp
condition_variable();
```

### <a name="remarks"></a>Açıklamalar

Yeterli kullanılabilir bellek yoksa, Oluşturucu `not_enough_memory` hata koduna sahip bir [system_error](../standard-library/system-error-class.md) nesnesi oluşturur. Başka bir kaynak kullanılabilir olmadığından nesne oluşturulamıyor, Oluşturucu `resource_unavailable_try_again` hata koduna sahip bir `system_error` nesnesi oluşturur.

## <a name="native_handle"></a>native_handle

Condition_variable tanıtıcısını temsil eden uygulamaya özel türü döndürür.

```cpp
native_handle_type native_handle();
```

### <a name="return-value"></a>Dönüş Değeri

`native_handle_type`, iç veri yapılarını Eşzamanlılık Çalışma Zamanı bir işaretçi olarak tanımlanır.

## <a name="notify_all"></a>notify_all

`condition_variable` nesnesi bekleyen tüm iş parçacıklarının engellemesini kaldırır.

```cpp
void notify_all() noexcept;
```

## <a name="notify_one"></a>notify_one

`condition_variable` nesnesinde bekleyen iş parçacıklarından birinin engellemesini kaldırır.

```cpp
void notify_one() noexcept;
```

## <a name="wait"></a>bekleneceğini

Bir iş parçacığını engeller.

```cpp
void wait(unique_lock<mutex>& Lck);

template <class Predicate>
void wait(unique_lock<mutex>& Lck, Predicate Pred);
```

### <a name="parameters"></a>Parametreler

*LCK*\
Bir [unique_lock\<mutex >](../standard-library/unique-lock-class.md) nesnesi.

*Pred*\
**True** veya **false**döndüren herhangi bir ifade.

### <a name="remarks"></a>Açıklamalar

İlk yöntem, `condition_variable` nesnesine [notify_one](#notify_one) veya [notify_all](#notify_all)çağrısı tarafından bildirilene kadar engeller. Ayrıca, uyanabilir 'i de uyandırabilirler.

Aslında, ikinci yöntem aşağıdaki kodu yürütür.

```cpp
while(!Pred())
    wait(Lck);
```

## <a name="wait_for"></a>wait_for

Bir iş parçacığını engeller ve sonra iş parçacığı bloklarından sonra bir zaman aralığı ayarlar.

```cpp
template <class Rep, class Period>
cv_status wait_for(
    unique_lock<mutex>& Lck,
    const chrono::duration<Rep, Period>& Rel_time);

template <class Rep, class Period, class Predicate>
bool wait_for(
    unique_lock<mutex>& Lck,
    const chrono::duration<Rep, Period>& Rel_time,
    Predicate Pred);
```

### <a name="parameters"></a>Parametreler

*LCK*\
Bir [unique_lock\<mutex >](../standard-library/unique-lock-class.md) nesnesi.

*Rel_time*\
İş parçacığı uyandırmadan önce geçen süreyi belirten `chrono::duration` nesnesi.

*Pred*\
**True** veya **false**döndüren herhangi bir ifade.

### <a name="return-value"></a>Dönüş Değeri

İlk yöntem, *Rel_time* geçtiğinde bekleme sona erdiğinde `cv_status::timeout` döndürür. Aksi takdirde, yöntem `cv_status::no_timeout`döndürür.

İkinci yöntem *Pred*değerini döndürür.

### <a name="remarks"></a>Açıklamalar

İlk yöntem, `condition_variable` nesne [notify_one](#notify_one) veya [notify_all](#notify_all) çağrısı tarafından veya zaman aralığı *Rel_time* bitene kadar sinyallene kadar engeller. Ayrıca, uyanabilir 'i de uyandırabilirler.

Aslında, ikinci yöntem aşağıdaki kodu yürütür.

```cpp
while(!Pred())
    if(wait_for(Lck, Rel_time) == cv_status::timeout)
    return Pred();

return true;
```

## <a name="wait_until"></a>wait_until

Bir iş parçacığını engeller ve iş parçacığı bloklarından en fazla bir zaman noktası ayarlar.

```cpp
template <class Clock, class Duration>
cv_status wait_until(
    unique_lock<mutex>& Lck,
    const chrono::time_point<Clock, Duration>& Abs_time);

template <class Clock, class Duration, class Predicate>
bool wait_until(
    unique_lock<mutex>& Lck,
    const chrono::time_point<Clock, Duration>& Abs_time,
    Predicate Pred);

cv_status wait_until(
    unique_lock<mutex>& Lck,
    const xtime* Abs_time);

template <class Predicate>
bool wait_until(
    unique_lock<mutex>& Lck,
    const xtime* Abs_time,
    Predicate Pred);
```

### <a name="parameters"></a>Parametreler

*LCK*\
Bir [unique_lock\<mutex >](../standard-library/unique-lock-class.md) nesnesi.

*Abs_time*\
Bir zaman [hatası:: time_point](../standard-library/time-point-class.md) nesnesi.

*Pred*\
**True** veya **false**döndüren herhangi bir ifade.

### <a name="return-value"></a>Dönüş Değeri

`cv_status` bir türü döndüren yöntemler *Abs_time* geçtiğinde bekleme sona erdiğinde `cv_status::timeout` döndürür. Aksi takdirde, Yöntemler `cv_status::no_timeout`döndürür.

Bir **bool** döndüren yöntemler *Pred*değerini döndürür.

### <a name="remarks"></a>Açıklamalar

İlk yöntem, `condition_variable` nesnesine [notify_one](#notify_one) veya [notify_all](#notify_all) ya da `Abs_time`kadar bir çağrı tarafından bildirilene kadar engeller. Ayrıca, uyanabilir 'i de uyandırabilirler.

Aslında, ikinci yöntem aşağıdaki kodu yürütür

```cpp
while(!Pred())
    if(wait_until(Lck, Abs_time) == cv_status::timeout)
    return Pred();

return true;
```

Üçüncü ve dördüncü Yöntemler `chrono::time_point` nesnesini değiştirmek için `xtime` türünde bir nesne işaretçisi kullanır. `xtime` nesnesi bir sinyal için beklenecek en uzun süreyi belirtir.

## <a name="see-also"></a>Ayrıca bkz.

[Üst bilgi dosyaları başvurusu](../standard-library/cpp-standard-library-header-files.md)\
[<condition_variable>](../standard-library/condition-variable.md)
