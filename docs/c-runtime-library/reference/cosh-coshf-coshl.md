---
title: cosh, coshf, coshl
ms.date: 4/2/2020
api_name:
- cosh
- coshf
- coshl
- _o_cosh
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
- cosh
- coshf
- coshl
helpviewer_keywords:
- cosh function
- coshf function
- coshl function
- trigonometric functions
- hyperbolic functions
ms.openlocfilehash: e5e313f08fc7e6d00a1cffc9522d3c8a818cd152
ms.sourcegitcommit: 5a069c7360f75b7c1cf9d4550446ec2fa2eb2293
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/07/2020
ms.locfileid: "82917225"
---
# <a name="cosh-coshf-coshl"></a>cosh, coshf, coshl

Hiperbolik kosinüsü hesaplar.

## <a name="syntax"></a>Sözdizimi

```C
double cosh( double x );
float coshf( float x );
long double coshl( long double x );
```

```cpp
float cosh( float x );  // C++ only
long double cosh( long double x );  // C++ only
```

### <a name="parameters"></a>Parametreler

*sayı*<br/>
Radyan cinsinden açı.

## <a name="return-value"></a>Dönüş Değeri

*X*'in hiperbolik kosinüsü.

Varsayılan olarak, sonuç bir **cosh**, **coshf**veya **coshl** çağrısında çok büyükse, işlev **HUGE_VAL** döndürür ve **errno** ' ı **ERANGE**olarak ayarlar.

|Giriş|SEH özel durumu|Matherr özel durumu|
|-----------|-------------------|-----------------------|
|± **QNAN**, **IND**|yok|**_DOMAIN**|
|*x* ≥ 7.104760 e + 002|**tam**+**taşma**|**TAŞMA**|

## <a name="remarks"></a>Açıklamalar

C++ aşırı yüklemeye izin verdiğinden, **float** veya **Long** **Double** değerleri alıp döndüren **cosh** aşırı yüklerini çağırabilirsiniz. C programında, **cosh** her zaman bir **Double**alır ve döndürür.

Varsayılan olarak, bu işlevin genel durumu uygulamanın kapsamına alınır. Bunu değiştirmek için bkz. [CRT Içindeki genel durum](../global-state.md).

## <a name="requirements"></a>Gereksinimler

|Yordam|Gerekli üst bilgi (C)|Gerekli üst bilgi (C++)|
|-------------|---------------------|-|
|**coshf**, **COSL**, **coshl**|\<Math. h>|\<cmath> veya \<Math. h>|

Ek uyumluluk bilgileri için bkz. [Uyumluluk](../../c-runtime-library/compatibility.md).

## <a name="example"></a>Örnek

[Sinh, sinhf, sinhl](sinh-sinhf-sinhl.md)içindeki örneğe bakın.

## <a name="see-also"></a>Ayrıca bkz.

[Kayan Nokta Desteği](../../c-runtime-library/floating-point-support.md)<br/>
[acosh, acoshf, acoshl](acosh-acoshf-acoshl.md)<br/>
[asinh, asinhf, asinhl](asinh-asinhf-asinhl.md)<br/>
[atanh, atanhf, atanhl](atanh-atanhf-atanhl.md)<br/>
[_matherr](matherr.md)<br/>
[sinh, sinhf, sinhl](sinh-sinhf-sinhl.md)<br/>
[tanh, tanhf, tanhl](tanh-tanhf-tanhl.md)<br/>
