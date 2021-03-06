---
title: OLE DB Mimari Tasarım Sorunları
ms.date: 05/09/2019
helpviewer_keywords:
- OLE DB, application design considerations
ms.assetid: 8caa7d99-d2bb-42c9-8884-74f228bb6ecc
ms.openlocfilehash: b481d9948d3055247bd284ca794a0fa65905e21b
ms.sourcegitcommit: fcb48824f9ca24b1f8bd37d647a4d592de1cc925
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/15/2019
ms.locfileid: "69501348"
---
# <a name="ole-db-architectural-design-issues"></a>OLE DB Mimari Tasarım Sorunları

> [!NOTE]
> ATL OLE DB Tüketici Sihirbazı, Visual Studio 2019 ve sonrasında kullanılamaz. İşlevselliği el ile de ekleyebilirsiniz. Daha fazla bilgi için bkz. [Sihirbaz kullanmadan tüketici oluşturma](creating-a-consumer-without-using-a-wizard.md).

OLE DB uygulamanızı başlatmadan önce aşağıdaki sorunları göz önünde bulundurun:

## <a name="what-programming-implementation-will-you-use-to-write-your-ole-db-application"></a>OLE DB uygulamanızı yazmak için hangi programlama uygulamasını kullanacaksınız?

Microsoft, bu görevi gerçekleştirmek için çeşitli kitaplıklar sunmaktadır: OLE DB SDK 'daki OLE DB Şablon kitaplığı, OLE DB öznitelikleri ve ham OLE DB arabirimleri. Ayrıca, programınızı yazmanıza yardımcı olan sihirbazlar de vardır. Bu uygulamalar [OLE DB şablonlar, öznitelikler ve diğer uygulamalarda](../../data/oledb/ole-db-templates-attributes-and-other-implementations.md)açıklanmıştır.

## <a name="do-you-need-to-write-your-own-provider"></a>Kendi sağlayıcınızı yazmanız mı gerekiyor?

Çoğu geliştiricilerin kendi sağlayıcısını yazması gerekmez. Microsoft çeşitli sağlayıcılar sağlar. Bir veri bağlantısı oluşturduğunuz zaman (örneğin, **ATL OLE DB Tüketici Sihirbazı 'nı**kullanarak projenize bir tüketici eklediğinizde), **veri bağlantısı özellikleri** iletişim kutusunda sisteminizde kayıtlı olan tüm mevcut sağlayıcılar listelenir. Sağlayıcılardan biri kendi veri deponuza ve veri erişim uygulamanıza uygunsa, en kolay şey bunlardan birini kullanmaktır. Ancak, veri depolubirisi bu kategorilerden birine sığmıyorsa, kendi sağlayıcınızı oluşturmanız gerekir. Sağlayıcılar oluşturma hakkında daha fazla bilgi için bkz. [OLE DB sağlayıcı şablonları](../../data/oledb/ole-db-provider-templates-cpp.md).

## <a name="what-level-of-support-do-you-need-for-your-consumer"></a>Tüketicinize gereken destek düzeyi nedir?

Bazı tüketiciler temel olabilir; bazıları karmaşık olabilir. OLE DB nesnelerinin işlevselliği, özelliklerle belirtilir. Bir sağlayıcı oluşturmak için bir tüketici veya **veritabanı sağlayıcı Sihirbazı** oluşturmak üzere **ATL OLE DB Tüketici Sihirbazı** 'nı kullandığınızda, size standart bir işlevler kümesi vermeniz için uygun nesne özelliklerini ayarlar. Bununla birlikte, sihirbaz tarafından oluşturulan tüketici veya sağlayıcı sınıfları, gerek duyduğunuz her şeyi desteklemiyorsa, [OLE DB şablonları kitaplığındaki](../../data/oledb/ole-db-templates.md)bu sınıfların arabirimlerine başvurmanız gerekir. Bu arabirimler, ham OLE DB arabirimlerini sararak sizin için daha kolay bir şekilde kullanılmasını sağlamak üzere ek uygulama sağlar.

Örneğin, bir satır kümesindeki verileri güncelleştirmek istiyorsanız, ancak Sihirbazı ile tüketiciyi oluştururken bunu belirtmeyi unuttuysanız, komut nesnesi üzerinde `DBPROP_IRowsetChange` ve `DBPROP_UPDATABILITY` özelliklerini ayarlayarak olguyu daha sonra belirtebilirsiniz. Sonra, satır kümesi oluşturulduğunda, `IRowsetChange` arabirimine sahiptir.

## <a name="do-you-have-older-code-using-another-data-access-technology-ado-odbc-or-dao"></a>Başka bir veri erişim teknolojisini (ADO, ODBC veya DAO) kullanarak daha eski bir kodunuz var mı?

Olası teknoloji birleşimleri (örneğin, OLE DB bileşenleri ile ADO bileşenlerini kullanma ve ODBC kodunu OLE DB olarak geçirme gibi) verildiğinde, tüm durumları kapsayan görsel C++ belgelerinin kapsamı ötesinde. Ancak, çeşitli senaryolar kapsayan birçok makale aşağıdaki Microsoft Web sitelerinde bulunabilir:

- [Microsoft Yardım ve Destek](https://support.microsoft.com/)

- [Microsoft veri erişimi teknik makalelerine genel bakış](/previous-versions/ms810811(v=msdn.10))

## <a name="see-also"></a>Ayrıca bkz.

[OLE DB Programlama](../../data/oledb/ole-db-programming.md)<br/>
[OLE DB Programlamaya Genel Bakış](../../data/oledb/ole-db-programming-overview.md)
