---
title: Saklı Yordamları Tanımlama
ms.date: 10/24/2018
helpviewer_keywords:
- stored procedures, syntax
- OLE DB, stored procedures
- stored procedures, defining
- stored procedures, OLE DB
ms.assetid: 54949b81-3275-4dd9-96e4-3eda1ed755f2
ms.openlocfilehash: 9bab086bf6982eae5779d3199cfd2ac2c8efe77f
ms.sourcegitcommit: 857fa6b530224fa6c18675138043aba9aa0619fb
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/24/2020
ms.locfileid: "80211010"
---
# <a name="defining-stored-procedures"></a>Saklı Yordamları Tanımlama

Saklı yordam çağrılmadan önce, [DEFINE_COMMAND](../../data/oledb/define-command.md) makrosunu kullanarak, önce onu tanımlamanız gerekir. Komutu tanımlarken parametre işaretçisi olarak bir soru işareti (?) ile parametreleri belirtin:

```cpp
DEFINE_COMMAND_EX(CMySProcAccessor, _T("{INSERT {name, phone} INTO shippers (?,?)}"))
```

Bu konudaki kod örneklerinde kullanılan sözdizimi (küme ayraçlarının kullanımı vb.) SQL Server özeldir. Saklı yordamlarınızda kullandığınız sözdizimi, kullandığınız sağlayıcıya göre değişiklik gösterebilir.

Ardından, parametre eşlemesinde, komutta kullanılan parametreleri belirtin ve parametreleri komutta gerçekleşdikleri sırada listeleme:

```cpp
BEGIN_PARAM_MAP(CMySProcAccessor)
   SET_PARAM_TYPE(DBPARAMIO_INPUT)
   COLUMN_ENTRY(1, m_Name)   // name corresponds to first '?' param
   SET_PARAM_TYPE(DBPARAMIO_INPUT)
   COLUMN_ENTRY(2, m_Phone)  // phone corresponds to second '?' param
END_PARAM_MAP()
```

Önceki örnekte olduğu gibi bir saklı yordam tanımlanmaktadır. Genellikle kodun verimli bir şekilde yeniden kullanılması için bir veritabanı `Sales by Year` veya `dt_adduserobject`gibi adlara sahip önceden tanımlanmış bir saklı yordamlar kümesi içerir. Tanımlarını SQL Server Enterprise Manager kullanarak görüntüleyebilirsiniz. Bunları şu şekilde çağırabilirsiniz (öğesinin yerleşimi *?* Parametreler, saklı yordamın arabirimine bağlıdır):

```cpp
DEFINE_COMMAND_EX(CMySProcAccessor, _T("{CALL \"Sales by Year\" (?,?) }"))
DEFINE_COMMAND_EX(CMySProcAccessor, _T("{CALL dbo.dt_adduserobject (?,?) }"))
```

Ardından komut sınıfını bildirin:

```cpp
class CMySProc : public CCommand<CAccessor<CMySProcAccessor>>
```

Son olarak, aşağıdaki gibi `OpenRowset` saklı yordamını çağırın:

```cpp
CSession m_session;

HRESULT OpenRowset()
{
   return CCommand<CAccessor<CMySProcAccessor>>::Open(m_session);
}
```

Ayrıca, veritabanı özniteliğini kullanarak [db_command](../../windows/db-command.md) aşağıdaki gibi bir saklı yordam tanımlayabileceğinizi unutmayın:

```cpp
db_command("{ ? = CALL dbo.dt_adduserobject }")
```

## <a name="see-also"></a>Ayrıca bkz.

[Saklı Yordamları Kullanma](../../data/oledb/using-stored-procedures.md)
