---
title: atexit
ms.date: 11/04/2016
api_name:
- atexit
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
- atexit
helpviewer_keywords:
- processing, at exit
- atexit function
ms.assetid: 92c156d2-8052-4e58-96dc-00128baac6f9
ms.openlocfilehash: b91e6dad81f006b0b94ac17a940e840386f6d2b1
ms.sourcegitcommit: f19474151276d47da77cdfd20df53128fdcc3ea7
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/12/2019
ms.locfileid: "70939653"
---
# <a name="atexit"></a>atexit

Çıkışta belirtilen işlevi işler.

## <a name="syntax"></a>Sözdizimi

```C
int atexit(
   void (__cdecl *func )( void )
);
```

### <a name="parameters"></a>Parametreler

*func*<br/>
Çağrılacak işlev.

## <a name="return-value"></a>Dönüş Değeri

**atexit** , başarılıysa 0 veya bir hata oluşursa sıfır dışında bir değer döndürür.

## <a name="remarks"></a>Açıklamalar

**Atexit** işlevi, program normal olarak sonlandırıldığında *çağrılan işlevin adresini* geçti. **Atexit** 'e yönelik art arda yapılan çağrılar, en son, ilk çıkar (LIFO) sırada yürütülen işlevlerin bir kaydını oluşturur. **Atexit** 'e geçirilen işlevler parametre alamaz. **atexit** ve **_onexit** işlev kaydını tutmak için yığını kullanır. Bu nedenle, kayıt olabilecek işlevlerin sayısı yalnızca yığın bellekle sınırlıdır.

**Atexit** işlevindeki kod, **atexit** işlevi çağrıldığında önceden KALDıRıLMıŞ olan herhangi bir dll üzerinde herhangi bir bağımlılık içermemelidir.

ANSI uyumlu bir uygulama oluşturmak için ANSI-standart **atexit** işlevini kullanın (benzer **_onexit** işlevi yerine).

## <a name="requirements"></a>Gereksinimler

|Yordam|Gerekli başlık|
|-------------|---------------------|
|**atexit**|\<Stdlib. h >|

## <a name="example"></a>Örnek

Bu program, bir **atexit** çağrıldığında yürütülecek işlev yığınına dört işlev iter. Program çıktığında, bu programlar en son bir ilk çıkar temelinde yürütülür.

```C
// crt_atexit.c
#include <stdlib.h>
#include <stdio.h>

void fn1( void ), fn2( void ), fn3( void ), fn4( void );

int main( void )
{
   atexit( fn1 );
   atexit( fn2 );
   atexit( fn3 );
   atexit( fn4 );
   printf( "This is executed first.\n" );
}

void fn1()
{
   printf( "next.\n" );
}

void fn2()
{
   printf( "executed " );
}

void fn3()
{
   printf( "is " );
}

void fn4()
{
   printf( "This " );
}
```

```Output
This is executed first.
This is executed next.
```

## <a name="see-also"></a>Ayrıca bkz.

[Süreç ve Ortam Denetimi](../../c-runtime-library/process-and-environment-control.md)<br/>
[abort](abort.md)<br/>
[exit, _Exit, _exit](exit-exit-exit.md)<br/>
[_onexit, _onexit_m](onexit-onexit-m.md)<br/>
