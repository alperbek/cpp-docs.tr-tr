---
title: _spawnvpe, _wspawnvpe
ms.date: 4/2/2020
api_name:
- _spawnvpe
- _wspawnvpe
- _o__spawnvpe
- _o__wspawnvpe
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
- api-ms-win-crt-process-l1-1-0.dll
- api-ms-win-crt-private-l1-1-0.dll
api_type:
- DLLExport
topic_type:
- apiref
f1_keywords:
- _spawnvpe
- wspawnvpe
- _wspawnvpe
helpviewer_keywords:
- _wspawnvpe function
- processes, creating
- _spawnvpe function
- processes, executing new
- wspawnvpe function
- process creation
- spawnvpe function
ms.assetid: 3db6394e-a955-4837-97a1-fab1db1e6092
ms.openlocfilehash: 8f974dcfe59551c2fd0fddd7d9c66fb3d46d9b7f
ms.sourcegitcommit: 5a069c7360f75b7c1cf9d4550446ec2fa2eb2293
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/07/2020
ms.locfileid: "82919706"
---
# <a name="_spawnvpe-_wspawnvpe"></a>_spawnvpe, _wspawnvpe

Yeni bir işlem oluşturur ve yürütür.

> [!IMPORTANT]
> Bu API, Windows Çalışma Zamanı yürütülen uygulamalarda kullanılamaz. Daha fazla bilgi için bkz. [Evrensel Windows platformu uygulamalarında CRT işlevleri desteklenmez](../../cppcx/crt-functions-not-supported-in-universal-windows-platform-apps.md).

## <a name="syntax"></a>Sözdizimi

```C
intptr_t _spawnvpe(
   int mode,
   const char *cmdname,
   const char *const *argv,
   const char *const *envp
);
intptr_t _wspawnvpe(
   int mode,
   const wchar_t *cmdname,
   const wchar_t *const *argv,
   const wchar_t *const *envp
);
```

### <a name="parameters"></a>Parametreler

*modundaysa*<br/>
Çağırma işlemi için yürütme modu

*cmdname*<br/>
Yürütülecek dosyanın yolu

*argv*<br/>
Bağımsız değişkenlere işaretçiler dizisi. *Argv*[0] bağımsız değişkeni, genellikle gerçek moddaki bir yolun veya korunan moddaki program adının bir işaretçisidir *ve argv*[**n**] arasındaki *argv*[1], yeni bağımsız değişken listesini oluşturan karakter dizelerinin işaretçileridir. *Argv*[**n** + 1] bağımsız değişkeni, bağımsız değişken listesinin sonunu işaretlemek için bir **null** işaretçi olmalıdır.

*envp*<br/>
Ortam ayarlarına işaretçiler dizisi

## <a name="return-value"></a>Dönüş Değeri

Zaman uyumlu bir **_spawnvpe** veya **_wspawnvpe** ( *mod*için belirtilen **_P_WAIT** ) dönüş değeri, yeni işlemin çıkış durumudur. Zaman uyumsuz bir **_spawnvpe** veya **_wspawnvpe** (**_P_NOWAIT** veya *mod*için belirtilen **_P_NOWAITO** ) dönüş değeri işlem tanıtıcıdır. İşlem normal şekilde sonlandırılırsa çıkış durumu 0 ' dır. Oluşturulan işlem özellikle **Çıkış** yordamını sıfır dışında bir bağımsız değişkenle çağırırsa çıkış durumunu sıfır dışında bir değere ayarlayabilirsiniz. Yeni işlem açıkça pozitif bir çıkış durumu ayarlanmamışsa, bir pozitif çıkış durumu, bir iptal veya kesme ile olağan dışı bir çıkış olduğunu gösterir. -1 ' in dönüş değeri bir hatayı gösterir (yeni işlem başlatılmaz). Bu durumda, **errno** aşağıdaki değerlerden birine ayarlanır:

|||
|-|-|
| **E2BIG** | Bağımsız değişken listesi 1024 baytı aşıyor. |
| **EıNVAL** | *Mode* bağımsız değişkeni geçersiz. |
| **ENOENT** | Dosya veya yol bulunamadı. |
| **ENOEXEC** | Belirtilen dosya yürütülebilir değil veya geçersiz yürütülebilir dosya biçimine sahip. |
| **ENOMEM** | Yeni işlemi yürütmek için yeterli kullanılabilir bellek yok. |

Bu ve diğer dönüş kodları hakkında daha fazla bilgi için bkz. [_doserrno, errno, _sys_errlist ve _sys_nerr](../../c-runtime-library/errno-doserrno-sys-errlist-and-sys-nerr.md) .

## <a name="remarks"></a>Açıklamalar

Bu işlevlerin her biri, komut satırı bağımsız değişkenlerine bir işaretçiler dizisi ve ortam ayarlarına bir işaretçiler dizisi geçirerek yeni bir işlem oluşturur ve yürütür. Bu işlevler, yürütülecek dosyayı bulmak için **Path** ortam değişkenini kullanır.

Bu işlevler, parametrelerini doğrular. *Cmdname* veya *argv* bir null işaretçisiyse ya da *argv* null işaretçisine işaret ediyorsa ya da *argv*[0] boş bir dize ise, [parametre doğrulama](../../c-runtime-library/parameter-validation.md) bölümünde açıklandığı gibi geçersiz parametre işleyicisi çağrılır. Yürütmenin devam etmesine izin veriliyorsa, bu işlevler **errno** ' ı **EINVAL**olarak ayarlar ve-1 döndürür. Yeni işlem oluşturulmadı.

Varsayılan olarak, bu işlevin genel durumu uygulamanın kapsamına alınır. Bunu değiştirmek için bkz. [CRT Içindeki genel durum](../global-state.md).

## <a name="requirements"></a>Gereksinimler

|Yordam|Gerekli başlık|
|-------------|---------------------|
|**_spawnvpe**|\<stdio. h> veya \<Process. h>|
|**_wspawnvpe**|\<stdio. h> veya \<wchar. h>|

Ek uyumluluk bilgileri için bkz. [Uyumluluk](../../c-runtime-library/compatibility.md).

## <a name="example"></a>Örnek

[_Spawn, _Wspawn işlevlerde](../../c-runtime-library/spawn-wspawn-functions.md)örneğe bakın.

## <a name="see-also"></a>Ayrıca bkz.

[durdurulmaya](abort.md)<br/>
[atexit](atexit.md)<br/>
[_exec, _wexec Işlevleri](../../c-runtime-library/exec-wexec-functions.md)<br/>
[exit, _Exit, _exit](exit-exit-exit.md)<br/>
[_flushall](flushall.md)<br/>
[_getmbcp](getmbcp.md)<br/>
[_onexit, _onexit_m](onexit-onexit-m.md)<br/>
[_setmbcp](setmbcp.md)<br/>
[system, _wsystem](system-wsystem.md)<br/>
