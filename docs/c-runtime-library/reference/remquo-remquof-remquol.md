---
title: remquo, remquof, remquol
ms.date: 4/2/2020
api_name:
- remquof
- remquo
- remquol
- _o_remquo
- _o_remquof
- _o_remquol
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
- api-ms-win-crt-math-l1-1-0.dll
- api-ms-win-crt-private-l1-1-0.dll
api_type:
- DLLExport
topic_type:
- apiref
f1_keywords:
- remquof
- remquol
- remquo
helpviewer_keywords:
- remquol function
- remquof function
- remquo function
ms.assetid: a1d3cb8b-8027-4cd3-8deb-04eb17f299fc
ms.openlocfilehash: 774a35f257b02c67b22618224a60ed501476a6f4
ms.sourcegitcommit: 5a069c7360f75b7c1cf9d4550446ec2fa2eb2293
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/07/2020
ms.locfileid: "82917827"
---
# <a name="remquo-remquof-remquol"></a>remquo, remquof, remquol

İki tamsayı değerinin kalanını hesaplar ve işaret ile bir tamsayı değeri ve bir parametrede belirtilen konumdaki alanın yaklaşık büyüklüğü ile birlikte depolar.

## <a name="syntax"></a>Sözdizimi

```C
double remquo( double numer, double denom, int* quo );
float remquof( float numer, float denom, int* quo );
long double remquol( long double numer, long double denom, int* quo );
```

```cpp
float remquo( float numer, float denom, int* quo ); /* C++ only */
long double remquo( long double numer, long double denom, int* quo ); /* C++ only */
```

### <a name="parameters"></a>Parametreler

*numer*<br/>
Pay.

*denom*<br/>
Payda.

*göster*<br/>
İşaretine ve bölümün yaklaşık büyüklüğüne sahip bir değeri depolamak için bir tamsayıya yönelik bir işaretçi.

## <a name="return-value"></a>Dönüş Değeri

**remquo** , *x* / *y*'nin kayan nokta kalanını döndürür. *Y* değeri 0,0 ise, **remquo** bir sessiz NaN döndürür. **Printf** ailesi tarafından sessiz bir NaN 'ın temsili hakkında daha fazla bilgi için bkz. [printf, _printf_l, wprintf, _wprintf_l](printf-printf-l-wprintf-wprintf-l.md).

## <a name="remarks"></a>Açıklamalar

**Remquo** işlevi *, x* / *y* \* *i* *y* *x* =  + *f*'nin kayan *nokta geri kalanını* hesaplar *, burada bir tamsayıdır,* *f* ise *x*ile aynı işarete sahiptir ve *f* 'nin mutlak değeri *y*'nin mutlak değerinden küçüktür.

C++ aşırı yüklemeye izin verdiğinden, **float** veya **Long** **Double** değerleri alıp döndüren **remquo** aşırı yüklerini çağırabilirsiniz. C programında, **remquo** her zaman iki **çift** bağımsız değişken alır ve bir **Double**döndürür.

Varsayılan olarak, bu işlevin genel durumu uygulamanın kapsamına alınır. Bunu değiştirmek için bkz. [CRT Içindeki genel durum](../global-state.md).

## <a name="requirements"></a>Gereksinimler

|İşlev|Gerekli üst bilgi (C)|Gerekli üst bilgi (C++)|
|--------------|---------------------|-|
|**remquo**, **remquof**, **remquol**|\<Math. h>|\<cmath> veya \<Math. h>|

Uyumluluk bilgileri için bkz. [Uyumluluk](../../c-runtime-library/compatibility.md).

## <a name="example"></a>Örnek

```C
// crt_remquo.c
// This program displays a floating-point remainder.

#include <math.h>
#include <stdio.h>

int main( void )
{
   double w = -10.0, x = 3.0, z;
   int quo = 0;

   z = remquo(w, x, &quo);
   printf("The remainder of %.2f / %.2f is %f\n", w, x, z);
   printf("Approximate signed quotient is %d\n", quo);
}
```

```Output
The remainder of -10.00 / 3.00 is -1.000000
Approximate signed quotient is -3
```

## <a name="see-also"></a>Ayrıca bkz.

[Kayan Nokta Desteği](../../c-runtime-library/floating-point-support.md)<br/>
[ldiv, lldiv](ldiv-lldiv.md)<br/>
[imaxdiv](imaxdiv.md)<br/>
[fmod, fmodf](fmod-fmodf.md)<br/>
[remainder, remainderf, remainderl](remainder-remainderf-remainderl.md)<br/>
