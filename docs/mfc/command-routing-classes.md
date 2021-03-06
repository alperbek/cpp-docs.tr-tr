---
title: Komut Yönlendirme Sınıfları
ms.date: 11/04/2016
f1_keywords:
- vc.classes.command
helpviewer_keywords:
- MFC, command routing
- command routing [MFC], classes
ms.assetid: 4b50e689-2c54-4e6c-90f0-37333e22b2a1
ms.openlocfilehash: d7ff275d373cf50ab8ebe52ed454bd25cd473e11
ms.sourcegitcommit: c21b05042debc97d14875e019ee9d698691ffc0b
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/09/2020
ms.locfileid: "84624835"
---
# <a name="command-routing-classes"></a>Komut Yönlendirme Sınıfları

Kullanıcı, fareyle menüler veya denetim çubuğu düğmeleri seçerek uygulamayla etkileşime geçtiğinde, uygulama etkilenen Kullanıcı arabirimi nesnesinden uygun bir komut hedefi nesnesine iletiler gönderir. Komut-hedef sınıflar, `CCmdTarget` [CWinApp](reference/cwinapp-class.md), [CWnd](reference/cwnd-class.md), [CDocTemplate](reference/cdoctemplate-class.md), [CDocument](reference/cdocument-class.md), [CView](reference/cview-class.md)ve bunlardan türetilmiş sınıflar içerir. Framework, komutların uygulamada etkin olan en uygun nesne tarafından işlenebilmesi için otomatik komut yönlendirmeyi destekler.

Bir sınıfının nesnesi, `CCmdUI` belirli bir komut için Kullanıcı arabiriminin durumunu (örneğin, menü öğelerinden denetimi denetlemek veya kaldırmak için) güncelleştirmenize olanak tanımak üzere komut hedeflerinizin ' güncelleştirme komutu Kullanıcı arabirimi ([ON_UPDATE_COMMAND_UI](reference/message-map-macros-mfc.md#on_update_command_ui)) işleyicilerine geçirilir. `CCmdUI`UI nesnesinin durumunu güncelleştirmek için nesnenin üye işlevlerini çağırın. Bu işlem, belirli bir komutla ilişkili UI nesnesinin bir menü öğesi ya da düğme ya da her ikisi de aynı olup olmadığı aynı.

[CCmdTarget](reference/ccmdtarget-class.md)<br/>
İletileri alabilen ve yanıtlayabildiği tüm nesne sınıfları için temel sınıf olarak işlev görür.

[CCmdUI](reference/ccmdui-class.md)<br/>
Menü öğeleri veya denetim çubuğu düğmeleri gibi kullanıcı arabirimi nesnelerini güncelleştirmek için programlı bir arabirim sağlar. Komut hedefi nesnesi, bu nesneyle Kullanıcı arabirimi nesnesini devre dışı bırakır, kaldırır, denetler ve/veya temizler.

## <a name="see-also"></a>Ayrıca bkz.

[Sınıfa genel bakış](class-library-overview.md)
