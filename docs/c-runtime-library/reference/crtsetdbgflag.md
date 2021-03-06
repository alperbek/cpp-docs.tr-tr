---
title: _CrtSetDbgFlag
ms.date: 11/04/2016
api_name:
- _CrtSetDbgFlag
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
api_type:
- DLLExport
topic_type:
- apiref
f1_keywords:
- _CRTDBG_REPORT_FLAG
- _CRTDBG_CHECK_EVERY_16_DF
- _CRTDBG_CHECK_DEFAULT_DF
- CRTDBG_CHECK_DEFAULT_DF
- CRTDBG_CHECK_EVERY_128_DF
- CRTDBG_CHECK_EVERY_1024_DF
- _CRTDBG_CHECK_EVERY_128_DF
- CrtSetDbgFlag
- CRTDBG_CHECK_EVERY_16_DF
- _CRTDBG_CHECK_EVERY_1024_DF
- _CrtSetDbgFlag
- CRTDBG_REPORT_FLAG
helpviewer_keywords:
- _CRTDBG_CHECK_EVERY_16_DF macro
- CRTDBG_CHECK_EVERY_16_DF macro
- _CRTDBG_CHECK_ALWAYS_DF macro
- _CRTDBG_CHECK_DEFAULT_DF macro
- CRTDBG_ALLOC_MEM_DF macro
- CRTDBG_CHECK_ALWAYS_DF macro
- _CRTDBG_ALLOC_MEM_DF macro
- _CRTDBG_REPORT_FLAG macro
- _CRTDBG_CHECK_EVERY_128_DF macro
- CRTDBG_REPORT_FLAG macro
- _CRTDBG_CHECK_EVERY_1024_DF macro
- CRTDBG_CHECK_DEFAULT_DF macro
- CRTDBG_CHECK_EVERY_1024_DF macro
- _CrtSetDbgFlag function
- CrtSetDbgFlag function
- _CRTDBG_DELAY_FREE_MEM_DF macro
- CRTDBG_CHECK_EVERY_128_DF macro
- CRTDBG_DELAY_FREE_MEM_DF macro
- CRTDBG_CHECK_CRT_DF macro
- _CRTDBG_CHECK_CRT_DF macro
ms.assetid: b5657ffb-6178-4cbf-9886-1af904ede94c
ms.openlocfilehash: 8506b593a579c8dd1791e56c320bd9d8e2ee9ba2
ms.sourcegitcommit: f19474151276d47da77cdfd20df53128fdcc3ea7
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/12/2019
ms.locfileid: "70938623"
---
# <a name="_crtsetdbgflag"></a>_CrtSetDbgFlag

Hata ayıklama yığını yöneticisinin (yalnızca hata ayıklama sürümü) ayırma davranışını denetlemek için **_Crtdbgflag** bayrağının durumunu alır veya değiştirir.

## <a name="syntax"></a>Sözdizimi

```C
int _CrtSetDbgFlag(
   int newFlag
);
```

### <a name="parameters"></a>Parametreler

*newFlag*<br/>
**_Crtdbgflag**için yeni durum.

## <a name="return-value"></a>Dönüş Değeri

**_Crtdbgflag**öğesinin önceki durumunu döndürür.

## <a name="remarks"></a>Açıklamalar

**_Crtsetdbgflag** işlevi, uygulamanın hata ayıklama yığın yöneticisinin **_Crtdbgflag** bayrağının bit alanlarını değiştirerek bellek ayırmalarını nasıl izlediğini denetlemesine olanak tanır. Bitleri (etkinleştirerek) ayarlayarak, uygulama hata ayıklama yığın yöneticisinden özel hata ayıklama işlemleri gerçekleştirmesini, uygulamanın ne zaman çıkıp raporlamadığında bellek sızıntılarını denetleme, düşük bellek koşullarını serbest bırakılan bellek bloklarının, yığının bağlantılı listesinde kalması ve her ayırma isteğindeki her bir bellek bloğunu inceleyerek yığının bütünlüğünü doğrulaması gerekir. [_Hata ayıklama](../../c-runtime-library/debug.md) tanımlanmadığında, **_Crtsetdbgflag** çağrısı, ön işleme sırasında kaldırılır.

