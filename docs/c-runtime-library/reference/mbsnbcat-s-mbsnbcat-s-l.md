---
title: _mbsnbcat_s, _mbsnbcat_s_l
ms.date: 4/2/2020
api_name:
- _mbsnbcat_s_l
- _mbsnbcat_s
- _o__mbsnbcat_s
- _o__mbsnbcat_s_l
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
- api-ms-win-crt-multibyte-l1-1-0.dll
- api-ms-win-crt-private-l1-1-0.dll
api_type:
- DLLExport
topic_type:
- apiref
f1_keywords:
- _mbsnbcat_s
- mbsnbcat_s
- _mbsnbcat_s_l
- mbsnbcat_s_l
helpviewer_keywords:
- _tcsncat function
- mbsnbcat_s function
- _mbsnbcat_s function
- _mbsnbcat_s_l function
- _tcsncat_s_l function
- tcsncat_s_l function
- mbsnbcat_s_l function
- tcsncat function
ms.assetid: 2c9e9be7-d979-4a54-8ada-23428b6648a9
ms.openlocfilehash: d731c94c879d0e4334dc3b57a19b94cc0378abaf
ms.sourcegitcommit: 5a069c7360f75b7c1cf9d4550446ec2fa2eb2293
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/07/2020
ms.locfileid: "82915640"
---
# <a name="_mbsnbcat_s-_mbsnbcat_s_l"></a>_mbsnbcat_s, _mbsnbcat_s_l

