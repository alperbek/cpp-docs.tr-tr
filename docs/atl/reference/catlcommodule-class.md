---
title: CAtlComModule Sınıfı
ms.date: 11/04/2016
f1_keywords:
- CAtlComModule
- ATLBASE/ATL::CAtlComModule
- ATLBASE/ATL::CAtlComModule::CAtlComModule
- ATLBASE/ATL::CAtlComModule::RegisterServer
- ATLBASE/ATL::CAtlComModule::RegisterTypeLib
- ATLBASE/ATL::CAtlComModule::UnregisterServer
- ATLBASE/ATL::CAtlComModule::UnRegisterTypeLib
helpviewer_keywords:
- CAtlComModule class
ms.assetid: af5dd71a-a0d1-4a2e-9a24-154a03381c75
ms.openlocfilehash: 4b8c98630b27c35ed6a7e32318c6ebad8a82a5c5
ms.sourcegitcommit: 2bc15c5b36372ab01fa21e9bcf718fa22705814f
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/27/2020
ms.locfileid: "82168841"
---
# <a name="catlcommodule-class"></a>CAtlComModule Sınıfı

Bu sınıf bir COM sunucu modülünü uygular.

## <a name="syntax"></a>Sözdizimi

```cpp
class CAtlComModule : public _ATL_COM_MODULE
```

## <a name="members"></a>Üyeler

### <a name="public-constructors"></a>Ortak Oluşturucular

