---
title: Tipik Bir Internet İstemci Uygulamasındaki Adımlar
ms.date: 11/04/2016
helpviewer_keywords:
- Internet client applications [MFC], general table
- WinInet classes [MFC], programming
- Internet applications [MFC], client applications
ms.assetid: 7aba135c-7c15-4e2f-8c34-bbaf792c89a6
ms.openlocfilehash: 9762e762680e2ac530b87baeac7afdea77ef6f14
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62306944"
---
# <a name="steps-in-a-typical-internet-client-application"></a>Tipik Bir Internet İstemci Uygulamasındaki Adımlar

Aşağıdaki tabloda, tipik bir Internet istemci uygulamasında gerçekleştirebileceğiniz adımlar gösterilmektedir.

|Amacınız|İşlemlerde|Etkiler|
|---------------|----------------------|-------------|
|Bir Internet oturumu başlayın.|Oluşturma bir [Cınternetsession](../mfc/reference/cinternetsession-class.md) nesne.|WinINet başlatır ve sunucusuna bağlanır.|
|Bir Internet sorgu seçeneği (zaman aşımı sınırı veya örneğin bir yeniden deneme) olarak ayarlayın.|Kullanım [CInternetSession::SetOption](../mfc/reference/cinternetsession-class.md#setoption).|İşlem başarısız olursa FALSE döndürür.|
|Oturum durumunu izlemek için bir geri çağırma işlevi oluşturun.|Kullanım [CInternetSession::EnableStatusCallback](../mfc/reference/cinternetsession-class.md#enablestatuscallback).|İçin bir geri çağırma oluşturur [CInternetSession::OnStatusCallback](../mfc/reference/cinternetsession-class.md#onstatuscallback). Geçersiz kılma `OnStatusCallback` kendi geri çağırma yordamı oluşturmak için.|
|Bir Internet sunucusu, intranet sunucusu veya yerel dosya bağlanın.|Kullanım [CInternetSession::OpenURL](../mfc/reference/cinternetsession-class.md#openurl).|URL ayrıştırır ve belirtilen sunucunun bir bağlantı açar. Döndürür bir [CStdioFile](../mfc/reference/cstdiofile-class.md) (geçirirseniz `OpenURL` bir yerel dosya adı). Bu, sunucu veya dosya alınan verilere erişim nesnesidir.|
|Dosyadan okuma.|Kullanım [CInternetFile::Read](../mfc/reference/cinternetfile-class.md#read).|Belirtilen sayıda baytı bir arabellek sağladığınız kullanarak okur.|
|Özel durumları işler.|Kullanım [Cınternetexception](../mfc/reference/cinternetexception-class.md) sınıfı.|Tüm ortak Internet özel durum türlerini işler.|
|Internet oturumunu sonlandırın.|Elden [Cınternetsession](../mfc/reference/cinternetsession-class.md) nesne.|Dosya tanıtıcılarını Aç ve bağlantıları tarafından otomatik olarak temizlenir.|

## <a name="see-also"></a>Ayrıca bkz.

[Win32 Internet Uzantıları (WinInet)](../mfc/win32-internet-extensions-wininet.md)<br/>
[Internet İstemci Sınıfları için Önkoşullar](../mfc/prerequisites-for-internet-client-classes.md)<br/>
[MFC WinInet Sınıfları Kullanarak Internet İstemci Uygulaması Yazma](../mfc/writing-an-internet-client-application-using-mfc-wininet-classes.md)
