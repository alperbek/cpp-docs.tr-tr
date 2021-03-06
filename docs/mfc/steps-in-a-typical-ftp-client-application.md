---
title: Tipik Bir FTP İstemci Uygulamasındaki Adımlar
ms.date: 11/04/2016
helpviewer_keywords:
- Internet client applications [MFC], FTP table
- FTP (File Transfer Protocol)
- WinInet classes [MFC], FTP
- FTP (File Transfer Protocol) [MFC], client applications
- Internet applications [MFC], FTP client applications
ms.assetid: 70bed7b5-6040-40d1-bc77-702e63a698f2
ms.openlocfilehash: d08edf704e748767f3b566252ad328baf40b55ea
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62307024"
---
# <a name="steps-in-a-typical-ftp-client-application"></a>Tipik Bir FTP İstemci Uygulamasındaki Adımlar

Tipik bir FTP istemci uygulaması oluşturan bir [Cınternetsession](../mfc/reference/cinternetsession-class.md) ve [CFtpConnection](../mfc/reference/cftpconnection-class.md) nesne. Bu MFC WinINet sınıfları gerçekten proxy türü ayarlarını kontrol olduğunu unutmayın. IIS yapar.

Aşağıdaki tabloda, tipik bir FTP istemci uygulamasında gerçekleştirebileceğiniz adımlar gösterilmektedir.

|Amacınız|İşlemlerde|Etkiler|
|---------------|----------------------|-------------|
|Bir FTP oturumunun başlayın.|Oluşturma bir [Cınternetsession](../mfc/reference/cinternetsession-class.md) nesne.|WinINet başlatır ve sunucusuna bağlanır.|
|Bir FTP sunucusuna bağlanın.|Kullanım [CInternetSession::GetFtpConnection](../mfc/reference/cinternetsession-class.md#getftpconnection).|Döndürür bir [CFtpConnection](../mfc/reference/cftpconnection-class.md) nesne.|
|Sunucuda yeni bir FTP dizinine geçin.|Kullanım [CFtpConnection::SetCurrentDirectory](../mfc/reference/cftpconnection-class.md#setcurrentdirectory).|Şu anda sunucu üzerinde bağlıyken dizinini değiştirir.|
|FTP dizin ilk dosyayı bulun.|Kullanım [CFtpFileFind::FindFile](../mfc/reference/cftpfilefind-class.md#findfile).|İlk dosya bulur. Dosya bulunamazsa false değerini döndürür.|
|FTP dizin sonraki dosyasını bulun.|Kullanım [CFtpFileFind::FindNextFile](../mfc/reference/cftpfilefind-class.md#findnextfile).|Sonraki dosya bulur. Dosya bulunamazsa false değerini döndürür.|
|Tarafından bulunan dosyayı açmak `FindFile` veya `FindNextFile` okuma veya yazma için.|Kullanım [CFtpConnection::OpenFile](../mfc/reference/cftpconnection-class.md#openfile), tarafından döndürülen dosya adını kullanarak [FindFile](../mfc/reference/cftpfilefind-class.md#findfile) veya ['larını](../mfc/reference/cftpfilefind-class.md#findnextfile).|Dosya sunucusunda okuma veya yazma için açar. Döndürür bir [Cınternetfile](../mfc/reference/cinternetfile-class.md) nesne.|
|Okuma veya dosyaya yazmak.|Kullanım [CInternetFile::Read](../mfc/reference/cinternetfile-class.md#read) veya [CInternetFile::Write](../mfc/reference/cinternetfile-class.md#write).|Okur veya sağladığınız bir arabelleği kullanarak belirtilen sayıda yazar.|
|Özel durumları işler.|Kullanım [Cınternetexception](../mfc/reference/cinternetexception-class.md) sınıfı.|Tüm ortak Internet özel durum türlerini işler.|
|FTP oturumunu sonlandırın.|Elden [Cınternetsession](../mfc/reference/cinternetsession-class.md) nesne.|Dosya tanıtıcılarını Aç ve bağlantıları tarafından otomatik olarak temizlenir.|

## <a name="see-also"></a>Ayrıca bkz.

[Win32 Internet Uzantıları (WinInet)](../mfc/win32-internet-extensions-wininet.md)<br/>
[Internet İstemci Sınıfları için Önkoşullar](../mfc/prerequisites-for-internet-client-classes.md)<br/>
[MFC WinInet Sınıfları Kullanarak Internet İstemci Uygulaması Yazma](../mfc/writing-an-internet-client-application-using-mfc-wininet-classes.md)
