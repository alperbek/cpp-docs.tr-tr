---
title: Bağlayıcı Araçları Uyarısı LNK4210
ms.date: 11/04/2016
f1_keywords:
- LNK4210
helpviewer_keywords:
- LNK4210
ms.assetid: db48cff8-a2be-4a77-8d03-552b42c228fa
ms.openlocfilehash: 75376129ce0033c717a4da3074cee9de132d357d
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62395072"
---
# <a name="linker-tools-warning-lnk4210"></a>Bağlayıcı Araçları Uyarısı LNK4210

> bölüm *bölümü* var; statik başlatıcılar veya sonlandırıcılar var. işlenmemiş

## <a name="remarks"></a>Açıklamalar

Bazı kod statik başlatıcılar veya sonlandırıcılar anlatılmıştır, ancak VCRuntime kitaplık başlatma kodu veya (Bu statik başlatıcılar veya sonlandırıcılar çalıştırması gereken) karşılığını uygulama başladığında çalıştırmak değil. Statik başlatıcılar veya sonlandırıcılar gerektiren kod bazı örnekleri aşağıda verilmiştir:

- Genel sınıf değişken Oluşturucu, yıkıcı veya sanal işlev tablosu.

- Küresel değişkeni, bir derleme zamanı sabiti ile başlatılamadı.

Bu sorunu gidermek için aşağıdakilerden birini deneyin:

- Tüm kod ile statik başlatıcılar kaldırın.

- Kullanmayın [/NOENTRY](../../build/reference/noentry-no-entry-point.md). / NOENTRY kaldırdıktan sonra da kaldırmak sahip olabilirsiniz [/nodefaultlıb](../../build/reference/nodefaultlib-ignore-libraries.md) bağlayıcı komut satırınızdan.

- Derleme/MT kullanıyorsa, LIBCMT.lib libvcruntime.lib ve libucrt.lib bağlayıcı komut satırına ekleyin. Derleme/mtd kullanıyorsa, lıbcmtd.lib vcruntimed.lib ve libucrtd.lib ekleyin.

- / CLR taşırken: / CLR, saf derlemeye kaldırmak [/Entry](../../build/reference/entry-entry-point-symbol.md) bağlayıcı satırından seçeneği. Bu, CRT başlatma sağlar ve uygulama başlangıcında yürütülecek statik başlatıcılar sağlar. **/CLR: pure** derleyici seçeneğini Visual Studio 2015'te kullanım dışı ve Visual Studio 2017'de desteklenmiyor.

[/GS](../../build/reference/gs-buffer-security-check.md) derleyici seçeneği tarafından başlatma gerektiriyor `__security_init_cookie` işlevi. Varsayılan olarak çalıştığı VCRuntime kitaplığı başlangıç kodunu bu başlatma sağlanan `_DllMainCRTStartup`.

- / Entry kullanarak projeniz derlendi ve/Entry dışındaki bir işleve geçirilen `_DllMainCRTStartup`, işlevini çağırmanız gerekir `_CRT_INIT` CRT başlatılamadı. DLL'niz /GS kullanıyorsa, statik başlatıcılar gerektirir ya da MFC veya ATL kodu bağlamında çağrılır, bu çağrı başına yeterli değildir. Bkz: [DLL'ler ve Visual C++ çalışma zamanı kitaplığı davranışı](../../build/run-time-library-behavior.md) daha fazla bilgi için.

## <a name="see-also"></a>Ayrıca bkz.

- [Bağlayıcı Seçeneklerini Ayarlama](../../build/reference/linking.md)