Aşağıdaki tabloda **_Crtdbgflag** için bit alanları listelenmiş ve davranışlarını açıklanmaktadır. BITS ayarı daha fazla tanılama çıktısı ve azaltılmış program yürütme hızı ile sonuçlandığından, bu bitler varsayılan olarak ayarlı değildir (kapalı değildir). Bu bit alanları hakkında daha fazla bilgi için bkz. [yığın durum raporlama işlevleri](/visualstudio/debugger/crt-debug-heap-details).

|Bit alanı|Varsayılan|Açıklama|
|---------------|-------------|-----------------|
|**_CRTDBG_ALLOC_MEM_DF**|DAYANIR|DAYANIR Hata ayıklama yığın ayırmalarını ve **_Client_block**gibi bellek blok türü tanımlayıcılarının kullanımını etkinleştirin. DIŞINA Yığının bağlantılı listesine yeni ayırmalar ekleyin, ancak blok türünü **_IGNORE_BLOCK**olarak ayarlayın.<br /><br /> Yığın frekansı denetim makrolarıyla de birleştirilebilir.|
|**_CRTDBG_CHECK_ALWAYS_DF**|KAPALI|DAYANIR Her ayırma ve ayırmayı kaldırma isteğinde [_Crtcheckmemory](crtcheckmemory.md) çağrısı yapın. Kapalı: **_Crtcheckmemory** açıkça çağrılmalıdır.<br /><br /> Yığın frekansı denetim makroları bu bayrak ayarlandığında hiçbir etkiye sahip değildir.|
|**_CRTDBG_CHECK_CRT_DF**|KAPALI|DAYANIR **_CRT_BLOCK** türlerini sızıntı algılama ve bellek durumu fark işlemlerine dahil edin. DIŞINA Çalışma zamanı kitaplığı tarafından dahili olarak kullanılan bellek bu işlemler tarafından yok sayılır.<br /><br /> Yığın frekansı denetim makrolarıyla de birleştirilebilir.|
|**_CRTDBG_DELAY_FREE_MEM_DF**|KAPALI|DAYANIR Serbest bırakılan bellek bloklarını yığının bağlantılı listesinde tutun, **_Free_block** türünü atayın ve bunları 0xDD bayt değeri ile doldurur. DIŞINA Serbest bırakılan blokları yığının bağlantılı listesinde tutmayın.<br /><br /> Yığın frekansı denetim makrolarıyla de birleştirilebilir.|
|**_CRTDBG_TAAK_CHECK_DF**|KAPALI|DAYANIR Bir [_Crtdumpmemorysızıntıları](crtdumpmemoryleaks.md) çağrısıyla otomatik sızıntı denetimi gerçekleştirin ve uygulamanın ayrılan tüm belleği serbest bir şekilde gerçekleştiremeyeceği bir hata raporu oluşturun. DIŞINA Program çıkışında sızıntı denetimini otomatik olarak gerçekleştirmeyin.<br /><br /> Yığın frekansı denetim makrolarıyla de birleştirilebilir.|

**Yığın denetimi sıklık makroları**

C çalışma zamanı kitaplığı 'nın, **malloc**, **realloc**, **Free**ve **_msize**çağrısı sayısına göre hata ayıklama yığınının ( **_CrtCheckMemory**) doğrulanmasını ne sıklıkta gerçekleştireceğini belirtebilirsiniz.

**_Crtsetdbgflag** daha sonra bir değer Için *newFlag* parametresinin üstteki 16 bitini inceler. Belirtilen değer, **_Crtcheckmemory** çağrıları arasındaki **malloc**, **realloc**, **ücretsiz**ve **_msize** çağrılarının sayısıdır. Bu amaçla önceden tanımlanmış dört makro sağlanır.

