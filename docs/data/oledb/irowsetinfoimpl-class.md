---
title: IRowsetInfoImpl Sınıfı
ms.date: 11/04/2016
f1_keywords:
- ATL.IRowsetInfoImpl
- IRowsetInfoImpl
- ATL::IRowsetInfoImpl
- ATL.IRowsetInfoImpl.GetProperties
- IRowsetInfoImpl.GetProperties
- ATL::IRowsetInfoImpl::GetProperties
- IRowsetInfoImpl::GetProperties
- ATL::IRowsetInfoImpl::GetReferencedRowset
- GetReferencedRowset
- ATL.IRowsetInfoImpl.GetReferencedRowset
- IRowsetInfoImpl.GetReferencedRowset
- IRowsetInfoImpl::GetReferencedRowset
- IRowsetInfoImpl::GetSpecification
- ATL.IRowsetInfoImpl.GetSpecification
- IRowsetInfoImpl.GetSpecification
- GetSpecification
- ATL::IRowsetInfoImpl::GetSpecification
helpviewer_keywords:
- IRowsetInfoImpl class
- GetProperties method
- GetReferencedRowset method
- GetSpecification method
ms.assetid: 9c654155-7727-464e-bd31-143e68391a47
ms.openlocfilehash: cf72aabce58237f470d536c02727f442404db030
ms.sourcegitcommit: 857fa6b530224fa6c18675138043aba9aa0619fb
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/24/2020
ms.locfileid: "80210450"
---
# <a name="irowsetinfoimpl-class"></a>IRowsetInfoImpl Sınıfı

[IRowsetInfo](/previous-versions/windows/desktop/ms724541(v=vs.85)) arabirimi için bir uygulama sağlar.

## <a name="syntax"></a>Sözdizimi

```cpp
template <class T, class PropClass = T>
class ATL_NO_VTABLE IRowsetInfoImpl :
   public IRowsetInfo,
   public CUtlProps<PropClass>
```

### <a name="parameters"></a>Parametreler

*Şı*<br/>
Sınıfınız `IRowsetInfoImpl`türetilir.

*PropClass*<br/>
Varsayılan olarak *T*olarak kullanılacak kullanıcı tanımlı bir özellik sınıfı.

## <a name="requirements"></a>Gereksinimler

**Üstbilgi:** altdb. h

## <a name="members"></a>Üyeler

### <a name="interface-methods"></a>Arabirim yöntemleri

|||
|-|-|
|[GetProperties](#getproperties)|Satır kümesi tarafından desteklenen tüm özelliklerin geçerli ayarlarını döndürür.|
|[GetReferencedRowset](#getreferencedrowset)|Bir yer işaretinin uygulandığı satır kümesine bir arabirim işaretçisi döndürür.|
|[GetSpecification](#getspecification)|Bu satır kümesini oluşturan nesne (komut veya oturum) üzerinde bir arabirim işaretçisi döndürür.|

## <a name="remarks"></a>Açıklamalar

Satır kümelerinde zorunlu bir arabirim. Bu sınıf, komut sınıfınıza tanımlanan [özellik kümesi eşlemesini](../../data/oledb/begin-propset-map.md) kullanarak satır kümesi özelliklerini uygular. Satır kümesi sınıfı komut sınıfı ' özellik kümelerini kullanıyor gibi görünse de, satır kümesi bir komut veya oturum nesnesi tarafından oluşturulduğunda çalışma zamanı özelliklerinin kendi kopyasıyla birlikte sağlanır.

## <a name="irowsetinfoimplgetproperties"></a><a name="getproperties"></a>IRowsetInfoImpl:: GetProperties

`DBPROPSET_ROWSET` grubundaki özelliklerin geçerli ayarlarını döndürür.

### <a name="syntax"></a>Sözdizimi

```cpp
STDMETHOD (GetProperties )(const ULONG cPropertyIDSets,
   const DBPROPIDSET rgPropertyIDSets[],
   ULONG* pcPropertySets,
   DBPROPSET** prgPropertySets);
```

#### <a name="parameters"></a>Parametreler

*OLE DB Programcı başvurusunda*bkz. [IRowsetInfo:: GetProperties](/previous-versions/windows/desktop/ms719611(v=vs.85)) .

## <a name="irowsetinfoimplgetreferencedrowset"></a><a name="getreferencedrowset"></a>IRowsetInfoImpl:: GetReferencedRowset

Bir yer işaretinin uygulandığı satır kümesine bir arabirim işaretçisi döndürür.

### <a name="syntax"></a>Sözdizimi

```cpp
STDMETHOD (GetReferencedRowset )(DBORDINAL iOrdinal,
   REFIID riid,
   IUnknown** ppReferencedRowset);
```

#### <a name="parameters"></a>Parametreler

*OLE DB Programcı başvurusunda*bkz. [IRowsetInfo:: GetReferencedRowset](/previous-versions/windows/desktop/ms721145(v=vs.85)) . *Iordinal* parametresi bir yer işareti sütunu olmalıdır.

## <a name="irowsetinfoimplgetspecification"></a><a name="getspecification"></a>IRowsetInfoImpl:: GetSpecification

Bu satır kümesini oluşturan nesne (komut veya oturum) üzerinde bir arabirim işaretçisi döndürür.

### <a name="syntax"></a>Sözdizimi

```cpp
STDMETHOD (GetSpecification )(REFIID riid,
   IUnknown** ppSpecification);
```

#### <a name="parameters"></a>Parametreler

*OLE DB Programcı başvurusunda*bkz. [IRowsetInfo:: GetSpecification](/previous-versions/windows/desktop/ms716746(v=vs.85)) .

### <a name="remarks"></a>Açıklamalar

Veri kaynağı nesnesinden özellikleri almak için bu yöntemi [IGetDataSourceImpl](../../data/oledb/igetdatasourceimpl-class.md) ile birlikte kullanın.

## <a name="see-also"></a>Ayrıca bkz.

[OLE DB sağlayıcı şablonları](../../data/oledb/ole-db-provider-templates-cpp.md)<br/>
[OLE DB Sağlayıcı Şablonu Mimarisi](../../data/oledb/ole-db-provider-template-architecture.md)
