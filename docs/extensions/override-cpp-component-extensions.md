---
title: geçersiz kılma (C + +/ CLI ve C + +/ CX)
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- overriding, override keyword [C++]
- override keyword [C++]
ms.assetid: 34d19257-1686-4fcd-96f5-af07c70ba914
ms.openlocfilehash: 8dc7a0a0e6cf759d956fd701d033bd773e572af3
ms.sourcegitcommit: c7f90df497e6261764893f9cc04b5d1f1bf0b64b
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/05/2019
ms.locfileid: "59025675"
---
# <a name="override--ccli-and-ccx"></a>geçersiz kılma (C + +/ CLI ve C + +/ CX)

**Geçersiz kılma** bağlama duyarlı anahtar sözcüğü bir tür üyesi bir temel sınıf veya temel arabirim üyesi kıldığını gösterir.

## <a name="remarks"></a>Açıklamalar

**Geçersiz kılma** (varsayılan derleyici seçeneği), yerel hedefler için derleme yaparken anahtar sözcüğü geçerli Windows çalışma zamanı hedefleri (`/ZW` derleyici seçeneği), veya ortak dil çalışma zamanı hedefleri (`/clr` derleyici seçeneği).

Geçersiz kılma tanımlayıcıları hakkında daha fazla bilgi için bkz. [geçersiz kılma belirticisi](../cpp/override-specifier.md) ve [geçersiz kılma tanımlayıcıları ve yerel derlemeler](../dotnet/how-to-declare-override-specifiers-in-native-compilations-cpp-cli.md).

Bağlama duyarlı anahtar sözcükler hakkında daha fazla bilgi için bkz. [Context-Sensitive Keywords](context-sensitive-keywords-cpp-component-extensions.md).

## <a name="examples"></a>Örnekler

Aşağıdaki kod örneği gösteren **geçersiz kılma** yerel derlemelerde de kullanılabilir.

```cpp
// override_keyword_1.cpp
// compile with: /c
struct I1 {
   virtual void f();
};

struct X : public I1 {
   virtual void f() override {}
};
```

### <a name="example"></a>Örnek

Aşağıdaki kod örneği gösteren **geçersiz kılma** Windows çalışma zamanı derlemeleri kullanılabilir.

```cpp
// override_keyword_2.cpp
// compile with: /ZW /c
ref struct I1 {
   virtual void f();
};

ref struct X : public I1 {
   virtual void f() override {}
};
```

#### <a name="requirements"></a>Gereksinimler

Derleyici seçeneği: `/ZW`

### <a name="example"></a>Örnek

Aşağıdaki kod örneği gösteren **geçersiz kılma** ortak dil çalışma zamanı derlemeleri kullanılabilir.

```cpp
// override_keyword_3.cpp
// compile with: /clr /c
ref struct I1 {
   virtual void f();
};

ref struct X : public I1 {
   virtual void f() override {}
};
```

#### <a name="requirements"></a>Gereksinimler

Derleyici seçeneği: `/clr`

## <a name="see-also"></a>Ayrıca bkz.

[override Tanımlayıcısı](../cpp/override-specifier.md)<br/>
[Geçersiz Kılma Tanımlayıcıları](override-specifiers-cpp-component-extensions.md)