|Makrosu|_CrtCheckMemory çağrıları arasındaki malloc, realloc, ücretsiz ve _msize çağrılarının sayısı|
|-----------|------------------------------------------------------------------------------------------|
|_CRTDBG_CHECK_EVERY_16_DF|16|
|_CRTDBG_CHECK_EVERY_128_DF|128|
|_CRTDBG_CHECK_EVERY_1024_DF|1024|
|_CRTDBG_CHECK_DEFAULT_DF|0 (varsayılan olarak, yığın denetimi yok)|

Varsayılan olarak, **_Crtcheckmemory** , her 1.024 kez **malloc**, **realloc**, **Free**ve **_msize**çağrısı yaptığınızda çağrılır.

Örneğin, aşağıdaki kod ile her 16 **malloc**, **realloc**, **ücretsiz**ve **_msize** işlemlerinde bir yığın denetimi belirtebilirsiniz:

```C
#include <crtdbg.h>
int main( )
{
    int tmp;

    // Get the current bits
    tmp = _CrtSetDbgFlag(_CRTDBG_REPORT_FLAG);

    // Clear the upper 16 bits and OR in the desired frequency
    tmp = (tmp & 0x0000FFFF) | _CRTDBG_CHECK_EVERY_16_DF;

    // Set the new bits
    _CrtSetDbgFlag(tmp);
}
```

_CRTDBG_CHECK_ALWAYS_DF belirtildiğinde *newFlag* parametresinin üst 16 biti yok sayılır. Bu durumda, **malloc**, **realloc**, **Free**ve **_Msize**her çağırdığınızda **_CrtCheckMemory** çağrılır.

*newFlag* , **_Crtdbgflag** öğesine uygulanacak yeni durumdur ve her bir bit alanı için değerlerin bir birleşimidir.

### <a name="to-change-one-or-more-of-these-bit-fields-and-create-a-new-state-for-the-flag"></a>Bu bit alanlarından bir veya daha fazlasını değiştirmek ve bayrak için yeni bir durum oluşturmak için

1. Geçerli **_crtDbgFlag** durumunu elde etmek ve döndürülen değeri geçici bir değişkende depolamak Için *newFlag* WITH **_Crtdbg_report_flag** Ile **_CrtSetDbgFlag** çağrısı yapın.

1. Karşılık gelen bit maskeleri olan (uygulama kodunda bildirim sabitlerine göre gösterilen) bir bit düzeyinde **veya** geçici değişkenin herhangi bir bitini açın.

1. Değişkeni uygun bit maskelerinden bit düzeyinde **olmayan** bir bit düzeyinde **ve**yaparak diğer bitleri kapatın.

1. **_Crtdbgflag**için yeni durum ayarlamak üzere geçici değişkende depolanan değere eşit olan *newFlag* Ile **_CrtSetDbgFlag** öğesini çağırın.

Aşağıdaki kod, serbest bırakılan bellek bloklarını yığının bağlantılı listesinde tutarak ve **_Crtcheckmemory** ' ın her ayırma isteğinde çağrılmasına engel olarak düşük bellekli koşulların benzetimini nasıl benzediğini göstermektedir:

```C
// Get the current state of the flag
// and store it in a temporary variable
int tmpFlag = _CrtSetDbgFlag( _CRTDBG_REPORT_FLAG );

// Turn On (OR) - Keep freed memory blocks in the
// heap's linked list and mark them as freed
tmpFlag |= _CRTDBG_DELAY_FREE_MEM_DF;

// Turn Off (AND) - prevent _CrtCheckMemory from
// being called at every allocation request
tmpFlag &= ~_CRTDBG_CHECK_ALWAYS_DF;

// Set the new state for the flag
_CrtSetDbgFlag( tmpFlag );
```

Bellek yönetimine ve hata ayıklama yığınına genel bakış için bkz. [CRT hata ayıklama yığını ayrıntıları](/visualstudio/debugger/crt-debug-heap-details).

**_Crtsetdbgflag** işleviyle bir bayrağı devre dışı bırakmak Için, **ve** bit seviyesinde bit düzeyinde **olmayan** bir değişken gerekir.

