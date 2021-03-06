---
title: 'Windows Yuvaları: Stream yuva'
ms.date: 11/04/2016
helpviewer_keywords:
- Windows Sockets [MFC], stream sockets
- sockets [MFC], stream sockets
- stream sockets [MFC]
ms.assetid: 31faaa34-a995-493f-a30b-b8115293d619
ms.openlocfilehash: 91f06c4a36e76638708edf085987e51418913fd6
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62337836"
---
# <a name="windows-sockets-stream-sockets"></a>Windows Yuvaları: Stream yuva

Bu makalede, akış yuvaları iki Windows yuva türlerinden birini açıklar. (Diğer tür [veri birimi yuva](../mfc/windows-sockets-datagram-sockets.md).)

Stream yuva sağlamak için bir veri akışı kayıt sınırlar olmadan: çift yönlü olabilir bayt akışı (tam çift yönlü uygulamasıdır: Bu hem aktarım hem de bir yuva alabildikleri). Akışlar üzerinde sıralı, unduplicated verileri sunmak için yararlandı. ("Sıralı" paketleri sıraya gönderilen teslim edilmesini anlamına gelir. "Unduplicated", belirli bir paket yalnızca bir kez elde anlamına gelir.) Stream iletilerinin garanti ve akışları büyük miktarlarda veri işleme için uygundur.

Ağ aktarım katmanı birden fazla veya verileri gruplandırmak paketlere makul bir boyutta olabilir. `CSocket` Sınıfı, paketleme ve sizin için akışının paketi açılırken işleyecek.

Akışlar, açık bağlantıları dayalı: Yuva A B; yuva bağlantı istekleri Yuva B kabul eder ya da bağlantı isteği reddeder.

Telefon görüşmesi, bir akış için iyi bir benzerliği sağlar. Normal koşullar altında alıcı tarafın, çoğaltma veya kaybı söylediğiniz, sırayla söylediğiniz duyar. Stream yuva uygulamaları gibi Dosya Aktarım Protokolü (hangi aktarma ASCII veya ikili dosyalarda rasgele boyutunun kolaylaştıran FTP), örneğin, için uygundur.

Stream yuva veri ulşamasını garanti gerekir ve veri boyutu büyük olduğunda veri birimi yuvaları için tercih edilir. Akış yuvaları hakkında daha fazla bilgi için Windows yuva belirtimi bakın. Belirtimi Windows SDK içinde kullanılabilir.

Akış yuvaları kullanılması nedeniyle yayın için ağdaki tüm alıcı yuva için bir veri birimi yuva kullanmak üzere tasarlanmış uygulamalar için üstün olabilir

- Taşma (veya "storm") ağ sorunları tabi yayın modelidir.

- Sonradan benimsenen istemci-sunucu modeli daha verimli olur.

- Akışı modeli, burada veri birimi model yok, güvenilir veri aktarımı sağlar.

- Son modelin CArchive CSocket sınıfı için uygundur. Bu sınıf yuva uygulamaları ANSI ve Unicode arasında iletişim olanağı yararlanır.

    > [!NOTE]
    >  Sınıfı kullanırsanız `CSocket`, bir akış kullanmanız gerekir. Yuva türü olarak belirtirseniz MFC onaylama başarısız **SOCK_DGRAM**.

## <a name="see-also"></a>Ayrıca bkz.

[MFC'de Windows Yuvaları](../mfc/windows-sockets-in-mfc.md)<br/>
[Windows Yuvaları: Arka Plan](../mfc/windows-sockets-background.md)