|Adı|Açıklama|
|----------|-----------------|
|[CAtlComModule:: CAtlComModule](#catlcommodule)|Oluşturucu.|
|[CAtlComModule:: ~ CAtlComModule](#dtor)|Yok edicisi.|

### <a name="public-methods"></a>Ortak Yöntemler

|Adı|Açıklama|
|----------|-----------------|
|[CAtlComModule:: RegisterServer](#registerserver)|Nesne eşlemesindeki her bir nesne için sistem kayıt defterini güncelleştirmek için bu yöntemi çağırın.|
|[CAtlComModule:: RegisterTypeLib](#registertypelib)|Bir tür kitaplığını kaydetmek için bu yöntemi çağırın.|
|[CAtlComModule:: UnregisterServer](#unregisterserver)|Nesne eşlemesindeki her nesnenin kaydını silmek için bu yöntemi çağırın.|
|[CAtlComModule:: UnRegisterTypeLib](#unregistertypelib)|Bir tür kitaplığının kaydını silmek için bu yöntemi çağırın.|

## <a name="remarks"></a>Açıklamalar

`CAtlComModule`bir COM sunucu modülünü uygular ve istemcinin modülün bileşenlerine erişmesine izin verir.

Bu sınıf, ATL 'nin önceki sürümlerinde kullanılan eski [CComModule](../../atl/reference/ccommodule-class.md) sınıfının yerini alır. Daha fazla ayrıntı için bkz. [ATL modül sınıfları](../../atl/atl-module-classes.md) .

## <a name="inheritance-hierarchy"></a>Devralma Hiyerarşisi

[_ATL_COM_MODULE](atl-typedefs.md#_atl_com_module)

`CAtlComModule`

## <a name="requirements"></a>Gereksinimler

**Üstbilgi:** atlbase. h

## <a name="catlcommodulecatlcommodule"></a><a name="catlcommodule"></a>CAtlComModule:: CAtlComModule

Oluşturucu.

```cpp
CAtlComModule() throw();
```

### <a name="remarks"></a>Açıklamalar

Modülünü başlatır.

## <a name="catlcommodulecatlcommodule"></a><a name="dtor"></a>CAtlComModule:: ~ CAtlComModule

Yok edicisi.

```cpp
~CAtlComModule();
```

### <a name="remarks"></a>Açıklamalar

Tüm sınıf fabrikalarını serbest bırakır.

## <a name="catlcommoduleregisterserver"></a><a name="registerserver"></a>CAtlComModule:: RegisterServer

Nesne eşlemesindeki her bir nesne için sistem kayıt defterini güncelleştirmek için bu yöntemi çağırın.

```cpp
HRESULT RegisterServer(BOOL bRegTypeLib = FALSE, const CLSID* pCLSID = NULL);
```

### <a name="parameters"></a>Parametreler

*bRegTypeLib*<br/>
Tür kitaplığının kaydı varsa TRUE. Varsayılan değer FALSE 'dur.

*pCLSID*<br/>
Kaydedilecek nesnenin CLSID değerini gösterir. NULL ise (varsayılan değer), nesne haritadaki tüm nesneler kaydedilir.

### <a name="return-value"></a>Dönüş Değeri

Başarılı S_OK veya hata durumunda HRESULT hatası döndürür.

### <a name="remarks"></a>Açıklamalar

[AtlComModuleRegisterServer](server-registration-global-functions.md#atlcommoduleregisterserver)genel işlevini çağırır.

## <a name="catlcommoduleregistertypelib"></a><a name="registertypelib"></a>CAtlComModule:: RegisterTypeLib

Bir tür kitaplığını kaydetmek için bu yöntemi çağırın.

```cpp
HRESULT RegisterTypeLib(LPCTSTR lpszIndex);
HRESULT RegisterTypeLib();
```

### <a name="parameters"></a>Parametreler

*lpszIndex*<br/>
"\\\N" biçiminde dize, burada N, TYPELIB kaynağının tamsayı dizinidir.

### <a name="return-value"></a>Dönüş Değeri

Başarılı S_OK veya hata durumunda HRESULT hatası döndürür.

### <a name="remarks"></a>Açıklamalar

Bir tür kitaplığı hakkında bilgileri sistem kayıt defterine ekler. Modül örneği birden çok tür kitaplığı içeriyorsa, hangi tür kitaplığının kullanılması gerektiğini belirtmek için bu yöntemin ilk sürümünü kullanın.

## <a name="catlcommoduleunregisterserver"></a><a name="unregisterserver"></a>CAtlComModule:: UnregisterServer

Nesne eşlemesindeki her nesnenin kaydını silmek için bu yöntemi çağırın.

```cpp
HRESULT UnregisterServer(
    BOOL bRegTypeLib = FALSE,
    const CLSID* pCLSID = NULL);
```

### <a name="parameters"></a>Parametreler

*bRegTypeLib*<br/>
Tür kitaplığının kaydı kaldırılacak ise TRUE. Varsayılan değer FALSE 'dur.

*pCLSID*<br/>
Kaydı kaldırılacak nesnenin CLSID değerini gösterir. NULL ise (varsayılan değer), nesne eşlemesindeki tüm nesnelerin kaydı silinir.

### <a name="return-value"></a>Dönüş Değeri

Başarılı S_OK veya hata durumunda HRESULT hatası döndürür.

### <a name="remarks"></a>Açıklamalar

[AtlComModuleUnregisterServer](server-registration-global-functions.md#atlcommoduleunregisterserver)genel işlevini çağırır.

## <a name="catlcommoduleunregistertypelib"></a><a name="unregistertypelib"></a>CAtlComModule:: UnRegisterTypeLib

Bir tür kitaplığının kaydını silmek için bu yöntemi çağırın.

```cpp
HRESULT UnRegisterTypeLib(LPCTSTR lpszIndex);
HRESULT UnRegisterTypeLib();
```

### <a name="parameters"></a>Parametreler

*lpszIndex*<br/>
"\\\N" biçiminde dize, burada N, TYPELIB kaynağının tamsayı dizinidir.

### <a name="remarks"></a>Açıklamalar

Bir tür kitaplığı hakkındaki bilgileri sistem kayıt defterinden kaldırır. Modül örneği birden çok tür kitaplığı içeriyorsa, hangi tür kitaplığının kullanılması gerektiğini belirtmek için bu yöntemin ilk sürümünü kullanın.

### <a name="return-value"></a>Dönüş Değeri

Başarılı S_OK veya hata durumunda HRESULT hatası döndürür.

## <a name="see-also"></a>Ayrıca bkz.

[_ATL_COM_MODULE](atl-typedefs.md#_atl_com_module)<br/>
[Sınıfa genel bakış](../../atl/atl-class-overview.md)
