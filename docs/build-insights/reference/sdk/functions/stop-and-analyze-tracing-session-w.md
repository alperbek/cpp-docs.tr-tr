---
title: Stopandçözümleyiciler Etracingsessionw
description: C++ BUILD Insights SDK Stopandçözümleyicileri Etracingsessionw işlev başvurusu.
ms.date: 02/12/2020
helpviewer_keywords:
- C++ Build Insights
- C++ Build Insights SDK
- StopAndAnalyzeTracingSessionW
- throughput analysis
- build time analysis
- vcperf.exe
ms.openlocfilehash: ec36162efcd2bfcf17cb07a997a7ff170338d3d2
ms.sourcegitcommit: 3e8fa01f323bc5043a48a0c18b855d38af3648d4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/05/2020
ms.locfileid: "78332672"
---
# <a name="stopandanalyzetracingsessionw"></a>Stopandçözümleyiciler Etracingsessionw

::: moniker range="<=vs-2015"

Build C++ Insights SDK 'Sı, Visual Studio 2017 ve üzeri ile uyumludur. Bu sürümlerin belgelerini görmek için, bu makalenin Visual Studio sürüm Seçicisi denetimini Visual Studio 2017 veya Visual Studio 2019 olarak ayarlayın.

::: moniker-end
::: moniker range=">=vs-2017"

`StopAndAnalyzeTracingSessionW` işlevi devam eden bir izleme oturumunu durduruyor ve elde edilen izlemeyi geçici bir dosyaya kaydeder. Daha sonra bir analiz oturumu, giriş olarak geçici dosyayı kullanmaya hemen başlatılır. Bu işlevi çağıran yürütülebilir dosyalar yönetici ayrıcalıklarına sahip olmalıdır.

## <a name="syntax"></a>Sözdizimi

```cpp
enum RESULT_CODE StopAndAnalyzeTracingSessionW(
    const wchar_t*              sessionName,
    TRACING_SESSION_STATISTICS* statistics,
    const ANALYSIS_DESCRIPTOR*  analysisDescriptor);
```

### <a name="parameters"></a>Parametreler

*oturumadı*\
Durdurulacak izleme oturumunun adı. [Starttracingsession](start-tracing-session.md), [starttracingsessiona](start-tracing-session-a.md)veya [starttracingsessionw](start-tracing-session-w.md)öğesine geçirilen oturum adını kullanın.

*istatistikler*\
[TRACING_SESSION_STATISTICS](../other-types/tracing-session-statistics-struct.md) nesnesine yönelik işaretçi. `StopAndAnalyzeTracingSessionW`, döndürmeden önce bu nesnedeki izleme toplama istatistiklerini yazar.

*Analysisdescriptor*\
[ANALYSIS_DESCRIPTOR](../other-types/analysis-descriptor-struct.md) nesnesine yönelik işaretçi. `StopAndAnalyzeTracingSessionW`tarafından başlatılan analiz oturumunu yapılandırmak için bu nesneyi kullanın.

### <a name="return-value"></a>Dönüş Değeri

[RESULT_CODE](../other-types/result-code-enum.md) numaralandırmasından elde edilen sonuç kodu.

::: moniker-end