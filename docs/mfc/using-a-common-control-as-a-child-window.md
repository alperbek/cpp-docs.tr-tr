---
title: Bir Ortak Denetimi Alt Pencere Olarak Kullanma
ms.date: 11/04/2016
helpviewer_keywords:
- controls [MFC], using as child windows
- windows [MFC], common controls as
- child windows [MFC], common controls as
- common controls [MFC], child windows
- Windows common controls [MFC], child windows
ms.assetid: 608f7d47-7854-4fce-bde9-856c51e76753
ms.openlocfilehash: 827690f273852dee8f9461aa9af51f1cf7f4ce6e
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62180576"
---
# <a name="using-a-common-control-as-a-child-window"></a>Bir Ortak Denetimi Alt Pencere Olarak Kullanma

Windows ortak denetimleri başka bir pencere bir alt pencere olarak kullanılabilir. Aşağıdaki yordam, ortak bir denetimi dinamik olarak oluşturmak ve onunla çalışan açıklar.

### <a name="to-use-a-common-control-as-a-child-window"></a>Bir ortak denetimi alt pencere olarak kullanmak için

1. Denetim, ilgili sınıf veya işleyici tanımlayın.

1. Denetimin geçersiz kılmasını kullanın [CWnd::Create](../mfc/reference/cwnd-class.md#create) Windows denetimi oluşturmak için yöntemi.

1. Denetim oluşturulduktan sonra (olarak erken `OnCreate` işleyicisi, denetimin alt), üye işlevleri kullanarak denetimi işleyebilirsiniz. Tek denetimleri açıklamaları görmek [denetimleri](../mfc/controls-mfc.md) yöntemleri hakkında ayrıntılı bilgi için.

1. Denetim ile işiniz bittiğinde, kullanın [CWnd::DestroyWindow](../mfc/reference/cwnd-class.md#destroywindow) kontrol edilecek.

## <a name="see-also"></a>Ayrıca bkz.

[Denetimleri Yapma ve Kullanma](../mfc/making-and-using-controls.md)<br/>
[Denetimler](../mfc/controls-mfc.md)
