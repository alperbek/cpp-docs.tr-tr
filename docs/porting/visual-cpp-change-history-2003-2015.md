---
title: Visual C++ değişiklik geçmişi 2003 - 2015
ms.date: 10/21/2019
helpviewer_keywords:
- breaking changes [C++]
ms.assetid: b38385a9-a483-4de9-99a6-797488bc5110
ms.openlocfilehash: 51de46487d85f4b8d7d357a0d1842f3d3192fff7
ms.sourcegitcommit: 6b3d793f0ef3bbb7eefaf9f372ba570fdfe61199
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/15/2020
ms.locfileid: "86404801"
---
# <a name="visual-c-change-history-2003---2015"></a>Visual C++ değişiklik geçmişi 2003 - 2015

Bu makalede, Visual Studio 2015 ' deki tüm önemli değişiklikler Visual Studio 2003 ' ye geri dönerek açıklanır ve bu makalede "yeni davranış" veya "Şimdi" terimleri Visual Studio 2015 ve sonraki bir sürüme başvurur. "Eski davranış" ve "Before" terimleri Visual Studio 2013 ve önceki sürümlere başvurur.

Visual Studio 'nun en son sürümü hakkında daha fazla bilgi için bkz. Visual Studio ['daki Visual C++](../overview/what-s-new-for-visual-cpp-in-visual-studio.md) yenilikler ve [visual Studio 'Da Visual C++ uyumluluk geliştirmeleri](../overview/cpp-conformance-improvements.md).

> [!NOTE]
> Visual Studio 2015 ve Visual Studio 2017 arasında ikili bir son değişiklik yoktur.

Visual Studio 'nun yeni bir sürümüne yükselttiğinizde, daha önce derlenmiş ve doğru şekilde çalıştığı kodda derleme ve/veya çalışma zamanı hatalarıyla karşılaşabilirsiniz. Yeni sürümdeki bu tür sorunlara neden olan değişiklikler, önemli *değişiklikler*olarak bilinir ve genellikle C++ dil standardı, işlev imzaları veya bellekteki nesnelerin düzeninde yapılan değişiklikler için gereklidir.

Algılaması ve tanılanması zor olan çalışma zamanı hatalarından kaçınmak için, farklı bir derleyicinin sürümü kullanılarak derlenen ikililer için hiçbir zaman statik olarak bağlantı oluşturmanız önerilir. Ayrıca, bir EXE veya DLL projesini yükseltirken, bağlantı verdiği kitaplıkları da yükselttiğinizden emin olun. Derleyicinin farklı sürümleri kullanılarak derlenen dll 'Ler dahil olmak üzere CRT (C çalışma zamanı) veya C++ standart kitaplığı (C++ Standart Kitaplığı) türlerini geçmeyin. Daha fazla bilgi için bkz. [CRT NESNELERINI DLL sınırları genelinde geçirme olası hataları](../c-runtime-library/potential-errors-passing-crt-objects-across-dll-boundaries.md).

COM arabirimi veya POD nesnesi olmayan bir nesne için belirli bir düzene bağlı olan kodu asla yazmanız gerekir. Bu tür bir kod yazarsanız, yükseltme sonrasında çalışmasını sağlamalısınız. Daha fazla bilgi için bkz. [ABI sınırları konumundaki taşınabilirlik](../cpp/portability-at-abi-boundaries-modern-cpp.md).

Ayrıca, derleyici uyumsuzluğuna yönelik sürekli geliştirmeler bazen derleyicinin mevcut kaynak kodunuzu nasıl anladığını değiştirebilir. Örneğin, derlemeniz sırasında yeni veya farklı hatalar bulabilir, hatta daha önce oluşturulmuş ve daha önce doğru şekilde çalışacak şekilde çalışan kodda davranış farklılıkları vardır. Bu geliştirmeler bu belgede ele alınanlara benzer değişiklikler olmamasına karşın, bu sorunları çözmek için kaynak kodunuzda değişiklikler yapmanız gerekebilir:

- [C çalışma zamanı (CRT) kitaplık bölünmesi değişiklikleri](#BK_CRT)

- [Standart C++ ve C++ standart kitaplığı önemli değişiklikleri](#BK_STL)

- [MFC ve ATL üzerinde önemli değişiklikler](#BK_MFC)

- [Eşzamanlılık Çalışma Zamanı son değişiklikler](#BK_ConcRT)

## <a name="visual-studio-2015-conformance-changes"></a><a name="VC_2015"></a>Visual Studio 2015 uygunluk değişiklikleri

### <a name="c-runtime-library-crt"></a><a name="BK_CRT"></a>C çalışma zamanı kitaplığı (CRT)

#### <a name="general-changes"></a>Genel değişiklikler

- **Yeniden düzenlenmiş ikilileri**

   CRT kitaplığı iki farklı ikiliye yeniden düzenlenmiş: bir Evrensel CRT (ucrtbase), standart işlevlerin çoğunu ve bir VC çalışma zamanı kitaplığı 'nı (vcruntime) içerir. Vcruntime kitaplığı, özel durum işleme ve iç bilgiler gibi derleyiciler ile ilgili işlevsellik içerir. Varsayılan proje ayarlarını kullanıyorsanız, bağlayıcı yeni varsayılan kitaplıkları otomatik olarak kullanacak şekilde bu değişiklik sizi etkilemez. Projenin **bağlayıcı** özelliğini **tüm varsayılan kitaplıkları** **Evet** olarak Yoksay veya `/NODEFAULTLIB` komut satırında bağlayıcı seçeneğini kullanıyorsanız, yeni, yeniden düzenlenmiş kitaplıklarını dahil etmek için kitaplıkların listesini ( **ek bağımlılıklar** özelliğinde) güncelleştirmeniz gerekir. Eski CRT kitaplığını (Libcmt. lib, libcmtd. lib, Msvcrt. lib, msvcrtd. lib) eşdeğer yeniden düzenlenmiş kitaplıklarıyla değiştirin. İki yeniden düzenlenmiş kitaplıklarının her biri için, statik (. lib) ve dinamik (. dll) sürümleri ve sürüm (son ek olmadan) ve hata ayıklama sürümleri ("d" sonekiyle birlikte) vardır. Dinamik sürümlerde, ile bağlantı oluşturduğunuz bir içeri aktarma kitaplığı vardır. İki yeniden düzenlenmiş kitaplığı Evrensel CRT, özellikle ucrtbase.dll veya uıcrtbase. lib, ucrtbased.dll veya uıcrtbased. lib ve VC çalışma zamanı kitaplığı, libvcruntime. lib, vcruntime*Sürüm*. dll, libvcruntimed. lib ve vcruntimed*Version*. dll ' dir. Hem Visual Studio 2015 hem de Visual Studio 2017 *sürümü* 140. Bkz. [CRT kitaplık özellikleri](../c-runtime-library/crt-library-features.md).

#### \<locale.h>

- **localeconv**

   Locale. h içinde belirtilen [localeconv](../c-runtime-library/reference/localeconv.md) işlevi, [iş parçacığı başına yerel ayar](../parallel/multithreading-and-locales.md) etkinleştirildiğinde artık doğru şekilde çalışır. Kitaplığın önceki sürümlerinde bu işlev, `lconv` iş parçacığının yerel ayarını değil genel yerel ayar için verileri döndürür.

   İş parçacığı başına yerel ayar kullanıyorsanız, kullanımını denetlemeniz gerekir `localeconv` . Kodunuz, `lconv` döndürülen verilerin genel yerel ayar için olduğunu varsaydığı takdirde düzeltmeniz gerekir.

#### \<math.h>

- **Matematik kitaplığı işlevlerinin C++ aşırı yüklemeleri**

   Önceki sürümlerde, \<math.h> matematik kitaplığı işlevleri Için C++ aşırı yüklemelerinin tümünü değil, hepsi tanımlanmış. Aşırı yüklemelerin geri kalanı \<cmath> üst bilgide vardı. Yalnızca dahil edilen kodda \<math.h> işlev aşırı yükleme çözümlemesi sorunları olabilir. Artık C++ aşırı yüklemeleri ' dan kaldırılmıştır \<math.h> ve yalnızca içinde bulunur \<cmath> .

   Hataları gidermek için, \<cmath> öğesinden kaldırılan işlevlerin bildirimlerini almak için öğesini ekleyin \<math.h> . Bu işlevler taşındı:

  - `double abs(double)` ve `float abs(float)`

  - `double pow(double, int)`, `float pow(float, float)`, `float pow(float, int)`, `long double pow(long double, long double)`, `long double pow(long double, int)`

  - `float``long double`kayan nokta işlevlerinin,,,,,,,,, `acos` `acosh` `asin` `asinh` `atan` `atanh` `atan2` `cbrt` `ceil` `copysign` , `cos` , `cosh` , `erf` `erfc` `exp` `exp2` `expm1` `fabs` `fdim` `floor` `fma` `fmax` `fmin` `fmod` `frexp` `hypot` `ilogb` `ldexp` `lgamma` `llrint` `llround` `log` `log10` `log1p` `log2` `lrint` `lround` `modf` `nearbyint` `nextafter` `nexttoward` `remainder` `remquo` `rint` `round` `scalbln` `scalbn` `sin` `sinh` `sqrt` `tan` `tanh` `tgamma` ,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,`trunc`

  `abs`Yalnızca üst bilgiyi içeren bir kayan nokta türü ile kullanan kodunuz varsa \<math.h> , kayan nokta sürümleri artık kullanılabilir olmayacaktır. Çağrı şimdi `abs(int)` , bir kayan nokta bağımsız değişkeni ile birlikte, bu hatayı oluşturan olarak çözümleniyor:

    ```Output
    warning C4244: 'argument' : conversion from 'float' to 'int', possible loss of data
    ```

  Bu uyarı için yapılan çağrı, bir `abs` `abs` `fabs` Double bağımsız değişkeni veya bir float bağımsız değişkeni gibi bir kayan nokta sürümü olan çağrısını değiştirmek `fabsf` veya \<cmath> üstbilgiyi içermesi ve kullanmaya devam `abs` etmek için kullanılır.

- **Kayan nokta uyumluluğu**

   , NaNs ve sonsuz gibi özel durum girdilerine göre IEEE-754 ve C11 ek F belirtimleriyle uyumluluğu artırmak için matematik kitaplığı 'nda birçok değişiklik yapılmıştır. Örneğin, genellikle kitaplığın önceki sürümlerinde hata olarak kabul edilen sessiz NaN girdileri artık hata olarak değerlendirilmez. [C11 standardının](https://www.iso.org/standard/57853.html) [IEEE 754 standardına](https://standards.ieee.org/standard/754-2008.html) ve ek F bölümüne bakın.

   Bu değişiklikler, derleme zamanı hatalarına neden olmaz, ancak programların standart 'e göre farklı ve doğru davranmasına neden olabilir.

- **FLT_ROUNDS**

   Visual Studio 2013, FLT_ROUNDS makrosu bir sabit ifadeye genişletilir, ancak bu, yuvarlama modu çalışma zamanında yapılandırılacağından, örneğin fesetround çağırarak yanlış. FLT_ROUNDS makro artık dinamiktir ve geçerli yuvarlama modunu doğru bir şekilde yansıtır.

#### <a name="new-and-newh"></a>\<new> ve \<new.h>

- **yeni ve Sil**

   Kitaplığın önceki sürümlerinde, uygulama tanımlı New ve delete işlevleri, çalışma zamanı kitaplığı DLL 'sinden (örneğin, msvcr120.dll) aktarılmış. Bu işleç işlevleri, çalışma zamanı kitaplığı dll 'Leri kullanılırken bile, ikili verilerinize her zaman statik olarak bağlanır.

   Bu, yerel veya karma kod () için bir değişiklik değildir `/clr` , ancak [/clr: Pure](../build/reference/clr-common-language-runtime-compilation.md)olarak derlenen kod için bu değişiklik kodunuzun derleyememesine neden olabilir. Kodu olarak derlerseniz `/clr:pure` , `#include <new>` `#include <new.h>` Bu değişiklik nedeniyle derleme hatalarına gerek veya çözüm eklemeniz gerekebilir. Bu `/clr:pure` seçenek Visual studio 2015 ' de kullanımdan kaldırılmıştır ve Visual studio 2017 ' de desteklenmez. "Saf" olması gereken kod C# ' ye eklenmelidir.

#### \<process.h>

- **_beginthread ve _beginthreadex**

   [_Beginthread](../c-runtime-library/reference/beginthread-beginthreadex.md) ve [_beginthreadex](../c-runtime-library/reference/beginthread-beginthreadex.md) işlevleri artık iş parçacığı yordamının iş parçacığı süresince tanımlandığı modüle bir başvuru tutar. Bu, bir iş parçacığının tamamlanmasını çalıştırana kadar modüllerin kaldırılmadığından emin olmaya yardımcı olur.

#### \<stdarg.h>

- **va_start ve başvuru türleri**

   C++ kodunu derlerken [va_start](../c-runtime-library/reference/va-arg-va-copy-va-end-va-start.md) artık derleme sırasında kendisine geçirilen bağımsız değişkenin başvuru türü olmadığını doğrular. Başvuru türü bağımsız değişkenleri C++ standardı tarafından yasaklanmıştır.

#### <a name="stdioh-and-conioh"></a><a name="stdio_and_conio"></a>\<stdio.h>ve\<conio.h>

- **Printf ve scanf ailesi işlevleri artık satır içi olarak tanımlanmıştır.**

   Tüm `printf` ve `scanf` işlevlerinin tanımları satır içinde \<stdio.h> , \<conio.h> ve diğer CRT üst bilgilerine taşınmıştır. Bu son değişiklik, uygun CRT üst bilgilerini eklemeden bu işlevleri yerel olarak bildirmeyen programlar için bir bağlayıcı hatasına (LNK2019, çözümlenmemiş dış sembol) yol açar. Mümkünse, kodu CRT üst bilgilerini (yani, Ekle `#include <stdio.h>` ) ve satır içi işlevleri içerecek şekilde güncelleştirmeniz gerekir, ancak kodunuzu bu üst bilgi dosyalarını içerecek şekilde değiştirmek istemiyorsanız, başka bir çözüm bağlayıcı girişinde ek bir kitaplık eklemektir legacy_stdio_definitions. lib.

   Bu kitaplığı IDE 'deki bağlayıcı girişine eklemek için, proje düğümünün bağlam menüsünü açın, **Özellikler**' i seçin, sonra **Proje özellikleri** iletişim kutusunda **bağlayıcı**' yı seçin ve **bağlayıcı girişini** `legacy_stdio_definitions.lib` noktalı virgülle ayrılmış listeye ekleyin.

   Projeniz 2015 'den önceki bir Visual Studio sürümü ile derlenen statik kitaplıklar ile bağlantı oluştursa, bağlayıcı çözümlenmemiş bir dış sembol bildirebilir. Bu hatalar `_iob` , `_iob_func` veya, belirli işlevler için, \<stdio.h> _imp_biçimindeki \* iç tanımlara başvurabilir. Microsoft, bir projeyi yükselttiğinizde tüm statik kitaplıkları C++ derleyicisinin ve kitaplıklarının en son sürümüyle yeniden derlemeniz önerilir. Kitaplık, kaynağın kullanılamadığı bir üçüncü taraf kitaplığsa, üçüncü taraftan güncelleştirilmiş bir ikili dosya istemeniz veya söz konusu kitaplığın kullanımını derleyicinin ve kitaplıkların eski sürümüyle derleyebileceğiniz ayrı bir DLL 'ye kapsületmeniz gerekir.

    > [!WARNING]
    > Windows SDK 8,1 veya önceki bir sürümü ile bağlanıyorsanız, bu çözümlenmemiş dış sembol hatalarıyla karşılaşabilirsiniz. Bu durumda, daha önce açıklandığı gibi bağlayıcı girişine legacy_stdio_definitions. lib ekleyerek hatayı çözmeniz gerekir.

   Çözümlenmemiş sembol hatalarını gidermek için, bir ikilide tanımlanan sembolleri incelemek üzere [dumpbin.exe](../build/reference/dumpbin-reference.md) kullanmayı deneyebilirsiniz. Bir kitaplıkta tanımlanan sembolleri görüntülemek için aşağıdaki komut satırını deneyin.

    ```cpp
    dumpbin.exe /LINKERMEMBER somelibrary.lib
    ```

- **alır ve _getws**

   [Al](../c-runtime-library/gets-getws.md) ve [_getws](../c-runtime-library/gets-getws.md) işlevleri kaldırılmıştır. Al işlevi, güvenli bir şekilde kullanılamadığından C11 içindeki C standart kitaplığından kaldırılmıştır. _Getws işlevi, geniş dizeler için al, ancak geniş dizeler için eşdeğer olan bir Microsoft uzantısıdır. Bu işlevlerin alternatifleri olarak, [fal](../c-runtime-library/reference/fgets-fgetws.md), [fgetws](../c-runtime-library/reference/fgets-fgetws.md), [gets_s](../c-runtime-library/reference/gets-s-getws-s.md)ve [_getws_s](../c-runtime-library/reference/gets-s-getws-s.md)kullanımını göz önünde bulundurun.

- **_cgets ve _cgetws**

   [_Cgets](../c-runtime-library/cgets-cgetws.md) ve [_cgetws](../c-runtime-library/cgets-cgetws.md) işlevleri kaldırılmıştır. Bu işlevlerin alternatifleri olarak [_cgets_s](../c-runtime-library/reference/cgets-s-cgetws-s.md) ve [_cgetws_s](../c-runtime-library/reference/cgets-s-cgetws-s.md)kullanımını göz önünde bulundurun.

- **Sonsuzluk ve NaN biçimlendirmesi**

   Önceki sürümlerde, sonsuz ve NaNs, MSVC 'e özgü bir Sentinel dizeleri kümesi kullanılarak biçimlendirilir.

  - Sonsuz: 1. #INF

  - Sessiz NaN: 1. #QNAN

  - İşaret NaN: 1. #SNAN

  - Sonsuz NaN: 1. #IND

  Bu biçimlerden herhangi biri bir işaret tarafından ön ekli olabilir ve alan genişliğine ve duyarlığına bağlı olarak biraz farklı şekilde formatlanabilir (örneğin, olağan dışı etkileri olan `printf("%.2f\n", INFINITY)` 1. #J, #INF 2 basamaklı bir duyarlığa "yuvarlanarak). C99, sonsuz ve NaNs 'ın nasıl biçimlendirileceği hakkında yeni gereksinimler sunmuştur. MSVC uygulama artık bu gereksinimlere uyar. Yeni dizeler aşağıdaki gibidir:

  - Infinity: inf

  - Sessiz NaN: Nan

  - Sinyal NaN: NaN (snan)

  - Sonsuz NaN: NaN (ind)

  Bunlardan herhangi birine bir işaret ön eki uygulanabilir. Büyük harfli bir biçim belirticisi kullanılırsa (% f yerine% F), dizeler `INF` gerekli olduğu gibi büyük harflerle (yerine `inf` ) yazdırılır.

  [Scanf](../c-runtime-library/reference/scanf-scanf-l-wscanf-wscanf-l.md) işlevleri bu yeni dizeleri ayrıştırmak üzere değiştirilmiştir. bu nedenle, bu dizeler artık ve arasında gidiş dönüş `printf` `scanf` .

- **Kayan nokta biçimlendirme ve ayrıştırma**

   Doğruluğu artırmak için yeni kayan nokta biçimlendirme ve ayrıştırma algoritmaları sunulmuştur. Bu değişiklik, [strtod](../c-runtime-library/reference/strtod-strtod-l-wcstod-wcstod-l.md)gibi işlevlerin yanı sıra [printf](../c-runtime-library/reference/printf-printf-l-wprintf-wprintf-l.md) ve [scanf](../c-runtime-library/reference/scanf-scanf-l-wscanf-wscanf-l.md) işlevlerini etkiler.

   Eski biçimlendirme algoritmaları yalnızca sınırlı sayıda basamak oluşturur, sonra kalan ondalık basamak sayısını sıfıra dolduracaktır. Genellikle özgün kayan nokta değerine geri dönüş yapan dizeler oluşturabilir, ancak tam değeri (veya en yakın ondalık gösterimi) istediğinizde harika değildir. Yeni biçimlendirme algoritmaları, değeri temsil etmek için gereken sayıda basamak üretir (veya belirtilen duyarlığı dolduracak şekilde). Geliştirme örneği olarak; İki ' un büyük bir kuvveti yazdırırken sonuçları göz önünde bulundurun:

    ```cpp
    printf("%.0f\n", pow(2.0, 80))
    ```

   Eski çıkış:

    ```Output
    1208925819614629200000000
    ```

   Yeni çıkış:

    ```Output
    1208925819614629174706176
    ```

   Eski ayrıştırma algoritmaları yalnızca giriş dizesindeki en fazla 17 önemli basamağı göz önünde bulundurarak basamakların geri kalanını atar. Bu yaklaşım, dize tarafından temsil edilen değerin yaklaşık bir kısmını oluşturmak için yeterlidir ve sonuç genellikle doğru bir şekilde yuvarlanmış sonuca yakın bir şekilde yakındır. Yeni uygulama tüm mevcut basamakları dikkate alır ve tüm girişler için doğru yuvarlanmış sonucu üretir (en fazla 768 basamak uzunluğunda olmalıdır). Ayrıca, bu işlevler artık yuvarlama moduna (fesetround ile denetlenebilir) göre yapılır.  Bu işlevler farklı sonuçlar çıktısı olabileceğinden, bu durum büyük olasılıkla bir davranış değişikliğine neden olur. Yeni sonuçlar her zaman eski sonuçlardan daha doğru olur.

- **Onaltılı ve sonsuz/NaN kayan nokta ayrıştırma**

   Kayan nokta ayrıştırma algoritmaları artık onaltılık kayan nokta dizelerini (% a ve% A printf biçim belirticileri tarafından oluşturulan olanlar gibi) ve `printf` yukarıda açıklandığı gibi işlevler tarafından oluşturulan tüm sonsuzluk ve Nan dizelerini ayrıştıracaktır.

- **% A ve %0 doldurma**

   % A ve% A biçim belirticileri bir kayan nokta sayısını onaltılık Mantis ve ikili üs olarak biçimlendirir. Önceki sürümlerde, `printf` işlevler hatalı şekilde sıfır-doldurma dizeleri olur. Örneğin, `printf("%07.0a\n", 1.0)` 00x1p + 0 yazdıracağından, burada 0x01p + 0 yazdırılır. Bu kusur düzeltildi.

- **% A ve% bir duyarlık**

   % A ve% a biçim belirticileri için varsayılan duyarlık, kitaplığın önceki sürümlerinde 6 ' tır. Varsayılan duyarlık, C standardı ile uyumluluk için artık 13 ' dir.

   Bu,% A veya% a ile bir biçim dizesi kullanan herhangi bir işlevin çıktısında bir çalışma zamanı davranışı değişikdir. Eski davranışta,% A belirticisi kullanılarak oluşan çıkış "1.1 A2B3Cp + 111" olabilir. Artık aynı değere ait çıkış "1.1 A2B3C4D5E6F7p + 111" dır. Eski davranışı sağlamak için duyarlık belirtebilirsiniz, örneğin,%. 6A. Bkz. [duyarlık belirtimi](../c-runtime-library/format-specification-syntax-printf-and-wprintf-functions.md#precision).

- **% F Belirleyicisi**

   % F biçim/dönüştürme belirticisi artık destekleniyor. Sonsuz ve NaNs 'ler büyük harfler kullanılarak biçimlendirilmediği sürece,% f biçim belirticisine işlevsel olarak eşdeğerdir.

   Önceki sürümlerde, F ve N 'yi uzunluk değiştiricilerini ayrıştırmak için kullanılan uygulama. Bu davranış, kesimli adres alanlarının yaşına geri dönme: Bu uzunluk değiştiricileri,% fp veya% NS içinde olduğu gibi, sırasıyla en çok ve yakın işaretçileri göstermek için kullanılır. Bu davranış kaldırılmıştır. % F ile karşılaşılırsa, artık% F biçim belirticisi olarak kabul edilir. % N ile karşılaşılırsa, artık geçersiz parametre olarak kabul edilir.

- **Üs biçimlendirme**

   % E ve% E biçim belirticileri bir kayan nokta sayısını ondalık Mantis ve üs olarak biçimlendirir. % G ve% G biçim belirticileri, bazı durumlarda bu formdaki sayıları de biçimlendirir. Önceki sürümlerde, CRT her zaman üç basamaklı üsler içeren dizeler oluşturur. Örneğin, `printf("%e\n", 1.0)` 1.000000 e + 000, yanlış bir şekilde yazdırılır. C, üs 'un yalnızca bir veya iki basamak kullanarak gösterilebilir olması gerekir, bu durumda yalnızca iki basamak yazdırılır.

   Visual Studio 2005 ' de küresel bir uyumluluk anahtarı eklenmiştir: [_set_output_format](../c-runtime-library/set-output-format.md). Bir program, uyumlu üs yazdırmayı etkinleştirmek için _TWO_DIGIT_EXPONENT bağımsız değişkeniyle bu işlevi çağırabilir. Varsayılan davranış, standartlara uygun üs yazdırma moduna değiştirilmiştir.

- **Biçim dizesi doğrulaması**

   Önceki sürümlerde `printf` ve `scanf` işlevleri, bazen olağan dışı efektlerle birçok geçersiz biçim dizesini sessizce kabul eder. Örneğin,% hlhlhld% d olarak değerlendirilir. Tüm geçersiz biçim dizeleri artık geçersiz parametre olarak kabul edilir.

- **fopen modu dize doğrulaması**

   Önceki sürümlerde, `fopen` işlevler ailesi gibi bazı geçersiz mod dizelerini sessizce kabul eder `r+b+` . Geçersiz mod dizeleri artık algılanır ve geçersiz parametre olarak kabul edilir.

- **_O_U8TEXT modu**

   [_Setmode](../c-runtime-library/reference/setmode.md) işlevi artık akışların açılan in_O_U8TEXT moduna yönelik modunu doğru şekilde bildiriyor. Kitaplığın önceki sürümlerinde, bu tür akışları _O_WTEXT açılmakta olarak raporlayabilir.

   Kodunuz, kodlamanın UTF-8 olduğu akışlar için _O_WTEXT modunu yorumlayacağından bu bir son değişiklik değildir. Uygulamanız UTF_8 desteklemiyorsa, giderek daha sık görülen bu kodlamaya yönelik destek eklemeyi göz önünde bulundurun.

- **snprintf ve vsnprintf**

   [Snprintf](../c-runtime-library/reference/snprintf-snprintf-snprintf-l-snwprintf-snwprintf-l.md) ve [vsnprintf](../c-runtime-library/reference/vsnprintf-vsnprintf-vsnprintf-l-vsnwprintf-vsnwprintf-l.md) işlevleri artık uygulandı. Daha eski kod genellikle, bu işlevlerin, CRT kitaplığı tarafından uygulanmadığı, ancak artık daha yeni sürümlerde gerekli olmadıkları için makro sürümlerini tanımlar. [Snprintf](../c-runtime-library/reference/snprintf-snprintf-snprintf-l-snwprintf-snwprintf-l.md) veya [vsnprintf](../c-runtime-library/reference/vsnprintf-vsnprintf-vsnprintf-l-vsnwprintf-vsnwprintf-l.md) dahil etmeden önce bir makro olarak tanımlanmışsa \<stdio.h> , derleme şimdi makronun nerede tanımlandığını belirten bir hata ile başarısız olur.

   Normalde, bu sorunun düzeltilmesi `snprintf` Kullanıcı kodundaki veya içindeki tüm bildirimleri silmektir `vsnprintf` .

- **tmpnam kullanılabilir dosya adları oluşturuyor**

   Önceki sürümlerde `tmpnam` ve `tmpnam_s` işlevleri, sürücünün kökünde (\sd3c.) dosya adları oluşturdu. Bu işlevler artık geçici bir dizinde kullanılabilir dosya adı yolları oluşturur.

- **DOSYA kapsülleme**

   Önceki sürümlerde, tüm dosya türü içinde genel olarak tanımlanmıştır \<stdio.h> , bu nedenle kullanıcı kodunun BIR dosyaya ulaşması ve iç bileşenlerini değiştirmesi olasıdır. Kitaplık, uygulama ayrıntılarını gizleyecek şekilde değiştirilmiştir. Bu değişikliğin bir parçası olarak, içinde tanımlanan dosya \<stdio.h> artık donuk bir tür ve ÜYELERI CRT dışında erişilemez.

- **_outp ve _inp**

   [_Outp](../c-runtime-library/outp-outpw-outpd.md), [_outpw](../c-runtime-library/outp-outpw-outpd.md), [_outpd](../c-runtime-library/outp-outpw-outpd.md), [_inp](../c-runtime-library/inp-inpw-inpd.md), [_inpw](../c-runtime-library/inp-inpw-inpd.md)ve [_inpd](../c-runtime-library/inp-inpw-inpd.md) işlevleri kaldırılmıştır.

#### <a name="stdlibh-malloch-and-sysstath"></a>\<stdlib.h>, \<malloc.h> ve\<sys/stat.h>

- **strtof ve wcstof**

   `strtof` `wcstof` `errno` Değer bir float olarak gösterilemeyen ve işlevleri ERANGE olarak ayarlanamadı. Bu hata, bu iki işleve özeldir; `strtod`,, `wcstod` , `strtold` ve `wcstold` işlevleri etkilenmemiştir. Bu sorun düzeltildi ve çalışma zamanı bölünmesi değişikliği.

- **Hizalanmış ayırma işlevleri**

   Önceki sürümlerde, hizalanmış ayırma işlevleri ( `_aligned_malloc` , `_aligned_offset_malloc` , vb.) 0 hizalamasına sahip bir blok için istekleri sessizce kabul eder. İstenen hizalama iki üssü olmalıdır. Bu değer sıfır olmayan bir değer değildir. İstenen 0 hizalaması artık geçersiz bir parametre olarak kabul edilir. Bu sorun düzeltildi ve çalışma zamanı bölünmesi değişikliği.

- **Yığın işlevleri**

   `_heapadd`, `_heapset` Ve `_heapused` işlevleri kaldırılmıştır. CRT, Windows yığınını kullanacak şekilde güncelleştirildiğinden bu işlevler işlevsiz.

- **smallheap**

   `smallheap`Bağlantı seçeneği kaldırılmıştır. Bkz. [bağlantı seçenekleri](../c-runtime-library/link-options.md).

#### \<string.h>

- **wcstok**

   İşlevin imzası, `wcstok` C standardı tarafından gerekenlerin eşleşmesi için değiştirilmiştir. Kitaplığın önceki sürümlerinde, bu işlevin imzası:

    ```cpp
    wchar_t* wcstok(wchar_t*, wchar_t const*)
    ```

   İçin yapılan çağrılar genelinde durumu izlemek üzere iç, iş parçacığı başına bağlam kullandı `strtok` . İşlev şimdi imzaya sahiptir `wchar_t* wcstok(wchar_t*, wchar_t const*, wchar_t**)` ve çağıranın bağlamı üçüncü bağımsız değişken olarak işleve geçmesini gerektirir.

   Yük `_wcstok` geçirilmesini kolaylaştırmak için eski imzaya sahip yeni bir işlev eklendi. C++ kodu derlenirken, eski imzaya sahip bir satır içi aşırı yüklemesi de vardır `wcstok` . Bu aşırı yükleme kullanım dışı olarak bildirildi. C kodunda, yerine kullanılmasına neden define_CRT_NON_CONFORMING_WCSTOK isteyebilirsiniz `_wcstok` `wcstok` .

#### \<time.h>

- **saat**

   Önceki sürümlerde [Clock](../c-runtime-library/reference/clock.md) IşLEVI Windows API [GetSystemTimeAsFileTime](/windows/win32/api/sysinfoapi/nf-sysinfoapi-getsystemtimeasfiletime)kullanılarak uygulanmıştır. Bu uygulamayla, saat işlevi sistem saatine duyarlıdır ve bu nedenle monotonic olması gerekmez. Clock işlevi, [QueryPerformanceCounter](/windows/win32/api/profileapi/nf-profileapi-queryperformancecounter) açısından yeniden uygulanmıştır ve artık monotonic.

- **fstat ve _utime**

   Önceki sürümlerde [_stat](../c-runtime-library/reference/stat-functions.md), [fstat](../c-runtime-library/reference/fstat-fstat32-fstat64-fstati64-fstat32i64-fstat64i32.md)ve [_utime](../c-runtime-library/reference/utime-utime32-utime64-wutime-wutime32-wutime64.md) işlevleri yaz tasarrufu süresini yanlış işler. Visual Studio 2013 önce, tüm bu işlevler, zaman yaz saati gibi standart zaman zamanlarını yanlış olarak ayarlamıştı.

   Visual Studio 2013, sorun **_stat** işlevleri ailesinde düzeltildi, ancak **fstat** ve **_utime** işlev ailelerindeki benzer sorunlar düzeltilmedi. Bu kısmi düzelme, İşlevler arasındaki tutarsızlık nedeniyle sorunlara yol açmıştır. İşlevlerin **fstat** ve **_utime** aileleri artık düzeltildi, bu nedenle tüm bu işlevler artık gün ışığından yararlanma süresini doğru ve tutarlı bir şekilde işler.

- **asctime**

   Önceki sürümlerde, [asctime](../c-runtime-library/reference/asctime-wasctime.md) işlevi önünde sıfır ile tek basamaklı günler, örneğin: `Fri Jun 06 08:00:00 2014` . Belirtim, içinde olduğu gibi, söz konusu günlerin önünde boşluk ile doldurulmuş olmasını gerektirir `Fri Jun  6 08:00:00 2014` . Bu sorun düzeltilmiştir.

- **strftime ve wcsftime**

   `strftime`Ve `wcsftime` işlevleri artık% C,% D,% e,% F,% g,% g,% h,% n,% r,% r,% t,% t,% u ve% V biçim belirticilerini destekliyor. Ayrıca, E ve O değiştiricileri ayrıştırılıp yok sayılır.

   % C Biçim Belirleyicisi, geçerli yerel ayar için "uygun tarih ve saat gösterimi" üretmek üzere belirtildi. C yerel ayarında, bu gösterimi ile aynı şekilde `%a %b %e %T %Y` , tarafından oluşturulan formla aynı olması gerekir `asctime` . Önceki sürümlerde,% c Biçim belirleyicisi bir temsili kullanılarak yanlış biçimlendirilmiş `MM/DD/YY HH:MM:SS` . Bu sorun düzeltilmiştir.

- **timespec ve TIME_UTC**

   \<time.h>Üst bilgi artık `timespec` türü ve `timespec_get` işlevi C11 standardını tanımlar. Ayrıca, işleviyle kullanım için TIME_UTC makrosu `timespec_get` artık tanımlanmıştır. Bu güncelleştirme, Bu tanımlayıcılardan herhangi biri için çakışan bir tanıma sahip kod için bir değişiklik değildir.

- **CLOCKS_PER_SEC**

   CLOCKS_PER_SEC makro artık `clock_t` C dilinin gerektirdiği şekilde türü bir tam sayı olarak genişletilir.

#### <a name="c-standard-library"></a><a name="BK_STL"></a>C++ standart kitaplığı

Yeni iyileştirmeleri ve hata ayıklama denetimlerini etkinleştirmek için, C++ Standart Kitaplığı'nın Visual Studio uygulaması bir sürümden sonraki bir sürüme ikili uyumluluğu kasıtlı olarak bozar. Bu nedenle, C++ Standart Kitaplığı kullanıldığında, farklı sürümlerin kullanımıyla derlenmiş nesne dosyaları ve statik kitaplıklar tek bir ikili dosya (EXE veya DLL) halinde karma yapılabilir ve C++ Standart Kitaplığı nesneleri, farklı sürümler kullanılarak derlenmiş ikili dosyalar arasında geçirilemez. Bu tür karmalar, _MSC_VER uyuşmazlıklarıyla ilgili bağlayıcı hataları verir. (_MSC_VER, derleyicinin ana sürümünü içeren makrodur — Örneğin, Visual Studio 2013 için 1800.) Bu denetim, DLL karıştırmasını algılayamaz ve Visual Studio 2008 veya önceki bir sürümünü içeren karıştırma 'yı algılayamaz.

- **C++ standart kitaplığı dosya ekleme**

   C++ standart kitaplığı üst bilgilerindeki ekleme yapısında bazı değişiklikler yapılmıştır. C++ standart kitaplık üst bilgilerine birbirini belirtilmeyen yollarla dahil etmek için izin verilir. Genellikle, kodunuzun C++ standardına göre ihtiyacı olan tüm üst bilgileri dikkatle eklemesi için kodunuzu yazmanız gerekir ve hangi C++ standart kitaplık başlıklarındaki diğer C++ standart kitaplık üstbilgilerini içerdiğini temel almaz. Bu, kodu sürümler ve platformlar arasında taşınabilir hale getirir. Visual Studio 2015 ' de en az iki başlık değişikliği Kullanıcı kodunu etkiler. Birincisi, \<string> artık şunları içermez \<iterator> . İkinci olarak, \<tuple> `std::array` \<array> Aşağıdaki kod yapıları birleşimi aracılığıyla kodu kesintiye uğramış olan tüm ' ı dahil etmeden bildirir: kodunuz "Array" adlı bir değişkene sahiptir ve bir using yönergesi olan "ad alanı std;" olan bir C++ standart kitaplık üst bilgisi (gibi \<functional> ) içerir \<tuple> `std::array` .

- **steady_clock**

   \<chrono> [Steady_clock](../standard-library/steady-clock-struct.md) uygulaması, steadiness ve monoton için C++ standart gereksinimlerini karşılayacak şekilde değiştirilmiştir. `steady_clock`Artık, [QueryPerformanceCounter](/windows/win32/api/profileapi/nf-profileapi-queryperformancecounter) 'yi temel alır ve `high_resolution_clock` artık için bir typedef `steady_clock` . Sonuç olarak, Visual Studio 'da `steady_clock::time_point` için bir typedef vardır `chrono::time_point<steady_clock>` ; ancak, diğer uygulamalar için bu durum böyle değildir.

- **ayrıcılar ve const**

   Artık her iki tarafta de const bağımsız değişkenlerini kabul etmek için ayırıcı eşitlik/eşitsizlik karşılaştırmaları gereklidir. Ayrılarınız bu işleçleri bu şekilde tanımladıysanız,

    ```cpp
    bool operator==(const MyAlloc& other)
    ```

   daha sonra bunları güncelleştirip const Üyeler olarak bildirmeniz gerekir:

    ```cpp
    bool operator==(const MyAlloc& other) const
    ```

- **const öğeleri**

   C++ standardı, her zaman yasak olan const öğeleri (vektör \<const T> veya küme gibi) kapsayıcıları vardır \<const T> . Visual Studio 2013 ve önceki sürümleri kabul etti. Geçerli sürümde, Bu kapsayıcılar derlenemeyebilir.

- **std:: ayırıcı::d eallocate**

   Visual Studio 2013 ve önceki sürümlerde, `std::allocator::deallocate(p, n)` *n*için geçirilen bağımsız değişkeni yok sayılır.  C++ standardı, her zaman *n* 'nin döndürülen p 'nin çağrılması için ilk bağımsız değişken olarak geçirilen değere eşit olması gerekiyordu `allocate` . *p* Ancak, geçerli sürümde *n* değeri denetlenir. Standart için gerekli olan, çalışma zamanında kilitlenebiliyor olan *n* için bağımsız değişkenleri geçiren kod.

- **hash_map ve hash_set**

   Standart olmayan başlık dosyaları \<hash_map> ve \<hash_set> Visual Studio 2015 ' de kullanımdan kaldırılmıştır ve gelecek sürümlerde kaldırılır. \<unordered_map> \<unordered_set> Bunun yerine ve kullanın.

- **Karşılaştırıcılar ve işleç ()**

   İlişkilendirilebilir kapsayıcılar ( \<map> Aile) artık Karşılaştırıcılar için sabit çağrılabilir işlev çağrısı işleçleri olmasını gerektirir. Bir karşılaştırıcı sınıfı bildiriminde aşağıdaki kod artık derlenemiyor:

    ```cpp
    bool operator()(const X& a, const X& b)
    ```

   Bu hatayı çözmek için, işlev bildirimini şu şekilde değiştirin:

    ```cpp
    bool operator()(const X& a, const X& b) const
    ```

- **tür nitelikleri**

   C++ taslak standardının önceki bir sürümünden tür nitelikleri için eski adlar kaldırılmıştır. Bunlar C++ 11 ' de değiştirilmiştir ve Visual Studio 2015 ' de C++ 11 değerlerine güncelleştirilmiştir. Aşağıdaki tabloda eski ve yeni adlar gösterilmektedir.

   |Eski ad|Yeni ad|
   |--------------|--------------|
   |add_reference|add_lvalue_reference|
   |has_default_constructor|is_default_constructible|
   |has_copy_constructor|is_copy_constructible|
   |has_move_constructor|is_move_constructible|
   |has_nothrow_constructor|is_nothrow_default_constructible|
   |has_nothrow_default_constructor|is_nothrow_default_constructible|
   |has_nothrow_copy|is_nothrow_copy_constructible|
   |has_nothrow_copy_constructor|is_nothrow_copy_constructible|
   |has_nothrow_move_constructor|is_nothrow_move_constructible|
   |has_nothrow_assign|is_nothrow_copy_assignable|
   |has_nothrow_copy_assign|is_nothrow_copy_assignable|
   |has_nothrow_move_assign|is_nothrow_move_assignable|
   |has_trivial_constructor|is_trivially_default_constructible|
   |has_trivial_default_constructor|is_trivially_default_constructible|
   |has_trivial_copy|is_trivially_copy_constructible|
   |has_trivial_move_constructor|is_trivially_move_constructible|
   |has_trivial_assign|is_trivially_copy_assignable|
   |has_trivial_move_assign|is_trivially_move_assignable|
   |has_trivial_destructor|is_trivially_destructible|

- **Launch:: any ve Launch:: Sync ilkeleri**

   Standart dışı `launch::any` ve `launch::sync` ilkeler kaldırıldı. Bunun yerine, için `launch::any` kullanın `launch:async | launch:deferred` . `launch::sync` için `launch::deferred`'i kullanın. Bkz. [başlatma numaralandırması](../standard-library/future-enums.md#launch).

#### <a name="mfc-and-atl"></a><a name="BK_MFC"></a>MFC ve ATL

- **Microsoft Foundation Sınıfları (MFC)**

   , büyük boyutu nedeniyle artık Visual Studio 'nun "tipik" yüklemesine dahil değildir. MFC 'yi yüklemek için Visual Studio 2015 kurulumunda **özel** yükleme seçeneğini belirleyin. Visual Studio 2015 zaten yüklüyse, **Visual Studio** kurulumunu YENIDEN çalıştırarak MFC 'yi yükleyebilirsiniz. **Özel** Install seçeneğini belirleyin ve ardından **Microsoft Foundation sınıfları**öğesini seçin. **Visual Studio** kurulumunu **Denetim Masası 'Ndaki** **Programlar ve Özellikler**' den veya yükleme medyasından çalıştırabilirsiniz.

   Visual C++ Yeniden Dağıtılabilir Paketi'nde bu kitaplık halen yer almaktadır.

#### <a name="concurrency-runtime"></a><a name="BK_ConcRT"></a>Eşzamanlılık Çalışma Zamanı

- **Windows. h 'den concurrency:: Context:: yield ile çakışan yield makrosu**

   Daha önce, `#undef` Windows. h h 'de ve işlevinde tanımlanan yield makrosu arasındaki çakışmaları önlemek için, daha önce yield makrosunu tanımlamak üzere kullanılan eşzamanlılık çalışma zamanı `concurrency::Context::Yield` . Bu `#undef` kaldırılmıştır ve yeni çakışmayan bir eşdeğer API çağrısı [concurrency:: Context:: Ödemedexecution](../parallel/concrt/reference/context-class.md#yieldexecution) eklenmiştir. Bir sorunu gidermek için, bu işlevi çağırmak üzere kodunuzu güncelleştirebilir `YieldExecution` ya da `Yield` Aşağıdaki örnekte olduğu gibi, çağıran sitelerde işlev adını parantez ile çevreleyin:

    ```cpp
    (concurrency::Context::Yield)();
    ```

## <a name="compiler-conformance-improvements-in-visual-studio-2015"></a>Visual Studio 2015 ' de derleyici uyumluluğu geliştirmeleri

Önceki sürümlerden kod yükseltirken, Visual Studio 2015 ' de yapılan uyumluluk geliştirmelerinden kaynaklanan derleyici hatalarıyla de karşılaşabilirsiniz. Bu geliştirmeler, Visual Studio 'nun önceki sürümlerinden ikili uyumluluğu kesmez, ancak daha önce hiç yayılmadığı derleyici hataları oluşturabilir. Daha fazla bilgi için bkz. yenilikler [2003 ile 2015 arasında Visual C++](../porting/visual-cpp-what-s-new-2003-through-2015.md).

Visual Studio 2015 ' de, derleyici uygunluk için devam eden geliştirmeler bazen derleyicinin mevcut kaynak kodunuzu nasıl anladığını değiştirebilir. Sonuç olarak, derlemeniz sırasında yeni veya farklı hatalarla karşılaşabilirsiniz, hatta daha önce oluşturulmuş ve daha önce doğru şekilde çalışacak şekilde çalışan kodda davranış farklılıkları da yaşayabilirsiniz.

Neyse ki, bu farkların çoğu kaynak kodunuzun büyük bir etkisi yoktur. Bu farklılıklara yönelik kaynak kodu veya diğer değişiklikler gerektiğinde, düzeltmeler küçük ve düz ileri doğru olur. Daha önceden kabul edilebilir kaynak kodu örnekleri, değiştirilmesi gerekebilecek *(önce)* ve bunları düzeltmek için düzeltmeler (daha *sonra)* ekledik.

Bu farklılıklar, kaynak kodunuzu veya diğer yapı yapıtlarınızı etkileyebilse de, Visual Studio sürümlerindeki güncelleştirmeler arasında ikili uyumluluğu etkilemez. Önemli bir *değişiklik* daha önemlidir ve ikili uyumluluğu etkileyebilir, ancak bu tür ikili uyumluluk sonları yalnızca Visual Studio 'nun ana sürümleri arasında (örneğin, Visual Studio 2013 ve visual Studio 2015 arasında) oluşur. Visual Studio 2013 ve Visual Studio 2015 arasında oluşan önemli değişiklikler hakkında daha fazla bilgi için bkz. [Visual studio 2015 uyum değişiklikleri](#VC_2015).

- [Visual Studio 2015 uyumluluk geliştirmeleri](#VS_RTM)

- [Güncelleştirme 1 ' deki uyumluluk geliştirmeleri](#VS_Update1)

- [Güncelleştirme 2 ' deki uyumluluk geliştirmeleri](#VS_Update2)

- [Güncelleştirme 3 ' te uyumluluk geliştirmeleri](#VS_Update3)

### <a name="conformance-improvements-in-visual-studio-2015"></a><a name="VS_RTM"></a>Visual Studio 2015 uyumluluk geliştirmeleri

- /Zc: forScope-seçenek

   Derleyici seçeneği `/Zc:forScope-` kullanımdan kaldırılmıştır ve gelecek sürümde kaldırılacaktır.

    ```cpp
    Command line warning  D9035: option 'Zc:forScope-' has been deprecated and will be removed in a future release
    ```

   Genellikle bu seçenek, standart olarak, kapsam dışı bir noktaya göre döngü değişkenlerini kullanan standart olmayan koda izin vermek için kullanılmıştır. Yalnızca `/Za` seçeneği olmadan, `/Za` döngü sonuna bir for döngüsü değişkeninin kullanılması her zaman izin verildiğinde gereklidir. Standartlara uygunluğu konusunda endişelenmezseniz (örneğin, kodunuz diğer derleyicilere taşınabilir değilse), `/Za` seçeneğini kapatabilir (veya **dil uzantılarını devre dışı bırak** özelliğini **Hayır**olarak ayarlayabilirsiniz). Taşınabilir, standartlara uyumlu kod yazma konusunda dikkatli değilseniz, bu tür değişkenlerin bildirimini döngü dışındaki bir noktaya taşıyarak, kodunuzu standart olacak şekilde yeniden yazmanız gerekir.

    ```cpp
    // C2065 expected
    int main() {
        // Uncomment the following line to resolve.
        // int i;
        for (int i = 0; i < 1; i++);
        i = 20;   // i has already gone out of scope under /Za
    }
    ```

- `/Zg`derleyici seçeneği

   `/Zg`Derleyici seçeneği (Işlev prototipleri üret) artık kullanılamıyor. Bu derleyici seçeneği daha önce kullanım dışıdır.

- Artık mstest.exe olan komut satırından C++/CLı ile birim testlerini çalıştıramazsınız. Bunun yerine vstest.console.exe kullanın. Bkz. [VSTest.Console.exe komut satırı seçenekleri](/visualstudio/test/vstest-console-options).

- **kesilebilir anahtar sözcüğü**

   Daha önce hata olmadan derlenen konumlarda **kesilebilir** depolama sınıfı belirticisine artık izin verilmez. Artık derleyici hata C2071 (Geçersiz depolama sınıfı) veriyor. Standart olarak, **kesilebilir** tanımlayıcı yalnızca sınıf veri üyelerinin adlarına uygulanabilir ve const veya static olarak belirtilen adlara uygulanamaz ve başvuru üyelerine uygulanamaz.

   Örneğin, aşağıdaki kodu göz önünde bulundurun:

    ```cpp
    struct S
    {
        mutable int &r;
    };
    ```

   Derleyicinin önceki sürümleri bunu kabul etti, ancak artık derleyici şu hatayı veriyor:

    ```Output
    error C2071: 'S::r': illegal storage class
    ```

   Hatayı onarmak için, gereksiz **kesilebilir** anahtar sözcüğünü kaldırın.

- **char_16_t ve char32_t**

   `char16_t` `char32_t` Bu türler artık yerleşik olarak değerlendirildiğinden, bir **typedef**içinde artık diğer adlar kullanılamaz. Kullanıcılar ve kitaplık yazarlarının `char16_t` `char32_t` `uint16_t` , sırasıyla ve ' nin diğer adlarını tanımlamak için yaygındır `uint32_t` .

    ```cpp
    #include <cstdint>

    typedef uint16_t char16_t; //C2628
    typedef uint32_t char32_t; //C2628

    int main(int argc, char* argv[])
    {
        uint16_t x = 1; uint32_t y = 2;
        char16_t a = x;
        char32_t b = y;
        return 0;
    }
    ```

   Kodunuzu güncelleştirmek için, **typedef** bildirimlerini kaldırın ve bu adlarla çakışan diğer tanımlayıcıları yeniden adlandırın.

- **Tür olmayan şablon parametreleri**

   Tür olmayan şablon parametreleri içeren bazı kodlar artık açık şablon bağımsız değişkenleri sağladığınızda tür uyumluluğu için doğru denetlenir. Örneğin, aşağıdaki kod Visual Studio 'nun önceki sürümlerinde hata olmadan derlendi.

    ```cpp
    struct S1
    {
        void f(int);
        void f(int, int);
    };

    struct S2
    {
        template <class C, void (C::*Function)(int) const> void f() {}
    };

    void f()
    {
        S2 s2;
        s2.f<S1, &S1::f>();
    }
    ```

   Şablon parametre türü şablon bağımsız değişkeniyle eşleşmediğinden geçerli derleyici doğru bir hata verir (parametre bir const üyesinin işaretçisi, ancak f işlevi const değil):

    ```Output
    error C2893: Failed to specialize function template 'void S2::f(void)'note: With the following template arguments:note: 'C=S1'note: 'Function=S1::f'
    ```

   Kodunuzda bu hatayı gidermek için kullandığınız şablon bağımsız değişkeninin türünün şablon parametresinin belirtilen türüyle eşleştiğinden emin olun.

- **__declspec (Hizala)**

   Derleyici artık işlevlerde kabul etmez `__declspec(align)` . Bu yapı her zaman yoksayıldı, ancak şimdi bir derleyici hatası veriyor.

    ```cpp
    error C3323: 'alignas' and '__declspec(align)' are not allowed on function declarations
    ```

   Bu sorunu gidermek için, `__declspec(align)` işlev bildiriminden kaldırın. Hiçbir etkisi olmadığından, kaldırma hiçbir şeyi değiştirmez.

- **Özel durum işleme**

   Özel durum işlemede birkaç değişiklik vardır. İlk olarak, özel durum nesnelerinin kopyalanabilir veya taşınabilir olması gerekir. Aşağıdaki kod Visual Studio 2013 derlenmiş, ancak Visual Studio 2015 ' de derlenmiyor:

    ```cpp
    struct S
    {
    public:
        S();
    private:
        S(const S &);
    };

    int main()
    {
        throw S(); // error
    }
    ```

   Bu sorun, kopya oluşturucusunun özel olması, bu nedenle bir özel durumu işlemenin normal sırasında nesne olduğu gibi kopyalanamaz. Kopya Oluşturucu **Açık**olarak bildirildiğinde aynı durum geçerlidir.

    ```cpp
    struct S
    {
        S();
        explicit S(const S &);
    };

    int main()
    {
        throw S(); // error
    }
    ```

   Kodunuzu güncelleştirmek için, özel durum nesnenizin kopya oluşturucusunun **ortak** olduğundan ve **Açık**olarak işaretlenmemiş olduğundan emin olun.

   Bir özel durumu değere göre yakalamak Ayrıca özel durum nesnesinin kopyalanabilir olmasını gerektirir. Aşağıdaki kod Visual Studio 2013 derlenmiş, ancak Visual Studio 2015 ' de derlenmiyor:

    ```cpp
    struct B
    {
    public:
        B();
    private:
        B(const B &);
    };

    struct D : public B {};

    int main()
    {
        try
        {
        }
        catch (D d) // error
        {
        }
    }
    ```

   **Catch** için parametre türünü bir başvuruya dönüştürerek bu sorunu çözebilirsiniz.

    ```cpp
    catch (D& d)
    {
    }
    ```

- **Dize sabit değerleri ve ardından makrolar**

   Derleyici artık Kullanıcı tanımlı değişmez değerleri desteklemektedir. Sonuç olarak, herhangi bir boşluk olmadan makro tarafından izlenen dize sabit değerleri, Kullanıcı tanımlı değişmez değerler olarak yorumlanır ve bu da hata veya beklenmedik sonuçlar doğurabilir. Örneğin, önceki derleyicilerde aşağıdaki kod başarıyla derlendi:

    ```cpp
    #define _x "there"
    char* func() {
        return "hello"_x;
    }
    int main()
    {
        char * p = func();
        return 0;
    }
    ```

   Derleyici bu kodu bir "Hello" dize sabit değeri olarak, ardından "orada" olarak genişletilen bir makro ve iki dize değişmez değerlerini de bir tane olarak yorumlar. Visual Studio 2015 ' de, derleyici bu sırayı Kullanıcı tanımlı değişmez değer olarak yorumlar, ancak tanımlı eşleşen kullanıcı tanımlı sabit değer olmadığından `_x` bir hata verir.

    ```Output
    error C3688: invalid literal suffix '_x'; literal operator or literal operator template 'operator ""_x' not found
    note: Did you forget a space between the string literal and the prefix of the following string literal?
    ```

   Bu sorunu gidermek için, dize sabiti ve makro arasına bir boşluk ekleyin.

- **Bitişik dize sabit değerleri**

   Benzer şekilde, dize ayrıştırması içindeki ilgili değişiklikler nedeniyle, herhangi bir boşluk olmadan bitişik dize değişmez değerleri (geniş veya dar karakter dizesi sabit değerleri), daha önceki Vizaul C++ sürümlerinde tek bir birleştirilmiş dize olarak yorumlanmıştı. Visual Studio 2015 ' de, artık iki dize arasına boşluk eklemeniz gerekir. Örneğin, aşağıdaki kod değiştirilmelidir:

    ```cpp
    char * str = "abc""def";
    ```

   Bu sorunu onarmak için iki dize arasına bir boşluk ekleyin:

    ```cpp
    char * str = "abc" "def";
    ```

- **Yeni yerleştirme ve silme**

   C++ 14 standardı ile uyumlu hale getirmek için **Delete** işlecinde bir değişiklik yapılmıştır. Standartlar değişikliğinin ayrıntıları, [C++ boyutunda ayırmayı kaldırma](https://isocpp.org/files/papers/n3778.html)' da bulunabilir. Değişiklikler, bir boyut parametresi alan Global **Delete** işlecinin bir formunu ekler. Son değişiklik, daha önce aynı imzaya sahip bir işleç **silme** işlemi ( **Yeni bir yerleştirme** işleçle karşılık gelen) kullandığınızda bir derleyici hatası (C2956 ' in, derleyicinin uygun bir eşleşen **silme** işlecini belirlemeyi denediği koddaki konum) ile karşılaşırsınız.

   İşlev, `void operator delete(void *, size_t)` c++ 11 ' deki **yerleştirme yeni** işlevine karşılık gelen bir **yerleşim silme** işleçiydi `void * operator new(size_t, size_t)` . C++ 14 boyutunda ayırmayı kaldırma ile, bu Delete işlevi artık *olağan bir ayırmayı kaldırma işlevidir* (Global **Delete** işleci). Standart, yeni bir yerleşim kullanılması karşılık gelen bir silme işlevini arar ve normal bir ayırmayı kaldırma işlevi bulursa programın hatalı biçimlendirilmiş olması gerekir.

   Örneğin, kodunuzun hem **yerleştirmesini** hem de bir **yerleşimi silmeyi**tanımladığını varsayalım:

    ```cpp
    void * operator new(std::size_t, std::size_t);
    void operator delete(void*, std::size_t) noexcept;
    ```

   Bu sorun, tanımladığınız bir **yerleşim silme** işleci ve yeni global boyutlu **silme** işleci arasındaki işlev imzalarındaki eşleşme nedeniyle oluşur. `size_t`Herhangi bir **yerleştirme New** ve **Delete** işleçleri için dışında farklı bir tür kullanıp kullanmayacağınızı göz önünde bulundurun. `size_t` **Typedef** 'in türü DERLEYICIYE bağımlıdır; MSVC içinde **işaretsiz int** için bir **typedef** . İyi bir çözüm, şöyle bir numaralandırılmış tür kullanmaktır:

    ```cpp
    enum class my_type : size_t {};
    ```

   Ardından, **yeni yerleştirme** tanımınızı değiştirin ve bu türü, yerine ikinci bağımsız değişken olarak kullanmak için **silin** `size_t` . Ayrıca yeni bir türü geçirmek (örneğin, `static_cast<my_type>` tam sayı değerinden dönüştürmek için kullanarak) ve **Yeni** ve **silme** tanımını tam sayı türüne dönüştürmek için yeni yerleştirme için yapılan çağrıları güncelleştirmeniz gerekir. Bunun için bir **enum** kullanmanız gerekmez; üye içeren bir sınıf türü `size_t` de çalışır.

   Alternatif bir çözüm de **yeni yerleşimi** tamamen ortadan kaldırabilmeyebilirsiniz. Kodunuz, yerleştirme bağımsız değişkeninin ayrılan veya Silinen nesnenin boyutu olduğu bir bellek havuzunu uygulamak için **yeni yerleştirme** kullanıyorsa, boyutu kaldırma özelliği kendi özel bellek havuzu kodunuzu değiştirmek için uygun olabilir ve yerleştirme işlevlerinin kurtulabileceği ve yerleştirme işlevleri yerine kendi iki bağımsız değişkenli **silme** işlecini kullanmanız yeterlidir.

   Kodunuzu hemen güncelleştirmek istemiyorsanız, derleyici seçeneğini kullanarak eski davranışa dönüştürebilirsiniz `/Zc:sizedDealloc-` . Bu seçeneği kullanırsanız, iki bağımsız değişken silme işlevi yoktur ve **yerleştirme silme** işleçle bir çakışmaya neden olmaz.

- **Birleşim veri üyeleri**

   Birleşimlerin veri üyeleri artık başvuru türlerine sahip olamaz. Aşağıdaki kod Visual Studio 2013 içinde başarıyla derlendi, ancak Visual Studio 2015 ' de hata veriyor.

    ```cpp
    union U1
    {
        const int i;
    };
    union U2
    {
        int & i;
    };
    union U3
    {
        struct { int & i; };
    };
    ```

   Yukarıdaki kod aşağıdaki hataları üretir:

    ```Output
    test.cpp(67): error C2625: 'U2::i': illegal union member; type 'int &' is reference type
    test.cpp(70): error C2625: 'U3::i': illegal union member; type 'int &' is reference type
    ```

   Bu sorunu gidermek için başvuru türlerini bir işaretçiye ya da değere değiştirin. Türü bir işaretçi olarak değiştirmek, birleşim alanını kullanan kodda değişiklik yapılmasını gerektirir. Kodu bir değere değiştirmek, birleşimde depolanan verileri değiştirecek, bu da birleşim türlerindeki alanlar aynı belleği paylaştığından diğer alanları etkiler. Değerin boyutuna bağlı olarak, birleşim boyutunu da değiştirebilir.

- Anonim birleşimler artık standart ile daha uyumlu. Derleyicinin önceki sürümleri anonim birleşimler için açık bir Oluşturucu ve yıkıcı oluşturdu. Derleyici tarafından üretilen bu işlevler, Visual Studio 2015 ' de silinir.

    ```cpp
    struct S
    {
        S();
    };

    union
    {
        struct
        {
            S s;
        };
    } u; // C2280
    ```

   Yukarıdaki kod, Visual Studio 2015 ' de aşağıdaki hatayı üretir:

    ```cpp
    error C2280: '<unnamed-type-u>::<unnamed-type-u>(void)': attempting to reference a deleted function
    note: compiler has generated '<unnamed-type-u>::<unnamed-type-u>' here
    ```

   Bu sorunu çözmek için oluşturucuya ve/veya yıkıcıya ait tanımlarınızı belirtin.

    ```cpp
    struct S
    {
        // Provide a default constructor by adding an empty function body.
        S() {}
    };

    union
    {
        struct
        {
            S s;
        };
    } u;
    ```

- **Anonim yapılar içeren birleşimler**

   Standart ile uyumlu olması için, Birleşimlerdeki anonim yapıların üyeleri için çalışma zamanı davranışı değişmiştir. Bir Union içindeki anonim yapı üyeleri için Oluşturucu artık böyle bir birleşim oluşturulduğunda örtük olarak çağrılmaz. Ayrıca, birleşim kapsam dışına geçtiğinde, bir Union içindeki anonim yapı üyeleri için yıkıcı artık örtük olarak çağrılmaz. Bir UNION U 'nın yok edicisi olan adlandırılmış üye yapısını içeren anonim bir yapı içerdiği aşağıdaki kodu göz önünde bulundurun.

    ```cpp
    #include <stdio.h>
    struct S
    {
        S() { printf("Creating S\n"); }
        ~S() { printf("Destroying S\n"); }
    };
    union U
    {
        struct {
            S s;
        };
        U() {}
        ~U() {}
    };

    void f()
    {
        U u;
        // Destructor implicitly called here.
    }

    int main()
    {
        f();

        char s[1024];
        printf("Press any key.\n");
        gets_s(s);
        return 0;
    }
    ```

   Visual Studio 2013 ' de, birleşim oluşturulduğunda for için oluşturucu çağrılır ve f işlevi için yığın temizlendiğinde, for için yıkıcısı çağrılır. Ancak Visual Studio 2015 ' de, Oluşturucu ve yıkıcısı çağrılmaz. Derleyici bu davranış değişikliği hakkında bir uyarı verir.

    ```Output
    warning C4587: 'U::s': behavior change: constructor is no longer implicitly calledwarning C4588: 'U::s': behavior change: destructor is no longer implicitly called
    ```

   Özgün davranışı geri yüklemek için anonim yapıya bir ad verin. Anonim olmayan yapıların çalışma zamanı davranışı, derleyici sürümünden bağımsız olarak aynıdır.

    ```cpp
    #include <stdio.h>

    struct S
    {
        S() { printf("Creating S.\n"); }
        ~S() { printf("Destroying S\n"); }
    };
    union U
    {
        struct
        {
            S s;
        } namedStruct;
        U() {}
        ~U() {}
    };

    void f()
    {
        U u;
    }

    int main()
    {
        f();

        char s[1024];
        printf("Press any key.\n");
        gets_s(s);
        return 0;
    }
    ```

   Alternatif olarak, oluşturucuyu ve yıkıcı kodu yeni işlevlere taşımayı deneyin ve birleşim için oluşturucudan ve yıkıcıdan bu işlevlere çağrı ekleyin.

    ```cpp
    #include <stdio.h>

    struct S
    {
        void Create() { printf("Creating S.\n"); }
        void Destroy() { printf("Destroying S\n"); }
    };
    union U
    {
        struct
        {
            S s;
        };
        U() { s.Create(); }
        ~U() { s.Destroy(); }
    };

    void f()
    {
        U u;
    }

    int main()
    {
        f();

        char s[1024];
        printf("Press any key.\n");
        gets_s(s);
        return 0;
    }
    ```

- **Şablon çözünürlüğü**

   Şablonların ad çözümlemesinde değişiklikler yapılmıştır. C++ ' da, bir ad çözümlemesi için aday düşünürken, olası eşleşmeler olarak dikkate alınması gereken bir veya daha fazla ad geçersiz bir şablon örneği oluşturuyor olabilir. Bu geçersiz örneklemeler normalde derleyici hatalarına neden olmaz, SFINAE olarak bilinen bir ilke (değiştirme hatası bir hata değildir).

   Şimdi, SFINAE derleyicinin bir sınıf şablonunun özelleştirimini örneğini oluşturmak isterse, bu işlem sırasında oluşan hatalar derleyici hatalardır. Önceki sürümlerde, derleyici bu tür hataları yoksayar. Örneğin, aşağıdaki kodu göz önünde bulundurun:

    ```cpp
    #include <type_traits>

    template< typename T>
    struct S
    {
        S() = default;
        S(const S&);
        S(S& &);

        template< typename U, typename = typename std::enable_if< std::is_base_of< T, U> ::value> ::type>
        S(S< U> & &);
    };

    struct D;

    void f1()
    {
        S< D> s1;
        S< D> s2(s1);
    }

    struct B
    {
    };

    struct D : public B
    {
    };

    void f2()
    {
        S< D> s1;
        S< D> s2(s1);
    }
    ```

   Geçerli derleyici ile derlerseniz, şu hatayı alırsınız:

    ```Output
    type_traits(1110): error C2139: 'D': an undefined class is not allowed as an argument to compiler intrinsic type trait '__is_base_of'
    ..\t331.cpp(14): note: see declaration of 'D'
    ..\t331.cpp(10): note: see reference to class template instantiation 'std::is_base_of<T,U>' being compiled
    with
    [
        T=D,
        U=D
    ]
    ```

   Bunun nedeni, sınıfın is_base_of ilk çağırma noktasında `D` henüz tanımlanmamıştır.

   Bu durumda, bu, sınıf tanımlanmadığı sürece bu tür nitelikleri kullanmamalıdır. `B`Ve tanımlarını `D` kod dosyasının başlangıcına taşırsanız, hata çözülür. Tanımlar üst bilgi dosyalarında ise, herhangi bir sınıf tanımının sorunlu şablonlar kullanılmadan önce derlendiğinden emin olmak için, üst bilgi dosyalarına dahil etme deyimlerinin sırasını kontrol edin.

- **Kopya oluşturucular**

   Hem Visual Studio 2013 hem de Visual Studio 2015 ' de, derleyici Kullanıcı tanımlı bir taşıma oluşturucusuna sahipse ancak kullanıcı tanımlı kopya Oluşturucusu yoksa bir sınıf için bir kopya Oluşturucu oluşturur. Dev14 ' de, örtülü olarak oluşturulan bu kopya Oluşturucusu Ayrıca "= Delete" olarak işaretlenir.

<!--From here to VS_Update1 added 04/21/2017-->

- **extern "C" olarak bildirildiği ana, şimdi bir dönüş türü gerektiriyor.**

   Aşağıdaki kod artık C4430 oluşturur.

    ```cpp
    extern "C" __cdecl main(){} // C4430
    ```

   Hatayı onarmak için, dönüş türünü ekleyin:

    ```cpp
    extern "C" int __cdecl main(){} // OK
    ```

- **üye başlatıcısında TypeName öğesine izin verilmiyor**

   Aşağıdaki kod artık C2059 üretir:

    ```cpp
    template<typename T>
    struct S1 : public T::type
    {
        S1() : typename T::type() // C2059
        {
        }
    };

    struct S2 {
        typedef S2 type;
    };

    S1<S2> s;
    ```

   Hatayı düzeltemedi, `typename` başlatıcıdan kaldırın:

    ```cpp
    S1() : T::type() // OK
    ...
    ```

- **Açık özelleştirilmiş bir depolama sınıfı yok sayılır.**

   Aşağıdaki kodda, statik depolama sınıfı Belirleyicisi yoksayıldı

    ```cpp
    template <typename T>
    void myfunc(T h)
    {
    }

    template<>
    static void myfunc(double h) // static is ignored
    {
    }
    ```

- **Sınıf şablonu içindeki bir static_assert kullanılan sabit her zaman başarısız olur.**

   Aşağıdaki kod, ' nin `static_assert` her zaman başarısız olmasına neden olur:

    ```cpp
    template <size_t some_value>
    struct S1
    {
        static_assert(false, "default not valid"); // always invoked

    };

    //other partial specializations here
    ```

   Bu sorunu geçici olarak çözmek için, değeri bir **yapıda**sarmalayın:

    ```cpp
    template <size_t some_value>
    struct constant_false {
        static const bool value = false;
    };

    template <size_t some_value>
    struct S1
    {
        static_assert(constant_false<some_value>::value, "default not valid");
    };

    //other partial specializations here
    ```

- **İletme bildirimleri için uygulanan kurallar. (Yalnızca C için geçerlidir.)**

   Aşağıdaki kod artık C2065 üretir:

    ```cpp
    struct token_s;
    typedef int BOOL;
    typedef int INT;

    typedef int(*PFNTERM)(PTOKEN, BOOL, INT); // C2065: 'PTOKEN' : undeclared identifier
    ```

   Bu sorunu gidermek için doğru iletme bildirimlerini ekleyin:

    ```cpp
    struct token_s;
    typedef int BOOL;
    typedef int INT;

    // forward declarations:
    typedef struct token_s TOKEN;
    typedef TOKEN *PTOKEN;

    typedef int(*PFNTERM)(PTOKEN, BOOL, INT);
    ```

- **İşlev işaretçisi türlerinin daha tutarlı bir şekilde uygulanması**

   Aşağıdaki kod artık C2197 üretir:

    ```cpp
    typedef int(*F1)(int);
    typedef int(*F2)(int, int);

    void func(F1 f, int v1, int v2)
    {
        f(v1, v2); // C2197
    }
    ```

- **Aşırı yüklenmiş işlevlere belirsiz çağrılar**

   Aşağıdaki kod artık C266 üretir: ' N:: bind ': aşırı yüklenmiş işleve belirsiz çağrı

    ```cpp
    template<typename R, typename T, typename T1, typename A1>
    void bind(R(T::*)(T1), A1&&);

    namespace N
    {
        template <typename T, typename R, typename ... Tx>
        void bind(R(T::*)(Tx...), T* ptr);
    }

    using namespace N;

    class Manager
    {
    public:
        void func(bool initializing);

        void mf()
        {
            bind(&Manager::func, this); //C2668
        }
    };
    ```

   Hatayı onarmak için, çağrısını tam olarak niteleyebilirsiniz `bind: N::bind(...)` . Ancak, bu değişiklik bildirilmemiş bir tanımlayıcı (C2065) aracılığıyla bildiriminizde, bunun yerine **using** bildirimiyle düzeltilmesi uygun olabilir.

   Bu model genellikle ComPtr ve ad alanındaki diğer türler ile gerçekleşir `Microsoft::WRL` .

- **Yanlış adresini çözme**

   Aşağıdaki kod şu anda C2440 oluşturuyor: ' = ': ' Type * ' iken ' Type ' olarak dönüştürülemez. Hatayı düzelmek için & (tür) ile (tür) ve (&f ()) öğesini (f ()) olarak değiştirin.

    ```cpp
    // C
    typedef void (*type)(void);

    void f(int i, type p);
    void g(int);
    void h(void)
    {
        f(0, &(type)g);
    }

    // C++
    typedef void(*type)(void);

    type f();

    void g(type);

    void h()
    {
        g(&f());
    }
    ```

- **Dize sabit değeri sabit bir dizidir**

   Aşağıdaki kod artık C2664 oluşturuyor: ' void f (void *) ': bağımsız değişken 1, ' const char (*) [2] ' öğesinden ' void * ' öğesine dönüştürülemez

    ```cpp
    void f(void *);

    void h(void)
    {
        f(&__FUNCTION__);
        void *p = &"";
    }
    ```

   Hatayı onarmak için, işlev parametre türünü olarak değiştirin `const void*` veya ' ın gövdesini `h` Şu örneğe benzer şekilde değiştirin:

    ```cpp
    void h(void)
    {
        char name[] = __FUNCTION__;
        f( name);
        void *p = &"";
    }
    ```

- **C++ 11 UDL dizeleri**

   Aşağıdaki kod şimdi hata C3688 oluşturuyor: geçersiz sabit değer soneki ' L '; Sabit işleç veya sabit değer operatörü şablonu ' operator "" L ' bulunamadı

    ```cpp
    #define MACRO

    #define STRCAT(x, y) x\#\#y

    int main(){

        auto *val1 = L"string"MACRO;
        auto *val2 = L"hello "L"world";

        std::cout << STRCAT(L"hi ", L"there");
    }
    ```

   Hatayı onarmak için, bir boşluk eklemek üzere kodu değiştirin:

    ```cpp
    #define MACRO

    // Remove ##. Strings are automatically
    // concatenated so they aren't needed
    #define STRCAT(x, y) x y

    int main(){
        //Add space after closing quote
        auto *val1 = L"string" MACRO;
        auto *val2 = L"hello " L"world";

        std::cout << STRCAT(L"hi ", L"there");
    }
    ```

   Yukarıdaki örnekte, `MACRO` artık iki belirteç (bir makro tarafından izlenen bir dize) olarak ayrıştırılmaz. Artık tek bir belirteç UDL olarak ayrıştırılır. Aynı, daha önce L "" ve L "" olarak Ayrıştırılan ve artık L "" L ve "" olarak ayrıştırılabilen L "" L "" için geçerlidir.

   Dize birleştirme kuralları da standart ile uyumlu hale getirildi, yani L "a" "b", L "AB" ile eşdeğerdir. Visual Studio 'nun önceki sürümleri, dizelerin farklı karakter genişliğine birleştirmesini kabul etmedi.

- **C++ 11 boş karakter kaldırıldı**

   Aşağıdaki kod artık hata C2137: boş karakter sabiti oluşturuyor

    ```cpp
    bool check(wchar_t c){
        return c == L''; //implicit null character
    }
    ```

   Hatayı düzelttikten sonra, null değeri açık yapmak için kodu değiştirin:

    ```cpp
    bool check(wchar_t c){
        return c == L'\0';
    }
    ```

- **MFC özel durumları kopyalanabilir olmadıkları için değere göre yakalanamıyor**

   Bir MFC uygulamasında bulunan aşağıdaki kod artık hata C2316: ' ' olarak neden oluyor: yıkıcı ve/veya kopya Oluşturucu erişilemez olduğu veya silindiği için yakalanamaz

    ```cpp
    struct B {
    public:
        B();
    private:
        B(const B &);
    };

    struct D : public B {
    };

    int main()
    {
        try
        {
        }
        catch (D) // C2316
        {
        }
    }
    ```

   Kodu onarmak için, catch bloğunu olarak değiştirebilirsiniz `catch (const D &)` ancak daha iyi çözüm genellıkle MFC try/catch makrolarını kullanır.

- **hizalama artık bir anahtar sözcük**

   Aşağıdaki kod şimdi hata C2332: ' class ': etiket adı eksik. Kodu gidermek için, sınıfını yeniden adlandırmanız gerekir ya da sınıf aynı işi **Hizalama**ile yapıyorsa, yalnızca sınıfını yeni anahtar sözcükle değiştirmelisiniz.

    ```cpp
    class alignof{}
    ```

- **constexpr artık bir anahtar sözcük**

   Aşağıdaki kod artık hata C2059 oluşturuyor: sözdizimi hatası: ') '. Kodu onarmak için, "constexpr" olarak adlandırılan işlev veya değişken adlarını yeniden adlandırmanız gerekir.

    ```cpp
    int constexpr() {return 1;}
    ```

- **Taşınabilir türler const olamaz**

   Bir işlev, taşınması amaçlanan bir tür döndürdüğünde, dönüş türü **const**olmamalıdır.

- **Silinen kopya oluşturucular**

   Aşağıdaki kod artık C2280 'S:: S (S &&) ': silinmiş bir işleve başvurulmaya çalışılıyor:

    ```cpp
    struct S{
        S(int, int);
        S(const S&) = delete;
        S(S&&) = delete;
    };

    S s2 = S(2, 3); //C2280
    ```

   Hatayı onarmak için, için doğrudan başlatma kullanın `S2` :

    ```cpp
    struct S{
        S(int, int);
        S(const S&) = delete;
        S(S&&) = delete;
    };

    S s2 = {2,3}; //OK
    ```

- **Yalnızca bir lambda yakalaması olmadığında oluşturulan işlev işaretçisine dönüştürme**

   Aşağıdaki kod, Visual Studio 2015 ' de C2664 oluşturur.

    ```cpp
    void func(int(*)(int)) {}

    int main() {

        func([=](int val) { return val; });
    }
    ```

   Hatayı onarmak için yakalama listesinden ' ı kaldırın `=` .

- **Dönüştürme işleçleri içeren belirsiz çağrılar**

   Aşağıdaki kod artık hata C2440: ' tür cast ': 2 ' den 1 ' e dönüştürülemez:

    ```cpp
    struct S1 {
        S1(int);
    };

    struct S2 {
        operator S1();
        operator int();
    };

    void f(S2 s2)
    {
        (S1)s2;
    }
    ```

   Hatayı düzeltemedi, açıkça dönüştürme işlecini çağırın:

    ```cpp
    void f(S2 s2)
    {
        //Explicitly call the conversion operator
        s2.operator S1();
        // Or
        S1((int)s2);
    }
    ```

   Aşağıdaki kod şu anda C2593 hatasını veriyor: ' operator = ' belirsiz:

    ```cpp
    struct S1 {};

    struct S2 {
        operator S1&();
        operator S1() const;
    };

    void f(S1 *p, S2 s)
    {
        *p = s;
    }
    ```

   Hatayı düzeltemedi, açıkça dönüştürme işlecini çağırın:

    ```cpp
    void f(S1 *p, S2 s)
    {
        *p = s.operator S1&();
    }
    ```

- **Statik olmayan veri üyesi başlatma (NSDMı) içinde geçersiz kopya başlatmayı çözme**

   Aşağıdaki kod şu anda C2664:1:: S1 (S1 &&) ' hatası veriyor: ' bool ' değerinden ' const S1 & ' türüne dönüştürülemiyor:

    ```cpp
    struct S1 {
        explicit S1(bool);
    };

    struct S2 {
        S1 s2 = true; // error
    };
    ```

   Hatayı onarmak için, doğrudan başlatma kullanın:

    ```cpp
    struct S2 {
    S1 s1{true}; // OK
    };
    ```

- **Decltype deyimleri içindeki oluşturuculara erişme**

   Aşağıdaki kod artık C2248:: S ': sınıfının ' de belirtilen özel üyeye erişilemiyor:

    ```cpp
    class S {
        S();
    public:
        int i;
    };

    class S2 {
        auto f() -> decltype(S().i);
    };
    ```

   Hatayı onarmak için, içinde için bir arkadaş bildirimi ekleyin `S2` `S` :

    ```cpp
    class S {
        S();
        friend class S2; // Make S2 a friend
    public:
        int i;
    };
    ```

- **Lambda varsayılan ctor 'ı örtük olarak silinir**

   Aşağıdaki kod şimdi hata C3497 oluşturuyor: bir lambda örneği oluşturamazsınız:

    ```cpp
    void func(){
        auto lambda = [](){};

        decltype(lambda) other;
    }
    ```

   Hatayı düzeltemedi, çağrılacak varsayılan oluşturucunun gereksinimini ortadan kaldırın. Lambda hiçbir şey yakalamasa da bir işlev işaretçisine dönüşebilir.

- **Silinmiş bir atama işleci olan Lambdalar**

   Aşağıdaki kod artık C2280 hatasını veriyor:

    ```cpp
    #include <memory>
    #include <type_traits>

    template <typename T, typename D>
    std::unique_ptr<T, typename std::remove_reference<D &&>::type> wrap_unique(T *p, D &&d);

    void f(int i)
    {
        auto encodedMsg = wrap_unique<unsigned char>(nullptr, [i](unsigned char *p) {
        });
        encodedMsg = std::move(encodedMsg);
    }
    ```

   Hatayı onarmak için lambdası bir functor sınıfıyla değiştirin veya atama işlecini kullanma gereksinimini kaldırın.

- **Silinen kopya oluşturucusuna bir nesne taşınmaya çalışılıyor**

   Aşağıdaki kod şu anda C2280 hatasını veriyor: ' taşınabilir:: taşınabilir (const taşınabilir &) ': silinmiş bir işleve başvurulmaya çalışılıyor

    ```cpp
    struct moveable {

        moveable() = default;
        moveable(moveable&&) = default;
        moveable(const moveable&) = delete;
    };

    struct S {
        S(moveable && m) :
            m_m(m)//copy constructor deleted
        {}
        moveable m_m;
    };
    ```

   Hatayı onarmak için şunu kullanın `std::move` :

    ```cpp
    S(moveable && m) :
        m_m(std::move(m))
    ```

- **Yerel sınıf, daha sonra aynı işlevde tanımlanmış diğer yerel sınıfa başvuramaz**

   Aşağıdaki kod şu anda C2079 hatasını oluşturuyor: ' ' Main:: S2 ' tanımsız yapısını kullanıyor

    ```cpp
    int main()
    {
        struct S2;
        struct S1 {
            void f() {
                S2 s;
            }
        };
        struct S2 {};
    }
    ```

   Hatayı onarmak için, şu tanımı yukarı taşıyın `S2` :

    ```cpp
    int main()
    {
        struct S2 { //moved up
        };

    struct S1 {
        void f() {
            S2 s;
            }
        };
    }
    ```

- **Türetilmiş ctor gövdesinde korunan bir temel ctor çağrılamaz.**

   Aşağıdaki kod artık hata C2248:1:: S1 ': sınıfın 1 ' de belirtilen korumalı üyeye erişilemiyor

    ```cpp
    struct S1 {
    protected:
        S1();
    };

    struct S2 : public S1 {
        S2() {
            S1();
        }
    };
    ```

   Hatayı onarmak için, `S2` öğesinden öğesine çağrıyı kaldırın `S1()` ve gerekirse onu başka bir işleve koyun.

- **{}işaretçiye dönüştürmeyi önler**

   Aşağıdaki kod şu anda C2439 ' i oluşturuyor::p ': üye başlatılamadı

    ```cpp
    struct S {
        S() : p({ 0 }) {}
        void *p;
    };
    ```

   Hatayı gidermek için, `0` Bu örnekte gösterildiği gibi, ya da başka bir şekilde bunun yerine **nullptr** kullanın:

    ```cpp
    struct S {
        S() : p(nullptr) {}
        void *p;
    };
    ```

- **Parantez ile yanlış makro tanımı ve kullanımı**

   Aşağıdaki örnek şu anda C2008 hatasını oluşturuyor: '; ': makro tanımında beklenmiyor

    ```cpp
    #define A; //cause of error

    struct S {
        A(); // error
    };
    ```

   Sorunu gidermek için en üstteki satırı şu şekilde değiştirin`#define A();`

   Aşağıdaki kod hata C2059 oluşturur: sözdizimi hatası: ') '

    ```cpp
    //notice the space after 'A'
    #define A () ;

    struct S {
        A();
    };
    ```

   Kodu onarmak için ve () arasındaki boşluğu kaldırın.

   Aşağıdaki kod C2091 hatasını üretir: işlev işlevi döndürüyor:

    ```cpp
    #define DECLARE void f()

    struct S {
        DECLARE();
    };
    ```

   Hatayı onarmak için, S: içinde BILDIRDIKTEN sonra ayraçları kaldırın `DECLARE;` .

   Aşağıdaki kod C2062 hatasını üretir: ' int ' türü beklenmiyor

    ```cpp
    #define A (int)

    struct S {
        A a;
    };
    ```

   Sorunu gidermek için aşağıdaki gibi tanımlayın `A` :

    ```cpp
    #define A int
    ```

- **Bildirimlerde ek parlar**

   Aşağıdaki kod C2062 hatasını üretir: ' int ' türü beklenmiyor

    ```cpp
    struct S {
        int i;
        (int)j;
    };
    ```

   Hatayı gidermek için etrafındaki parantezleri kaldırın `j` . Parantezler açıklık için gerekliyse, bir **typedef**kullanın.

- **Derleyici tarafından oluşturulan oluşturucular ve __declspec (novtable)**

   Visual Studio 2015 ' de, sanal temel sınıflar içeren soyut sınıfların derleyicinin ürettiği satır içi oluşturucuların, ile birlikte kullanıldığında yanlış kullanımını açığa çıkarmasına neden olabilecek bir olasılık daha vardır `__declspec(novtable)` `__declspec(dllimport)` .

- **otomatik olarak doğrudan liste başlatılmasında tek bir ifade gerekiyor**

   Aşağıdaki kod şu anda C3518: ' testPositions ' hatası veriyor: doğrudan liste başlatma bağlamında ' Auto ' türü yalnızca tek bir başlatıcı ifadeden çıkarılabilir

    ```cpp
    auto testPositions{
        std::tuple<int, int>{13, 33},
        std::tuple<int, int>{-23, -48},
        std::tuple<int, int>{38, -12},
        std::tuple<int, int>{-21, 17}
    };
    ```

   Hatayı düzeltemedi, bir olasılık `testPositions` aşağıdaki şekilde başlatılacak:

    ```cpp
    std::tuple<int, int> testPositions[]{
        std::tuple<int, int>{13, 33},
        std::tuple<int, int>{-23, -48},
        std::tuple<int, int>{38, -12},
        std::tuple<int, int>{-21, 17}
    };
    ```

- **Türler ve is_convertible için türlere işaretçiler denetleniyor**

   Aşağıdaki kod şu anda statik onaylama işlemi başarısız olmasına neden olur.

    ```cpp
    struct B1 {
    private:
        B1(const B1 &);
    };
    struct B2 : public B1 {};
    struct D : public B2 {};

    static_assert(std::is_convertible<D, B2>::value, "fail");
    ```

   Hatayı onarmak için, ' yi, `static_assert` işaretçilerle ve ile karşılaştırılmasını sağlayacak şekilde değiştirin `D` `B2` :

    ```cpp
    static_assert(std::is_convertible<D*, B2*>::value, "fail");
    ```

- **__declspec (novtable) bildirimleri tutarlı olmalıdır**

   `__declspec`bildirimlerin tüm kitaplıklar arasında tutarlı olması gerekir. Aşağıdaki kod artık tek tanımlı bir kural (ODR) ihlaline neden olacak:

    ```cpp
    //a.cpp
    class __declspec(dllexport)
        A {
    public:
        A();
        A(const A&);
        virtual ~A();
    private:
        int i;
    };

    A::A() {}
    A::~A() {}
    A::A(const A&) {}

    //b.cpp
    // compile with cl.exe /nologo /LD /EHsc /Osx b.cpp
    #pragma comment(lib, "A")
    class __declspec(dllimport) A
    {
    public: A();
            A(const A&);
            virtual ~A();
    private:
        int i;
    };

    struct __declspec(novtable) __declspec(dllexport) B
        : virtual public A {
        virtual void f() = 0;
    };

    //c.cpp
    #pragma comment(lib, "A")
    #pragma comment(lib, "B")
    class __declspec(dllimport) A
    {
    public:
        A();
        A(const A&);
        virtual ~A();
    private:
        int i;
    };
    struct  /* __declspec(novtable) */ __declspec(dllimport) B // Error. B needs to be novtable here also.
        : virtual public A
    {
        virtual void f() = 0;
    };

    struct C : virtual B
    {
        virtual void f();
    };

    void C::f() {}
    C c;
    ```

### <a name="conformance-improvements-in-update-1"></a><a name="VS_Update1"></a>Güncelleştirme 1 ' deki uyumluluk geliştirmeleri

- **Özel sanal temel sınıflar ve dolaylı devralma**

   Derleyicinin önceki sürümlerinde, türetilmiş bir sınıfın dolaylı olarak türetilen temel sınıfların üye işlevlerini çağırması için izin verilir `private virtual` . Bu eski davranış yanlıştı ve C++ standardına uymuyor. Derleyici artık bu şekilde yazılmış kodu kabul etmez ve sonuç olarak derleyici hatası C2280 yayınlar.

    ```Output
    error C2280: 'void *S3::__delDtor(unsigned int)': attempting to reference a deleted function
    ```

   Örnek (önce)

    ```cpp
    class base
    {
    protected:
        base();
        ~base();
    };

    class middle : private virtual base {}; class top : public virtual middle {};

    void destroy(top *p)
    {
        delete p;  //
    }
    ```

   Örnek (sonrasında)

    ```cpp
    class base;  // as above

    class middle : protected virtual base {};
    class top : public virtual middle {};

    void destroy(top *p)
    {
        delete p;
    }
    ```

   \-veya

    ```cpp
    class base;  // as above

    class middle : private virtual base {};
    class top : public virtual middle, private virtual bottom {};

    void destroy(top *p)
    {
        delete p;
    }
    ```

- **Yeni işleç New ve delete işleci**

   Derleyicinin önceki sürümleri, üyenin üye olmayan **işlecine** **ve üyenin statik** olarak bildirilmesini ve genel ad alanından farklı ad alanlarında bildirilmesine izin verilir.  Bu eski davranış, programın programladığı **Yeni** veya **silme** işletmeni uygulamasını çağırmayacağı ve sessiz bozuk çalışma zamanı davranışına neden olan bir risk oluşturdu. Derleyici artık bu şekilde yazılmış kodu kabul etmez ve bunun yerine derleyici hatası C2323 yayınlar.

    ```Output
    error C2323: 'operator new': non-member operator new or delete functions may not be declared static or in a namespace other than the global namespace.
    ```

   Örnek (önce)

    ```cpp
    static inline void * __cdecl operator new(size_t cb, const std::nothrow_t&)  // error C2323
    ```

   Örnek (sonrasında)

    ```cpp
    void * __cdecl operator new(size_t cb, const std::nothrow_t&)  // removed 'static inline'
    ```

   Ayrıca, derleyici belirli bir tanılama sunmasa da, **Yeni** satır içi işleç hatalı biçimlendirilmiş olarak kabul edilir.

- **Sınıf olmayan türlerde ' operator *Type*() ' (Kullanıcı tanımlı dönüştürme) çağrılıyor**

   Derleyicinin önceki sürümleri ' işleç *türü*() ', sessizce yoksayılıp, sınıf olmayan türlerde çağrılabilir. Bu eski davranış sessiz hatalı kod oluşturma riskini oluşturdu, bu durum öngörülemeyen çalışma zamanı davranışına neden oldu. Derleyici artık bu şekilde yazılmış kodu kabul etmez ve bunun yerine derleyici hatası C2228 yayınlar.

    ```Output
    error C2228: left of '.operator type' must have class/struct/union
    ```

   Örnek (önce)

    ```cpp
    typedef int index_t;
    void bounds_check(index_t index);
    void login(int column)
    {
        bounds_check(column.operator index_t());  // error C2228
    }
    ```

   Örnek (sonrasında)

    ```cpp
    typedef int index_t;
    void bounds_check(index_t index);
    void login(int column)
    {
        bounds_check(column);  // removed cast to 'index_t', 'index_t' is an alias of 'int'
    }
    ```

- **Ayrıntılı tür tanımlayıcıda gereksiz TypeName**

   Derleyicinin önceki sürümlerinde, bir ayrıntılı tür tanımlayıcıda **TypeName** değeri verilir, ancak bu şekilde yazılan kod anlam yanlış olur. Derleyici artık bu şekilde yazılmış kodu kabul etmez ve bunun yerine derleyici hatası C3406 yayınlar.

    ```Output
    error C3406: 'typename' cannot be used in an elaborated type specifier
    ```

   Örnek (önce)

    ```cpp
    template <typename class T>
    class container;
    ```

   Örnek (sonrasında)

    ```cpp
    template <class T>  // alternatively, could be 'template <typename T>'; 'typename' is not elaborating a type specifier in this case
    class container;
    ```

- **Bir başlatıcı listesinden dizilere ait tür kesintisi**

   Derleyicinin önceki sürümleri Başlatıcı listesinden dizilerin tür kesintiyi desteklemiyor. Derleyici artık bu tür kesintiyi destekler ve sonuç olarak, başlatıcı listeleri kullanılarak işlev şablonlarına yapılan çağrılar artık belirsiz olabilir veya derleyicinin önceki sürümlerinden farklı bir aşırı yükleme seçilebilir. Bu sorunları çözmek için program artık programcı tarafından hedeflenen aşırı yüklemeyi açıkça belirtmelidir.

   Bu yeni davranış, aşırı yükleme çözümüne geçmiş aday kadar eşit olan ek bir aday göz önünde bulundurmasına neden olursa, çağrı belirsiz hale gelir ve derleyici sonuç olarak derleyici hatası C2668 yayınlar.

    ```Output
    error C2668: 'function' : ambiguous call to overloaded function.
    ```

   Örnek 1: aşırı yüklenmiş işleve belirsiz çağrı (önce)

    ```cpp
    // In previous versions of the compiler, code written in this way would unambiguously call f(int, Args...)
    template < typename... Args>
    void f(int, Args...);  //

    template < int N, typename... Args>
    void f(const int(&)[N], Args...);

    int main()
    {
        // The compiler now considers this call ambiguous, and issues a compiler error
         f({ 3 });   error C2668 : 'f' ambiguous call to overloaded function
    }
    ```

   Örnek 1: aşırı yüklenmiş işleve belirsiz çağrı (sonrasında)

    ```cpp
    template < typename... Args>
    void f(int, Args...);  //

    template < int N, typename... Args>
    void f(const int(&)[N], Args...);

    int main()
    {
        // To call f(int, Args...) when there is just one expression in the initializer list, remove the braces from it.
        f(3);
    }
    ```

   Bu yeni davranış, aşırı yüklenmiş adayından daha iyi eşleşen ek bir aday göz önünde bulundurmasına neden olur. çağrı yeni aday için kesin bir şekilde çözümlenir ve bu da program davranışından farklı bir şekilde bir değişikliğe neden olur.

   Örnek 2: aşırı yükleme çözünürlüğünde değişiklik (önce)

    ```cpp
    // In previous versions of the compiler, code written in this way would unambiguously call f(S, Args...)
    struct S
    {
        int i;
        int j;
    };

    template < typename... Args>
    void f(S, Args...);

    template < int N, typename... Args>
    void f(const int *&)[N], Args...);

    int main()
    {
        // The compiler now resolves this call to f(const int (&)[N], Args...) instead
         f({ 1, 2 });
    }
    ```

   Örnek 2: aşırı yükleme çözünürlüğünde değişiklik (sonrasında)

    ```cpp
    struct S;  // as before

    template < typename... Args>
    void f(S, Args...);

    template < int N, typename... Args>
    void f(const int *&)[N], Args...);

    int main()
    {
        // To call f(S, Args...), perform an explicit cast to S on the initializer list.
        f(S{ 1, 2 });
    }
    ```

- **Switch ifadesinin uyarılarını geri yükleme**

   Derleyicinin önceki bir sürümü, **Switch** deyimleriyle ilgili bazı uyarıları kaldırdı; Bu uyarılar artık geri yüklendi. Derleyici artık geri yüklenen uyarıları verir ve belirli durumlar (varsayılan durum dahil) ile ilgili uyarılar artık switch ifadesinin son satırı yerine sorunlu durumu içeren satıra çıkarılır. Artık bu uyarıların geçmiş dışında farklı satırlarda verilmesi sonucunda, daha önce kullanılarak gizlenen uyarılar `#pragma warning(disable:####)` amaçlanan şekilde gizlemeyebilir. Bu uyarıların istendiği şekilde görüntülenmesini sağlamak için, `#pragma warning(disable:####)` yönergeyi ilk sorunlu durumun üzerindeki bir satıra taşımak gerekebilir. Geri yüklenen uyarılar aşağıda verilmiştir:

    ```Output
    warning C4060: switch statement contains no 'case' or 'default' labels
    ```

    ```Output
    warning C4061: enumerator 'bit1' in switch of enum 'flags' is not explicitly handled by a case label
    ```

    ```Output
    warning C4062: enumerator 'bit1' in switch of enum 'flags' is not handled
    ```

    ```Output
    warning C4063: case 'bit32' is not a valid value for switch of enum 'flags'
    ```

    ```Output
    warning C4064: switch of incomplete enum 'flags'
    ```

    ```Output
    warning C4065: switch statement contains 'default' but no 'case' labels
    ```

    ```Output
    warning C4808: case 'value' is not a valid value for switch condition of type 'bool'
    ```

    ```Output
    Warning C4809: switch statement has redundant 'default' label; all possible 'case' labels are given
    ```

   C4063 (öncesi) örneği

    ```cpp
    class settings
    {
    public:
        enum flags
        {
            bit0 = 0x1,
            bit1 = 0x2,
            ...
        };
        ...
    };

    int main()
    {
        auto val = settings::bit1;

        switch (val)
        {
        case settings::bit0:
            break;

        case settings::bit1:
            break;

             case settings::bit0 | settings::bit1:  // warning C4063
                break;
        }
    };
    ```

   C4063 örneği (sonra)

    ```cpp
    class settings { ... };  // as above
    int main()
    {
        // since C++11, use std::underlying_type to determine the underlying type of an enum
        typedef std::underlying_type< settings::flags> ::type flags_t;

            auto val = settings::bit1;

        switch (static_cast< flags_t> (val))
        {
        case settings::bit0:
            break;

        case settings::bit1:
            break;

        case settings::bit0 | settings::bit1:  // ok
            break;
        }
    };
    ```

   Diğer geri yüklenen uyarıların örnekleri belgelerde verilmiştir.

- **#include: PathName 'teki '.. ' üst dizin belirticisinin kullanımı** (yalnızca etkiler `/Wall` `/WX` )

   Derleyicinin önceki sürümleri, '.. ' üst dizin belirticisinin kullanımını algılamadı `#include`yönergelerinin yol. Bu şekilde yazılan kod, genellikle proje ile ilgili yollar kullanarak proje dışında var olan üst bilgilerin dahil edilmesine yöneliktir. Bu eski davranış, programın, programcı tarafından amaçlanan farklı bir kaynak dosyası ekleyerek derlenebilecek veya bu göreli yolların diğer derleme ortamlarına taşınmayan bir risk oluşturdu. Derleyici artık kod Programlayıcısının bu şekilde yazıldığını algılar ve bildirir ve etkinleştirilirse isteğe bağlı bir derleyici uyarısı C4464 yayınlar.

    ```Output
    warning C4464: relative include path contains '..'
    ```

   Örnek (önce)

    ```cpp
    #include "..\headers\C4426.h"  // emits warning C4464
    ```

   Örnek (sonrasında)

    ```cpp
    #include "C4426.h"  // add absolute path to 'headers\' to your project's include directories
    ```

   Ayrıca, derleyici belirli bir tanılama yapmasa da, projenizin içerme dizinlerini belirtmek için ".." üst dizin belirticisinin kullanılmaması önerilir.

- **#pragma optimize () üst bilgi dosyasının sonunu genişletiyor** (yalnızca etkiler `/Wall` `/WX` )

   Önceki derleyicinin sürümleri, bir çeviri birimi içinde yer alan bir üst bilgi dosyası ile çıkış yapan iyileştirme bayrağı ayarlarında yapılan değişiklikleri algılamadı. Derleyici artık, kod programcısında bu şekilde yazılmış kodu algılar ve bildirir ve etkinleştiriliyorsa, soruna neden olan isteğe bağlı bir derleyici uyarısı C4426 yayınlar `#include` . Bu uyarı yalnızca, derleyici için komut satırı bağımsız değişkenleri tarafından ayarlanan iyileştirme bayraklarıyla çakışırsa değişiklikler yapılır.

    ```Output
    warning C4426: optimization flags changed after including header, may be due to #pragma optimize()
    ```

   Örnek (önce)

    ```cpp
    // C4426.h
    #pragma optimize("g", off)
    ...
    // C4426.h ends

    // C4426.cpp
    #include "C4426.h"  // warning C4426
    ```

   Örnek (sonrasında)

    ```cpp
    // C4426.h
    #pragma optimize("g", off)
                ...
    #pragma optimize("", on)  // restores optimization flags set via command-line arguments
    // C4426.h ends

    // C4426.cpp
    #include "C4426.h"
    ```

- **Eşleşmeyen #pragma warning (push)** ve **#pragma warning (pop)** (yalnızca etkiler `/Wall` `/WX` )

   Derleyicinin önceki sürümleri `#pragma warning(push)` `#pragma warning(pop)` , farklı bir kaynak dosyadaki durum değişiklikleriyle eşleştirmekte olan durum değişikliklerinin algılanmadığını algılamadı, ancak nadiren tasarlanmıştır. Bu eski davranış, programın, programcı tarafından amaçlanan farklı bir uyarı kümesiyle derlenmesi, büyük olasılıkla sessiz hatalı çalışma zamanı davranışına neden olduğundan bir risk oluşturdu. Derleyici artık kod programcısının bu şekilde yazılmış olduğunu algılar ve bildirir ve etkinleştirilirse, isteğe bağlı bir derleyici uyarısı C5031, bu şekilde eşleşen konuma sorun verir `#pragma warning(pop)` . Bu uyarı, karşılık gelen #pragma uyarının (push) konumuna başvuran bir nota sahiptir.

    ```Output
    warning C5031: #pragma warning(pop): likely mismatch, popping warning state pushed in different file
    ```

   Örnek (önce)

    ```cpp
    // C5031_part1.h
    #pragma warning(push)
    #pragma warning(disable:####)
    ...
    // C5031_part1.h ends without #pragma warning(pop)

    // C5031_part2.h
    ...
    #pragma warning(pop)  // pops a warning state not pushed in this source file
    ...
    // C5031_part1.h ends

    // C5031.cpp
    #include "C5031_part1.h" // leaves #pragma warning(push) 'dangling'
    ...
    #include "C5031_part2.h" // matches 'dangling' #pragma warning(push), resulting in warning C5031
    ...
    ```

   Örnek (sonrasında)

    ```cpp
    // C5031_part1.h
    #pragma warning(push)
    #pragma warning(disable:####)
    ...
    #pragma warning(pop)  // pops the warning state pushed in this source file
    // C5031_part1.h ends without #pragma warning(pop)

    // C5031_part2.h
    #pragma warning(push)  // pushes the warning state pushed in this source file
    #pragma warning(disable:####)
    ...
    #pragma warning(pop)
    // C5031_part1.h ends

    // C5031.cpp
    #include "C5031_part1.h" // #pragma warning state changes are self-contained and independent of other source files or their #include order.
    ...
    #include "C5031_part2.h"
    ...
    ```

   Yaygın olarak, bu şekilde yazılan kod bazen bilerek yapılır. Bu şekilde yazılan kod, sırayla yapılan değişikliklere duyarlıdır `#include` ; mümkün olduğunda, kaynak kodu dosyalarının uyarı durumunu kendi kendine içeren bir şekilde yönetmesini öneririz.

- **Eşleşmeyen #pragma Uyarısı (gönderim)** (yalnızca etkiler `/Wall` `/WX` )

   Derleyicinin önceki sürümleri, `#pragma warning(push)` bir çeviri biriminin sonunda eşleşmeyen durum değişikliklerini algılamadı. Derleyici artık kod programcısının bu şekilde yazıldığını algılar ve bildirir ve etkinleştirilirse, eşleşmeyen bir derleyici uyarı C5032 `#pragma warning(push)` . Bu uyarı yalnızca çeviri biriminde derleme hatası yoksa verilir.

    ```Output
    warning C5032: detected #pragma warning(push) with no corresponding #pragma warning(pop)
    ```

   Örnek (önce)

    ```cpp
    // C5032.h
    #pragma warning(push)
    #pragma warning(disable:####)
    ...
    // C5032.h ends without #pragma warning(pop)

    // C5032.cpp
    #include "C5032.h"
    ...
    // C5032.cpp ends -- the translation unit is completed without #pragma warning(pop), resulting in warning C5032 on line 1 of C5032.h
    ```

   Örnek (sonrasında)

    ```cpp
    // C5032.h
    #pragma warning(push)
    #pragma warning(disable:####)
    ...
    #pragma warning(pop) // matches #pragma warning (push) on line 1
    // C5032.h ends

    // C5032.cpp
    #include "C5032.h"
    ...
    // C5032.cpp ends -- the translation unit is completed without unmatched #pragma warning(push)
    ```

- **Gelişmiş #pragma uyarı durumu izlemenin sonucu olarak ek uyarılar verilebilir**

   Derleyicinin önceki sürümleri #pragma uyarı durumu değişikliği, tüm amaçlanan uyarıları vermek için yeterince iyi bir şekilde değişiklik göstermemektedir. Bu davranış, belirli uyarıların, programcı tarafından farklı koşullarda etkili bir şekilde gizleneceği bir risk oluşturdu. Derleyici artık `#pragma warning` daha fazla robustly durumu izler; özellikle de `#pragma warning` Şablonlar içindeki durum değişiklikleriyle ilgilidir ve isteğe bağlı olarak, programcının ve ' ın istenmeyen kullanımlarını bulmasını sağlayan yeni uyarılar C5031 ve C5032 ' ı verir `#pragma warning(push)` `#pragma warning(pop)` .

   Geliştirilmiş `#pragma warning` durum değişikliği izlemenin bir sonucu olarak, daha önce yanlış bir şekilde gizlenen uyarılar ya da daha önce yanlış tanılanmış sorunlarla ilgili uyarılar artık verilebilir.

- **Erişilemeyen kodun geliştirilmiş kimliği**

   C++ standart kitaplığı değişiklikleri ve derleyicinin önceki sürümleri üzerinden satır içi işlev çağrılarının geliştirilmiş özelliği, derleyicinin belirli bir kodun artık ulaşılamaz olduğunu kanıtlamasını sağlayabilir. Bu yeni davranış, yeni ve daha sık verilen uyarı C4720 örneklerinin oluşmasına neden olabilir.

    ```Output
    warning C4720: unreachable code
    ```

   Çoğu durumda, bu uyarı yalnızca iyileştirmeler etkinken derlenirken verilebilir, çünkü iyileştirmeler daha fazla işlev çağrısı yapabilir, gereksiz kodu ortadan kaldırabilir, aksi takdirde belirli kodun ulaşılamaz olduğunu belirlemeyi mümkün hale getirir. Özellikle de [std:: Find](../standard-library/algorithm-functions.md#find)kullanımı ile ilgili olarak **try/catch** blokları içinde yeni uyarı C4720 örneklerinin oluştuğunu gözlemliyoruz.

   Örnek (önce)

    ```cpp
    try
    {
        auto iter = std::find(v.begin(), v.end(), 5);
    }
    catch (...)
    {
        do_something();   // ok
    }
    ```

   Örnek (sonrasında)

    ```cpp
    try
    {
        auto iter = std::find(v.begin(), v.end(), 5);
    }
    catch (...)
    {
        do_something();   // warning C4702: unreachable code
    }
    ```

### <a name="conformance-improvements-in-update-2"></a><a name="VS_Update2"></a>Güncelleştirme 2 ' deki uyumluluk geliştirmeleri

- **Ek uyarılar ve hatalar, SFıNAE ifadesi için kısmi destek sonucu olarak verilebilir.**

   Derleyicinin önceki sürümleri, SFıNAE ifadesi için destek eksikliği nedeniyle, **decltype** belirticileri içindeki belirli tür ifadeleri ayrıştırmadı. Bu eski davranış yanlıştı ve C++ standardına uymuyor. Derleyici artık bu ifadeleri ayrıştırır ve sürekli uyumluluk geliştirmeleri nedeniyle ifade SFıNAE için kısmi desteğe sahiptir. Sonuç olarak, derleyici artık derleyicinin önceki sürümlerinin ayrıştırmadığı ifadelerde bulunan uyarıları ve hataları verir.

   Bu yeni davranış, henüz bildirilmemiş bir tür içeren bir **decltype** ifadesini ayrıştırdığında, derleyici bir sonuç olarak derleyici hatası C2039 yayınlar.

    ```Output
    error C2039: 'type': is not a member of '`global namespace''
    ```

   Örnek 1: bildirilmemiş bir türün kullanımı (önce)

    ```cpp
    struct s1
    {
        template < typename T>
        auto f() - > decltype(s2< T> ::type::f());  // error C2039

        template< typename>
        struct s2 {};
    }
    ```

   Örnek 1 (sonra)

    ```cpp
    struct s1
    {
        template < typename>  // forward declare s2struct s2;

            template < typename T>
        auto f() - > decltype(s2< T> ::type::f());

        template< typename>
        struct s2 {};
    }
    ```

   Bu yeni davranış, bağımlı bir adın bir tür olduğunu belirtmek için **TypeName** anahtar sözcüğünün gerekli bir kullanımı eksik olan bir **decltype** ifadesini ayrıştırdığında, derleyici derleyici uyarısı C4346 derleyici hatası C2923 ile birlikte yayınlar.

    ```Output
    warning C4346: 'S2<T>::Type': dependent name is not a type
    ```

    ```Output
    error C2923: 's1': 'S2<T>::Type' is not a valid template type argument for parameter 'T'
    ```

   Örnek 2: bağımlı ad bir tür değil (önce)

    ```cpp
    template < typename T>
    struct s1
    {
        typedef T type;
    };

    template < typename T>
    struct s2
    {
        typedef T type;
    };

    template < typename T>
    T declval();

    struct s
    {
        template < typename T>
        auto f(T t) - > decltype(t(declval< S1< S2< T> ::type> ::type> ()));  // warning C4346, error C2923
    };
    ```

   Örnek 2 (sonra)

    ```cpp
    template < typename T> struct s1 { ... };  // as above
    template < typename T> struct s2 { ... };  // as above

    template < typename T>
    T declval();

    struct s
    {
        template < typename T>
        auto f(T t) - > decltype(t(declval< S1< typename S2< T> ::type> ::type> ()));
    };
    ```

- `volatile`**üye değişkenleri örtük olarak tanımlanmış oluşturucuları ve atama işleçlerini önler**

   Derleyicinin önceki sürümlerinde, varsayılan kopyalama/taşıma oluşturucuları ve varsayılan kopyalama/taşıma atama işleçleri otomatik olarak oluşturulan **geçici** üye değişkenlerine sahip bir sınıf izin verilir. Bu eski davranış yanlıştı ve C++ standardına uymuyor. Derleyici artık, bu işleçlerin varsayılan uygulamalarının otomatik olarak oluşturulmasını önleyen, önemsiz olmayan oluşturma ve atama işleçleri olan **geçici** üye değişkenlerine sahip bir sınıfı kabul eder. Böyle bir sınıf bir birleşimin üyesi (veya bir sınıfın içindeki anonim bir birleşim) olduğunda, birleşimin kopyalama/taşıma oluşturucuları ve kopyalama/taşıma atama işleçleri (veya anonim birleşim içeren sınıf) örtük olarak silindi olarak tanımlanır. Açıkça tanımlanmaksızın birleşim (veya anonim birleşim içeren sınıf) oluşturmaya veya kopyalamaya çalışılması bir hatadır ve derleyici sonuç olarak derleyici hatası C2280 yayınlar.

    ```Output
    error C2280: 'B::B(const B &)': attempting to reference a deleted function
    ```

   Örnek (önce)

    ```cpp
    struct A
    {
        volatile int i;
        volatile int j;
    };

    extern A* pa;

    struct B
    {
        union
        {
            A a;
            int i;
        };
    };

    B b1{ *pa };
    B b2(b1);  // error C2280
    ```

   Örnek (sonrasında)

    ```cpp
    struct A
    {
        int i; int j;
    };

    extern volatile A* pa;

    A getA()  // returns an A instance copied from contents of pa
    {
        A a;
        a.i = pa - > i;
        a.j = pa - > j;
        return a;
    }

    struct B;  // as above

    B b1{ GetA() };
    B b2(b1);  // error C2280
    ```

- **Statik üye işlevleri CV niteleyicilerini desteklemez.**

   Önceki Visual Studio 2015 sürümleri, statik üye işlevlerinin CV niteleyicilerine sahip olmasına izin verilir. Bu davranış, Visual Studio 2015 ve Visual Studio 2015 güncelleştirme 1 ' deki bir gerileme nedeniyle yapılır; Visual Studio 2013 ve önceki derleyici sürümleri bu şekilde yazılmış kodu reddeder. Visual Studio 2015 ve Visual Studio 2015 güncelleştirme 1 ' in davranışı yanlış ve C++ standardına uymuyor.  Visual Studio 2015 güncelleştirme 2 bu şekilde yazılmış kodu reddeder ve bunun yerine derleyici hatası C2511 yayınlar.

    ```Output
    error C2511: 'void A::func(void) const': overloaded member function not found in 'A'
    ```

   Örnek (önce)

    ```cpp
    struct A
    {
        static void func();
    };

    void A::func() const {}  // C2511
    ```

   Örnek (sonrasında)

    ```cpp
    struct A
    {
        static void func();
    };

    void A::func() {}  // removed const
    ```

- **WinRT kodunda, enum iletme bildirimine izin verilmiyor** (yalnızca etkiler `/ZW` )

   Windows Çalışma Zamanı (WinRT) için derlenen kod, yönetilen C++ kodunun derleyici anahtarı kullanılarak .NET Framework için derlendiğine benzer şekilde, **numaralandırma** türlerinin ileri olarak bildirilmesine izin vermez `/clr` . Bu davranış, bir numaralandırma boyutunun her zaman bilinmesini ve WinRT türü sistemine doğru şekilde yansıtılmasını sağlar. Derleyici bu şekilde yazılmış kodu reddeder ve derleyici hatası C3197 ile birlikte derleyici hatası C2599 yayınlar.

    ```Output
    error C2599: 'CustomEnum': the forward declaration of a WinRT enum is not allowed
    ```

    ```Output
    error C3197: 'public': can only be used in definitions
    ```

   Örnek (önce)

    ```cpp
    namespace A {
        public enum class CustomEnum : int32;  // forward declaration; error C2599, error C3197
    }

    namespace A {
        public enum class CustomEnum : int32
        {
            Value1
        };
    }

    public ref class Component sealed
    {
    public:
        CustomEnum f()
        {
            return CustomEnum::Value1;
        }
    };
    ```

   Örnek (sonrasında)

    ```cpp
              // forward declaration of CustomEnum removed
    namespace A {
        public enum class CustomEnum : int32
        {
            Value1
        };
    }

    public ref class Component sealed
    {
    public:
        CustomEnum f()
        {
            return CustomEnum::Value1;
        }
    };
    ```

- **Aşırı yüklenmiş üye olmayan işleç New ve delete işleci satır içi olarak bildirilemez** (düzey 1 ( `/W1` )-varsayılan)

   Önceki derleyicinin sürümleri, üye olmayan operator new ve operator delete işlevleri satır içi olarak bildirildiğinde bir uyarı vermez. Bu şekilde yazılan kod hatalı biçimlendirilmiş (Tanılama gerekmez) ve eşleşmeyen yeni ve silme işleçlerinden kaynaklanan bellek sorunlarına neden olabilir (özellikle de boyutu kaldırma ile birlikte kullanıldığında), tanılanması zor olabilir. Derleyici artık bu şekilde yazılmış kodu belirlemesine yardımcı olmak için derleyici uyarısı C4595 ' i yayınlar.

    ```Output
    warning C4595: 'operator new': non-member operator new or delete functions may not be declared inline
    ```

   Örnek (önce)

    ```cpp
    inline void* operator new(size_t sz)  // warning C4595
    {
        ...
    }
    ```

   Örnek (sonrasında)

    ```cpp
    void* operator new(size_t sz)  // removed inline
    {
        ...
    }
    ```

   Bu şekilde yazılmış kodu düzeltme, işleç tanımlarının bir üstbilgi dosyasından ve karşılık gelen bir kaynak dosyaya taşınmasını gerektirebilir.

### <a name="conformance-improvements-in-update-3"></a><a name="VS_Update3"></a>Güncelleştirme 3 ' te uyumluluk geliştirmeleri

- **std:: is_convertable artık kendinden atamayı algılar** (Standart Kitaplığı)

   Nitelik türünün önceki sürümleri, `std::is_convertable` kopya Oluşturucusu silindiği veya özel bir sınıf türünün kendi kendine atamasını doğru bir şekilde algılamadı. Şimdi, `std::is_convertable<>::value` Silinmiş veya özel kopya Oluşturucusu olan bir sınıf türüne uygulandığında doğru olarak **false** olarak ayarlanmıştır.

   Bu değişiklik ile ilişkili bir derleyici tanılaması yok.

   Örnek

    ```cpp
    #include <type_traits>

    class X1
    {
                public:
                X1(const X1&) = delete;
                };

    class X2
    {
                private:
                X2(const X2&);
                };

    static_assert(std::is_convertible<X1&, X1>::value, "BOOM");static_assert(std::is_convertible<X2&, X2>::value, "BOOM");
    ```

   Derleyicinin önceki sürümlerinde, bu örneğin en altındaki statik onaylar, `std::is_convertable<>::value` yanlış olarak **doğru**olarak ayarlandığından geçer. Artık `std::is_convertable<>::value` **yanlış**olarak ayarlanmıştır, statik onayların başarısız olmasına neden olur.

- **Varsayılan olarak ayarlanmış veya silinmiş önemsiz kopyalama ve taşıma oluşturucuları erişim belirticilerine göre**

   Derleyicinin önceki sürümleri, çağrılmalarına izin vermeden önce, varsayılan olarak ayarlanmış veya silinmiş Önemsiz kopya ve taşıma oluşturucularının erişim belirticisini denetmedi. Bu eski davranış yanlıştı ve C++ standardına uymuyor. Bazı durumlarda, bu eski davranış sessiz hatalı kod oluşturma riskini oluşturmuştur ve bu da öngörülemeyen çalışma zamanı davranışına neden olur. Derleyici artık, çağrılabilir olup olmadığını anlamak için varsayılan olarak ayarlanmış veya silinmiş önemsiz kopyalama ve taşıma oluşturucularının erişim belirticisini denetler ve bu durumda, bir sonuç olarak derleyici uyarısı C2248 yayınlar.

    ```Output
    error C2248: 'S::S' cannot access private member declared in class 'S'
    ```

   Örnek (önce)

    ```cpp
    class S {
    public:
        S() = default;
    private:
        S(const S&) = default;
    };

    void f(S);  // pass S by value

    int main()
    {
        S s;
        f(s);  // error C2248, can't invoke private copy constructor
    }
    ```

   Örnek (sonrasında)

    ```cpp
    class S {
    public:
        S() = default;
    private:
        S(const S&) = default;
    };

    void f(const S&);  // pass S by reference

    int main()
    {
        S s;
        f(s);
    }
    ```

- **ÖZNITELIKLI atl kod desteğinin kullanımdan kaldırılması** (düzey 1 ( `/W1` )-varsayılan)

   Derleyicinin önceki sürümleri, öznitelikli ATL kodunu destekliyordu. [Visual Studio 2008 ' de başlayan](../porting/visual-cpp-what-s-new-2003-through-2015.md#whats-new-for-c-in-visual-studio-2008)öznitelikli atl kodu desteğini kaldırmanın sonraki aşaması olarak, öznitelikli atl kodu kaldırılmıştır. Derleyici artık bu tür kullanım dışı kodu belirlemesine yardımcı olmak için derleyici uyarısı C4467 ' i yayınlar.

    ```Output
    warning C4467: Usage of ATL attributes is deprecated
    ```

   Destek derleyicisinden kaldırılana kadar öznitelikli ATL kodu kullanmaya devam etmek istiyorsanız, `/Wv:18` veya `/wd:4467` komut satırı bağımsız değişkenlerini derleyiciye geçirerek veya kaynak kodunuza ekleyerek bu uyarıyı devre dışı bırakabilirsiniz `#pragma warning(disable:4467)` .

   Örnek 1 (önceki)

    ```cpp
              [uuid("594382D9-44B0-461A-8DE3-E06A3E73C5EB")]
    class A {};
    ```

   Örnek 1 (sonra)

    ```cpp
    __declspec(uuid("594382D9-44B0-461A-8DE3-E06A3E73C5EB")) A {};
    ```

   Bazen, aşağıdaki örnek kodda olduğu gibi kullanım dışı ATL özniteliklerini kullanmaktan kaçınmak için bir IDL dosyası oluşturmanız gerekebilir veya bir IDL dosyası oluşturmak isteyebilirsiniz.

   Örnek 2 (önce)

    ```cpp
    [emitidl];
    [module(name = "Foo")];

    [object, local, uuid("9e66a290-4365-11d2-a997-00c04fa37ddb")]
    __interface ICustom {
        HRESULT Custom([in] long l, [out, retval] long *pLong);
        [local] HRESULT CustomLocal([in] long l, [out, retval] long *pLong);
    };

    [coclass, appobject, uuid("9e66a294-4365-11d2-a997-00c04fa37ddb")]
    class CFoo : public ICustom
    {
        // ...
    };
    ```

   İlk olarak, *. IDL dosyasını oluşturun; vc140. IDL tarafından oluşturulan dosya, \* arabirimleri ve ek açıklamaları içeren bir. IDL dosyası elde etmek için kullanılabilir.

   Ardından, C++ arabirim tanımlarının oluşturulduğundan emin olmak için, derlemenize bir MıDL adımı ekleyin.

   Örnek 2 IDL (sonra)

    ```cpp
    import "docobj.idl";

    [
        object, local, uuid(9e66a290 - 4365 - 11d2 - a997 - 00c04fa37ddb)
    ]

    interface ICustom : IUnknown {
        HRESULT  Custom([in] long l, [out, retval] long *pLong);
        [local] HRESULT  CustomLocal([in] long l, [out, retval] long *pLong);
    };

    [version(1.0), uuid(29079a2c - 5f3f - 3325 - 99a1 - 3ec9c40988bb)]
    library Foo
    {
        importlib("stdole2.tlb");
    importlib("olepro32.dll");
    [
        version(1.0),
        appobject,uuid(9e66a294 - 4365 - 11d2 - a997 - 00c04fa37ddb)
    ]

    coclass CFoo {
        interface ICustom;
    };
    }
    ```

   Ardından, aşağıdaki örnek kodda olduğu gibi doğrudan uygulama dosyasında ATL kullanın.

   Örnek 2 uygulama (sonrasında)

    ```cpp
    #include <idl.header.h>
    #include <atlbase.h>

    class ATL_NO_VTABLE CFooImpl :
        public ICustom,
        public ATL::CComObjectRootEx< CComMultiThreadModel>
    {
    public:
        BEGIN_COM_MAP(CFooImpl)
            COM_INTERFACE_ENTRY(ICustom)
        END_COM_MAP()
    };
    ```

- **Önceden derlenmiş üstbilgi (pch) dosyaları ve eşleşmeyen #include yönergeleri** (yalnızca etkiler `/Wall` `/WX` )

   Derleyicinin önceki sürümleri, `#include` `-Yc` `-Yu` önceden derlenmiş üst bilgi (pch) dosyaları kullanılırken ve derlemeler arasında kaynak dosyalarda eşleşmeyen yönergeleri kabul etti. Bu şekilde yazılan kod artık derleyici tarafından kabul edilmez.   Derleyici artık, PCH dosyalarını kullanırken eşleşmeyen yönergeleri tanımlamanızı sağlamak için derleyici uyarısı CC4598 ' i yayınlar `#include` .

    ```Output
    warning C4598: 'b.h': included header file specified for Ycc.h at position 2 does not match Yuc.h at that position
    ```

   Örnek (öncesi):

   X. cpp (-YCC. h)

    ```cpp
    #include "a.h"
    #include "b.h"
    #include "c.h"
    ```

   Z. cpp (-yuc. h)

    ```cpp
    #include "b.h"
    #include "a.h"  // mismatched order relative to X.cpp
    #include "c.h"
    ```

   Örnek (sonrasında)

   X. cpp (-YCC. h)

    ```cpp
    #include "a.h"
    #include "b.h"
    #include "c.h"
    ```

   Z. cpp (-yuc. h)

    ```cpp
    #include "a.h"
    #include "b.h" // matched order relative to X.cpp
    #include "c.h"
    ```

- **Ön derlenmiş üstbilgi (pch) dosyaları ve eşleşmeyen dizinleri Ekle** (yalnızca etkiler `/Wall` `/WX` )

   Derleyicinin önceki sürümleri, `-I` `-Yc` `-Yu` önceden derlenmiş üst bilgi (pch) dosyaları kullanırken ve derlemeler arasında derleyiciye dizin () komut satırı bağımsız değişkenleri içerir. Bu şekilde yazılan kod artık derleyici tarafından kabul edilmez. Derleyici artık, PCH dosyalarını kullanırken eşleşmeyen içerme dizini ( `-I` ) komut satırı bağımsız değişkenlerini tanımlamanızı sağlamak için derleyici uyarısı CC4599 ' i yayınlar.

    ```Output
    warning C4599: '-I..' : specified for Ycc.h at position 1 does not match Yuc.h at that position
    ```

   Örnek (önce)

    ```ms-dos
    cl /c /Wall /Ycc.h -I.. X.cpp
    cl /c /Wall /Yuc.h Z.cpp
    ```

   Örnek (sonrasında)

    ```ms-dos
    cl /c /Wall /Ycc.h -I.. X.cpp
    cl /c /Wall /Yuc.h -I.. Z.cpp
    ```

## <a name="visual-studio-2013-conformance-changes"></a>Uyumluluk değişikliklerini Visual Studio 2013

### <a name="compiler"></a>Derleyici

- **Final** anahtar sözcüğü artık daha önce derlenebilecek çözümlenmemiş bir sembol hatası oluşturuyor:

    ```cpp
    struct S1 {
        virtual void f() = 0;
    };

    struct S2 final : public S1 {
        virtual void f();
    };

    int main(S2 *p)
    {
        p->f();
    }
    ```

   Önceki sürümlerde, çağrı **sanal** bir çağrı olduğundan bir hata verilmedi; Bununla birlikte, program çalışma zamanında çökebilir. Artık, sınıfın son olduğu bilindiğinden bir bağlayıcı hatası verilmektedir. Bu örnekte, hatayı düzeltemedi, tanımını içeren obj 'e göre bağlantı oluşturursunuz `S2::f` .

- Ad alanlarında arkadaş işlevlerini kullandığınızda, ona başvurmadan önce arkadaş işlevini yeniden bildirmeniz gerekir, aksi durumda derleyici artık ISO C++ standardına uygun olduğundan bir hata alırsınız. Örneğin, bu örnek artık derlenmezse:

    ```cpp
    namespace NS {
        class C {
            void func(int);
            friend void func(C* const) {}
        };

        void C::func(int) {
            NS::func(this);  // error
        }
    }
    ```

   Bu kodu düzeltmek için **arkadaş** işlevini bildirin:

    ```cpp
    namespace NS {
        class C {
            void func(int);
            friend void func(C* const) {}
        };

        void func(C* const);  // conforming fix

        void C::func(int) {
            NS::func(this);
        }
    ```

- C++ standardı bir sınıfta açık özelleştirmeye izin vermez. Microsoft C++ derleyicisi, bazı durumlarda buna izin verse de, aşağıdaki örnekte olduğu gibi, derleyici ikinci işlevi birincinin özelleştirmesi olarak düşünmediğinden bir hata oluşturulur.

    ```cpp
    template < int N>
    class S {
    public:
        template  void f(T& val);
        template < > void f(char val);
    };

    template class S< 1>;
    ```

   Bu kodu düzeltmek için ikinci işlevi değiştirin:

    ```cpp
    template <> void f(char& val);
    ```

- Derleyici artık aşağıdaki örnekteki iki işlevi belirsizliğini ortadan kaldırmaya çalışır ve şimdi bir hata yayar:

    ```cpp
    template< typename T> void Func(T* t = nullptr);
    template< typename T> void Func(...);

    int main() {
        Func< int>(); // error
    }
    ```

   Bu kodu düzeltmek için çağrıyı netleştirin:

    ```cpp
    template< typename T> void Func(T* t = nullptr);
    template< typename T> void Func(...);

    int main() {
        Func< int>(nullptr); // ok
    }
    ```

- Derleyici ISO C++ 11 ile uyumlu hale getirilmesinden önce aşağıdaki kod derlenir ve `x` **int**türünde çözümlenmesine neden olur:

    ```cpp
    auto x = {0};
    int y = x;
    ```

   Bu kod `x` , bir türü olarak çözümlenmektedir `std::initializer_list<int>` ve int türüne atamaya çalışan bir sonraki satırda hataya neden olur `x` . **int** (Varsayılan olarak dönüştürme yoktur.) Bu kodu düzeltmek için, **Auto**yerine **int** kullanın:

    ```cpp
    int x = {0};
    int y = x;
    ```

- Sağ değerin türü başlatılmış olan sol taraftaki değerin türüyle eşleşmediği zaman toplu başlatmaya artık izin verilmez ve ISO C++ 11 standardı, bir hata verilir çünkü ISO C++ 11 standardı, Dönüştürmelere daraltmaya gerek kalmadan Tekdüzen başlatması gerektirir. Daha önce, bir daraltma dönüştürmesi kullanılabilirse bir hata yerine bir [Derleyici Uyarısı (düzey 4) C4242](../error-messages/compiler-warnings/compiler-warning-level-4-c4242.md) uyarısı verilir.

    ```cpp
    int i = 0;
    char c = {i}; // error
    ```

   Bu kodu düzeltmek için açık bir daraltma dönüşümü ekleyin:

    ```cpp
    int i = 0;
    char c = {static_cast<char>(i)};
    ```

- Şu başlatmaya artık izin verilmiyor:

    ```cpp
    void *p = {{0}};
    ```

   Bu kodu düzeltmek için şu formlardan birini kullanın:

    ```cpp
    void *p = 0;
    // or
    void *p = {0};
    ```

- Ad arama değiştirildi. Aşağıdaki kod, Visual Studio 2012 ve Visual Studio 2013 içindeki C++ derleyicisinde farklı şekilde çözümlenir:

    ```cpp
    enum class E1 { a };
    enum class E2 { b };

    int main()
    {
        typedef E2 E1;
        E1::b;
    }
    ```

   Visual Studio 2012 ' de, `E1` ın ifadesi `E1::b` `::E1` genel kapsamda olarak çözümlenir. Visual Studio 2013 içinde, `E1` ifadesinde `E1::b` `typedef E2` tanımına çözümler `main()` ve türü vardır `::E2` .

- Nesne düzeni değişti. x64 üzerinde, bir sınıfın nesne düzeni önceki sürümlere göre değişebilmektedir. Bir **sanal** işlevi varsa, ancak **sanal** işlevine sahip bir taban sınıfı yoksa, derleyicinin nesne modeli, veri üyesi düzeninden sonra **sanal** işlev tablosuna bir işaretçi ekler. Başka bir deyişle, ilgili düzen her durumda en uygun düzen olmayabilir. Önceki sürümlerde, x64 için en iyi duruma getirme sizin için düzeni iyileştirmeye çalışır, ancak karmaşık kod durumlarında düzgün şekilde çalışamadığı için Visual Studio 2013 kaldırılmıştır. Örneğin, aşağıdaki kodu düşünün:

    ```cpp
    __declspec(align(16)) struct S1 {
    };

    struct S2 {
        virtual ~S2();
        void *p;
        S1 s;
    };
    ```

- Visual Studio 2013, `sizeof(S2)` x64 üzerindeki sonucu 48, ancak önceki sürümlerde 32 olarak değerlendirilir. Bu işlemi x64 için Visual Studio 2013 C++ derleyicisinde 32 olarak değerlendirmek için **sanal** işleve sahip bir kukla taban sınıfı ekleyin:

    ```cpp
    __declspec(align(16)) struct S1 {
    };

    struct dummy {
        virtual ~dummy() {}
    };
    struct S2 : public dummy {
        virtual ~S2();
        void *p;
        S1 s;
    };
    ```

   Kodunuzda daha önceki bir sürümün iyileştirmeye çalıştığı yerleri bulmak için, derleyici seçeneğiyle birlikte bu sürümden bir derleyici kullanın `/W3` ve uyarı C4370 ' ı açın. Örneğin:

    ```cpp
    #pragma warning(default:4370)

    __declspec(align(16)) struct S1 {
    };

    struct S2 {
        virtual ~S2();
        void *p;
        S1 s;
    };
    ```

   Visual Studio 2013 önce, bu kod şu iletiyi çıkarır: "Warning C4370:2": sınıfının yerleşimi daha iyi paketleme nedeniyle derleyicinin önceki bir sürümünden değişti ".

   X86 derleyicisi, derleyicinin tüm sürümlerinde aynı alt nesne düzeni sorununa sahiptir. Örneğin, bu kod x86 için derlenirse:

    ```cpp
    struct S {
        virtual ~S();
        int i;
        double d;
    };
    ```

   Sonucu 24 ' `sizeof(S)` dir. Ancak, x64 için belirtilen geçici çözümü kullanıyorsanız, 16 ' ya azaltılabilir:

    ```cpp
    struct dummy {
        virtual ~dummy() {}
    };

    struct S : public dummy {
        virtual ~S();
        int i;
        double d;
    };
    ```

### <a name="standard-library"></a>Standart Kitaplık

Visual Studio 2013 C++ derleyicisi, Visual Studio 2010 ' de uygulanmış olan _ITERATOR_DEBUG_LEVEL uyuşmazlıkları algılar ve RuntimeLibrary ile uyuşmuyor. Bu uyuşmazlıklar derleyici seçenekleri `/MT` (statik sürüm), `/MTd` (statik hata ayıklama), `/MD` (dinamik sürüm) ve `/MDd` (dinamik hata ayıklama) karmaysa oluşur.

- Kodunuz önceki sürümün benzetimli diğer ad şablonlarını alıyorsa, bunu değiştirmeniz gerekir. Örneğin, yerine `allocator_traits<A>::rebind_alloc<U>::other` artık söylemeniz gerekir `allocator_traits<A>::rebind_alloc<U>` . Artık gerekli olmasa da, artık daha `ratio_add<R1, R2>::type` önce söylediğimiz için, daha az bir `ratio_add<R1, R2>` `ratio<N, D>` oran için "tür" typedef olması gerektiğinden, daha önce derlenmeye devam eder.

- Veya öğesini çağırdığınızda kullanmanız gerekir `#include <algorithm>` `std::min()` `std::max()` .

- Mevcut kodunuz önceki sürümün benzetimli kapsamlı numaralandırmalarını kullanıyorsa (ad alanlarına sarmalanmış geleneksel kapsamlı numaralandırmalar), bunu değiştirmeniz gerekir. Örneğin, türüne başvurdıysanız `std::future_status::future_status` , artık söylemeniz gerekir `std::future_status` . Ancak, çoğu kod etkilenmez; Örneğin, `std::future_status::ready` hala derlenir.

- `explicit operator bool()`belirtilmemiş-bool-Type () işleçinden daha katı. `explicit operator bool()`Açık dönüştürmelerin bool değerine izin verir — örneğin, `shared_ptr<X> sp` hem hem `static_cast<bool>(sp)` de `bool b(sp)` geçerlidir ve Boole-testable "bağlamsal dönüşümler", örneğin, her `if (sp)` ne olur `!sp` `sp &&` . Ancak, `explicit operator bool()` örtük dönüştürmeleri bool olarak yasaklıyor, bu yüzden `bool b = sp;` bir bool dönüş türü söylerseniz ve bu tür bir bool dönüş türü verilmeyebilir `return sp` .

- Artık gerçek değişken bağımsız olmayan şablonlar uygulandığına göre _VARIADIC_MAX ve ilgili makroların hiçbir etkisi yoktur. Hala _VARIADIC_MAX tanımlıyorsanız yok sayılır. Benzetilmiş değişen sayıda bağımsız değişken içeren şablonları farklı bir şekilde desteklemeye yönelik makro makinemizi kabul ettiyseniz, kodunuzu değiştirmeniz gerekir.

- Normal anahtar sözcüklere ek olarak, C++ standart kitaplık üstbilgileri artık, içerik duyarlı anahtar sözcüklerin **geçersiz kılınmasına** **ve sonuna**kadar makro değişimini yasaklamıştır.

- `reference_wrapper`, `ref()` , ve `cref()` Şimdi geçici nesnelere bağlamayı yasaklaın.

- \<random>Şimdi derleme zamanı ön koşulları 'nı kesinlikle zorluyor.

- Çeşitli C++ standart kitaplığı tür nitelikleri, "T 'nin tamamı bir tür olacaktır" önkoşuluna sahiptir. Derleyici artık bu önkoşula daha katı zorsa da, tüm durumlarda bu uygulamayı zorlamayabilir. (C++ standart kitaplığı önkoşul ihlalleri tanımsız davranışı tetikleyeceğinden, standart zorlamayı garanti etmez.)

- C++ standart kitaplığı desteklemez `/clr:oldSyntax` .

- Common_type<> için C++ 11 belirtimi beklenmeyen ve istenmeyen sonuçlara sahipti; Özellikle, common_type \<int, int> :: Type int&& döndürür. Bu nedenle, derleyici, kitaplık çalışma grubu sorunu 2141 için önerilen çözümü uygular. Bu, common_type \<int, int=""> :: Type int döndürecek şekilde gelir.

   Bu değişikliğin yan etkisi olarak, kimlik durumu artık çalışmaz (common_type \<T> her zaman t türünde sonuç vermez). Bu davranış önerilen çözünürlüğe uyar, ancak önceki davranışa bağlı olan tüm kodları keser.

   Bir kimlik türü nitelik gerekliyse, içinde tanımlı standart olmayan ' ı kullanmayın, `std::identity` \<type_traits> çünkü için çalışmaz \<void> . Bunun yerine, gereksinimlerinize uyan kendi kimlik türü ayırt edici niteliğini uygulayın. Aşağıda bir örnek verilmiştir:

    ```cpp
    template < typename T> struct Identity {
        typedef T type;
    };
    ```

### <a name="mfc-and-atl"></a>MFC ve ATL

- **Yalnızca Visual Studio 2013**: Unicode çok popüler olduğundan ve MBCS 'nin kullanımı önemli ölçüde reddettiğinden, MFC MBCS kitaplığı Visual Studio 'ya dahil değildir. Yeni denetimlerin ve iletilerin çoğu salt Unicode olduğundan, bu değişiklik aynı zamanda MFC'yi Windows SDK ile daha paralel halde tutar. Ancak, MFC MBCS kitaplığını kullanmaya devam etmeniz gerekiyorsa, [Visual Studio 2013 Için çok BAYTLı MFC kitaplığındaki](https://www.microsoft.com/download/details.aspx?id=40770)Microsoft İndirme Merkezi ' nden indirebilirsiniz. Visual C++ Yeniden Dağıtılabilir Paketi'nde bu kitaplık halen yer almaktadır.  (Note: MBCS DLL, Visual Studio 2015 ve üzeri sürümlerde C++ Kurulum bileşenlerine dahildir).

- MFC şeridi için erişilebilirlik değiştirilmiştir.  Tek düzey mimari yerine artık hiyerarşik bir mimari vardır. ' I çağırarak eski davranışı kullanmaya devam edebilirsiniz `CRibbonBar::EnableSingleLevelAccessibilityMode()` .

- `CDatabase::GetConnect`Yöntem kaldırılır. Güvenliği artırmak için bağlantı dizesi artık şifrelenmiş olarak depolanır ve yalnızca gerektiğinde çözülür. düz metin olarak döndürülemez.  Dize yöntemi kullanılarak elde edilebilir `CDatabase::Dump` .

- İmzası `CWnd::OnPowerBroadcast` değiştirildi. Bu ileti işleyicisinin imzası ikinci parametre olarak bir LPARAM alacak şekilde değiştirilir.

- İmzalar ileti işleyicileri ile uyumlu olacak şekilde değiştirilir. Aşağıdaki işlevlerin parametre listeleri yeni eklenen ON_WM_* ileti işleyicilerini kullanacak şekilde değiştirilmiştir:

  - `CWnd::OnDisplayChange`Yeni ON_WM_DISPLAYCHANGE makrosunun ileti eşlemesinde kullanılabilmesi için (WPARAM, LPARAM) yerine (UINT, int, int) olarak değiştirildi.

  - `CFrameWnd::OnDDEInitiate`Yeni ON_WM_DDE_INITIATE makrosunun ileti eşlemesinde kullanılabilmesi için (WPARAM, LPARAM) yerine (CWnd *, UINT, UNIT) olarak değiştirildi.

  - `CFrameWnd::OnDDEExecute`Yeni ON_WM_DDE_EXECUTE makrosunun ileti eşlemesinde kullanılabilmesi için (WPARAM, LPARAM) yerine (CWnd *, tanıtıcı) olarak değiştirildi.

  - `CFrameWnd::OnDDETerminate`Yeni ON_WM_DDE_TERMINATE makrosunun ileti eşlemesinde kullanılabilmesi için (WPARAM, LPARAM) yerine parametresi olarak (CWnd *) olarak değiştirildi.

  - `CMFCMaskedEdit::OnCut`Yeni ON_WM_CUT makrosunun ileti eşlemesinde kullanılabilmesi için (WPARAM, LPARAM) yerine parametre yok olarak değiştirilmiştir.

  - `CMFCMaskedEdit::OnClear`Yeni ON_WM_CLEAR makrosunun ileti eşlemesinde kullanılabilmesi için (WPARAM, LPARAM) yerine parametre yok olarak değiştirilmiştir.

  - `CMFCMaskedEdit::OnPaste`Yeni ON_WM_PASTE makrosunun ileti eşlemesinde kullanılabilmesi için (WPARAM, LPARAM) yerine parametre yok olarak değiştirilmiştir.

- `#ifdef`MFC üstbilgi dosyalarındaki yönergeler kaldırılır. `#ifdef`MFC üstbilgi dosyalarındaki Windows 'un desteklenmeyen sürümleriyle ilişkili çok sayıda yönergeler (WINVER &lt; 0x0501) kaldırılır.

- ATL DLL (atl120.dll) kaldırıldı. ATL artık, üst bilgiler ve statik kitaplık (atls.lib) olarak sağlanmaktadır.

- Atlsd. lib, atlsn. lib ve atlsnd. lib kaldırılır. Atls.lib artık, karakter kümesi bağımlılıkları veya hata ayıklamaya/yayınlamaya özgü kod içermez. Unicode/ANSI ve hata ayıklama/yayınlama için aynı çalıştığından, kitaplığın yalnızca tek bir sürümü gereklidir.

- ATL/MFC Izleme Aracı, ATL DLL ile birlikte kaldırılır ve izleme mekanizması basitleştirilir. `CTraceCategory`Oluşturucu artık bir parametre (kategori adı) alır ve izleme MAKROLARı CRT hata ayıklama raporlama işlevlerini çağırır.

## <a name="visual-studio-2012-breaking-changes"></a>Visual Studio 2012 son değişiklikleri

### <a name="compiler"></a>Derleyici

- `/Yl`Derleyici seçeneği değişti. Varsayılan olarak, derleyici bu seçeneği kullanarak belirli koşullar altında LNK2011 hatalara yol açabilir. Daha fazla bilgi için bkz. [/Rivl (hata ayıklama kitaplığı IÇIN PCH başvurusu Ekle)](../build/reference/yl-inject-pch-reference-for-debug-library.md).

- Kullanılarak derlenen kodda `/clr` , **enum** sınıfı anahtar sözcüğü, ortak dil çalışma zamanı (CLR) sabit listesini değil bir c++ 11 sabit listesini tanımlar. Bir CLR numaralandırması tanımlamak için, erişilebilirliği hakkında açık olması gerekir.

- Bağımlı bir adı (C++ dili standart uyumluluğu) açıkça ayırt etmek için şablon anahtar sözcüğünü kullanın. Aşağıdaki örnekte, vurgulanan şablon anahtar sözcüğü belirsizliği çözümlemek için zorunludur. Daha fazla bilgi için bkz. [bağımlı türler Için ad çözümlemesi](../cpp/name-resolution-for-dependent-types.md).

    ```cpp
    template < typename X = "", typename = "" AY = "">
    struct Container { typedef typename AY::template Rebind< X> ::Other AX; };
    ```

- Aşağıdaki örnekte gösterildiği gibi float türündeki sabit ifadeye artık şablon bağımsız değişkeni olarak izin verilmez.

    ```cpp
    template<float n=3.14>
    struct B {};  // error C2993: 'float': illegal type for non-type template parameter 'n'
    ```

- `/GS`Komut satırı seçeneği kullanılarak derlenen ve bir tek başına güvenlik açığı olan kod, aşağıdaki sözde kod örneğinde gösterildiği gibi çalışma zamanında işlem sonlandırmasına yol açabilir.

    ```cpp
    char buf[MAX]; int cch; ManipulateString(buf, &cch); // ... buf[cch] = '\0'; // if cch >= MAX, process will terminate
    ```

- X86 derlemeleri için varsayılan mimari SSE2 olarak değiştirilir; Bu nedenle, derleyici SSE yönergelerini yayabilir ve kayan nokta hesaplamaları gerçekleştirmek için XMM kayıtlarını kullanacaktır. Önceki davranışa geri dönmek istiyorsanız, `/arch:IA32` MIMARIYI IA32 olarak belirtmek için derleyici bayrağını kullanın.

- Derleyici, uyarı [derleyicisi Uyarısı (düzey 4) C4703](../error-messages/compiler-warnings/compiler-warning-level-4-c4703.md) ve C4701 daha önce olmadığı durumlarda verebilir. Derleyici, işaretçi türündeki başlatılmamış yerel değişkenlerin kullanımı için daha güçlü denetimler uygular.

- Yeni bağlayıcı bayrağı `/HIGHENTROPYVA` belirtildiğinde, Windows 8 genellikle bellek ayırmalarının 64 bitlik bir adres döndürmesini sağlar. (Windows 8 ' den önce, bu ayırmalar daha fazla 2 GB 'tan az olan adresler döndürür.) Bu değişiklik, var olan koddaki işaretçi kesme hatalarını ortaya çıkabilir. Bu anahtar varsayılan olarak açık olur. Bu davranışı devre dışı bırakmak için, belirtin `/HIGHENTROPYVA:NO` .

- Yönetilen derleyici (Visual Basic/C#) `/HIGHENTROPYVA` yönetilen derlemeler için de destekler.  Ancak bu durumda, `/HIGHENTROPYVAswitch` Varsayılan olarak kapalıdır.

### <a name="ide"></a>IDE

- C++/CLı ' da Windows Forms uygulamalar oluşturmasanız da mevcut C++/CLı UI uygulamalarının Bakımı desteklenir. Windows Forms bir uygulama veya başka bir .NET UI uygulaması oluşturmanız gerekiyorsa, C# veya Visual Basic kullanın. Yalnızca birlikte çalışabilirlik amaçları için C++/CLı kullanın.

### <a name="parallel-patterns-library-and-concurrency-runtime-library"></a>Paralel Desenler kitaplığı ve Eşzamanlılık Çalışma Zamanı Kitaplığı

`SchedulerType`Numaralandırması `UmsThreadDefault` kullanım dışıdır. Belirtimi `UmsThreadDefault` kullanım dışı bir uyarı üretir ve dahili olarak öğesine geri eşlenir `ThreadScheduler` .

### <a name="standard-library"></a>Standart Kitaplık

- C++ 98/03 ve C++ 11 standartları arasında önemli bir değişiklikten sonra, çağrısı yapılacak açık şablon bağımsız değişkenlerini `make_pair()` (içinde olduğu gibi) kullanarak, `make_pair<int, int>(x, y)` genellikle Visual Studio 2012 ' de Visual C++ derlenmez. Çözüm, `make_pair()` içinde olduğu gibi, her zaman açık şablon bağımsız değişkenleri olmadan çağrlamadır `make_pair(x, y)` . Açık şablon bağımsız değişkenlerinin sağlanması işlevin amacını erteler. Elde edilen tür üzerinde kesin denetim gerekiyorsa, `pair` yerine kullanın `make_pair` `pair<short, short>(int1, int2)` .

- C++ 98/03 ve C++ 11 standartları arasında başka bir önemli değişiklik: A örtük olarak B 'ye dönüştürülebilir ve B, açıkça C 'ye dönüştürülebilir, ancak C, C++ 98/03 ve Visual Studio 2010 'e örtülü olarak dönüştürülebilir `pair<A, X>` (örtük veya açık olarak) `pair<C, X>` . (Diğer tür olan X, burada ilgilenmez ve çiftin ilk türüne özgü değildir.) Visual Studio 2012 ' de C++ derleyicisi, bir ' ın örtük olarak C 'ye dönüştürümediğini algılar ve aşırı yükleme çözünürlüğünden çift dönüştürmeyi kaldırır. Bu değişiklik birçok senaryo için pozitif bir değer. Örneğin, aşırı yükleme `func(const pair<int, int>&)` ve `func(const pair<string, string>&)` `func()` ile çağırma `pair<const char *, const char *>` Bu değişiklik ile derlenir. Ancak, bu değişiklik ısrarlı çift Dönüştürmelere bağlı kodu keser. Bu tür kodlar genellikle dönüştürmenin bir parçası açıkça (örneğin, `make_pair(static_cast<B>(a), x)` bekleyen bir işleve geçirerek) düzeltilebilir `pair<C, X>` .

- Visual Studio 2010 benzetimi yapılmış bağımsız şablonlar — Örneğin, `make_shared<T>(arg1, arg2, argN)` en fazla 10 bağımsız değişken, ön yükleme ve uzmanlık alanı Önişlemci makineler ile zaman damgalandırabilir. Visual Studio 2012 ' de, bu sınır, çoğu kullanıcı için derleme sürelerini ve derleyici bellek tüketimini geliştirmek üzere beş bağımsız değişkene indirilir. Ancak, _VARIADIC_MAX bir önceki sınırı, açıkça 10, proje genelinde tanımlayarak ayarlayabilirsiniz.

- C++ 11 17.6.4.3.1 [Macro. Names]/2 yasaklıyor C++ standart kitaplık başlıkları dahil edildiğinde anahtar kelimelerin Makro değişikliği. Üstbilgiler, makro tarafından değiştirilmiş anahtar sözcükleri algılarsa artık derleyici hatalarını yayar. (_ALLOW_KEYWORD_MACROS tanımlama, bu tür kodun derlenmesine izin verir, ancak bu kullanımı kesinlikle önermiyoruz.) Bir özel durum olarak, `new` üst bilgilerin ' ı kullanarak kendi kendini savunması nedeniyle, varsayılan olarak öğesinin makro biçimine izin verilir `#pragma push_macro("new")` / `#undef new` / `#pragma pop_macro("new")` . _ENFORCE_BAN_OF_MACRO_NEW tanımlama, tam olarak adının ne kadar ifade olduğunu gösterir.

- Çeşitli iyileştirmeler ve hata ayıklama denetimleri uygulamak için C++ standart kitaplığı uygulaması, Visual Studio sürümleri arasında (2005, 2008, 2010, 2012) ikili uyumluluğu kasıtlı olarak keser. C++ Standart Kitaplığı kullanıldığında, farklı sürümler kullanılarak derlenen nesne dosyalarının ve statik kitaplıkların tek bir ikili (EXE veya DLL) içinde karıştırılması ve farklı sürümler kullanılarak derlenen ikili dosyalar arasında C++ standart kitaplık nesnelerinin geçirilmesi yasaklıyor. Nesne dosyalarının ve statik kitaplıkların karıştırılması (Visual Studio 2010 kullanılarak derlenen C++ standart kitaplığı, Visual Studio 2012 'da C++ derleyicisi kullanılarak derlenmiş olan C++ standart kitaplığını kullanarak), _MSC_VER derleyicinin ana sürümünü (Visual Studio 2012 ' te Visual C++ için 1700) içeren makro olduğu _MSC_VER uyuşmazlığı hakkında bağlayıcı hataları yayar. Bu denetim, DLL karıştırmasını algılayamaz ve Visual Studio 2008 veya önceki bir sürümünü içeren karıştırma 'yı algılayamaz.

- Visual Studio 2010 ' de uygulanan _ITERATOR_DEBUG_LEVEL uyuşmazlıklarını algılamaya ek olarak, Visual Studio 2012 ' de C++ derleyicisi çalışma zamanı kitaplığı uyuşmazlıklarını algılar. Bu uyuşmazlıklar derleyici seçenekleri `/MT` (statik sürüm), `/MTd` (statik hata ayıklama), `/MD` (dinamik sürüm) ve `/MDd` (dinamik hata ayıklama) karmaysa oluşur.

- `operator<()`, `operator>()` , `operator<=()` ve `operator>=()` daha önce kapsayıcı aileleri için kullanılabilir `std::unordered_map` `stdext::hash_map` , ancak uygulamaları yararlı olmasa da. Bu standart olmayan operatörler, Visual Studio 2012 ' de Visual C++ kaldırılmıştır. Ayrıca, `operator==()` `operator!=()` ailesi için ve `std::unordered_map` ailesi, aileyi kapsayacak şekilde genişletilmiştir `stdext::hash_map` . ( `stdext::hash_map` Ailenin yeni koddaki kullanımını önlemenize öneririz.)

- C++ 11 22.4.1.4 [locale. codecvt], bu olduğunu belirtir `codecvt::length()` ve `codecvt::do_length()` değiştirilebilir `stateT&` Parametreler almalıdır, ancak Visual Studio 2010 sürdü `const stateT&` . Visual Studio 2012 ' de C++ derleyicisi, `stateT&` Standart tarafından uygulanan olarak alır. Bu fark, sanal işlevi geçersiz kılmaya çalışan herkes için önemlidir `do_length()` .

### <a name="crt"></a>CRT

- New ve malloc () için kullanılan C çalışma zamanı (CRT) yığını artık özel değildir. CRT şimdi işlem yığınını kullanır. Bu, bir DLL kaldırıldığında yığının yok edilmeyeceği anlamına gelir. bu nedenle, statik olarak CRT 'ye bağlanan dll 'Ler bellekten kaldırılmadan önce temizlenir.

- `iscsymf()`İşlevi negatif değerlerle onaylar.

- `threadlocaleinfostruct`Yapı, yerel ayar işlevlerine yapılan değişikliklere uyum sağlayacak şekilde değiştirilmiştir.

- Gibi karşılık gelen iç bilgileri olan CRT işlevleri `memxxx()` `strxxx()` Intrin. h öğesinden kaldırılır. Intrin. h ' yi yalnızca bu işlevler için eklediyseniz, artık karşılık gelen CRT üst bilgilerini eklemeniz gerekir.

### <a name="mfc-and-atl"></a>MFC ve ATL

- Fusion desteği kaldırıldı (afxcomctl32. h); Bu nedenle, içinde tanımlanan tüm yöntemler \<afxcomctl32.h> kaldırılmıştır. Üst bilgi dosyaları \<afxcomctl32.h> ve \<afxcomctl32.inl> silinmiş.

- Adı `CDockablePane::RemoveFromDefaultPaneDividier` olarak değiştirildi `CDockablePane::RemoveFromDefaultPaneDivider` .

- İmzasını, `CFileDialog::SetDefExt` LPCTSTR kullanacak şekilde değiştirdi; bu nedenle Unicode derlemeler etkilenir.

- Kullanılmayan ATL İzleme kategorileri kaldırıldı.

- ' A ait imzayı `CBasePane::MoveWindow` alacak şekilde değiştirdi `const CRect` .

- İmzasını değiştirdi `CMFCEditBrowseCtrl::EnableBrowseButton` .

- `CMFCBaseTabCtrl` içinden `m_fntTabs` ve `m_fntTabsBold` kaldırıldı.

- Oluşturuculara bir parametre eklendi `CMFCRibbonStatusBarPane` . (Bu, varsayılan bir parametredir ve bu nedenle kaynak bölünmez.)

- Oluşturucuya bir parametre eklendi `CMFCRibbonCommandsListBox` . (Bu, varsayılan bir parametredir ve bu nedenle kaynak bölünmez.)

- `AFXTrackMouse`API (ve ilgili süreölçer proc) kaldırıldı. `TrackMouseEvent`Bunun yerine Win32 API 'sini kullanın.

- Oluşturucuya bir parametre eklendi `CFolderPickerDialog` . (Bu, varsayılan bir parametredir ve bu nedenle kaynak bölünmez.)

- `CFileStatus`yapı boyutu değişti: `m_attribute` üye bayttan DWORD 'e (döndürülen değerle eşleşecek şekilde `GetFileAttributes` ) değişti.

- `CRichEditCtrl`ve `CRichEditView` Unicode derlemeleriyle RICHEDIT_CLASS (richedit 3,0 denetimi) yerine MSFTEDIT_CLASS (richedit 4,1 denetim) kullanın.

- `AFX_GLOBAL_DATA::IsWindowsThemingDrawParentBackground`Windows Vista, Windows 7 ve Windows 8 ' de her zaman doğru olduğundan kaldırıldı.

- `AFX_GLOBAL_DATA::IsWindowsLayerSupportAvailable`Windows Vista, Windows 7 ve Windows 8 ' de her zaman doğru olduğundan kaldırıldı.

- Kaldırıldı `AFX_GLOBAL_DATA::DwmExtendFrameIntoClientArea` . Windows Vista, Windows 7 ve Windows 8 ' de doğrudan Windows API 'yi çağırın.

- Kaldırıldı `AFX_GLOBAL_DATA::DwmDefWindowProc` . Windows Vista, Windows 7 ve Windows 8 ' de doğrudan Windows API 'yi çağırın.

- `AFX_GLOBAL_DATA::DwmIsCompositionEnabled` `IsDwmCompositionEnabled` Ad çarpışmasını ortadan kaldırmak için olarak yeniden adlandırıldı.

- Bir dizi MFC iç zamanlayıcılar için tanımlayıcılar değiştirildi ve tanımları afxres. h (AFX_TIMER_ID_ *) öğesine taşındı.

- `OnExitSizeMove`ON_WM_EXITSIZEMOVE makrosunu kabul etmek için yönteminin imzasını değiştirdi:

  - `CFrameWndEx`

  - `CMDIFrameWndEx`

  - `CPaneFrameWnd`

- Adı ve imzası `OnDWMCompositionChanged` ON_WM_DWMCOMPOSITIONCHANGED makroyla kabul edilecek şekilde değiştirildi:

  - `CFrameWndEx`

  - `CMDIFrameWndEx`

  - `CPaneFrameWnd`

- `OnMouseLeave`ON_WM_MOUSELEAVE makrosunu kabul etmek için yönteminin imzasını değiştirdi:

  - `CMFCCaptionBar`

  - `CMFCColorBar`

  - `CMFCHeaderCtrl`

  - `CMFCProperySheetListBox`

  - `CMFCRibbonBar`

  - `CMFCRibbonPanelMenuBar`

  - `CMFCRibbonRichEditCtrl`

  - `CMFCSpinButtonCtrl`

  - `CMFCToolBar`ReplaceThisText

  - `CMFCToolBarComboBoxEdit`

  - `CMFCToolBarEditCtrl`

  - `CMFCAutoHideBar`

- İmza `OnPowerBroadcast` ON_WM_POWERBROADCAST makro ile kabul edilecek şekilde değiştirildi:

  - `CFrameWndEx`

  - `CMDIFrameWndEx`

- İmza `OnStyleChanged` ON_WM_STYLECHANGED makro ile kabul edilecek şekilde değiştirildi:

  - `CMFCListCtrl`

  - `CMFCStatusBar`

- İç yöntemi olarak yeniden `FontFamalyProcFonts` adlandırıldı `FontFamilyProcFonts` .

- `CString`Bazı durumlarda (#defines ile değiştirilmiş) ve aşağıdaki sınıf üyesi değişkenleriyle bellek sızıntılarını ortadan kaldırmak için çok sayıda genel statik nesne kaldırıldı:

  - `CKeyBoardManager::m_strDelimiter`

  - `CMFCPropertyGridProperty::m_strFormatChar`

  - `CMFCPropertyGridProperty::m_strFormatShort`

  - `CMFCPropertyGridProperty::m_strFormatLong`

  - `CMFCPropertyGridProperty::m_strFormatUShort`

  - `CMFCPropertyGridProperty::m_strFormatULong`

  - `CMFCPropertyGridProperty::m_strFormatFloat`

  - `CMFCPropertyGridProperty::m_strFormatDouble`

  - `CMFCToolBarImages::m_strPngResType`

  - `CMFCPropertyGridProperty::m_strFormat`

- İmzası değiştirildi `CKeyboardManager::ShowAllAccelerators` ve Hızlandırıcı sınırlayıcısı parametresi kaldırıldı.

- `CPropertyPage::GetParentSheet`, Ve ' a eklenen, `CPropertyPage` `GetParent` üst veya bir üst pencere olabilecek doğru üst sayfa penceresini almak için yerine bunu çağırın `CPropertyPage` . Yerine çağırmak için kodunuzu değiştirmeniz gerekebilir `GetParentSheet` `GetParent` .

- ATLBASE 'de dengesiz #pragma Uyarısı (push) düzeltildi. Uyarı, uyarıların yanlış şekilde devre dışı bırakılmasının oluşmasına neden olur. Bu uyarılar artık ATLBASE sonrasında doğru şekilde etkinleştirilmiştir. H ayrıştırıldı.

- D2D ile ilgili yöntemleri AFX_GLOBAL_DATA 'den _AFX_D2D_STATE taşındı:

  - `GetDirectD2dFactory`

  - `GetWriteFactory`

  - `GetWICFactory`

  - `InitD2D`

  - `ReleaseD2DRefs`

  - `IsD2DInitialized`

  - `D2D1MakeRotateMatrix`

  - Örneğin, çağırmak yerine, çağrısı yapın `afxGlobalData.IsD2DInitialized` `AfxGetD2DState->IsD2DInitialized` .

- Kullanılmayan ATL * kaldırıldı. \Atlmfc\include\ klasöründen CPP dosyaları.

- `afxGlobalData`Gereksinimleri karşılamak için başlatma, CRT başlatma süresi yerine isteğe bağlı olarak taşındı `DLLMain` .

- `RemoveButtonByIndex`Yöntemi `CMFCOutlookBarPane` sınıfına eklendi.

- `CMFCCmdUsageCount::IsFreqeuntlyUsedCmd`Olarak düzeltildi `IsFrequentlyUsedCmd` .

- İçin birkaç örneği düzeltildi `RestoreOriginalstate` `RestoreOriginalState (CMFCToolBar, CMFCMenuBar, CMFCOutlookBarPane)` .

- Kullanılmayan Yöntemler şuradan kaldırıldı `CDockablePane` : `SetCaptionStyle` , `IsDrawCaption` , `IsHideDisabledButtons` , `GetRecentSiblingPaneInfo` , ve `CanAdjustLayout` .

- `CDockablePane`Statik üye değişkenleri `m_bCaptionText` ve kaldırılır `m_bHideDisabledButtons` .

- İçin bir geçersiz kılma `DeleteString` yöntemi eklendi `CMFCFontComboBox` .

- Kullanılmayan Yöntemler şuradan kaldırıldı `CPane` : `GetMinLength` ve `IsLastPaneOnLastRow` .

- Olarak yeniden adlandırıldı `CPane::GetDockSiteRow(CDockingPanesRow *)` `CPane::SetDockSiteRow` .

## <a name="visual-studio-2010-breaking-changes"></a>Visual Studio 2010 son değişiklikleri

### <a name="compiler"></a>Derleyici

- **Auto** anahtar sözcüğünün yeni bir varsayılan anlamı vardır. Eski anlamının kullanılması nadir olduğundan, çoğu uygulama bu değişiklikten etkilenmez.

- Yeni **static_assert** anahtar sözcüğü tanıtılmıştır, bu, kodunuzda bu adda bir tanımlayıcı zaten varsa ad çakışmasına neden olur.

- Yeni lambda gösterimi desteği, bir IDL UUID özniteliğinde tırnak işareti olmayan bir GUID kodlama desteğini dışlar.

- .NET Framework 4, bozuk durum özel durumları kavramını tanıtır, bu, bir işlemi kurtarılamaz bozulmuş bir durumda bırakır. Varsayılan olarak, diğer tüm özel durumları yakalayan/EHa derleyici seçeneğiyle birlikte bozuk bir durum özel durumu yakalayamaz.                 Bozuk bir durum özel durumunu açık bir şekilde yakalamak için __try \_ _Except deyimlerini kullanın. Ya da, bozuk durum özel durumlarını yakalamak için bir işlevi etkinleştirmek üzere [HandledProcessCorruptedStateExceptions] özniteliğini uygulayın.  Bu değişiklik, bozuk bir durum özel durumunu yakalamak zorunda olabilecek öncelikle sistem programcıları etkiler. Sekiz özel durum STATUS_ACCESS_VIOLATION, STATUS_STACK_OVERFLOW, EXCEPTION_ILLEGAL_INSTRUCTION, EXCEPTION_IN_PAGE_ERROR, EXCEPTION_INVALID_DISPOSITION, EXCEPTION_NONCONTINUABLE_EXCEPTION, EXCEPTION_PRIV_INSTRUCTION, STATUS_UNWIND_CONSOLIDATE.                 Bu özel durumlar hakkında daha fazla bilgi için bkz. [GetExceptionCode](/windows/win32/Debug/getexceptioncode) makrosu.

- `/GS`Arabellek taşmalarına karşı yeniden düzenlenen derleyici seçenek koruyucuları, önceki sürümlerden daha kapsamlı olarak daha anlaşılır. Bu sürüm, yığındaki, performansı azaletkileyebilecek ek güvenlik denetimleri ekleyebilir. `__declspec(safebuffers)`Derleyiciye belirli bir işlev için güvenlik denetimleri eklemediğini bildirmek için New anahtar sözcüğünü kullanın.

- Hem `/GL` (program iyileştirmesi) hem de `/clr` (ortak dil çalışma zamanı derlemesi) derleyici seçenekleriyle derlerseniz, `/GL` seçenek yok sayılır. Derleyici seçeneklerinin birleşimi çok az avantaj sağladığından bu değişiklik yapılmıştır. Bu değişikliğin sonucu olarak, yapı performansı geliştirilmiştir.

- Varsayılan olarak, trigraf desteği Visual Studio 2010 ' de devre dışıdır. `/Zc:trigraphs`Trigraf desteğini etkinleştirmek için derleyici seçeneğini kullanın. Üçlü grafik, birbirini izleyen iki soru işaretinden ("??") ve ardından benzersiz bir üçüncü karakterle oluşur. Derleyici, bir trigraf ile karşılık gelen noktalama karakterini değiştirir. Örneğin, derleyici `??=` trigraf ' # ' karakteriyle değiştirilir. Bazı noktalama karakterleri için kullanışlı grafik gösterimleri içermeyen bir karakter kümesi kullanan C kaynak dosyalarında trigraf kullanın.

- Bağlayıcı artık Windows 98 için iyileştirme 'yi desteklemiyor. `/OPT`Veya belirtirseniz (iyileştirmeler) seçeneği bir derleme zamanı hatası üretir `/OPT:WIN98` `/OPT:NOWIN98` .

- RuntimeLibrary ve DebugInformationFormat derleme sistemi özellikleri tarafından belirtilen varsayılan derleyici seçenekleri değiştirildi. Varsayılan olarak, bu derleme özellikleri 7,0 ile 10,0 arasında Visual C++ yayımları tarafından oluşturulan projelerde belirtilmiştir. Visual C++ 6,0 tarafından oluşturulan bir projeyi geçiriyorsanız, bu özellikler için bir değer belirtip belirtmeyeceğinizi göz önünde bulundurun.

- Visual Studio 2010, RuntimeLibrary = çok Iş parçacıklı ( `/MD` ) ve DebugInformationFormat = ProgramDatabase ( `/Zi` ) içinde. Visual C++ 9,0, RuntimeLibrary = çok Iş parçacıklı ( `/MT` ) ve DebugInformationFormat = Disabled.

### <a name="clr"></a>CLR

- Microsoft C# ve Visual Basic derleyicileri artık hiç bir birincil birlikte çalışma derlemesi (No-PIA) oluşturabilir. PIA olmayan bir derleme ilgili birincil birlikte çalışma derlemesinin (PIA) dağıtımı olmadan COM türlerini kullanabilir. Visual C# veya Visual Basic tarafından üretilen PIA derlemelerini tüketerek, kitaplığı kullanan PIA olmayan bir derlemeye başvurmadan önce derleme komutunda PIA derlemesine başvurmanız gerekir.

### <a name="visual-studio-c-projects-and-msbuild"></a>Visual Studio C++ projeleri ve MSBuild

- Visual Studio C++ projeleri artık MSBuild aracını temel alır. Sonuç olarak, proje dosyaları yeni bir XML dosya biçimi ve. vcxproj dosya sonekini kullanır. Visual Studio 2010, Visual Studio 'nun önceki sürümlerinden proje dosyalarını otomatik olarak yeni dosya biçimine dönüştürür. Varolan bir proje, önceki derleme aracına, VCBUILD.exe veya proje dosyası sonekine (. vcproj) bağımlıysa etkilenir.

- Daha önceki sürümlerde, Visual C++ Özellik sayfalarının geç değerlendirmesini destekliyordu. Örneğin, bir üst özellik sayfası bir alt özellik sayfasını içeri aktarabilir ve üst öğe diğer değişkenleri tanımlamak için alt öğede tanımlanan bir değişken kullanabilir. Geç değerlendirme, alt özellik sayfası içeri aktarılmadan önce bile alt değişkeni kullanmak için üst öğeyi etkinleştirdi. Visual Studio 2010 ' de, MSBuild yalnızca erken değerlendirmeyi desteklediğinden, proje sayfası değişkeni tanımlanmadan önce kullanılamaz.

### <a name="ide"></a>IDE

- Uygulama sonlandırma iletişim kutusu artık bir uygulamayı sonlandırmayacaktır. Önceki sürümlerde, `abort()` veya `terminate()` işlevi bir uygulamanın perakende derlemesini kapattığı zaman, C çalışma zamanı kitaplığı bir konsol penceresinde veya iletişim kutusunda bir uygulama sonlandırma iletisi görüntülendi. İleti, "Bu uygulama çalışma zamanının olağan dışı bir şekilde sonlanma biçimini istedi. Daha fazla bilgi için lütfen uygulamanın destek ekibine başvurun. " Windows daha sonra Windows Hata Bildirimi (Dr. Watson) iletişim kutusu veya Visual Studio hata ayıklayıcısı olan geçerli sonlandırma işleyicisini görüntülendiğinden, uygulama sonlandırma iletisi gereksizdir. Visual Studio 2010 ' den başlayarak, C çalışma zamanı kitaplığı iletiyi görüntülemez. Ayrıca, çalışma zamanı bir hata ayıklayıcı başlamadan önce uygulamanın sonlandırmasını önler. Bu, yalnızca uygulama sonlandırma iletisinin önceki davranışına bağlı olduğunuzda son bir değişiklikten oluşur.

- Özellikle Visual Studio 2010 için IntelliSense, C++/CLı kodu veya öznitelikleri için çalışmaz, **tüm başvuruları bul** yerel değişkenler için çalışmaz ve kod modeli içeri aktarılan derlemelerden tür adlarını almaz ya da türleri tamamen nitelenmiş adlarına çözmez.

### <a name="libraries"></a>Kitaplıklar

- SafeInt sınıfı Visual C++ eklenmiştir ve artık ayrı bir indirme işlemi içinde değildir. Bu, yalnızca "SafeInt" adlı bir sınıf geliştirdiyseniz bir son değişiklik olur.

- Kitaplıklar dağıtım modeli, dinamik bağlantı kitaplığının belirli bir sürümünü bulmak için artık bildirimleri kullanmaz. Bunun yerine, her dinamik bağlantı kitaplığının adı sürüm numarasını içerir ve bu adı kitaplığı bulmak için kullanırsınız.

- Visual Studio 'nun önceki sürümlerinde çalışma zamanı kitaplıklarını yeniden oluşturabilirsiniz. Visual Studio 2010 artık C çalışma zamanı kitaplık dosyalarının kopyalarını oluşturmayı desteklememektedir.

### <a name="standard-library"></a>Standart Kitaplık

- \<iterator>Üst bilgi artık diğer birçok üstbilgi dosyası tarafından otomatik olarak dahil değildir. Bunun yerine, üst bilgide tanımlanan tek başına yineleyiciler için desteğe ihtiyacınız varsa bu üstbilgiyi açık bir şekilde ekleyin. Varolan bir proje, önceki derleme aracına, VCBUILD.exe veya proje dosya sonekine (. vcproj. Iterator) bağımlıysa etkilenir.

- \<algorithm>Üst bilgide, checked_ * ve unchecked_ \* işlevleri kaldırılır. \<iterator>> üst bilgisinde, `checked_iterator` sınıfı kaldırılır ve `unchecked_array_iterator` sınıfı eklenmiştir.

- `CComPtr::CComPtr(int)`Oluşturucu kaldırılır. Bu Oluşturucu, `CComPtr` null makrodan bir nesnenin oluşturulmasını izin verdi, ancak gereksizdir ve sıfır olmayan tamsayılarla izin verilen nonsensical kurulumlarını.

   `CComPtr`Yine de 0 olarak tanımlanan null 'dan oluşturulabilir, ancak 0 ' dan farklı bir tamsayıdan oluşturulmuşsa başarısız olur. Bunun yerine **nullptr** kullanın.

- Aşağıdaki `ctype` üye işlevleri kaldırılmıştır: `ctype::_Do_narrow_s` , `ctype::_Do_widen_s` , `ctype::_narrow_s` , `ctype::_widen_s` . Bir uygulama bu üye işlevlerinden birini kullanıyorsa, bunu karşılık gelen güvenli olmayan sürümle değiştirmelisiniz: `ctype::do_narrow` , `ctype::do_widen` , `ctype::narrow` , `ctype::widen` .

### <a name="crt-mfc-and-atl-libraries"></a>CRT, MFC ve ATL kitaplıkları

- Kullanıcıların CRT, MFC ve ATL kitaplıklarını oluşturması için destek kaldırılmıştır. Örneğin, uygun NMAKE dosyası sağlanmaz. Ancak, kullanıcıların bu kitaplıkların kaynak koduna erişimi hala vardır. Ve Microsoft 'un bu kitaplıkları oluşturmak için kullandığı MSBuild seçeneklerini tanımlayan bir belge, büyük olasılıkla bir Visual C++ ekip bloguna gönderilir.

- IA64 için MFC desteği kaldırılmıştır. Ancak, ıA64 üzerinde CRT ve ATL desteği yine de sağlanır.

- Sıra sayıları artık MFC modül tanımı (. def) dosyalarında yeniden kullanılamaz. Bu değişiklik sıra sayıları alt sürümler arasında farklı olmayacaktır ve hizmet paketleri ve hızlı çözüm mühendislik sürümleri için ikili uyumluluk iyileştirilen anlamına gelir.

- Sınıfa yeni bir sanal işlev eklendi `CDocTemplate` . Bu yeni sanal işlev [CDocTemplate sınıfıdır](../mfc/reference/cdoctemplate-class.md). Önceki sürümünde `OpenDocumentFile` iki parametre vardı. Yeni sürümün üç parametresi vardır. Yeniden başlatma yöneticisini desteklemek için, öğesinden türetilmiş herhangi bir sınıf `CDocTemplate` üç parametreye sahip sürümü uygulamalıdır. Yeni parametresi `bAddToMRU` .

### <a name="macros-and-environment-variables"></a>Makrolar ve ortam değişkenleri

- Ortam değişkeni __MSVCRT_HEAP_SELECT artık desteklenmiyor. Bu ortam değişkeni kaldırılır ve değişiklik yoktur.

### <a name="microsoft-macro-assembler-reference"></a>Microsoft Macro Assembler Başvurusu

- Microsoft Macro Assembler başvurusu derleyicisinden birkaç yönergeler kaldırılmıştır. Kaldırılan yönergeler,,,,, ve ' dir `.186` `.286` `.286P` `.287` `.8086` `.8087` `.NO87` .

## <a name="visual-studio-2008-breaking-changes"></a>Visual Studio 2008 son değişiklikleri

### <a name="compiler"></a>Derleyici

- Windows 95, Windows 98, Windows ME ve Windows NT platformları artık desteklenmemektedir. Bu işletim sistemleri Hedeflenen platformlar listesinden kaldırılmıştır.

- Derleyici artık doğrudan ATL sunucusu ile ilişkili birden çok özniteliği desteklememektedir. Aşağıdaki öznitelikler artık desteklenmiyor:

  - perf_counter

  - perf_object

  - sin

  - request_handler

  - soap_handler

  - soap_header

  - soap_method

  - tag_name

### <a name="visual-studio-c-projects"></a>Visual Studio C++ projeleri

- Projeleri Visual Studio 'nun önceki sürümlerinden yükseltirken, WINVER ve _WIN32_WINNT makrolarını, 0x0500 ' dan büyük veya buna eşit olacak şekilde değiştirmeniz gerekebilir.

- Visual Studio 2008 ' den başlayarak yeni proje Sihirbazı, C++ SQL Server projesi oluşturma seçeneğine sahip değildir. Visual Studio 'nun önceki bir sürümü kullanılarak oluşturulan SQL Server projeler yine de derleyip doğru çalışacaktır.

- Windows API üstbilgi dosyası Wınable. h kaldırılmıştır. Bunun yerine Winuser. h ekleyin.

- Windows API kitaplığı Rpcndr. lib kaldırılmıştır. Bunun yerine rpcrt4. lib ile bağlantı yapın.

### <a name="crt"></a>CRT

- Windows 95, Windows 98, Windows Millennium Edition ve Windows NT 4,0 desteği kaldırılmıştır.

- Aşağıdaki genel değişkenler kaldırılmıştır:

  - _osplatform

  - _osver

  - _winmajor

  - _winminor

  - _winver

- Aşağıdaki işlevler kaldırılmıştır. Windows API işlevlerini kullanın `GetVersion` veya `GetVersionEx` bunun yerine:

  - _get_osplatform

  - _get_osver

  - _get_winmajor

  - _get_winminor

  - _get_winver

- SAL ek açıklamaları için sözdizimi değişti. Daha fazla bilgi için bkz. [sal ek açıklamaları](../c-runtime-library/sal-annotations.md).

- IEEE filtresi artık SSE 4,1 yönerge kümesini desteklemektedir. Daha fazla bilgi için bkz. [_fpieee_flt](../c-runtime-library/reference/fpieee-flt.md)_fpieee_flt.

- Visual Studio ile birlikte gelen C çalışma zamanı kitaplıkları artık sistem DLL msvcrt.dll bağımlı değildir.

### <a name="standard-library"></a>Standart Kitaplık

- Windows 95, Windows 98, Windows Millennium Edition ve Windows NT 4,0 desteği kaldırılmıştır.

- Hata ayıklama modunda derlenirken _HAS_ITERATOR_DEBUGGING tanımlı (Visual Studio 2010 ' den sonra [_ITERATOR_DEBUG_LEVEL](../standard-library/iterator-debug-level.md) tarafından değiştirildi), bir yineleyici, temel alınan kapsayıcının sınırlarını arttırmak veya azaltmak istediğinde bir uygulama artık bu şekilde değişir.

- Stack sınıfının c üyesi değişkeni artık korumalı olarak bildirilmiştir. Daha önce Bu üye değişkeni genel olarak bildirildi.

- Davranışı `money_get::do_get` değişti. Daha önce, tarafından için çağrılmasından daha fazla kesir basamağıyla bir parasal tutar ayrıştırılırken `frac_digits` , `do_get` Tümünü tüketmek için kullanılır. Şimdi, `do_get` en çok karakter tükettikten sonra ayrıştırmayı durduruyor `frac_digits` .

### <a name="atl"></a>ATL

- ATL, CRT üzerinde bağımlılık olmadan derlenebilir. Visual Studio 'nun önceki sürümlerinde, #define ATL_MIN_CRT kullanarak ATL projesini CRT 'ye en az bağımlı hale getirebilirsiniz. Visual Studio 2008 ' de, ATL_MIN_CRT tanımlanıp tanımlanmadığına bakılmaksızın tüm ATL projeleri CRT 'ye göre en düşük düzeyde bağımlıdır.

- ATL sunucu kod temeli, CodePlex 'te paylaşılan kaynak proje olarak yayımlanmıştır ve Visual Studio 'nun bir parçası olarak yüklenmez. Atlenc. h ve yardımcı program işlevleri ve, atlutil. h ve atlpath. h tarafından oluşturulan işlevlerin ve Kodlamadaki veri kodlama ve kod çözme sınıfları tutulmuştur ve artık ATL Kitaplığı 'nın bir parçasıdır. ATL Server ile ilişkili birçok dosya artık Visual Studio 'nun bir parçası değildir.

- Bazı işlevler artık DLL 'ye dahil değildir. İçeri aktarma kitaplığı 'nda hala bulunur. Bu, işlevleri statik olarak kullanan kodu etkilemez. Bu, yalnızca dinamik olarak bu işlevleri kullanan kodu etkileyecektir.

- PROP_ENTRY ve PROP_ENTRY_EX makrolar kullanımdan kaldırılmıştır ve PROP_ENTRY_TYPE makrolar ile değiştirilmiştir ve güvenlik nedenleriyle PROP_ENTRY_TYPE_EX.

### <a name="atlmfc-shared-classes"></a>ATL/MFC Paylaşılan Sınıfları

- ATL, CRT üzerinde bağımlılık olmadan derlenebilir. Visual Studio 'nun önceki sürümlerinde, `#define ATL_MIN_CRT` ATL PROJESINI CRT 'ye en düşük düzeyde bağımlı hale getirmek için kullanabilirsiniz. Visual Studio 2008 ' de, ATL_MIN_CRT tanımlanıp tanımlanmadığına bakılmaksızın tüm ATL projeleri CRT 'ye göre en düşük düzeyde bağımlıdır.

- ATL sunucu kod temeli, CodePlex 'te paylaşılan kaynak proje olarak yayımlanmıştır ve Visual Studio 'nun bir parçası olarak yüklenmez. Atlenc. h ve yardımcı program işlevleri ve, atlutil. h ve atlpath. h tarafından oluşturulan işlevlerin ve Kodlamadaki veri kodlama ve kod çözme sınıfları tutulmuştur ve artık ATL Kitaplığı 'nın bir parçasıdır. ATL Server ile ilişkili birçok dosya artık Visual Studio 'nun bir parçası değildir.

- Bazı işlevler artık DLL 'ye dahil değildir. İçeri aktarma kitaplığı 'nda hala bulunur. Bu, işlevleri statik olarak kullanan kodu etkilemez. Bu, yalnızca dinamik olarak bu işlevleri kullanan kodu etkileyecektir.

### <a name="mfc"></a>MFC

- `CTime`Sınıf: `CTime` sınıf artık 1/1/1900 'den başlayan tarihleri kabul C.E. yerine 1/1/1970 C.E.

- MFC iletişim kutularında denetimlerin sekme sırası: bir MFC iletişim kutusunda birden fazla denetimin doğru sekme düzeni, bir MFC ActiveX denetimi sekme sırasına eklenirse, bu durumda olur. Bu değişiklik, bu sorunu düzeltir.

   Örneğin, ActiveX denetimine ve birkaç düzenleme denetimine sahip bir MFC iletişim uygulaması oluşturun. ActiveX denetimini düzenleme denetimlerinin sekme sırasının ortasına konumlandırın. Uygulamayı başlatın, sekme sırası ActiveX denetiminden sonra gelen bir düzenleme denetimine tıklayın ve sonra sekme. bu değişiklikten önce, odak, sekme düzeninde bulunan bir sonraki düzenleme denetimi yerine, ActiveX denetimini izleyen düzenleme denetimine gitti.

- `CFileDialog`Sınıf: sınıf için özel şablonlar `CFileDialog` Windows Vista 'ya otomatik olarak alınamaz. Bunlar hala kullanılabilir, ancak ek işlevlere veya Windows Vista stil iletişim kutularına bakmayacak.

- `CWnd`Sınıf ve `CFrameWnd` sınıf: `CWnd::GetMenuBarInfo` Yöntem kaldırılmıştır.

   `CFrameWnd::GetMenuBarInfo`Yöntemi artık sanal olmayan bir yöntemdir. Daha fazla bilgi için Windows SDK **GetMenuBarInfo işlevine** bakın.

- MFC ISAPI desteği: MFC artık Internet sunucusu uygulama programı arabirimi (ISAPI) ile uygulama oluşturmayı desteklememektedir. Bir ISAPI uygulaması oluşturmak istiyorsanız, ISAPI uzantılarını doğrudan çağırın.

- Kullanım dışı bırakılmış ANSI API 'Leri: birkaç MFC yönteminin ANSI sürümleri kullanım dışıdır. Gelecekteki uygulamalarınızda bu yöntemlerin Unicode sürümlerini kullanın. Daha fazla bilgi için bkz. **Windows Vista ortak denetimleri Için derleme gereksinimleri**.

## <a name="visual-studio-2005-breaking-changes"></a>Visual Studio 2005 son değişiklikleri

### <a name="crt"></a>CRT

- Birçok işlev kullanımdan kaldırılmıştır. Bkz. **kullanım DıŞı CRT işlevleri**.

- Birçok işlev artık parametrelerini doğrular, geçersiz parametreler verildiğinde yürütmeyi durdurur. Bu doğrulama, geçersiz parametreleri geçen ve bunları yoksayma veya yalnızca bir hata kodu döndüren işleve dayanan kodu bozabilir. Bkz. **parametre doğrulama**.

- Dosya tanımlayıcısı değeri-2 artık, `stdout` `stderr` Örneğin, konsol penceresi olmayan bir Windows uygulamasında çıktı için kullanılabilir olmadığını belirtmek için kullanılır. Kullanılan önceki değer-1 ' dir. Daha fazla bilgi için bkz. [_fileno](../c-runtime-library/reference/fileno.md).

- Tek iş parçacıklı CRT kitaplıklar (libc. lib ve libcd. lib) kaldırılmıştır. Çok iş parçacıklı CRT kitaplıklarını kullanın. `/ML`Derleyici bayrağı artık desteklenmiyor. Çok iş parçacıklı kod ve tek iş parçacıklı kod arasındaki performans farkının potansiyel olarak önemli olduğu durumlarda bazı işlevlerin kilitleme dışı sürümleri eklenmiştir.

- Pow, Double POW (int, int) aşırı yüklemesi, standart ile daha iyi uyum sağlamak için kaldırılmıştır.

- % N Biçim Belirleyicisi, doğal olarak güvenli olmayan işlevlerin hiçbirinde varsayılan olarak desteklenmemektedir. % N ile karşılaşılırsa, varsayılan davranış geçersiz parametre işleyicisini çağırmak olur. % N desteğini etkinleştirmek için kullanın `_set_printf_count_output` (Ayrıca bkz `_get_printf_count_output` .).

- `sprintf`Şimdi işaretli sıfır eksi işaretini yazdırır.

- `swprintf`, standart ile uyumlu olacak şekilde değiştirilmiştir; Artık bir boyut parametresi gerektirir. `swprintf`Boyut parametresi olmayan biçim kullanım dışı bırakılmıştır.

- `_set_security_error_handler`kaldırıldı. Bu işleve yapılan çağrıları kaldırın; varsayılan işleyici, güvenlik hatalarıyla ilgilenmenin çok daha güvenli bir yoludur.

- `time_t`Artık 64 bitlik bir değerdir (_USE_32BIT_TIME_T tanımlanmadığı müddetçe).

- , `_spawn` `_wspawn` Işlevleri artık `errno` C standardı tarafından belirtildiği gibi, başarılı ' i dokunulmamış olarak bırakır.

- RTC artık varsayılan olarak geniş karakterler kullanıyor.

- Kayan nokta denetimi sözcük desteği işlevleri, veya ile derlenen uygulamalar için kullanımdan kaldırılmıştır `/CLR` `/CLR:PURE` . Etkilenen işlevler,,,,, `_clear87` `_clearfp` `_control87` `_controlfp` `_fpreset` `_status87` , `_statusfp` . _CRT_MANAGED_FP_NO_DEPRECATE tanımlayarak kullanımdan kaldırma uyarısını devre dışı bırakabilirsiniz, ancak bu işlevlerin yönetilen kodda kullanılması tahmin edilemez ve desteklenmez.

- Bazı işlevler artık const işaretçileri döndürüyor. Eski, const olmayan davranış _CONST_RETURN tanımlayarak daha sonra belirtilebilir. Etkilenen işlevler şunlardır

  - memchr, wmemchr

  - strchr, wcschr, _mbschr, _mbschr_l

  - strpbrk, wcspbrk, _mbspbrk, _mbspbrk_l

  - strrchr, wcsrchr, _mbsrchr, _mbsrchr_l

  - strstr, wcsstr, _mbsstr, _mbsstr_l

- Setargv. obj veya Wsetargv. obj ile bağlantı sırasında, bir joker karakteri çift tırnak içine alarak komut satırında genişletmeyi bastırmak artık mümkün değildir. Daha fazla bilgi için bkz. [joker karakter bağımsız değişkenlerini genişletme](../c-language/expanding-wildcard-arguments.md).

### <a name="standard-library-2005"></a>Standart Kitaplık (2005)

- Özel durum sınıfı ( \<exception> üst bilgide bulunur) `std` ad alanına taşınmıştır. Önceki sürümlerde bu sınıf genel ad alanıdır. Özel durum sınıfının bulunamadığını belirten hataları çözmek için, aşağıdaki using ifadesini kodunuza ekleyin:`using namespace std;`

- `valarray::resize()`' I çağırırken, öğesinin içeriği `valarray` kaybedilir ve varsayılan değerlerle değiştirilirler. `resize()`Yöntemi, `valarray` bir vektör gibi dinamik olarak büyütmek yerine, yeniden başlatılmaya yöneliktir.

- Yineleyiciler hata ayıklaması: C çalışma zamanı kitaplığı 'nın hata ayıklama sürümüyle oluşturulmuş uygulamalar ve yineleyiciler kullanan uygulamalar, çalışma zamanında onayları görmeyi başlayabilir. Bu onayları devre dışı bırakmak için, _HAS_ITERATOR_DEBUGGING tanımlamanız gerekir (Visual Studio 2010 ' den sonra [_ITERATOR_DEBUG_LEVEL](../standard-library/iterator-debug-level.md) ile yenisiyle değiştirilmiştir) 0 olarak tanımlamalısınız. Daha fazla bilgi için bkz. [hata ayıklama Yineleyici desteği](../standard-library/debug-iterator-support.md)

## <a name="visual-c-net-2003-breaking-changes"></a>Visual C++ .NET 2003 son değişiklikleri

### <a name="compiler"></a>Derleyici

- Tanımlanan Önişlemci yönergesi için kapatma parantezi artık gereklidir (C2004).

- Açık uzmanlık, artık birincil şablondan şablon parametreleri bulmayacak ([derleyici hatası C2146](../error-messages/compiler-errors-1/compiler-error-c2146.md)).

- Korunan bir üyeye (n) yalnızca, (n) öğesinin üyesi olduğu sınıftan (A) devralan bir sınıfın (B) üye işlevi üzerinden erişilebilir ([derleyici hatası C2247](../error-messages/compiler-errors-1/compiler-error-c2247.md)).

- Derleyicide geliştirilmiş erişilebilirlik denetimleri artık erişilemeyen temel sınıfları ([derleyici hatası C2248](../error-messages/compiler-errors-1/compiler-error-c2248.md)) tespit ediyor.

- Yıkıcı ve/veya kopya Oluşturucusu erişilebilir değilse (C2316) bir özel durum yakalanamıyor.

- İşlevlere yönelik işaretçilerde varsayılan bağımsız değişkenlere artık izin verilmez ([derleyici hatası C2383](../error-messages/compiler-errors-1/compiler-error-c2383.md)).

- Statik veri üyesi türetilmiş sınıf aracılığıyla başlatılamaz ([derleyici hatası C2477](../error-messages/compiler-errors-1/compiler-error-c2477.md)).

- Bir **typedef** 'in başlatılmasına standart tarafından izin verilmiyor ve şimdi bir derleyici hatası oluşturuyor ([derleyici hatası C2513](../error-messages/compiler-errors-2/compiler-error-c2513.md)).

- **bool** artık uygun bir türdür ([derleyici hatası C2632](../error-messages/compiler-errors-2/compiler-error-c2632.md)).

- Bir UDC artık aşırı yüklenmiş işleçlerle ([C2666](../error-messages/compiler-errors-2/compiler-error-c2666.md)) belirsizlik oluşturabilir.

- Daha fazla ifade artık geçerli boş işaretçi sabitleri olarak kabul edilir ([derleyici hatası C2668](../error-messages/compiler-errors-2/compiler-error-c2668.md)).

- Şablon<> artık derleyicinin daha önce ([derleyici hatası C2768](../error-messages/compiler-errors-2/compiler-error-c2768.md)) olduğu yerlerde gereklidir.

- İşlev bir şablon sınıfı özelleştirmesi ([derleyici hatası C2910](../error-messages/compiler-errors-2/compiler-error-c2910.md)) aracılığıyla açıkça özelleştirilmemişse, bir üye işlevinin sınıf dışındaki açık özelleştirmesi geçerli değildir.

- Kayan nokta türü olmayan şablon parametrelerine artık izin verilmiyor ([derleyici hatası C2993](../error-messages/compiler-errors-2/compiler-error-c2993.md)).

- Şablon türü bağımsız değişkenleri olarak sınıf şablonlarına izin verilmez (C3206).

- Arkadaş işlev adları artık kapsayan ad alanına tanıtılmadı ([derleyici hatası C3767](../error-messages/compiler-errors-2/compiler-error-c3767.md)).

- Derleyici, bir makroda artık ek virgüller kabul etmez (C4002).

- Formun bir başlatıcısıyla oluşturulan POD türünde bir nesne () varsayılan olarak başlatılır (C4345).

- bağımsız bir ad bir tür olarak değerlendirilip ([Derleyici Uyarısı (düzey 1) C4346](../error-messages/compiler-warnings/compiler-warning-level-1-c4346.md)), TypeName artık gereklidir.

- Şablon Uzmanlıkları yanlış olarak kabul edilen işlevler artık dikkate alınmaz (C4347).

- Statik veri üyeleri türetilmiş sınıf (C4356) üzerinden başlatılamaz.

- Bir sınıf şablonu özelleştirmenin bir dönüş türünde kullanılmadan önce tanımlanması gerekir ([Derleyici Uyarısı (düzey 3) C4686](../error-messages/compiler-warnings/compiler-warning-level-3-c4686.md)).

- Derleyici artık ulaşılamaz kodu (C4702) bildiriyor.

## <a name="see-also"></a>Ayrıca bkz.

[Visual Studio 'daki Visual C++ yenilikler](../overview/what-s-new-for-visual-cpp-in-visual-studio.md)
