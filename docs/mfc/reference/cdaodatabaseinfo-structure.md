---
title: CDaoDatabaseInfo Yapısı
ms.date: 09/17/2019
f1_keywords:
- CDaoDatabaseInfo
helpviewer_keywords:
- CDaoDatabaseInfo structure [MFC]
- DAO (Data Access Objects), Databases collection
ms.assetid: 68e9e0da-8382-4fc6-8115-1b1519392ddb
ms.openlocfilehash: 60972aa3ecaef4d38c9a0d0ecc70477796aa37aa
ms.sourcegitcommit: 069e3833bd821e7d64f5c98d0ea41fc0c5d22e53
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/21/2019
ms.locfileid: "74304259"
---
# <a name="cdaodatabaseinfo-structure"></a>CDaoDatabaseInfo Yapısı

`CDaoDatabaseInfo` yapısı, veri erişim nesneleri (DAO) için tanımlanan bir veritabanı nesnesi hakkında bilgi içerir. DAO 3,6 son sürümdür ve artık kullanılmıyor olarak kabul edilir.

## <a name="syntax"></a>Sözdizimi

```
struct CDaoDatabaseInfo
{
    CString m_strName;       // Primary
    BOOL m_bUpdatable;       // Primary
    BOOL m_bTransactions;    // Primary
    CString m_strVersion;    // Secondary
    long m_lCollatingOrder;  // Secondary
    short m_nQueryTimeout;   // Secondary
    CString m_strConnect;    // All
};
```

#### <a name="parameters"></a>Parametreler

