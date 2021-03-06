---
title: Ağaç Denetimlerini Kullanma
ms.date: 11/04/2016
helpviewer_keywords:
- CTreeCtrl class [MFC], using
- tree controls [MFC], about tree controls
ms.assetid: 4e92941a-e477-4fb1-b1ce-4abeafbef1c1
ms.openlocfilehash: 9cff48018d728ef9578be38c0d94300011265fa1
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62411454"
---
# <a name="using-tree-controls"></a>Ağaç Denetimlerini Kullanma

Ağaç denetimi tipik kullanımını ([CTreeCtrl](../mfc/reference/ctreectrl-class.md)) aşağıdaki deseni izler:

- Denetim oluşturulur. Denetim bir iletişim kutusu şablonunda belirtilirse veya kullanıyorsanız `CTreeView`, oluşturma, iletişim kutusu ya da Görünüm oluşturulduğunda otomatiktir. Ağaç denetimi başka bir pencere bir alt pencere olarak oluşturmak istediğiniz kullanırsanız [Oluştur](../mfc/reference/ctreectrl-class.md#create) üye işlevi.

- Görüntüleri kullanmak için ağaç denetimi istiyorsanız, bir görüntü listesi çağırarak ayarlayın [SetImageList](../mfc/reference/ctreectrl-class.md#setimagelist). Çağırarak girinti değiştirebilirsiniz [SetIndent](../mfc/reference/ctreectrl-class.md#setindent). Bunu yapmak için iyi bir zaman yer [OnInitDialog](../mfc/reference/cdialog-class.md#oninitdialog) (için iletişim kutularındaki denetimler) veya [OnInitialUpdate](../mfc/reference/cview-class.md#oninitialupdate) (için görünümler).

- Çağırarak denetime verilerinizden `CTreeCtrl`'s [InsertItem](../mfc/reference/ctreectrl-class.md#insertitem) işlevi için her bir veri öğesi için bir kez. `InsertItem` öğesine daha sonra ne zaman gibi başvurduğu için kullanabileceğiniz bir tanıtıcı döndürür, alt öğe ekleme. Verileri başlatma zamanı bulunduğu `OnInitDialog` (için iletişim kutularındaki denetimler) veya `OnInitialUpdate` (için görünümler).

- Kullanıcı denetimle etkileşim gibi çeşitli bildirim iletileri gönderir. Her on_notıfy_reflect makrosu ileti eşlemede denetimi pencerenin ekleme veya ana pencerenin ileti eşlemesi için on_notıfy makrosu ekleyerek işlemek istediğiniz tüm iletileri işlemek için bir işlev belirtebilirsiniz. Bkz: [ağaç denetimi bildirim iletileri](../mfc/tree-control-notification-messages.md) olası bildirimler listesi için bu konuda daha sonra.

- Denetim değerlerini ayarlamak için çeşitli küme üyesi işlevleri çağırın. Yaptığınız değişiklikler girinti ayarlama ve text, Image veya bir öğeyle ilişkili veri değiştirme içerir.

- Denetimin içeriğini incelemek için çeşitli Get işlevlerini kullanın. Ağaç denetimi üst, alt ve eşdüzey belirtilen öğe tanıtıcıları almanızı sağlayan işlevler ile içeriğini çapraz geçiş yapabilirsiniz. Belirli bir düğüm alt bile sıralayabilirsiniz.

- Denetim ile işiniz bittiğinde, düzgün bir şekilde imha emin olun. Ağaç denetimi içinde bir iletişim kutusu ise ya da bir görünüm ise bunu ve `CTreeCtrl` nesne otomatik olarak silinecektir. Her iki denetim sağlamak ihtiyacınız değil, varsa ve `CTreeCtrl` nesne düzgün bir şekilde yok.

## <a name="see-also"></a>Ayrıca bkz.

[CTreeCtrl Kullanma](../mfc/using-ctreectrl.md)<br/>
[Denetimler](../mfc/controls-mfc.md)
