---
title: Derleyici Hatası C2338
ms.date: 11/04/2016
f1_keywords:
- C2338
helpviewer_keywords:
- C2338
ms.assetid: 49bba575-1de4-4963-86c6-ce3226a2ba51
ms.openlocfilehash: 2a76ecaf78b117b0c1acabd9fcd50c9ae0f73b98
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62188302"
---
# <a name="compiler-error-c2338"></a>Derleyici Hatası C2338

> *hata iletisi*

Bu hataya neden olabilir bir `static_assert` derleme sırasında hata oluştu. İleti tarafından sağlanan `static_assert` parametreleri.

Bu hata iletisi, dış sağlayıcıları için derleyici tarafından da oluşturulabilir. Çoğu durumda, bu hata, bir öznitelik sağlayıcısı ATLPROV gibi DLL tarafından raporlanır. Bu iletinin bazı ortak biçimleri şunlardır:

- '*özniteliği*' Atl özniteliği sağlayıcısı: hata ATL*numarası* *iletisi*

- Öznitelik yanlış kullanımı '*özniteliği*'

- '*kullanım*': 'kullanımı' özniteliği için yanlış biçim

Bu hatalar genellikle kurtarılamaz olarak kabul edilir ve önemli bir derleyici hatası tarafından izlenebilir.

Bu sorunları düzeltmek için öznitelik kullanımı düzeltin. Örneğin, kullanılabilmesi için önce bazı durumlarda, öznitelik parametreleri bildirilmesi gerekir. Bir ATL hata numarası sağlanmazsa, daha fazla bilgi için hata belgelerine bakın.
