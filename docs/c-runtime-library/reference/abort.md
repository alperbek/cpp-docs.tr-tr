---
title: durdur
ms.date: 4/2/2020
api_name:
- abort
- _o_abort
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
- Abort
helpviewer_keywords:
- aborting current process
- abort function
- processes, aborting
ms.openlocfilehash: f330d53df5af0efa41f4e3b3bb843bdc95210c70
ms.sourcegitcommit: 5a069c7360f75b7c1cf9d4550446ec2fa2eb2293
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/07/2020
ms.locfileid: "82910913"
---
# <a name="abort"></a>durdur

Geçerli işlemi iptal eder ve bir hata kodu döndürür.

> [!NOTE]
> Test veya hata ayıklama senaryoları dışında Microsoft Store bir uygulama veya Evrensel Windows Platformu (UWP) uygulamasını kapatmak için bu yöntemi kullanmayın. Bir mağaza uygulamasını kapatmak için programlı veya Kullanıcı arabirimi yollarına [Microsoft Store ilkelerine](/legal/windows/agreements/store-policies)göre izin verilmez. Daha fazla bilgi için bkz. [UWP uygulama yaşam döngüsü](/windows/uwp/launch-resume/app-lifecycle).

## <a name="syntax"></a>Sözdizimi

```C
void abort( void );
```

## <a name="return-value"></a>Dönüş Değeri

**Abort** , çağırma işlemine denetim döndürmüyor. Varsayılan olarak, bir durdurma sinyali işleyicisini denetler ve bir ayarlanırsa, `SIGABRT` yükseltir. Ardından **iptal** , geçerli işlemi sonlandırır ve üst işleme bir çıkış kodu döndürür.

## <a name="remarks"></a>Açıklamalar

**Microsoft'a Özgü**

Varsayılan olarak, bir uygulama hata ayıklama çalışma zamanı kitaplığıyla oluşturulduğunda, **durdurma** yordamı oluşturulmadan önce `SIGABRT` bir hata mesajı görüntüler. Konsol modunda çalışan konsol uygulamaları için ileti gönderilir `STDERR`. Pencereli modda çalışan Windows Masaüstü uygulamaları ve konsol uygulamaları iletiyi bir ileti kutusunda görüntüler. İletiyi bastırmak için, `_WRITE_ABORT_MSG` bayrağı temizlemek için [_set_abort_behavior](set-abort-behavior.md) kullanın. Görünen ileti, kullanılan çalışma zamanı ortamının sürümüne bağlıdır. Visual C++ en son sürümleri kullanılarak oluşturulan uygulamalar için, ileti şuna benzer:

> R6010-Abort () çağrıldı

C çalışma zamanı kitaplığı 'nın önceki sürümlerinde bu ileti görüntülendi:

> Bu uygulama, çalışma zamanının olağan dışı bir şekilde sonlanmasına istedi. Daha fazla bilgi için lütfen uygulamanın destek ekibine başvurun.

Program hata ayıklama modunda derlendiğinde, ileti kutusu **iptal**etme, **yeniden deneme**veya **yoksayma**seçeneklerini görüntüler. Kullanıcı **iptal**' i seçerse program hemen sonlanır ve 3 çıkış kodu döndürür. Kullanıcı **yeniden dene**' yi seçerse, varsa, tam zamanında hata ayıklama için bir hata ayıklayıcı çağırılır. Kullanıcı **Yoksay**' ı seçerse, **Durdur** normal işlemeye devam eder.

Hem perakende hem de hata ayıklama yapılarında, **iptal** etme sinyali işleyicisinin ayarlanmış olup olmadığını denetler. Varsayılan olmayan bir sinyal işleyicisi ayarlandıysa, çağrıları `raise(SIGABRT)` **iptal** edin. Bir durdurma [signal](signal.md) sinyali işleyicisi işlevini `SIGABRT` sinyalle ilişkilendirmek için sinyal işlevini kullanın. Özel eylemleri gerçekleştirebilir — Örneğin, kaynakları veya günlük bilgilerini temizleyebilir — ve uygulamayı işleyici işlevindeki kendi hata kodunuzla sonlandırabilirsiniz. Özel bir sinyal işleyicisi tanımlanmamışsa, **Abort** , `SIGABRT` sinyali oluşturmaz.