Çok baytlı bir karakter dizesine, en fazla bir çok baytlı karakter dizesinin ilk **n** baytını ekler. Bunlar, [CRT 'Daki güvenlik özellikleri](../../c-runtime-library/security-features-in-the-crt.md)bölümünde açıklandığı gibi güvenlik geliştirmeleri olan [_mbsnbcat_l _mbsnbcat](mbsnbcat-mbsnbcat-l.md) sürümleridir.

> [!IMPORTANT]
> Bu API, Windows Çalışma Zamanı yürütülen uygulamalarda kullanılamaz. Daha fazla bilgi için bkz. [Evrensel Windows platformu uygulamalarında CRT işlevleri desteklenmez](../../cppcx/crt-functions-not-supported-in-universal-windows-platform-apps.md).

## <a name="syntax"></a>Sözdizimi

```C
errno_t _mbsnbcat_s(
   unsigned char *dest,
   size_t sizeInBytes,
   const unsigned char *src,
   size_t count
);
errno_t _mbsnbcat_s_l(
   unsigned char *dest,
   size_t sizeInBytes,
   const unsigned char *src,
   size_t count,
   _locale_t locale
);
template <size_t size>
errno_t _mbsnbcat_s(
   unsigned char (&dest)[size],
   const unsigned char *src,
   size_t count
); // C++ only
template <size_t size>
errno_t _mbsnbcat_s_l(
   unsigned char (&dest)[size],
   const unsigned char *src,
   size_t count,
   _locale_t locale
); // C++ only
```

### <a name="parameters"></a>Parametreler

*HD*<br/>
Null ile sonlandırılmış çok baytlı karakter hedef dizesi.

*sizeInBytes*<br/>
*Hedef* arabelleğin bayt cinsinden boyutu.

*src*<br/>
Null ile sonlandırılmış çok baytlı karakter kaynak dizesi.

*biriktirme*<br/>
*Src* 'den *hedefe*eklenecek bayt sayısı.

*locale*<br/>
Kullanılacak yerel ayar.

## <a name="return-value"></a>Dönüş Değeri

Başarılıysa sıfır; Aksi takdirde, bir hata kodu.

### <a name="error-conditions"></a>Hata koşulları

|**HD**|*sizeInBytes*|*src*|Döndürülen değer|
|------------|-------------------|-----------|------------------|
|**DEĞER**|kaydedilmemiş|kaydedilmemiş|**EıNVAL**|
|Herhangi biri|<= 0|kaydedilmemiş|**EıNVAL**|
|Herhangi biri|kaydedilmemiş|**DEĞER**|**EıNVAL**|

Hata koşullarından herhangi biri gerçekleşirse, işlev [parametre doğrulamasında](../../c-runtime-library/parameter-validation.md)açıklanan şekilde geçersiz bir parametre hatası oluşturur. Hata işlenirse, işlev **EINVAL** döndürür ve **errno** 'u **EINVAL**olarak ayarlar.

## <a name="remarks"></a>Açıklamalar

**_Mbsnbcat_s** işlevi, en çok *,* *src*'nin ilk *sayım* baytlarına ekler. *Hedef* karakterdeki null karakterden hemen önce gelen bayt bir ön bayt ise, *src*'nin ilk baytından üzerine yazılır. Aksi takdirde, *src* 'nin ilk baytı, *hedef*alanının Sonlandırıcı null karakterinin üzerine yazar. *Src* içinde bir null bayt *görünürse,* *count* baytları eklenmeden önce, **_mbsnbcat_s** tüm baytları null karaktere kadar ekler. *Count* değeri *src*'nin uzunluğundan büyükse, *src* 'nin uzunluğu *Count*yerine kullanılır. Elde edilen dize, null bir karakter tarafından sonlandırılır. Çakışan dizeler arasında kopyalama gerçekleşmesi durumunda davranış tanımsızdır.

Çıkış değeri yerel ayarın **LC_CTYPE** kategori ayarı ayarından etkilenir; daha fazla bilgi için bkz. [setlocale, _wsetlocale](setlocale-wsetlocale.md) . Bu işlevlerin sürümleri aynıdır, çünkü **_l** sonekine sahip olmayanlar geçerli yerel ayarı kullanır, bunun yerine **_l** sonekine sahip olanlar, geçirilen yerel ayar parametresini kullanır. Daha fazla bilgi için bkz. [locale](../../c-runtime-library/locale.md).

C++ ' da, bu işlevlerin kullanımı şablon aşırı yüklemeleri tarafından basitleştirilmiştir; aşırı yüklemeler arabellek uzunluğunu otomatik olarak çıkarabilir ve böylece bir boyut bağımsız değişkeni belirtme gereksinimini ortadan kaldırabilir ve daha eski, daha az güvenli işlevlerini değiştirmek için daha yeni, daha güvenli işlevlerini otomatik olarak kullanabilir. Daha fazla bilgi için bkz. [Güvenli şablon aşırı yüklemeleri](../../c-runtime-library/secure-template-overloads.md).

Bu işlevlerin hata ayıklama Kitaplığı sürümleri ilk olarak arabelleği 0xFE ile doldurur. Bu davranışı devre dışı bırakmak için [_CrtSetDebugFillThreshold](crtsetdebugfillthreshold.md)kullanın.

Varsayılan olarak, bu işlevin genel durumu uygulamanın kapsamına alınır. Bunu değiştirmek için bkz. [CRT Içindeki genel durum](../global-state.md).

### <a name="generic-text-routine-mappings"></a>Genel Metin Yordam Eşleşmeleri

|Tchar.h yordamı|_UNICODE ve _MBCS tanımlanmaz|_MBCS tanımlanmış|_UNICODE tanımlanmış|
|---------------------|--------------------------------------|--------------------|-----------------------|
|**_tcsncat**|[strncat](strncat-strncat-l-wcsncat-wcsncat-l-mbsncat-mbsncat-l.md)|**_mbsnbcat_s**|[wcsncat](strncat-strncat-l-wcsncat-wcsncat-l-mbsncat-mbsncat-l.md)|
|**_tcsncat_s_l**|**_strncat_s_l**|**_mbsnbcat_s_l**|**_wcsncat_s_l**|

## <a name="requirements"></a>Gereksinimler

|Yordam|Gerekli başlık|
|-------------|---------------------|
|**_mbsnbcat_s**|\<mbstring. h>|
|**_mbsnbcat_s_l**|\<mbstring. h>|

Daha fazla uyumluluk bilgisi için bkz. [Uyumluluk](../../c-runtime-library/compatibility.md).

## <a name="see-also"></a>Ayrıca bkz.

[Dize Düzenlemesi](../../c-runtime-library/string-manipulation-crt.md)<br/>
[_mbsnbcmp, _mbsnbcmp_l](mbsnbcmp-mbsnbcmp-l.md)<br/>
[_strncnt, _wcsncnt, _mbsnbcnt, _mbsnbcnt_l, _mbsnccnt, _mbsnccnt_l](strncnt-wcsncnt-mbsnbcnt-mbsnbcnt-l-mbsnccnt-mbsnccnt-l.md)<br/>
[_mbsnbcpy, _mbsnbcpy_l](mbsnbcpy-mbsnbcpy-l.md)<br/>
[_mbsnbcpy_s, _mbsnbcpy_s_l](mbsnbcpy-s-mbsnbcpy-s-l.md)<br/>
[_mbsnbset, _mbsnbset_l](mbsnbset-mbsnbset-l.md)<br/>
[strncat, _strncat_l, wcsncat, _wcsncat_l, _mbsncat, _mbsncat_l](strncat-strncat-l-wcsncat-wcsncat-l-mbsncat-mbsncat-l.md)<br/>
[strncat_s, _strncat_s_l, wcsncat_s, _wcsncat_s_l, _mbsncat_s, _mbsncat_s_l](strncat-s-strncat-s-l-wcsncat-s-wcsncat-s-l-mbsncat-s-mbsncat-s-l.md)<br/>
