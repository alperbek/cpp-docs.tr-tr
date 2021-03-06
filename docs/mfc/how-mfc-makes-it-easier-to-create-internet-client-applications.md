---
title: MFC'nin Internet İstemci Uygulamaları Oluşturmayı Kolaylaştırması
ms.date: 11/04/2016
helpviewer_keywords:
- Internet client applications [MFC], MFC
- Internet applications [MFC], MFC
- MFC, Internet applications
ms.assetid: 94437b3f-f15c-437d-b5fd-264a2efec9ab
ms.openlocfilehash: 71b72a3079cd0d0c87289c1813c09a24d9f75c89
ms.sourcegitcommit: c21b05042debc97d14875e019ee9d698691ffc0b
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/09/2020
ms.locfileid: "84618552"
---
# <a name="how-mfc-makes-it-easier-to-create-internet-client-applications"></a>MFC'nin Internet İstemci Uygulamaları Oluşturmayı Kolaylaştırması

Microsoft Foundation Sınıfları, Win32 Internet Uzantısı (WinInet) işlevlerini MFC programcıları için tanıdık bir bağlam sağlayan bir şekilde kapsüller. MFC, [CStdioFile](reference/cstdiofile-class.md) sınıfından türetilmiş üç Internet dosya sınıfı ([CInternetFile](reference/cinternetfile-class.md), [CHttpFile](reference/chttpfile-class.md)ve [CGopherFile](reference/cgopherfile-class.md)) sağlar. Bu sınıfların değil, yerel dosyalar için kullanılan programcılar hakkında tanıdık Internet verilerini alma ve düzenleme `CStdioFile` , ancak bu sınıflarla, yerel dosyaları ve Internet dosyalarını tutarlı ve saydam bir şekilde idare edebilirsiniz.

MFC WinInet sınıfları, `CStdioFile` Internet üzerinden aktarılan veriler için aynı işlevleri sağlar. Bu sınıflar, uygulamaların Internet 'e duyarlı hale getirilmesi için hızlı ve kolay bir yol sağlayarak HTTP, FTP ve gopher için Internet protokollerini üst düzey bir uygulama programlama arabirimine soyutlar. Örneğin, bir FTP sunucusuna bağlanmak yine de düşük düzeyde birkaç adım gerektirir, ancak MFC geliştiricisi olarak bu bağlantıyı oluşturmak için yalnızca bir çağrısı yapmanız gerekir `CInternetSession::GetFTPConnection` .

Ayrıca, MFC WinInet sınıfları aşağıdaki avantajları sağlar:

- Arabellekli g/ç

- Verileriniz için tür açısından güvenli tutamaçlar

- Birçok işlev için varsayılan parametreler

- Yaygın Internet hataları için özel durum işleme

- Açık tutamaçlar ve bağlantıları otomatik temizleme

## <a name="see-also"></a>Ayrıca bkz.

[Win32 Internet Uzantıları (Winınet)](win32-internet-extensions-wininet.md)<br/>
[Winınet 'in Internet Istemci uygulamaları oluşturmayı kolaylaştırması](how-wininet-makes-it-easier-to-create-internet-client-applications.md)
