---
title: AgileEventSource sınıfı
ms.date: 10/03/2018
ms.topic: reference
f1_keywords:
- event/Microsoft::WRL::AgileEventSource
helpviewer_keywords:
- AgileEventSource class
ms.openlocfilehash: 71a70f783d8f8967d755bb788f4aae4861340d64
ms.sourcegitcommit: 857fa6b530224fa6c18675138043aba9aa0619fb
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/24/2020
ms.locfileid: "80214194"
---
# <a name="agileeventsource-class"></a>AgileEventSource sınıfı

Herhangi bir iş parçacığından erişilebilen bir bileşen olan çevik bir bileşen tarafından oluşturulan bir olayı temsil eder. , [EventSource](eventsource-class.md) 'tan devralır ve çevik olayını çağırma seçeneklerini belirtmek için `Add` üye işlevini ek bir tür parametresiyle geçersiz kılar.

## <a name="syntax"></a>Sözdizimi

```cpp
template<
    typename TDelegateInterface,
    typename TEventSourceOptions = Microsoft::WRL::InvokeModeOptions<FireAll>
>
class AgileEventSource :
    public Microsoft::WRL::EventSource<
        TDelegateInterface, TEventSourceOptions>;
```

## <a name="parameters"></a>Parametreler

*Tdelegateınterface*<br/>
Bir olay işleyicisini temsil eden bir temsilci için arabirim.

*TEventSourceOptions*<br/>
Invokemode alanı `InvokeMode::StopOnFirstError` veya `InvokeMode::FireAll`olarak ayarlanan [ınvokemodeoptions](invokemodeoptions-structure.md) yapısı.

## <a name="remarks"></a>Açıklamalar

Windows Çalışma Zamanı bileşenlerin büyük çoğunluğu çevik bileşenlerdir. Daha fazla bilgi için bkz. [Threading and MarshalC++(/CX)](../../cppcx/threading-and-marshaling-c-cx.md).

## <a name="inheritance-hierarchy"></a>Devralma Hiyerarşisi

`EventSource`

`AgileEventSource`

## <a name="requirements"></a>Gereksinimler

**Üstbilgi:** Event. h

**Ad alanı:** Microsoft:: WRL

## <a name="members"></a>Üyeler

### <a name="public-methods"></a>Ortak Yöntemler

|Ad|Açıklama|
|----------|-----------------|
|[AgileEventSource:: Add yöntemi](#add)|Belirtilen temsilci arabirimiyle temsil edilen çevik olay işleyicisini geçerli **Agileeventsource** nesnesinin olay işleyicileri kümesine ekler.|

## <a name="agileeventsourceadd-method"></a><a name="add"></a>AgileEventSource:: Add yöntemi

Belirtilen temsilci arabirimiyle temsil edilen olay işleyicisini geçerli [EventSource](eventsource-class.md) nesnesinin olay işleyicileri kümesine ekler.

### <a name="syntax"></a>Sözdizimi

```cpp
HRESULT Add(
   _In_ TDelegateInterface* delegateInterface,
   _Out_ EventRegistrationToken* token
);
```

### <a name="parameters"></a>Parametreler

*Delegateınterface*<br/>
Bir olay işleyicisini temsil eden bir temsilci nesnesine arabirim.

*simgesinde*<br/>
Bu işlem tamamlandığında, olayı temsil eden bir tanıtıcı. Olay işleyicisini atmak için `Remove()` metoduna parametre olarak bu belirteci kullanın.

### <a name="return-value"></a>Dönüş Değeri

Başarılı olursa S_OK; Aksi takdirde, hatayı gösteren bir HRESULT.

## <a name="see-also"></a>Ayrıca bkz.

[Microsoft::WRL Ad Alanı](microsoft-wrl-namespace.md)
