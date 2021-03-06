---
title: 'Özel Durumlar: Kendi İşlevlerinizden Özel Durum Atma'
ms.date: 11/04/2016
helpviewer_keywords:
- throwing exceptions [MFC], from functions
- functions [MFC], throwing exceptions
- exceptions [MFC], throwing
ms.assetid: 492976e8-8804-4234-8e8f-30dffd0501be
ms.openlocfilehash: ebdfea18e6e8445dd734bf43fb6a4ecf422975e9
ms.sourcegitcommit: c21b05042debc97d14875e019ee9d698691ffc0b
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/09/2020
ms.locfileid: "84622741"
---
# <a name="exceptions-throwing-exceptions-from-your-own-functions"></a>Özel Durumlar: Kendi İşlevlerinizden Özel Durum Atma

MFC özel durum işleme paradigmasını yalnızca MFC veya diğer kitaplıklardaki işlevlere göre oluşturulan özel durumları yakalamak için kullanabilirsiniz. Kitaplık kodu tarafından oluşturulan özel durumları yakalama konusuna ek olarak, özel durumlar oluşturabilecek işlevler yazıyorsanız kendi kodunuzda özel durumlar da oluşturabilirsiniz.

Bir özel durum oluştuğunda, geçerli işlevin yürütülmesi durdurulur ve doğrudan en içteki özel durum çerçevesinin **catch** bloğuna atlar. Özel durum mekanizması, bir işlevden normal çıkış yolunu atlar. Bu nedenle, normal bir çıkışta silinecek olan bellek bloklarını silmeniz gerekir.

#### <a name="to-throw-an-exception"></a>Özel durum oluşturmak için

1. MFC Yardımcısı işlevlerinden birini (gibi) kullanın `AfxThrowMemoryException` . Bu işlevler uygun türde önceden ayrılmış bir özel durum nesnesi oluşturur.

   Aşağıdaki örnekte, bir işlev iki bellek bloğu ayırmaya çalışır ve ayırma başarısız olursa bir özel durum oluşturur:

   [!code-cpp[NVC_MFCExceptions#17](codesnippet/cpp/exceptions-throwing-exceptions-from-your-own-functions_1.cpp)]

   İlk ayırma başarısız olursa, yalnızca bellek özel durumunu oluşturabilirsiniz. İlk ayırma başarılı olursa ancak ikinci bir hata başarısız olursa, özel durumu oluşturmadan önce ilk ayırma bloğunu serbest yapmanız gerekir. Her iki ayırma da başarılı olursa, normal olarak devam edebilir ve işlevden çıkarken blokları serbest bırakabilirsiniz.

     - veya

1. Bir sorun koşulunu göstermek için Kullanıcı tanımlı bir özel durum kullanın. Özel durum olarak tüm sınıf bile herhangi bir türde bir öğe oluşturabilirsiniz.

   Aşağıdaki örnek, bir sesi bir Wave cihazından yürütmeye çalışır ve bir hata oluşursa özel durum oluşturur.

   [!code-cpp[NVC_MFCExceptions#18](codesnippet/cpp/exceptions-throwing-exceptions-from-your-own-functions_2.cpp)]

> [!NOTE]
> MFC 'nin varsayılan özel durum işlemesi yalnızca nesnelere işaretçiler için geçerlidir `CException` (ve `CException` türetilmiş sınıfların nesneleri). Yukarıdaki örnek, MFC 'nin özel durum mekanizmasını atlar.

## <a name="see-also"></a>Ayrıca bkz.

[Özel Durum İşleme](exception-handling-in-mfc.md)
