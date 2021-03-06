---
title: cancellation_token_source Sınıfı
ms.date: 11/04/2016
f1_keywords:
- cancellation_token_source
- PPLCANCELLATION_TOKEN/concurrency::cancellation_token_source
- PPLCANCELLATION_TOKEN/concurrency::cancellation_token_source::cancellation_token_source
- PPLCANCELLATION_TOKEN/concurrency::cancellation_token_source::cancel
- PPLCANCELLATION_TOKEN/concurrency::cancellation_token_source::create_linked_source
- PPLCANCELLATION_TOKEN/concurrency::cancellation_token_source::get_token
helpviewer_keywords:
- cancellation_token_source class
ms.assetid: 3548b1a0-12b0-4334-95db-4bf57141c066
ms.openlocfilehash: 131c4155ad902221d14f90f750f89c31479e2067
ms.sourcegitcommit: a8ef52ff4a4944a1a257bdaba1a3331607fb8d0f
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 02/11/2020
ms.locfileid: "77142226"
---
# <a name="cancellation_token_source-class"></a>cancellation_token_source Sınıfı

`cancellation_token_source` sınıfı, bazı iptal edilebilen işlemleri iptal etme yeteneğini temsil eder.

## <a name="syntax"></a>Sözdizimi

```cpp
class cancellation_token_source;
```

## <a name="members"></a>Üyeler

### <a name="public-constructors"></a>Ortak Oluşturucular

|Ad|Açıklama|
|----------|-----------------|
|[cancellation_token_source](#ctor)|Fazla Yüklendi. Yeni bir `cancellation_token_source`oluşturur. Kaynak, bazı iptal edilebilen bir işlemin iptal edilmesini işaretlemek için kullanılabilir.|
|[~ cancellation_token_source yok edici](#dtor)||

### <a name="public-methods"></a>Ortak Yöntemler

|Ad|Açıklama|
|----------|-----------------|
|[İptal](#cancel)|Belirteci iptal eder. Belirteci kullanan `task_group`, `structured_task_group`veya `task`, bu çağrıdan sonra iptal edilir ve sonraki kesinti noktasında bir özel durum oluşturur.|
|[create_linked_source](#create_linked_source)|Fazla Yüklendi. Belirtilen belirteç iptal edildiğinde iptal edilen bir `cancellation_token_source` oluşturur.|
|[get_token](#get_token)|Bu kaynakla ilişkili bir iptal belirteci döndürür. Döndürülen belirteç iptal için yoklanabilir veya iptal gerçekleştiğinde bir geri çağırma sağlayabilir.|

### <a name="public-operators"></a>Ortak İşleçler

|Ad|Açıklama|
|----------|-----------------|
|[operator!=](#operator_neq)||
|[işleç =](#operator_eq)||
|[işleç = =](#operator_eq_eq)||

## <a name="inheritance-hierarchy"></a>Devralma Hiyerarşisi

`cancellation_token_source`

## <a name="requirements"></a>Gereksinimler

**Üst bilgi:** pplcancellation_token. h

**Ad alanı:** eşzamanlılık

## <a name="dtor"></a>~ cancellation_token_source

```cpp
~cancellation_token_source();
```

## <a name="cancel"></a>İptal

Belirteci iptal eder. Belirteci kullanan `task_group`, `structured_task_group`veya `task`, bu çağrıdan sonra iptal edilir ve sonraki kesinti noktasında bir özel durum oluşturur.

```cpp
void cancel() const;
```

## <a name="ctor"></a>cancellation_token_source

Yeni bir `cancellation_token_source`oluşturur. Kaynak, bazı iptal edilebilen bir işlemin iptal edilmesini işaretlemek için kullanılabilir.

```cpp
cancellation_token_source();

cancellation_token_source(const cancellation_token_source& _Src);

cancellation_token_source(cancellation_token_source&& _Src);
```

### <a name="parameters"></a>Parametreler

*_Src*<br/>
Kopyalanacak veya taşınacak nesne.

## <a name="create_linked_source"></a>create_linked_source

Belirtilen belirteç iptal edildiğinde iptal edilen bir `cancellation_token_source` oluşturur.

```cpp
static cancellation_token_source create_linked_source(
    cancellation_token& _Src);

template<typename _Iter>
static cancellation_token_source create_linked_source(_Iter _Begin, _Iter _End);
```

### <a name="parameters"></a>Parametreler

*_Iter*<br/>
Yineleyici türü.

*_Src*<br/>
İptali döndürülen belirteç kaynağının iptaline neden olacak bir belirteç. Döndürülen belirteç kaynağının bu parametrenin içerdiği kaynaktan bağımsız olarak da iptal edilip olamayacağını unutmayın.

*_Begin*<br/>
İptali C++ için dinlenecek belirteçler aralığının başlangıcına karşılık gelen standart kitaplık Yineleyici.

*_End*<br/>
İptali C++ için dinlemek üzere belirteçleri aralığının sonuna karşılık gelen standart kitaplık Yineleyici.

### <a name="return-value"></a>Dönüş Değeri

`_Src` parametresi tarafından belirtilen belirteç iptal edildiğinde iptal edilen `cancellation_token_source`.

## <a name="get_token"></a>get_token

Bu kaynakla ilişkili bir iptal belirteci döndürür. Döndürülen belirteç iptal için yoklanabilir veya iptal gerçekleştiğinde bir geri çağırma sağlayabilir.

```cpp
cancellation_token get_token() const;
```

### <a name="return-value"></a>Dönüş Değeri

Bu kaynakla ilişkili bir iptal belirteci.

## <a name="operator_neq"></a>işleç! =

```cpp
bool operator!= (const cancellation_token_source& _Src) const;
```

### <a name="parameters"></a>Parametreler

*_Src*<br/>
Değişkeni.

### <a name="return-value"></a>Dönüş Değeri

## <a name="operator_eq"></a>işleç =

```cpp
cancellation_token_source& operator= (const cancellation_token_source& _Src);

cancellation_token_source& operator= (cancellation_token_source&& _Src);
```

### <a name="parameters"></a>Parametreler

*_Src*<br/>
Değişkeni.

### <a name="return-value"></a>Dönüş Değeri

## <a name="operator_eq_eq"></a>işleç = =

```cpp
bool operator== (const cancellation_token_source& _Src) const;
```

### <a name="parameters"></a>Parametreler

*_Src*<br/>
Değişkeni.

### <a name="return-value"></a>Dönüş Değeri

## <a name="see-also"></a>Ayrıca bkz.

[Eşzamanlılık Ad Alanı](concurrency-namespace.md)