Varsayılan olarak, masaüstü veya konsol uygulamalarının hata ayıklama olmayan Derlemeleriyle, **Durdur** ' u daha sonra hataları Microsoft 'a bildirmek Için Windows hata bildirimi hizmet mekanizmasını (eskiden Dr. Watson olarak biliniyordu) çağırır. Bu davranış, `_set_abort_behavior` `_CALL_REPORTFAULT` bayrağı çağırarak veya maskeleyerek etkinleştirilebilir veya devre dışı bırakılabilir. Bayrak ayarlandığında, Windows "bir sorun" programın düzgün çalışmayı durdurmasına neden oldu "gibi metin içeren bir ileti kutusu görüntüler. Kullanıcı hata **ayıklama** düğmesi ile bir hata ayıklayıcı çağırmayı seçebilir veya uygulamayı işletim sistemi tarafından tanımlanan bir hata koduyla sonlandırmak Için **programı kapat** düğmesini seçebilirsiniz.

Windows hata bildirimi işleyicisi çağrılmadığından, çıkış kodu 3 ile işlemi sonlandırmak için [_exit](exit-exit-exit.md) çağrıları **iptal** edin ve denetimi üst işleme veya işletim sistemine döndürür. `_exit`akış arabelleklerini temizlemez veya `atexit` / `_onexit` işleme yapmaz.

CRT hata ayıklama hakkında daha fazla bilgi için bkz. [CRT hata ayıklama teknikleri](/visualstudio/debugger/crt-debugging-techniques).

**Son Microsoft 'a özgü**

Varsayılan olarak, bu işlevin genel durumu uygulamanın kapsamına alınır. Bunu değiştirmek için bkz. [CRT Içindeki genel durum](../global-state.md).

## <a name="requirements"></a>Gereksinimler

|Yordam|Gerekli başlık|
|-------------|---------------------|
|**durdurulmaya**|\<Process. h> veya \<Stdlib. h>|

## <a name="example"></a>Örnek

Aşağıdaki program bir dosyayı açmaya çalışır ve deneme başarısız olursa iptal eder.

```C
// crt_abort.c
// compile with: /TC
// This program demonstrates the use of
// the abort function by attempting to open a file
// and aborts if the attempt fails.

#include  <stdio.h>
#include  <stdlib.h>

int main( void )
{
    FILE    *stream = NULL;
    errno_t err = 0;

    err = fopen_s(&stream, "NOSUCHF.ILE", "r" );
    if ((err != 0) || (stream == NULL))
    {
        perror( "File could not be opened" );
        abort();
    }
    else
    {
        fclose( stream );
    }
}
```

```Output
File could not be opened: No such file or directory
```

## <a name="see-also"></a>Ayrıca bkz.

[abort Kullanma](../../cpp/using-abort.md)<br/>
[abort İşlevi](../../c-language/abort-function-c.md)<br/>
[Süreç ve Ortam Denetimi](../../c-runtime-library/process-and-environment-control.md)<br/>
[_exec, _wexec Işlevleri](../../c-runtime-library/exec-wexec-functions.md)<br/>
[exit, _Exit, _exit](exit-exit-exit.md)<br/>
[yükseltmek](raise.md)<br/>
[sinyal](signal.md)<br/>
[_spawn, _wspawn İşlevleri](../../c-runtime-library/spawn-wspawn-functions.md)<br/>
[_DEBUG](../../c-runtime-library/debug.md)<br/>
[_set_abort_behavior](set-abort-behavior.md)
