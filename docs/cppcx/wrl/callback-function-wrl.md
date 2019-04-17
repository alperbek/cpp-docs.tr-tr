---
title: Geri çağırma işlevi (WRL)
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- event/Microsoft::WRL::Callback
ms.assetid: afb15d25-3230-44f7-b321-e17c54872943
ms.openlocfilehash: d37e6fdd2521f07728305bfbf5441cebb363030a
ms.sourcegitcommit: c7f90df497e6261764893f9cc04b5d1f1bf0b64b
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/05/2019
ms.locfileid: "59041396"
---
# <a name="callback-function-wrl"></a>Geri çağırma işlevi (WRL)

Üye işlevi bir geri çağırma yöntemi olan nesne oluşturur.

## <a name="syntax"></a>Sözdizimi

```cpp
template<
   typename TDelegateInterface,
   typename TCallback
>
ComPtr<TDelegateInterface> Callback(
   TCallbackcallback
);
template<
   typename TDelegateInterface,
   typename TCallbackObject
>
ComPtr<TDelegateInterface> Callback(
   _In_ TCallbackObject *object,
   _In_ HRESULT (TCallbackObject::* method)()
);
template<
   typename TDelegateInterface,
   typename TCallbackObject,
   typename TArg1
>
ComPtr<TDelegateInterface> Callback(
   _In_ TCallbackObject *object,
   _In_ HRESULT (TCallbackObject::* method)(TArg1)
);
template<
   typename TDelegateInterface,
   typename TCallbackObject,
   typename TArg1,
   typename TArg2
>
ComPtr<TDelegateInterface> Callback(
   _In_ TCallbackObject *object,
   _In_ HRESULT (TCallbackObject::* method)(TArg1,
   TArg2)
);
template<
   typename TDelegateInterface,
   typename TCallbackObject,
   typename TArg1,
   typename TArg2,
   typename TArg3
>
ComPtr<TDelegateInterface> Callback(
   _In_ TCallbackObject *object,
   _In_ HRESULT (TCallbackObject::* method)(TArg1,
   TArg2,
   TArg3)
);
template<
   typename TDelegateInterface,
   typename TCallbackObject,
   typename TArg1,
   typename TArg2,
   typename TArg3,
   typename TArg4
>
ComPtr<TDelegateInterface> Callback(
   _In_ TCallbackObject *object,
   _In_ HRESULT (TCallbackObject::* method)(TArg1,
   TArg2,
   TArg3,
   TArg4)
);
template<
   typename TDelegateInterface,
   typename TCallbackObject,
   typename TArg1,
   typename TArg2,
   typename TArg3,
   typename TArg4,
   typename TArg5
>
ComPtr<TDelegateInterface> Callback(
   _In_ TCallbackObject *object,
   _In_ HRESULT (TCallbackObject::* method)(TArg1,
   TArg2,
   TArg3,
   TArg4,
   TArg5)
);
template<
   typename TDelegateInterface,
   typename TCallbackObject,
   typename TArg1,
   typename TArg2,
   typename TArg3,
   typename TArg4,
   typename TArg5,
   typename TArg6
>
ComPtr<TDelegateInterface> Callback(
   _In_ TCallbackObject *object,
   _In_ HRESULT (TCallbackObject::* method)(TArg1,
   TArg2,
   TArg3,
   TArg4,
   TArg5,
   TArg6)
);
template<
   typename TDelegateInterface,
   typename TCallbackObject,
   typename TArg1,
   typename TArg2,
   typename TArg3,
   typename TArg4,
   typename TArg5,
   typename TArg6,
   typename TArg7
>
ComPtr<TDelegateInterface> Callback(
   _In_ TCallbackObject *object,
   _In_ HRESULT (TCallbackObject::* method)(TArg1,
   TArg2,
   TArg3,
   TArg4,
   TArg5,
   TArg6,
   TArg7)
);
template<
   typename TDelegateInterface,
   typename TCallbackObject,
   typename TArg1,
   typename TArg2,
   typename TArg3,
   typename TArg4,
   typename TArg5,
   typename TArg6,
   typename TArg7,
   typename TArg8
>
ComPtr<TDelegateInterface> Callback(
   _In_ TCallbackObject *object,
   _In_ HRESULT (TCallbackObject::* method)(TArg1,
   TArg2,
   TArg3,
   TArg4,
   TArg5,
   TArg6,
   TArg7,
   TArg8)
);
template<
   typename TDelegateInterface,
   typename TCallbackObject,
   typename TArg1,
   typename TArg2,
   typename TArg3,
   typename TArg4,
   typename TArg5,
   typename TArg6,
   typename TArg7,
   typename TArg8,
   typename TArg9
>
ComPtr<TDelegateInterface> Callback(
   _In_ TCallbackObject *object,
   _In_ HRESULT (TCallbackObject::* method)(TArg1,
   TArg2,
   TArg3,
   TArg4,
   TArg5,
   TArg6,
   TArg7,
   TArg8,
   TArg9)
);
```

### <a name="parameters"></a>Parametreler

*TDelegateInterface*<br/>
Şablon parametresi bir olay oluştuğunda çağrılacak temsilci arabirimini belirtir.

*TCallback*<br/>
Şablon parametresi bir nesne ve onun üye geri çağırma işlevini temsil eden bir nesne türünü belirtir.

*TCallbackObject*<br/>
Şablon parametresi, üye işlevi olay oluştuğunda çağrılacak yöntem olan nesneyi belirtir.

*TArg1*<br/>
Şablon parametresi ilk geri çağırma yöntemi bağımsız değişken türünü belirtir.

*TArg2*<br/>
Şablon parametresi ikinci geri çağırma yöntemi bağımsız değişken türünü belirtir.

*TArg3*<br/>
Şablon parametresi üçüncü geri çağırma yöntemi bağımsız değişken türünü belirtir.

*TArg4*<br/>
Şablon parametresi dördüncü geri çağırma yöntemi bağımsız değişken türünü belirtir.

*TArg5*<br/>
Şablon parametresi beşinci geri çağırma yöntemi bağımsız değişken türünü belirtir.

*TArg6*<br/>
Şablon parametresi altıncı geri çağırma yöntemi bağımsız değişken türünü belirtir.

*TArg7*<br/>
Şablon parametresi yedinci geri çağırma yöntemi bağımsız değişken türünü belirtir.

*TArg8*<br/>
Şablon parametresi sekizinci geri çağırma yöntemi bağımsız değişken türünü belirtir.

*TArg9*<br/>
Şablon parametresi dokuzuncu geri çağırma yöntemi bağımsız değişken türünü belirtir.

*geri arama*<br/>
Geri çağırma nesnesi ve onun üye işlevini temsil eden bir nesne.

*nesne*<br/>
Bir olay oluştuğunda üye işlevi çağrılan nesne.

*yöntemi*<br/>
Bir olay oluştuğunda çağrılacak üye işlevi.

## <a name="return-value"></a>Dönüş Değeri

Üye işlevi, belirtilen geri çağırma yöntemi olan nesne.

## <a name="remarks"></a>Açıklamalar

Bir temsilci nesnesinin temeli olmalıdır `IUnknown`değil `IInspectable`.

## <a name="requirements"></a>Gereksinimler

**Başlık:** event.h

**Namespace:** Microsoft::WRL

## <a name="see-also"></a>Ayrıca bkz.

[Microsoft::WRL Ad Alanı](microsoft-wrl-namespace.md)