---
title: _setmaxstdio
ms.date: 05/21/2019
api_name:
- _setmaxstdio
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
- api-ms-win-crt-stdio-l1-1-0.dll
api_type:
- DLLExport
topic_type:
- apiref
f1_keywords:
- setmaxstdio
- _setmaxstdio
helpviewer_keywords:
- maximum open files
- _setmaxstdio function
- setmaxstdio function
- open files, maximum
ms.assetid: 9e966875-9ff5-47c4-9b5f-e79e83b70249
ms.openlocfilehash: 620213b4df9ea555189a1403b3c9e83b55cad6c6
ms.sourcegitcommit: f19474151276d47da77cdfd20df53128fdcc3ea7
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/12/2019
ms.locfileid: "70948229"
---
# <a name="_setmaxstdio"></a>_setmaxstdio

Akış g/ç düzeyindeki eşzamanlı açık dosya sayısı için bir üst sınır ayarlar.

## <a name="syntax"></a>Sözdizimi

```C
int _setmaxstdio(
   int new_max
);
```

### <a name="parameters"></a>Parametreler

*new_max*<br/>
Akış g/ç düzeyinde aynı anda açık dosya sayısı için yeni en yüksek değer.

## <a name="return-value"></a>Dönüş Değeri

Başarılı olursa *new_max* döndürür; -1 Aksi takdirde.

*New_max* , **_Iob_entries**değerinden küçükse veya işletim sisteminde kullanılabilir olan en fazla tanıtıcı sayısından büyükse, [parametre doğrulama](../../c-runtime-library/parameter-validation.md)bölümünde açıklandığı gibi geçersiz parametre işleyicisi çağrılır. Yürütmenin devam etmesine izin veriliyorsa, bu işlev-1 döndürür ve **errno** 'ı **EINVAL**olarak ayarlar.

Bu ve diğer hata kodları hakkında daha fazla bilgi için bkz. [_doserrno, errno, _sys_errlist ve _sys_nerr](../../c-runtime-library/errno-doserrno-sys-errlist-and-sys-nerr.md).

## <a name="remarks"></a>Açıklamalar

**_Setmaxstdio** işlevi, akış g/ç düzeyinde aynı anda açık olabilecek dosya sayısı için maksimum değeri değiştirir.

C çalışma zamanı g/ç artık [düşük g/ç düzeyinde](../../c-runtime-library/low-level-i-o.md)aynı anda en fazla 8.192 dosyayı destekler. Bu düzey, açılan ve g/ç işlevlerinin **_açık**, **_Okuma**ve **yazma** ailesi işlevleri kullanılarak erişilen dosyaları içerir. Varsayılan olarak, en çok 512 dosya [akış g/ç düzeyinde](../../c-runtime-library/stream-i-o.md)eşzamanlı olarak açılabilir. Bu düzey, **fopen**, **fgetc**ve **fputc** ailesi işlevleri kullanılarak açılan ve erişilen dosyaları içerir. Akış g/ç düzeyindeki 512 açık dosya sınırı, **_setmaxstdio** işlevi kullanılarak en fazla 8.192 ' e artırılabilir.

**Fopen**gibi akış g/ç düzeyi işlevleri düşük g/ç düzeyi işlevlerinin üzerine inşa edildiğinden, en fazla 8.192, C çalışma zamanı kitaplığı aracılığıyla erişilen aynı anda açık dosya sayısı için sabit bir üst sınırdır.

> [!NOTE]
> Bu üst sınır, belirli bir Win32 platformu ve yapılandırması tarafından desteklenenden daha fazla olabilir.

## <a name="requirements"></a>Gereksinimler

|Yordam|Gerekli başlık|
|-------------|---------------------|
|**_setmaxstdio**|\<stdio. h >|

Daha fazla uyumluluk bilgisi için bkz. [Uyumluluk](../../c-runtime-library/compatibility.md).

## <a name="example"></a>Örnek

**_Setmaxstdio**kullanımı örneği için bkz. [_getmaxstdio](getmaxstdio.md) .

## <a name="see-also"></a>Ayrıca bkz.

[Akış g/ç](../../c-runtime-library/stream-i-o.md)<br/>
