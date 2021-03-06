---
title: __clrcall
ms.date: 11/04/2016
f1_keywords:
- __clrcall_cpp
helpviewer_keywords:
- __clrcall keyword [C++]
ms.assetid: 92096695-683a-40ed-bf65-0c8443572152
ms.openlocfilehash: 6eb1a05eaf6669daa4cb7142ff16a57f7caf39cd
ms.sourcegitcommit: a6d63c07ab9ec251c48bc003ab2933cf01263f19
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/05/2019
ms.locfileid: "74857612"
---
# <a name="__clrcall"></a>__clrcall

Bir işlevin yalnızca yönetilen koddan çağrılabilecek olduğunu belirtir.  Yalnızca yönetilen koddan çağrılacak tüm sanal işlevler için **__clrcall** kullanın. Ancak, bu çağırma kuralı yerel koddan çağrılacak işlevler için kullanılamaz. **__Clrcall** değiştiricisi Microsoft 'a özgüdür.

Yönetilen bir işlevden sanal yönetilen işleve veya yönetilen işlevden işaretçi aracılığıyla yönetilen işleve çağrı yaparken performansı artırmak için **__clrcall** kullanın.

Giriş noktaları ayrı, derleyici tarafından oluşturulan işlevlerdir. Bir işlevde hem yerel hem de yönetilen giriş noktaları varsa, bunlardan biri işlev uygulamasıyla gerçek işlev olur. Diğer işlev ise gerçek işleve çağıran ayrı bir işlev (bir dönüştürücü) olacaktır ve ortak dil çalışma zamanının PInvoke gerçekleştirmesini sağlar. Bir işlevi **__clrcall**olarak işaretlerken, Işlev uygulamasının MSIL olması gerektiğini ve yerel giriş noktası işlevinin üretilmeyeceğini belirtirsiniz.

**__Clrcall** belirtilmemişse, yerel bir işlevin adresini alırken, derleyici yerel giriş noktasını kullanır. **__clrcall** , işlevin yönetildiğini ve yönetilen ' dan Native ' e geçiş işlemi yapmanız gerekmediğini gösterir. Bu durumda, derleyici yönetilen giriş noktasını kullanır.

`/clr` (`/clr:pure` veya `/clr:safe`) kullanıldığında ve **__clrcall** kullanılmazsa, bir işlevin adresini almak her zaman yerel giriş noktası işlevinin adresini döndürür. **__Clrcall** kullanıldığında, yerel giriş noktası işlevi oluşturulmaz, bu nedenle bir giriş noktası dönüştürücü işlevi değil, yönetilen işlevin adresini alırsınız. Daha fazla bilgi için bkz. [Double thunking](../dotnet/double-thunking-cpp.md). **/Clr: Pure** ve **/clr: Safe** derleyici seçenekleri Visual Studio 2015 ' de kullanımdan kaldırılmıştır ve Visual Studio 2017 ' de desteklenmez.

[/clr (ortak dil çalışma zamanı derlemesi)](../build/reference/clr-common-language-runtime-compilation.md) , tüm işlevlerin ve işlev işaretçilerinin **__clrcall** olduğunu ve derleyicinin compiland içindeki bir işlevin **__clrcall**dışında bir şey işaretlenmesini sağlar. **/Clr: Pure** kullanıldığında, **__clrcall** yalnızca işlev işaretçilerinde ve dış bildirimlerde belirtilebilir.

İşlevin MSIL uygulamasına sahip olduğu sürece **/clr** kullanılarak C++ derlenen mevcut koddan doğrudan **__clrcall** işlevlerini çağırabilirsiniz. **__clrcall** işlevler, satır içi asm içeren işlevlerden doğrudan çağrılamaz ve örneğin, bu işlevler `/clr`ile derlense bıle, CPU 'ya özgü ıntrinıics 'ı çağırır.

**__clrcall** işlev işaretçilerinin yalnızca oluşturuldukları uygulama etki alanında kullanılması amaçlanmıştır.  Uygulama etki alanları arasında **__clrcall** işlev işaretçileri geçirmek yerine <xref:System.CrossAppDomainDelegate>kullanın. Daha fazla bilgi için bkz. [uygulama etki alanları C++ve görsel ](../dotnet/application-domains-and-visual-cpp.md).

## <a name="example"></a>Örnek

Bir işlev **__clrcall**ile bildirildiğinde, gerektiğinde kod oluşturulacaktır; Örneğin, işlev çağrıldığında.

```cpp
// clrcall2.cpp
// compile with: /clr
using namespace System;
int __clrcall Func1() {
   Console::WriteLine("in Func1");
   return 0;
}

// Func1 hasn't been used at this point (code has not been generated),
// so runtime returns the adddress of a stub to the function
int (__clrcall *pf)() = &Func1;

// code calls the function, code generated at difference address
int i = pf();   // comment this line and comparison will pass

int main() {
   if (&Func1 == pf)
      Console::WriteLine("&Func1 == pf, comparison succeeds");
   else
      Console::WriteLine("&Func1 != pf, comparison fails");

   // even though comparison fails, stub and function call are correct
   pf();
   Func1();
}
```

```Output
in Func1
&Func1 != pf, comparison fails
in Func1
in Func1
```

## <a name="example"></a>Örnek

Aşağıdaki örnek, işlev işaretçisinin yalnızca yönetilen koddan çağrılacağını bildiren bir işlev işaretçisi tanımlayabileceğiniz gösterilmektedir. Bu, derleyicinin yönetilen işlevi doğrudan çağırması ve yerel giriş noktasını (çift dönüştürücü sorunu) önlemek için izin verir.

```cpp
// clrcall3.cpp
// compile with: /clr
void Test() {
   System::Console::WriteLine("in Test");
}

int main() {
   void (*pTest)() = &Test;
   (*pTest)();

   void (__clrcall *pTest2)() = &Test;
   (*pTest2)();
}
```

## <a name="see-also"></a>Ayrıca bkz.

[Bağımsız Değişkeni Geçirme ve Adlandırma Kuralları](../cpp/argument-passing-and-naming-conventions.md)<br/>
[Anahtar Sözcükler](../cpp/keywords-cpp.md)
