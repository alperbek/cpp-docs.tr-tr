---
title: _get_doserrno
ms.date: 4/2/2020
api_name:
- _get_doserrno
- _o__get_doserrno
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
- api-ms-win-crt-runtime-l1-1-0.dll
- api-ms-win-crt-private-l1-1-0.dll
api_type:
- DLLExport
topic_type:
- apiref
f1_keywords:
- _get_doserrno
- get_doserrno
helpviewer_keywords:
- get_doserrno function
- _get_doserrno function
ms.assetid: 7fec7be3-6e39-4181-846b-8ef24489361c
ms.openlocfilehash: 7b889bccc0b1f1fd99a9a0526bbfb42a2e520970
ms.sourcegitcommit: 5a069c7360f75b7c1cf9d4550446ec2fa2eb2293
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/07/2020
ms.locfileid: "82919379"
---
# <a name="_get_doserrno"></a>_get_doserrno

Bir **errno** değerine çevrilmeden önce işletim sistemi tarafından döndürülen hata değerini alır.

## <a name="syntax"></a>Sözdizimi

```C
errno_t _get_doserrno(
   int * pValue
);
```

### <a name="parameters"></a>Parametreler

*pValue*<br/>
**_Doserrno** genel makrosunun geçerli değeriyle doldurulacak bir tamsayıya yönelik bir işaretçi.

## <a name="return-value"></a>Dönüş Değeri

**_Get_doserrno** başarılı olursa, sıfır döndürür; başarısız olursa, bir hata kodu döndürür. *PValue* **null**ise, [parametre doğrulama](../../c-runtime-library/parameter-validation.md)bölümünde açıklandığı gibi geçersiz parametre işleyicisi çağrılır. Yürütmenin devam etmesine izin veriliyorsa, bu işlev **errno** ' ı **EINVAL** olarak ayarlar ve **EINVAL**döndürür.

## <a name="remarks"></a>Açıklamalar

**_Doserrno** genel makro, işlem yürütme başlamadan önce CRT başlatma sırasında sıfır olarak ayarlanır. Bu, işletim sistemi hatası döndüren herhangi bir sistem düzeyi işlev çağrısıyla döndürülen işletim sistemi hata değerine ayarlanır ve yürütme sırasında hiçbir şekilde sıfıra sıfırlanmaz. Bir işlev tarafından döndürülen hata değerini denetlemek için kod yazdığınızda, işlev çağrısından önce [_set_doserrno](set-doserrno.md) kullanarak **_doserrno** her zaman temizleyin. Başka bir işlev çağrısı **_doserrno**üzerine yazılabileceğinden, işlev çağrısından hemen sonra **_get_doserrno** kullanarak değeri denetleyin.

Taşınabilir hata kodları için **_get_doserrno** yerine [_get_errno](get-errno.md) önerilir.

**_Doserrno** olası değerleri errno. h \<> içinde tanımlanmıştır.

Varsayılan olarak, bu işlevin genel durumu uygulamanın kapsamına alınır. Bunu değiştirmek için bkz. [CRT Içindeki genel durum](../global-state.md).

## <a name="requirements"></a>Gereksinimler

|Yordam|Gerekli başlık|İsteğe bağlı başlık|
|-------------|---------------------|---------------------|
|**_get_doserrno**|\<Stdlib. h>, \<cstdlib> (C++)|\<errno. h>, \<cerrno> (C++)|

**_get_doserrno** bir Microsoft uzantısıdır. Daha fazla uyumluluk bilgisi için bkz. [Uyumluluk](../../c-runtime-library/compatibility.md).

## <a name="see-also"></a>Ayrıca bkz.

[_set_doserrno](set-doserrno.md)<br/>
[errno, _doserrno, _sys_errlist, and _sys_nerr](../../c-runtime-library/errno-doserrno-sys-errlist-and-sys-nerr.md)<br/>
