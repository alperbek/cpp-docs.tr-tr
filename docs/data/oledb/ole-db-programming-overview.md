---
title: OLE DB Programlamaya Genel Bakış
ms.date: 10/22/2018
helpviewer_keywords:
- Universal Data Access
- OLE DB, about OLE DB
ms.assetid: a5a69730-2793-4277-a67d-6f3c8edab6df
ms.openlocfilehash: 2b855e0917ba9cdbdaa38a92473d7bddb4279101
ms.sourcegitcommit: 857fa6b530224fa6c18675138043aba9aa0619fb
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/24/2020
ms.locfileid: "80210082"
---
# <a name="ole-db-programming-overview"></a>OLE DB Programlamaya Genel Bakış

OLE DB, yüksek performanslı, COM tabanlı bir veritabanı teknolojisidir. Verilerin depolandığı formdan bağımsız olarak erişmek için ortak bir yol sağlar. Tipik bir iş durumunda kurumsal veritabanlarında büyük miktarda bilgi depolanmaz. Bu bilgiler dosya sistemlerinde (FAT veya NTFS gibi), dizinli sıralı dosyalar, kişisel veritabanları (erişim gibi), elektronik tablolar (Excel gibi), proje planlama uygulamaları (proje gibi) ve e-posta (Outlook gibi) içinde bulunur. OLE DB, veri deposu bir OLE DB sağlayıcısına sahip olduğu sürece her türlü veri deposuna aynı şekilde erişmenizi sağlar.

OLE DB, DBMS olmasına bakılmaksızın farklı veri kaynaklarına erişen uygulamalar geliştirmenize olanak tanır. OLE DB, belirli bir veri kaynağı için uygun DBMS işlevlerini destekleyen COM arabirimlerini kullanarak evrensel erişimi mümkün hale getirir. COM, yalnızca veri kaynakları ve aynı zamanda diğer uygulamalar arasında değil, hizmetlerin gereksiz şekilde çoğaltılmasını ve büyütülmüş birlikte çalışabilirliğini azaltır.

## <a name="benefits-of-com"></a>COM 'un avantajları

Bu, COM 'un geldiği yerdir. OLE DB bir COM arabirimleri kümesidir. Tek bir arabirim kümesi üzerinden verilere erişerek bir veritabanını birlikte çalışan bileşenler matrisine düzenleyebilirsiniz.

OLE DB, COM belirtimine göre, DBMS işlevselliğinin tutarlı, yeniden kullanılabilir kısımlarını çarpanlara kattan ve kapsülleyen genişletilebilir ve sürdürülebilir arabirimlerin bir koleksiyonunu tanımlar. Bu arabirimler, farklı bilgi kaynaklarına Tekdüzen işlem erişimini etkinleştiren satır kapsayıcıları, sorgu işlemcileri ve işlem koordinatörleri gibi DBMS bileşenlerinin sınırlarını tanımlar.

## <a name="see-also"></a>Ayrıca bkz.

[OLE DB Programlama](../../data/oledb/ole-db-programming.md)<br/>
[OLE DB tüketici şablonları](../../data/oledb/ole-db-consumer-templates-cpp.md)<br/>
[OLE DB sağlayıcı şablonları](../../data/oledb/ole-db-provider-templates-cpp.md)<br/>
[OLE DB Şablonları](../../data/oledb/ole-db-templates.md)
