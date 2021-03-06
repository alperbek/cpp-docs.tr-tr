---
title: 'Windows Yuvaları: Yuva sınıflarından türetme'
ms.date: 11/04/2016
helpviewer_keywords:
- derived classes [MFC], from socket classes
- Windows Sockets [MFC], deriving from socket classes
- sockets [MFC], deriving from socket classes
ms.assetid: 3a26e67a-e323-433b-9b05-eca018799801
ms.openlocfilehash: 12ab66cfd9212cd79752e2f6359b857194c6428c
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62385264"
---
# <a name="windows-sockets-deriving-from-socket-classes"></a>Windows Yuvaları: Yuva sınıflarından türetme

Bu makalede kendi sınıf bir yuva sınıflarından türetme tarafından elde edebilir işlevsellik açıklanır.

Kendi yuva sınıflarından herhangi birinden türetebilirsiniz [Casyncsocket'ini](../mfc/reference/casyncsocket-class.md) veya [CSocket](../mfc/reference/csocket-class.md) kendi işlevselliği eklemek için. Özellikle, çok sayıda kılabileceğiniz sanal üye işlev bu sınıfları sağlar. Bu işlevler dahil [OnReceive](../mfc/reference/casyncsocket-class.md#onreceive), [OnSend](../mfc/reference/casyncsocket-class.md#onsend), [OnAccept](../mfc/reference/casyncsocket-class.md#onaccept), [tetiklediğinde çalıştırılan](../mfc/reference/casyncsocket-class.md#onconnect), ve [OnClose](../mfc/reference/casyncsocket-class.md#onclose). İşlevleri ağ olaylar meydana geldiğinde sağladıkları bildirimleri yararlanmak için türetilmiş yuva sınıfınızda geçersiz kılabilirsiniz. Framework, giriş verilerinin gibi önemli yuva olayları okumaya başlayabilirsiniz bildirmek için bu bildirimi geri çağırma işlevleri çağırır. Bildirim işlevler hakkında daha fazla bilgi için bkz. [Windows Yuvaları: Yuva bildirimleri](../mfc/windows-sockets-socket-notifications.md).

Buna ek olarak, sınıf `CSocket` sağlayan [OnMessagePending](../mfc/reference/csocket-class.md#onmessagepending) üye işlevi (Gelişmiş bir geçersiz kılınabilir). Yuva, Windows tabanlı iletileri Pompalama sırada MFC bu işlevi çağırır. Geçersiz kılabilirsiniz `OnMessagePending` Windows belirli iletileri arama ve onlara yanıt vermek için.

Varsayılan sürümü `OnMessagePending` sınıfında sağlanan `CSocket` mesaj kuyruğu WM_PAINT iletileri için bir engelleme çağrısının tamamlanması beklenirken inceler. Bu görüntü kalitesini artırmak için boyama iletileri gönderir. Yararlı bir şeyi yapmanın yanı sıra, bu işlev geçersiz kılabilir bir yolu kendiniz gösterilmektedir. Başka bir örnek olarak kullanmayı `OnMessagePending` aşağıdaki görev. Bir ağ işlemin tamamlanması beklenirken modsuz iletişim kutusu görüntüler varsayalım. İletişim kutusu, kullanıcının çok uzun süren durdurma işlemi iptal etmek için kullanabileceğiniz bir iptal düğmesi içerir. `OnMessagePending` Geçersiz kılma için bu modsuz iletişim kutusu ilgili iletiler pompa.

İçinde `OnMessagePending` geçersiz, ya da dönüş **TRUE** veya temel sınıf sürümü bir çağrıdan dönüş `OnMessagePending`. Yine de istediğiniz işlerini gerçekleştirir, temel sınıf sürümü çağırın.

Daha fazla bilgi için bkz.:

- [Windows Yuvaları: Yuvaları Arşivlerle Kullanma](../mfc/windows-sockets-using-sockets-with-archives.md)

- [Windows Yuvaları: CAsyncSocket Sınıfını Kullanma](../mfc/windows-sockets-using-class-casyncsocket.md)

- [Windows Yuvaları: Engelleme](../mfc/windows-sockets-blocking.md)

- [Windows Yuvaları: Bayt Sıralama](../mfc/windows-sockets-byte-ordering.md)

- [Windows Yuvaları: Dizeleri Dönüştürme](../mfc/windows-sockets-converting-strings.md)

## <a name="see-also"></a>Ayrıca bkz.

[MFC'de Windows Yuvaları](../mfc/windows-sockets-in-mfc.md)