*NewFlag* geçerli bir değer değilse, bu Işlev [parametre doğrulama](../../c-runtime-library/parameter-validation.md)bölümünde açıklandığı gibi geçersiz parametre işleyicisini çağırır. Yürütmenin devam etmesine izin veriliyorsa, bu işlev **errno** ' ı **EINVAL** olarak ayarlar ve **_crtDbgFlag**öğesinin önceki durumunu döndürür.

## <a name="requirements"></a>Gereksinimler

|Yordam|Gerekli başlık|
|-------------|---------------------|
|**_CrtSetDbgFlag**|\<Crtdbg. h >|

Daha fazla uyumluluk bilgisi için bkz. [Uyumluluk](../../c-runtime-library/compatibility.md).

## <a name="libraries"></a>Kitaplıklar

Yalnızca [C çalışma zamanı kitaplıklarının](../../c-runtime-library/crt-library-features.md) sürümlerini ayıklayın.

## <a name="example"></a>Örnek

```C
// crt_crtsetdflag.c
// compile with: /c -D_DEBUG /MTd -Od -Zi -W3 /link -verbose:lib /debug

// This program concentrates on allocating and freeing memory
// blocks to test the functionality of the _crtDbgFlag flag.

#include <string.h>
#include <malloc.h>
#include <crtdbg.h>

int main( )
{
    char *p1, *p2;
    int tmpDbgFlag;

    _CrtSetReportMode( _CRT_ERROR, _CRTDBG_MODE_FILE );
    _CrtSetReportFile( _CRT_ERROR, _CRTDBG_FILE_STDERR );

    // Set the debug-heap flag to keep freed blocks in the
    // heap's linked list - This will allow us to catch any
    // inadvertent use of freed memory
    tmpDbgFlag = _CrtSetDbgFlag(_CRTDBG_REPORT_FLAG);
    tmpDbgFlag |= _CRTDBG_DELAY_FREE_MEM_DF;
    tmpDbgFlag |= _CRTDBG_LEAK_CHECK_DF;
    _CrtSetDbgFlag(tmpDbgFlag);

    // Allocate 2 memory blocks and store a string in each
    p1 = malloc( 34 );
    p2 = malloc( 38 );
    strcpy_s( p1, 34, "p1 points to a Normal allocation block" );
    strcpy_s( p2, 38, "p2 points to a Client allocation block" );

    // Free both memory blocks
    free( p2 );
    free( p1 );

    // Set the debug-heap flag to no longer keep freed blocks in the
    // heap's linked list and turn on Debug type allocations (CLIENT)
    tmpDbgFlag = _CrtSetDbgFlag(_CRTDBG_REPORT_FLAG);
    tmpDbgFlag |= _CRTDBG_ALLOC_MEM_DF;
    tmpDbgFlag &= ~_CRTDBG_DELAY_FREE_MEM_DF;
    _CrtSetDbgFlag(tmpDbgFlag);

    // Explicitly call _malloc_dbg to obtain the filename and
    // line number of our allocation request and also so we can
    // allocate CLIENT type blocks specifically for tracking
    p1 = _malloc_dbg( 40, _NORMAL_BLOCK, __FILE__, __LINE__ );
    p2 = _malloc_dbg( 40, _CLIENT_BLOCK, __FILE__, __LINE__ );
    strcpy_s( p1, 40, "p1 points to a Normal allocation block" );
    strcpy_s( p2, 40, "p2 points to a Client allocation block" );

    // _free_dbg must be called to free the CLIENT block
    _free_dbg( p2, _CLIENT_BLOCK );
    free( p1 );

    // Allocate p1 again and then exit - this will leave unfreed
    // memory on the heap
    p1 = malloc( 10 );
}
```

## <a name="see-also"></a>Ayrıca bkz.

[Hata Ayıklama Yordamları](../../c-runtime-library/debug-routines.md)<br/>
[_crtDbgFlag](../../c-runtime-library/crtdbgflag.md)<br/>
[_CrtCheckMemory](crtcheckmemory.md)<br/>