*m_strName*<br/>
Veritabanı nesnesini benzersiz olarak adlandırır. Bu özelliği doğrudan almak için, [CDaoDatabase:: GetName](../../mfc/reference/cdaodatabase-class.md#getname)' i çağırın. Ayrıntılar için, DAO yardımı 'nda "ad özelliği" konusuna bakın.

*m_bUpdatable*<br/>
Veritabanında değişiklik yapılıp yapılmadığını belirtir. Bu özelliği doğrudan almak için, [CDaoDatabase:: CanUpdate](../../mfc/reference/cdaodatabase-class.md#canupdate)çağırın. Ayrıntılar için, DAO yardımı 'nda "güncelleştirilebilir özellik" konusuna bakın.

*m_bTransactions*<br/>
Bir veri kaynağının işlemleri destekleyip desteklemediğini belirtir — daha sonra geri alınacak (iptal edilen) veya kaydedilmiş (kaydedilmiş) bir dizi değişikliğin kaydı. Bir veritabanı Microsoft Jet veritabanı altyapısını temel alıyorsa, Işlemler özelliği sıfır değildir ve işlemleri kullanabilirsiniz. Diğer veritabanı motorları işlemleri desteklemiyor olabilir. Bu özelliği doğrudan almak için, [CDaoDatabase:: CanTransact](../../mfc/reference/cdaodatabase-class.md#cantransact)öğesini çağırın. Ayrıntılar için, DAO yardımı 'nda "Işlemler özelliği" konusuna bakın.

*m_strVersion*<br/>
Microsoft Jet veritabanı altyapısının sürümünü gösterir. Bu özelliğin değerini doğrudan almak için, veritabanı nesnesinin [GetVersion](../../mfc/reference/cdaodatabase-class.md#getversion) üye işlevini çağırın. Ayrıntılar için, DAO yardımı 'nda "sürüm özelliği" konusuna bakın.

*m_lCollatingOrder*<br/>
Dize karşılaştırma veya sıralama için metin olarak sıralama düzeni sırasını belirtir. Olası değerler şunlardır:

- `dbSortGeneral` genel (Ingilizce, Fransızca, Almanca, Portekizce, Italyanca ve modern Ispanyolca) sıralama sırasını kullanın.

- `dbSortArabic` Arapça sıralama düzenini kullanır.

- `dbSortCyrillic` Rusça sıralama sırasını kullanın.

- Çek sıralama düzenini kullanmak `dbSortCzech`.

- `dbSortDutch` Hollanda sıralama sırasını kullanın.

- `dbSortGreek` Yunan sıralama düzenini kullanın.

- `dbSortHebrew` Ibranice sıralama sırasını kullanın.

- `dbSortHungarian`, Macarca sıralama sırasını kullanın.

- `dbSortIcelandic`, Izlanda sıralama sırasını kullanın.

- `dbSortNorwdan` Norveç veya Danca sıralama sırasını kullanın.

- `dbSortPDXIntl` Paradox Uluslararası sıralama sırasını kullanın.

- `dbSortPDXNor`, Paradox Norveççe veya Danca sıralama sırasını kullanın.

- `dbSortPDXSwe`, Paradox Isveççe veya Fince sıralama sırasını kullanın.

- `dbSortPolish` Lehçe sıralama sırasını kullanın.

- `dbSortSpanish` Ispanyolca sıralama düzenini kullanın.

- `dbSortSwedFin` Isveç veya Fince sıralama sırasını kullanın.

- `dbSortTurkish` Türkçe sıralama düzenini kullanın.

- sıralama düzeni tanımsız veya bilinmiyor `dbSortUndefined`.

Daha fazla bilgi için, DAO yardımı 'nda "veri erişimi için Windows kayıt defteri ayarlarını özelleştirme" konusuna bakın.

*m_nQueryTimeout*<br/>
ODBC veritabanında bir sorgu çalıştırıldığında, bir zaman aşımı hatası oluştuktan önce Microsoft Jet veritabanı altyapısının bekleyeceği saniye sayısı. Varsayılan zaman aşımı değeri 60 saniyedir. QueryTimeout değeri 0 olarak ayarlandığında zaman aşımı oluşmaz; Bu, programın yanıt vermemesine neden olabilir. Bu özelliğin değerini doğrudan almak için veritabanı nesnesinin [GetQueryTimeout](../../mfc/reference/cdaodatabase-class.md#getquerytimeout) üye işlevini çağırın. Ayrıntılar için, DAO yardımı 'nda "QueryTimeout özelliği" konusuna bakın.

*m_strConnect*<br/>
Açık bir veritabanının kaynağı hakkında bilgi sağlar. Bağlantı dizeleri hakkında daha fazla bilgi için ve bu özelliğin değerini doğrudan alma hakkında bilgi için, bkz. [CDaoDatabase:: GetConnect](../../mfc/reference/cdaodatabase-class.md#getconnect) member işlevi. Daha fazla bilgi için, DAO yardımı 'nda "bağlama özelliği" konusuna bakın.

## <a name="remarks"></a>Açıklamalar

Veritabanı, [CDaoDatabase](../../mfc/reference/cdaodatabase-class.md)sınıfının MFC nesnesini temel alan bir DAO nesnesidir. Yukarıdaki birincil, Ikincil ve tüm başvurular, bilgilerin [CDaoWorkspace:: GetDatabaseInfo](../../mfc/reference/cdaoworkspace-class.md#getdatabaseinfo) üye işlevi tarafından nasıl döndürüleceğini gösterir.

[CDaoWorkspace:: GetDatabaseInfo](../../mfc/reference/cdaoworkspace-class.md#getdatabaseinfo) üye işlevi tarafından alınan bilgiler `CDaoDatabaseInfo` bir yapıda depolanıyor. Veritabanları koleksiyonundaki veritabanı nesnesinin depolandığı `CDaoWorkspace` nesnesi için `GetDatabaseInfo` çağırın. `CDaoDatabaseInfo` Ayrıca hata ayıklama yapılarında bir `Dump` member işlevi tanımlar. Bir `CDaoDatabaseInfo` nesnesinin içeriğini dökmek için `Dump` kullanabilirsiniz.

## <a name="requirements"></a>Gereksinimler

**Üstbilgi:** afxdao. h

## <a name="see-also"></a>Ayrıca bkz.

[Yapılar, Stiller, Geri Çağrılar ve İleti Eşlemeleri](../../mfc/reference/structures-styles-callbacks-and-message-maps.md)<br/>
[CDaoWorkspace Sınıfı](../../mfc/reference/cdaoworkspace-class.md)<br/>
[CDaoDatabase Sınıfı](../../mfc/reference/cdaodatabase-class.md)
