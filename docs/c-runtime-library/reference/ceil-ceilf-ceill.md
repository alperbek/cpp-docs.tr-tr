---
title: ceil, ceilf, ceill
ms.date: 6/5/2020
api_name:
- ceilf
- ceil
- ceill
- _o_ceil
- _o_ceilf
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
- ntdll.dll
- api-ms-win-crt-math-l1-1-0.dll
- api-ms-win-crt-private-l1-1-0.dll
api_type:
- DLLExport
topic_type:
- apiref
f1_keywords:
- ceil
- ceilf
- ceill
helpviewer_keywords:
- calculating value ceilings
- ceill function
- ceil function
- ceilf function
ms.assetid: f4e5acab-5c8f-4b10-9ae2-9561e6453718
ms.openlocfilehash: 284443f511217be7873a7d7b02562484b32cefca
ms.sourcegitcommit: fe146adb3a02872538637196bb3c45aeeeaaf5c2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/08/2020
ms.locfileid: "84507085"
---
# <a name="ceil-ceilf-ceill"></a>ceil, ceilf, ceill

Bir değerin tavan değerini hesaplar.

## <a name="syntax"></a>Söz dizimi

```C
double ceil(
   double x
);
float ceil(
   float x
);  // C++ only
long double ceil(
   long double x
);  // C++ only
float ceilf(
   float x
);
long double ceill(
   long double x
);
```

### <a name="parameters"></a>Parametreler

*x*<br/>
Kayan nokta değeri.

## <a name="return-value"></a>Dönüş Değeri

**CEIL** işlevleri, *x*değerinden büyük veya buna eşit en küçük tamsayıyı temsil eden bir kayan nokta değeri döndürür. Hata döndürme yok.

|Giriş|SEH özel durumu|Matherr özel durumu|
|-----------|-------------------|-----------------------|
|± **QNAN**, **IND**|yok|**_DOMAIN**|

**CEIL** 'de Streaming SIMD Extensions 2 (SSE2) kullanan bir uygulama vardır. SSE2 uygulamasını kullanma hakkında bilgi ve sınırlamalar için bkz. [_set_SSE2_enable](set-sse2-enable.md).

## <a name="remarks"></a>Açıklamalar

C++ aşırı yüklemeye izin verdiğinden, **kayan** veya **uzun** **çift** türleri alan **CEIL** 'nin aşırı yüklerini çağırabilirsiniz. C programında **CEIL** her zaman bir **Double**alır ve döndürür.

Varsayılan olarak, bu işlevin genel durumu uygulamanın kapsamına alınır. Bunu değiştirmek için bkz. [CRT Içindeki genel durum](../global-state.md).

## <a name="requirements"></a>Gereksinimler

|Yordam|Gerekli başlık|
|-------------|---------------------|
|**ceil**, **ceilf**, **ceill**|\<math.h>|

Ek uyumluluk bilgileri için bkz. [Uyumluluk](../../c-runtime-library/compatibility.md).

## <a name="example"></a>Örnek

[Taban](floor-floorf-floorl.md)için örneğe bakın.

## <a name="see-also"></a>Ayrıca bkz.

[Kayan nokta desteği](../../c-runtime-library/floating-point-support.md)<br/>
[floor, floorf, floorl](floor-floorf-floorl.md)<br/>
[fmod, fmodf](fmod-fmodf.md)<br/>
[round, roundf, roundl](round-roundf-roundl.md)<br/>
