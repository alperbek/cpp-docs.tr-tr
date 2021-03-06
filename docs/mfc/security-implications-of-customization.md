---
title: Özelleştirmenin Güvenlikle İlgili Etkileri
ms.date: 11/04/2016
helpviewer_keywords:
- security, MFC Feature Pack
- MFC Feature Pack, security
ms.assetid: 9be96b12-be38-43bd-a133-5d671265f7a1
ms.openlocfilehash: 9164983a6634e069195f3498bea56b595a2a2381
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62308479"
---
# <a name="security-implications-of-customization"></a>Özelleştirmenin Güvenlikle İlgili Etkileri

Bu konu, olası bir güvenlik açığına MFC'de açıklar.

## <a name="potential-security-weakness"></a>Olası güvenlik açıklarına neden olabileceği

MFC sağlayan kullanıcı bir uygulama kullanıcı arabirimi, örneğin, düğmeler ve simgeler görünümünü görünümünü özelleştirebilirsiniz. MFC Kabuk komutları yürütmek kullanıcının olanak sağlayan kullanıcı tanımlı araçlar da destekler. Bir güvenlik açığı özelleştirilmiş uygulamanın kayıt defteri kullanıcı profiline kaydedilir doğurur. Kayıt defteri erişebilen herkesin bu ayarları düzenleyebilir ve uygulama görünümünü veya davranışını değiştirin. Örneğin, bilgisayarda yönetici kullanıcının uygulama rasgele programlar (bile bir ağ paylaşımından) yürütmek neden olarak bir kullanıcının kimliğine bürünme.

## <a name="workarounds"></a>Geçici Çözümler

Kayıt defteri güvenlik açıklarını kapatmak için bu üç yoldan herhangi birini öneririz:

- Burada depolanan verileri şifrele

- Kayıt defteri güvenli dosyasında yerine data Store.

   Bu ilk iki yoldan birini gerçekleştirmek için öğesinden bir sınıf türetin [CSettingsStore sınıfı](../mfc/reference/csettingsstore-class.md) ve şifreleme veya kayıt defteri dışında depolama uygulamak için kendi yöntemleri geçersiz kılın.

- Özelleştirmeleri uygulamanızda da devre dışı bırakabilirsiniz.

## <a name="see-also"></a>Ayrıca bkz.

[MFC için Özelleştirme](../mfc/customization-for-mfc.md)
