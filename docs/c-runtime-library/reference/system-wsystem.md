---
title: system, _wsystem
ms.date: 4/2/2020
api_name:
- system
- _wsystem
- _o__wsystem
- _o_system
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
- _tsystem
- _wsystem
helpviewer_keywords:
- _wsystem function
- wsystem function
- tsystem function
- _tsystem function
- system function
- commands, executing
- command interpreter
ms.assetid: 7d3df2b6-f742-49ce-bf52-012b0aee3df5
ms.openlocfilehash: 09353c9cda2bc85d91f57806bc3497e49a19f803
ms.sourcegitcommit: 5a069c7360f75b7c1cf9d4550446ec2fa2eb2293
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/07/2020
ms.locfileid: "82912388"
---
# <a name="system-_wsystem"></a>system, _wsystem

Bir komutu yürütür.

> [!IMPORTANT]
> Bu API, Windows Çalışma Zamanı yürütülen uygulamalarda kullanılamaz. Daha fazla bilgi için bkz. [Evrensel Windows platformu uygulamalarında CRT işlevleri desteklenmez](../../cppcx/crt-functions-not-supported-in-universal-windows-platform-apps.md).

## <a name="syntax"></a>Sözdizimi

```C
int system(
   const char *command
);
int _wsystem(
   const wchar_t *command
);
```

### <a name="parameters"></a>Parametreler

*komutundaki*<br/>
Yürütülecek komut.

## <a name="return-value"></a>Dönüş Değeri

*Komut* **null** ise ve komut yorumlayıcı bulunursa, sıfır dışında bir değer döndürür. Komut yorumlayıcı bulunamazsa, 0 döndürür ve **errno** değerini **ENOENT**olarak ayarlar. *Komut* **null**değilse, **sistem** komut yorumlayıcı tarafından döndürülen değeri döndürür. Yalnızca komut yorumlayıcı 0 değerini döndürürse 0 değerini döndürür. -1 ' in dönüş değeri bir hatayı gösterir ve **errno** aşağıdaki değerlerden birine ayarlanır:

|||
|-|-|
| **E2BIG** | Bağımsız değişken listesi (sisteme bağımlı) çok büyük. |
| **ENOENT** | Komut yorumlayıcı bulunamıyor. |
| **ENOEXEC** | Biçim geçerli olmadığından, komut yorumlayıcı dosyası yürütülemiyor. |
| **ENOMEM** | Komutu yürütmek için yeterli bellek yok; veya kullanılabilir bellek bozulmuş; ya da çağrıyı yapan işlemin doğru şekilde ayrılmadığını gösteren geçerli olmayan bir blok vardır. |

Bu dönüş kodları hakkında daha fazla bilgi için bkz. [_doserrno, errno, _sys_errlist ve _sys_nerr](../../c-runtime-library/errno-doserrno-sys-errlist-and-sys-nerr.md) .

## <a name="remarks"></a>Açıklamalar

**Sistem** işlevi, dizeyi bir işletim sistemi komutu olarak *yürüten komut yorumlayıcıya geçirir.* **sistem** , cmd. exe komut yorumlayıcı dosyasını bulmak Için **ComSpec** ve **Path** ortam değişkenlerini kullanır. *Komut* **null**ise, işlev yalnızca komut yorumlayıcısının var olup olmadığını denetler.

**System**çağrısından önce [fflush](fflush.md) veya [_flushall](flushall.md)kullanarak veya herhangi bir akışı kapatarak açıkça temizlenmesi gerekir.

**_wsystem** , **sistemin**geniş karakterli bir sürümüdür; _wsystem *komut* bağımsız değişkeni **_wsystem** geniş karakterli bir dizedir. Bu işlevler, aynı şekilde davranır.

Varsayılan olarak, bu işlevin genel durumu uygulamanın kapsamına alınır. Bunu değiştirmek için bkz. [CRT Içindeki genel durum](../global-state.md).

### <a name="generic-text-routine-mappings"></a>Genel Metin Yordam Eşleşmeleri

|TCHAR.H yordamı|_UNICODE & _MBCS tanımlanmadı|_MBCS tanımlanmış|_UNICODE tanımlanmış|
|---------------------|------------------------------------|--------------------|-----------------------|
|**_tsystem**|**sistem**|**sistem**|**_wsystem**|

## <a name="requirements"></a>Gereksinimler

|Yordam|Gerekli başlık|
|-------------|---------------------|
|**sistem**|\<Process. h> veya \<Stdlib. h>|
|**_wsystem**|\<Process. h> veya \<Stdlib. h> ya \<da wchar. h>|

Ek uyumluluk bilgileri için bkz. [Uyumluluk](../../c-runtime-library/compatibility.md).

## <a name="example"></a>Örnek

Bu örnek, bir metin dosyası yazmak için **sistemini** kullanır.

```C
// crt_system.c

#include <process.h>

int main( void )
{
   system( "type crt_system.txt" );
}
```

### <a name="input-crt_systemtxt"></a>Giriş: crt_system. txt

```Input
Line one.
Line two.
```

### <a name="output"></a>Çıktı

```Output
Line one.
Line two.
```

## <a name="see-also"></a>Ayrıca bkz.

[Süreç ve Ortam Denetimi](../../c-runtime-library/process-and-environment-control.md)<br/>
[_exec, _wexec Işlevleri](../../c-runtime-library/exec-wexec-functions.md)<br/>
[exit, _Exit, _exit](exit-exit-exit.md)<br/>
[_flushall](flushall.md)<br/>
[_spawn, _wspawn İşlevleri](../../c-runtime-library/spawn-wspawn-functions.md)<br/>
