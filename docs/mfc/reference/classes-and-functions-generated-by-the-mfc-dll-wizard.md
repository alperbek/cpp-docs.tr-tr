---
title: MFC DLL Sihirbazı Tarafından Üretilen Sınıfları ve İşlevler
ms.date: 11/04/2016
helpviewer_keywords:
- functions [MFC]
- functions [MFC], DLLs
- MFC DLL Wizard
- DLLs [MFC], wizard classes and functions
- classes [MFC], generated by MFC DLL wizard
- code [MFC], generated by MFC DLL wizard
ms.assetid: e69e62fe-4953-42bf-a2fc-50bbf9bdaeaf
ms.openlocfilehash: add914f18ab961ff6dbc5cb056e2f2a81c252a48
ms.sourcegitcommit: 7a6116e48c3c11b97371b8ae4ecc23adce1f092d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/22/2020
ms.locfileid: "81754913"
---
# <a name="classes-and-functions-generated-by-the-mfc-dll-wizard"></a>MFC DLL Sihirbazı Tarafından Üretilen Sınıfları ve İşlevler

MFC DLL Sihirbazı'nın oluşturduğu kod, oluşturduğunuz DLL türüne ve seçtiğiniz seçeneklere bağlıdır. MFC DLL Sihirbazı, normal MFC DL'lerin her iki formu için de aynı kodu oluşturur.

|DLL Türü|Seçenek|Sınıflar|İşlevler|
|-----------------|------------|-------------|---------------|
|[Dahili numara](../../build/extension-dlls-overview.md)|Hiçbiri|Hiçbiri|`DllMain`|
|[Normal](../../build/regular-dlls-dynamically-linked-to-mfc.md)|Hiçbiri|Uygulama sınıfı türetilmiş`CWinApp`|Hiçbiri|
|[Normal](../../build/regular-dlls-dynamically-linked-to-mfc.md)|Otomasyon|Uygulama sınıfı türetilmiş`CWinApp`|`DllGetClassObject` `DllCanUnloadNow` `DllRegisterServer`|
|[Dahili numara](../../build/extension-dlls-overview.md)|Pencere Soketi|Hiçbiri|`DllMain`|
|[Normal](../../build/regular-dlls-dynamically-linked-to-mfc.md)|Pencere Soketi|Uygulama sınıfı türetilmiş`CWinApp`|`InitInstance`için çağrı içerir`AfxSocketInit`|

## <a name="see-also"></a>Ayrıca bkz.

[MFC DLL Sihirbazı](../../mfc/reference/mfc-dll-wizard.md)
