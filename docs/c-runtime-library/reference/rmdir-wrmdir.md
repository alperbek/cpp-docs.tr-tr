---
title: _rmdir, _wrmdir
ms.date: 4/2/2020
api_name:
- _wrmdir
- _rmdir
- _o__rmdir
- _o__wrmdir
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
- api-ms-win-crt-filesystem-l1-1-0.dll
- api-ms-win-crt-private-l1-1-0.dll
api_type:
- DLLExport
topic_type:
- apiref
f1_keywords:
- trmdir
- _trmdir
- wrmdir
- _rmdir
- _wrmdir
helpviewer_keywords:
- _rmdir function
- directories [C++], deleting
- rmdir function
- directories [C++], removing
- trmdir function
- _trmdir function
- _wrmdir function
- wrmdir function
ms.assetid: 652c2a5a-b0ac-4493-864e-1edf484333c5
ms.openlocfilehash: c0c5055a499614f364370b7aa90697898dc510ab
ms.sourcegitcommit: 5a069c7360f75b7c1cf9d4550446ec2fa2eb2293
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/07/2020
ms.locfileid: "82916925"
---
# <a name="_rmdir-_wrmdir"></a>_rmdir, _wrmdir

Bir dizini siler.

## <a name="syntax"></a>Sözdizimi

```C
int _rmdir(
   const char *dirname
);
int _wrmdir(
   const wchar_t *dirname
);
```

### <a name="parameters"></a>Parametreler

*DizinAdı*<br/>
Kaldırılacak dizinin yolu.

## <a name="return-value"></a>Dönüş Değeri

Bu işlevlerin her biri, dizin başarıyla silinirse 0 döndürür. -1 ' in dönüş değeri bir hatayı gösterir ve **errno** aşağıdaki değerlerden birine ayarlanır:

|errno değeri|Koşul|
|-|-|
| **ENOTEMPTY** | Verilen yol bir dizin değil, dizin boş değil veya dizin geçerli çalışma dizini ya da kök dizin. |
| **ENOENT** | Yol geçersiz. |
| **EACCES** | Bir programın dizine yönelik açık bir tutamacı vardır. |

Bu ve diğer dönüş kodları hakkında daha fazla bilgi için bkz. [_doserrno, errno, _sys_errlist ve _sys_nerr](../../c-runtime-library/errno-doserrno-sys-errlist-and-sys-nerr.md).

## <a name="remarks"></a>Açıklamalar

**_Rmdir** işlevi, *DizinAdı*tarafından belirtilen dizini siler. Dizinin boş olması ve geçerli çalışma dizini veya kök dizin olmaması gerekir.

**_wrmdir** , **_rmdir**geniş karakterli bir sürümüdür; _wrmdir *DizinAdı* bağımsız değişkeni **_wrmdir** geniş karakterli bir dizedir. **_wrmdir** ve **_rmdir** aynı şekilde davranır.

Varsayılan olarak, bu işlevin genel durumu uygulamanın kapsamına alınır. Bunu değiştirmek için bkz. [CRT Içindeki genel durum](../global-state.md).

### <a name="generic-text-routine-mappings"></a>Genel Metin Yordam Eşleşmeleri

|Tchar.h yordamı|_UNICODE ve _MBCS tanımlanmaz|_MBCS tanımlanmış|_UNICODE tanımlanmış|
|---------------------|--------------------------------------|--------------------|-----------------------|
|**_trmdir**|**_rmdir**|**_rmdir**|**_wrmdir**|

## <a name="requirements"></a>Gereksinimler

|Yordam|Gerekli başlık|
|-------------|---------------------|
|**_rmdir**|\<Direct. h>|
|**_wrmdir**|\<Direct. h> veya \<wchar. h>|

Daha fazla uyumluluk bilgisi için bkz. [Uyumluluk](../../c-runtime-library/compatibility.md).

## <a name="libraries"></a>Kitaplıklar

[C çalışma zamanı kitaplıklarının](../../c-runtime-library/crt-library-features.md)tüm sürümleri.

## <a name="example"></a>Örnek

[_Mkdir](mkdir-wmkdir.md)için örneğe bakın.

## <a name="see-also"></a>Ayrıca bkz.

[Dizin denetimi](../../c-runtime-library/directory-control.md)<br/>
[_chdir, _wchdir](chdir-wchdir.md)<br/>
[_mkdir, _wmkdir](mkdir-wmkdir.md)<br/>
