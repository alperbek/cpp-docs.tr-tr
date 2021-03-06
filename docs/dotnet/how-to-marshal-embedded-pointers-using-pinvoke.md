---
title: 'Nasıl yapılır: PInvoke kullanarak katıştırılmış işaretçileri sıralama'
ms.custom: get-started-article
ms.date: 11/04/2016
helpviewer_keywords:
- embedded pointers [C++]
- interop [C++], embedded pointers
- platform invoke [C++], embedded pointers
- marshaling [C++], embedded pointers
- data marshaling [C++], embedded pointers
ms.assetid: f12c1b9a-4f82-45f8-83c8-3fc9321dbb98
ms.openlocfilehash: 943a1a2784a37353157cd38da7ebdc9827006fe5
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62325214"
---
# <a name="how-to-marshal-embedded-pointers-using-pinvoke"></a>Nasıl yapılır: PInvoke kullanarak katıştırılmış işaretçileri sıralama

Platform Çağırma (P/Invoke) işlevini kullanarak yönetilen koddan yönetilmeyen DLL'ler uygulanan işlevler çağrılabilir. DLL kaynak kodunu kullanılabilir durumda değilse, P/Invoke birlikte çalışma için tek seçenektir. Ancak, diğer .NET dilleri farklı olarak, Visual C++ P/Invoke bir alternatif sunar. Daha fazla bilgi için [C++ Çalışabilirliği kullanma (örtük PInvoke)](../dotnet/using-cpp-interop-implicit-pinvoke.md) ve [nasıl yapılır: C++ birlikte çalışması kullanarak katıştırılmış işaretçileri sıralama](../dotnet/how-to-marshal-embedded-pointers-using-cpp-interop.md).

## <a name="example"></a>Örnek

Yerel koda yapıları geçirme yerel yapısı için veri düzeni bakımından eşdeğer olan yönetilen bir yapının oluşturulması gerekir. Ancak, işaretçiler içeren yapılar özel işleme gerektirir. Yerel yapısında katıştırılmış işaretçi için her yönetilen sürüm yapısı örneği içermelidir <xref:System.IntPtr> türü. Ayrıca, bellek Bu örnekler açıkça ayrılması için başlatılmış ve kullanılarak serbest <xref:System.Runtime.InteropServices.Marshal.AllocCoTaskMem%2A>, <xref:System.Runtime.InteropServices.Marshal.StructureToPtr%2A>, ve <xref:System.Runtime.InteropServices.Marshal.FreeCoTaskMem%2A> yöntemleri.

Aşağıdaki kod, yönetilmeyen ve yönetilen bir modül oluşur. Yönetilmeyen bir işaretçi içeren ListString adlı bir yapıyı kabul eden bir işlev ve TakesListStruct adlı bir işlevi tanımlayan bir DLL modülüdür. Yönetilen modül TakesListStruct işlevini alır ve çift * ile temsil edilen dışında yerel ListStruct ile eşdeğer olan MListStruct adlı bir yapıyı tanımlayan bir komut satırı uygulamasıdır bir <xref:System.IntPtr> örneği. Main işlevi TakesListStruct öğesini çağırmadan önce ayırır ve bu alana başvuran belleği başlatır.

```cpp
// TraditionalDll6.cpp
// compile with: /EHsc /LD
#include <stdio.h>
#include <iostream>
#define TRADITIONALDLL_EXPORTS
#ifdef TRADITIONALDLL_EXPORTS
#define TRADITIONALDLL_API __declspec(dllexport)
#else
#define TRADITIONALDLL_API __declspec(dllimport)
#endif

#pragma pack(push, 8)
struct ListStruct {
   int count;
   double* item;
};
#pragma pack(pop)

extern "C" {
   TRADITIONALDLL_API void TakesListStruct(ListStruct);
}

void TakesListStruct(ListStruct list) {
   printf_s("[unmanaged] count = %d\n", list.count);
   for (int i=0; i<list.count; i++)
      printf_s("array[%d] = %f\n", i, list.item[i]);
}
```

```cpp
// EmbeddedPointerMarshalling.cpp
// compile with: /clr
using namespace System;
using namespace System::Runtime::InteropServices;

[StructLayout(LayoutKind::Sequential, Pack=8)]
value struct MListStruct {
   int count;
   IntPtr item;
};

value struct TraditionalDLL {
    [DllImport("TraditionalDLL6.dll")]
   static public void TakesListStruct(MListStruct);
};

int main() {
   array<double>^ parray = gcnew array<double>(10);
   Console::WriteLine("[managed] count = {0}", parray->Length);

   Random^ r = gcnew Random();
   for (int i=0; i<parray->Length; i++) {
      parray[i] = r->NextDouble() * 100.0;
      Console::WriteLine("array[{0}] = {1}", i, parray[i]);
   }

   int size = Marshal::SizeOf(double::typeid);
   MListStruct list;
   list.count = parray->Length;
   list.item = Marshal::AllocCoTaskMem(size * parray->Length);

   for (int i=0; i<parray->Length; i++) {
      IntPtr t = IntPtr(list.item.ToInt32() + i * size);
      Marshal::StructureToPtr(parray[i], t, false);
   }

   TraditionalDLL::TakesListStruct( list );
   Marshal::FreeCoTaskMem(list.item);
}
```

DLL hiçbir kısmı geleneksel kullanarak yönetilen kod için kullanıma sunulduğunu unutmayın #include yönergesi. Aslında, ile içeri aktarılan işlevlere sahip sorunlar için DLL yalnızca çalışma zamanında erişilir <xref:System.Runtime.InteropServices.DllImportAttribute> derleme zamanında algılanmaz.

## <a name="see-also"></a>Ayrıca bkz.

[C++'ta Açık PInvoke Kullanma (DllImport Özniteliği)](../dotnet/using-explicit-pinvoke-in-cpp-dllimport-attribute.md)
