---
title: wctrans
ms.date: 11/04/2016
api_name:
- wctrans
api_location:
- msvcrt.dll
- msvcr80.dll
- msvcr90.dll
- msvcr100.dll
- msvcr100_clr0400.dll
- msvcr110.dll
- msvcr110_clr0400.dll
- msvcr120.dll
- msvcr120_clr0400.dll
- ucrtbase.dll
- api-ms-win-crt-convert-l1-1-0.dll
api_type:
- DLLExport
topic_type:
- apiref
f1_keywords:
- wctrans
helpviewer_keywords:
- character codes, wctrans
- characters, codes
- characters, converting
- wctrans function
ms.assetid: 215404bf-6d60-489c-9ae9-880e6b586162
ms.openlocfilehash: a75de3b699d0eb5ec6117d0f627e6a8ba34dbc62
ms.sourcegitcommit: f19474151276d47da77cdfd20df53128fdcc3ea7
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/12/2019
ms.locfileid: "70944883"
---
# <a name="wctrans"></a>wctrans

Bir karakter kodu kümesinden diğerine eşlemeyi belirler.

## <a name="syntax"></a>Sözdizimi

```C
wctrans_t wctrans(
   const char *property
);
```

### <a name="parameters"></a>Parametreler

*property*<br/>
Geçerli dönüşümlerinden birini belirten bir dize.

## <a name="return-value"></a>Dönüş Değeri

Geçerli yerel ayarın **LC_CTYPE** kategorisi, adı özellik dizesi *özelliği*ile eşleşen bir eşleme tanımlamıyorsa, işlev sıfır döndürür. Aksi halde, sonraki [towctrans](towctrans.md)çağrısının ikinci bağımsız değişkeni olarak kullanılmak üzere uygun olmayan bir değer döndürür.

## <a name="remarks"></a>Açıklamalar

Bu işlev, bir karakter kodu kümesinden diğerine eşlemeyi belirler.

Aşağıdaki çağrı çiftleri tüm yerel ayarlarda aynı davranışa sahiptir, ancak "C" yerel ayarında bile ek eşlemeler tanımlamak mümkündür:

|İşlev|Aynı|
|--------------|-------------|
|ToLower (c)|towctrans (c, wctrans ("towlower"))|
|kasaüst (c)|towctrans (c, wctrans ("ToUpper"))|

## <a name="requirements"></a>Gereksinimler

|Yordam|Gerekli üst bilgi|
|-------------|---------------------|
|**wctrans**|\<wctype. h >|

Ek uyumluluk bilgileri için bkz. [Uyumluluk](../../c-runtime-library/compatibility.md).

## <a name="example"></a>Örnek

```C
// crt_wctrans.cpp
// compile with: /EHsc
// This example determines a mapping from one set of character
// codes to another.

#include <wchar.h>
#include <wctype.h>
#include <stdio.h>
#include <iostream>

int main()
{
    wint_t c = 'a';
    printf_s("%d\n",c);

    wctrans_t i = wctrans("toupper");
    printf_s("%d\n",i);

    wctrans_t ii = wctrans("towlower");
    printf_s("%d\n",ii);

    wchar_t wc = towctrans(c, i);
    printf_s("%d\n",wc);
}
```

```Output
97
1
0
65
```

## <a name="see-also"></a>Ayrıca bkz.

[Veri Dönüştürme](../../c-runtime-library/data-conversion.md)<br/>
[setlocale, _wsetlocale](setlocale-wsetlocale.md)<br/>
