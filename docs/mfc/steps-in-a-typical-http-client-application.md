---
title: Tipik Bir HTTP İstemci Uygulamasındaki Adımlar
ms.date: 11/04/2016
helpviewer_keywords:
- HTTP client applications [MFC]
- client applications [MFC], HTTP
- Internet applications [MFC], HTTP client applications
- applications [MFC], HTTP client
- Internet client applications [MFC], HTTP table
- WinInet classes [MFC], HTTP
ms.assetid: f86552e8-8acd-4b23-bdc5-0c3a247ebd74
ms.openlocfilehash: 59b585d3e6b8c9f13c585f5a712d33abd6123f67
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62306970"
---
# <a name="steps-in-a-typical-http-client-application"></a>Tipik Bir HTTP İstemci Uygulamasındaki Adımlar

Aşağıdaki tabloda, tipik bir HTTP istemci uygulamasında gerçekleştirebileceğiniz adımlar gösterilmektedir:

|Amacınız|İşlemlerde|Etkiler|
|---------------|----------------------|-------------|
|Bir HTTP oturumu başlayın.|Oluşturma bir [Cınternetsession](../mfc/reference/cinternetsession-class.md) nesne.|WinINet başlatır ve sunucusuna bağlanır.|
|Bir HTTP sunucusuna bağlanın.|Kullanım [CInternetSession::GetHttpConnection](../mfc/reference/cinternetsession-class.md#gethttpconnection).|Döndürür bir [CHttpConnection](../mfc/reference/chttpconnection-class.md) nesne.|
|Bir HTTP isteği açın.|Kullanım [CHttpConnection::OpenRequest](../mfc/reference/chttpconnection-class.md#openrequest).|Döndürür bir [CHttpFile](../mfc/reference/chttpfile-class.md) nesne.|
|Bir HTTP isteği gönder.|Kullanım [CHttpFile::AddRequestHeaders](../mfc/reference/chttpfile-class.md#addrequestheaders) ve [CHttpFile::SendRequest](../mfc/reference/chttpfile-class.md#sendrequest).|Dosyayı bulur. Dosya bulunamazsa false değerini döndürür.|
|Dosyadan okuma.|Kullanım [CHttpFile](../mfc/reference/chttpfile-class.md).|Belirtilen sayıda baytı bir arabellek sağladığınız kullanarak okur.|
|Özel durumları işler.|Kullanım [Cınternetexception](../mfc/reference/cinternetexception-class.md) sınıfı.|Tüm ortak Internet özel durum türlerini işler.|
|HTTP oturumunu sonlandırın.|Elden [Cınternetsession](../mfc/reference/cinternetsession-class.md) nesne.|Dosya tanıtıcılarını Aç ve bağlantıları tarafından otomatik olarak temizlenir.|

## <a name="see-also"></a>Ayrıca bkz.

[Win32 Internet Uzantıları (WinInet)](../mfc/win32-internet-extensions-wininet.md)<br/>
[Internet İstemci Sınıfları için Önkoşullar](../mfc/prerequisites-for-internet-client-classes.md)<br/>
[MFC WinInet Sınıfları Kullanarak Internet İstemci Uygulaması Yazma](../mfc/writing-an-internet-client-application-using-mfc-wininet-classes.md)
