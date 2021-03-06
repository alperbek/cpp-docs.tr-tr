---
title: Eski Kod için Çoklu İş Parçacığı Kullanma Desteği (Visual C++)
ms.date: 08/27/2018
helpviewer_keywords:
- threading [C++]
- multiple threads
- concurrent programming [C++]
- programming [C++], multithreaded
- multithreading [C++], about multithreading
- multiple concurrent threads
- multithreading [C++]
ms.assetid: 24425b1f-5031-4c6b-aac7-017115a40e7c
ms.openlocfilehash: 6f76ff42d2e28afe251ce234220051111736d3c9
ms.sourcegitcommit: 857fa6b530224fa6c18675138043aba9aa0619fb
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/24/2020
ms.locfileid: "80215091"
---
# <a name="multithreading-support-for-older-code-visual-c"></a>Eski Kod için Çoklu İş Parçacığı Kullanma Desteği (Visual C++)

Visual C++ , aynı anda birden çok eşzamanlı yürütme iş parçacığının çalıştırılmasına izin verir. Çoklu iş parçacıklı ile arka plan görevlerini kapatabilir, eşzamanlı giriş akışlarını yönetebilir, bir kullanıcı arabirimini yönetebilir ve çok daha fazlasını yapabilirsiniz.

## <a name="in-this-section"></a>Bu Bölümde

[C ve Win32 ile Çoklu İş Parçacığı Kullanımı](multithreading-with-c-and-win32.md)<br/>
Microsoft Windows ile çoklu iş parçacıklı uygulamalar oluşturmaya yönelik destek sağlar

[C++ ve MCF ile Çoklu İş Parçacığı Kullanımı](multithreading-with-cpp-and-mfc.md)<br/>
İşlem ve iş parçacıklarının ne olduğunu ve çoklu iş parçacıklı MFC yaklaşımının ne olduğunu açıklar.

[Çoklu İş Parçacığı Kullanımı ve Yerel Ayarlar](multithreading-and-locales.md)<br/>
Hem C çalışma zamanı kitaplığının hem de çok iş parçacıklı uygulamadaki C++ standart kitaplığın yerel ayar işlevselliği kullanılırken ortaya çıkan sorunları açıklar.

## <a name="related-sections"></a>İlgili Bölümler

[CWinThread](../mfc/reference/cwinthread-class.md)<br/>
Bir uygulama içindeki yürütmenin iş parçacığını temsil eder.

[CSyncObject](../mfc/reference/csyncobject-class.md)<br/>
Win32 içindeki eşitleme nesneleri için ortak işlevselliği sağlayan saf bir sanal sınıfı açıklar.

[Csemafor](../mfc/reference/csemaphore-class.md)<br/>
Bir veya daha fazla işlemde sınırlı sayıda iş parçacığına bir kaynağa erişmesi için bir eşitleme nesnesi olan bir semaforu temsil eder.

[CMutex](../mfc/reference/cmutex-class.md)<br/>
Bir iş parçacığının bir kaynağa birbirini dışlamalı erişimine izin veren bir eşitleme nesnesi olan bir mutex 'i temsil eder.

[Ckritiksection](../mfc/reference/ccriticalsection-class.md)<br/>
Bir kaynağa veya kod bölümüne erişmek için bir seferde bir iş parçacığına izin veren bir eşitleme nesnesi olan kritik bir bölümü temsil eder.

[CEvent](../mfc/reference/cevent-class.md)<br/>
Bir olay oluştuğunda bir iş parçacığının bilgilendirmek için bir iş parçacığına izin veren bir eşitleme nesnesi olan bir olayı temsil eder.

[CMultiLock](../mfc/reference/cmultilock-class.md)<br/>
Çok iş parçacıklı bir programdaki kaynaklara erişimi denetlemek için kullanılan erişim denetimi mekanizmasını temsil eder.

[CSingleLock](../mfc/reference/csinglelock-class.md)<br/>
Çok iş parçacıklı programda bir kaynağa erişimi denetlemek için kullanılan erişim denetimi mekanizmasını temsil eder.
