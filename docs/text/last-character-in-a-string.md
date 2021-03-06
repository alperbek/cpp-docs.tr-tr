---
title: Dizedeki Son Karakter
ms.date: 11/04/2016
helpviewer_keywords:
- last character in string
- MBCS [C++], last character in string
ms.assetid: 0a180376-4e55-41e8-9c64-539c7b6d8047
ms.openlocfilehash: 4c99628cd12738fabb877a94cfd04a4033ee45aa
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62410680"
---
# <a name="last-character-in-a-string"></a>Dizedeki Son Karakter

Aşağıdaki ipuçlarını kullanın:

- ASCII karakter kümesini çoğu durumda izi bayt aralıkları çakışıyor. Bu gibi durumlarda, dizede taramalar güvenli bir şekilde, denetim karakterlerini (32 den küçük) için kullanabilirsiniz.

- Bir dizedeki son karakter bir ters eğik çizgi karakteri olup olmadığını görmek için denetimi yapıyor olabilir kod, aşağıdaki satırı göz önünde bulundurun:

    ```cpp
    if ( sz[ strlen( sz ) - 1 ] == '\\' )    // Is last character a '\'?
        // . . .
    ```

   Çünkü `strlen` MBCS tanımayan çok baytlı bir dize karakter sayısını değil bayt sayısını döndürür. Ayrıca, bazı kod sayfalarında (örneğin, 932), Not '\\' (0x5c) olan geçerli bir bayt (`sz` C dizesi).

   Bu şekilde, yeniden kod yazmak için olası bir çözüm şöyledir:

    ```cpp
    char *pLast;
    pLast = _mbsrchr( sz, '\\' );    // find last occurrence of '\' in sz
    if ( pLast && ( *_mbsinc( pLast ) == '\0' ) )
        // . . .
    ```

   Bu kod MBCS işlevlerini kullanır `_mbsrchr` ve `_mbsinc`. Bu işlevler MBCS kullanan olduğundan, bunlar arasında ayrım yapabilme kolaylığı bir '\\'karakteri ve sondaki baytı'\\'. Dizedeki son karakter ('\0') null ise kod bazı eylemleri gerçekleştirir.

## <a name="see-also"></a>Ayrıca bkz.

[MBCS Programlama İpuçları](../text/mbcs-programming-tips.md)<br/>
[Karakter Atama](../text/character-assignment.md)
