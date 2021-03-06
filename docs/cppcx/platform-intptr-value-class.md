---
title: Platform::IntPtr değer sınıfı
ms.date: 12/30/2016
ms.topic: reference
f1_keywords:
- VCCORLIB/PlatformIntPtr::IntPtr
- VCCORLIB/PlatformIntPtr::op_explicit Operator
- VCCORLIB/PlatformIntPtr::ToInt32
helpviewer_keywords:
- Platform::IntPtr Struct
ms.assetid: 6c0326e8-edfd-4e53-a963-240b845dcde8
ms.openlocfilehash: 8101fa2c82a0ac3e3b573384d14d9a7eff6ecf61
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62152746"
---
# <a name="platformintptr-value-class"></a>Platform::IntPtr değer sınıfı

İmzalı bir işaretçi veya tanıtıcı ve ayarlanmış gösteren boyutudur, platforma özgü (32 bit veya 64-bit).

## <a name="syntax"></a>Sözdizimi

```cpp
public value struct IntPtr
```

### <a name="members"></a>Üyeler

IntPtr aşağıdaki üyeleri içerir:

|Üye|Açıklama|
|------------|-----------------|
|[IntPtr::IntPtr](#ctor)|IntPtr yeni bir örneğini başlatır.|
|[IntPtr::op_explicit Operator](#op-explicit)|Belirtilen parametre bir IntPtr ya da bir işaretçi bir IntPtr değerine dönüştürür.|
|[IntPtr::ToInt32](#toint32)|Geçerli IntPtr bir 32-bit tamsayıya dönüştürür.|

### <a name="requirements"></a>Gereksinimler

**En düşük desteklenen istemci:** Windows 8

**Sunucu desteklenen en düşük:** Windows Server 2012

**Namespace:** Platform

**Meta veri:** platform.winmd

## <a name="ctor"> </a> IntPtr::IntPtr Oluşturucusu

Belirtilen değerle bir IntPtr yeni bir örneğini başlatır.

### <a name="syntax"></a>Sözdizimi

```cpp
IntPtr( __int64 handle-or-pointer );   IntPtr( void* value );   IntPtr( int 32-bit_value );
```

### <a name="parameters"></a>Parametreler

*value*<br/>
Bir 64-bit tanıtıcı veya işaretçi veya 64-bit bir değer ya da bir 64-bit değere dönüştürülebilir 32-bit bir değer için bir işaretçi.

## <a name="op-explicit"> </a> IntPtr::op_explicit Operator

Belirtilen parametre bir IntPtr ya da bir işaretçi bir IntPtr değerine dönüştürür.

### <a name="syntax"></a>Sözdizimi

```cpp
static IntPtr::operator IntPtr( void* value1);   static IntPtr::operator IntPtr( int value2);   static IntPtr::operator void*( IntPtr value3 );
```

### <a name="parameters"></a>Parametreler

*Değer1*<br/>
Tanıtıcı ya da IntPtr yönelik işaretçi.

*Value2*<br/>
İçin bir IntPtr dönüştürülebilir bir 32 bit tamsayı.

*Değeri3*<br/>
Bir IntPtr.

### <a name="return-value"></a>Dönüş Değeri

Birinci ve ikinci işleçleri bir IntPtr döndürür. Üçüncü işleci bir işaretçi geçerli IntPtr tarafından temsil edilen değeri döndürür.

## <a name="toint32"> </a> IntPtr::ToInt32 yöntemi

Geçerli IntPtr değer 32-bit tamsayıya dönüştürür.

### <a name="syntax"></a>Sözdizimi

```cpp
int32 IntPtr::ToInt32();
```

### <a name="return-value"></a>Dönüş Değeri

Bir 32 bit tamsayı.

## <a name="see-also"></a>Ayrıca bkz.

[Platform ad alanı](../cppcx/platform-namespace-c-cx.md)
