---
title: Birleşik Giriş Kutusu İşleyicileri
ms.date: 11/04/2016
f1_keywords:
- ON_CBN_KILLFOCUS
- ON_CBN_ERRSPACE
- ON_CBN_EDITCHANGE
- ON_CBN_CLOSEUP
- ON_CBN_DBLCLK
- ON_CBN_EDITUPDATE
- ON_CBN_DROPDOWN
- ON_CBN_SELENDOK
- ON_CBN_SELCHANGE
- ON_CBN_SETFOCUS
- ON_CBN_SELENDCANCEL
helpviewer_keywords:
- ON_CBN_CLOSEUP
- ON_CBN_SETFOCUS
- ON_CBN_DBLCLK
- ON_CBN_SELENDCANCEL
- ON_CBN_DROPDOWN
- ON_CBN_EDITUPDATE
- ON_CBN_KILLFOCUS
- combo boxes [MFC], handlers
- ON_CBN_EDITCHANGE
- ON_CBN_ERRSPACE
- ON_CBN_SELENDOK
- ON_CBN_SELCHANGE
ms.assetid: 7f092412-01b7-4242-95ec-41ba506b9d71
ms.openlocfilehash: ed83bcf565ec420d159c73ddfd82827aac88693f
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62373264"
---
# <a name="combo-box-handlers"></a>Birleşik Giriş Kutusu İşleyicileri

Aşağıdaki eşleme girişleri için işlev prototipleri karşılık gelir.

|Eşleme girişi|İşlev prototipi|
|---------------|------------------------|
|ON_CBN_CLOSEUP ( \<kimliği >, \<memberFxn >)|afx_msg void memberFxn (.)|
|ON_CBN_DBLCLK( \<id>, \<memberFxn> )|afx_msg void memberFxn ();|
|ON_CBN_DROPDOWN( \<id>, \<memberFxn> )|afx_msg void memberFxn ();|
|ON_CBN_EDITCHANGE ( \<kimliği >, \<memberFxn >)|afx_msg void memberFxn ();|
|ON_CBN_EDITUPDATE ( \<kimliği >, \<memberFxn >)|afx_msg void memberFxn ();|
|ON_CBN_ERRSPACE ( \<kimliği >, \<memberFxn >)|afx_msg void memberFxn ();|
|ON_CBN_KILLFOCUS( \<id>, \<memberFxn> )|afx_msg void memberFxn ();|
|ON_CBN_SELCHANGE( \<id>, \<memberFxn> )|afx_msg void memberFxn ();|
|ON_CBN_SELENDCANCEL( \<id>, \<memberFxn> )|afx_msg void memberFxn ();|
|ON_CBN_SELENDOK( \<id>, \<memberFxn> )|afx_msg void memberFxn ();|
|ON_CBN_SETFOCUS( \<id>, \<memberFxn> )|afx_msg void memberFxn ();|

## <a name="see-also"></a>Ayrıca bkz.

[İleti eşlemeleri](../../mfc/reference/message-maps-mfc.md)
