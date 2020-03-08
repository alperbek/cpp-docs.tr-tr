---
title: SymbolName sınıfı
description: C++ Build Insights SDK 'Sı symbolname sınıf başvurusu.
ms.date: 02/12/2020
helpviewer_keywords:
- C++ Build Insights
- C++ Build Insights SDK
- SymbolName
- throughput analysis
- build time analysis
- vcperf.exe
ms.openlocfilehash: b5e9a9b22db99c099b9f7dc1813fb335358a83e8
ms.sourcegitcommit: 3e8fa01f323bc5043a48a0c18b855d38af3648d4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/05/2020
ms.locfileid: "78333001"
---
# <a name="symbolname-class"></a>SymbolName sınıfı

::: moniker range="<=vs-2015"

Build C++ Insights SDK 'Sı, Visual Studio 2017 ve üzeri ile uyumludur. Bu sürümlerin belgelerini görmek için, bu makalenin Visual Studio sürüm Seçicisi denetimini Visual Studio 2017 veya Visual Studio 2019 olarak ayarlayın.

::: moniker-end
::: moniker range=">=vs-2017"

`SymbolName` sınıfı [Matchevent](../functions/match-event.md), [matcheventınmemberfunction](../functions/match-event-in-member-function.md), [Matcheventstack](../functions/match-event-stack.md)ve [matcheventstackinmemberfunction](../functions/match-event-stack-in-member-function.md) işlevleriyle birlikte kullanılır. Bunu bir [SYMBOL_NAME](../event-table.md#symbol-name) olayına uyacak şekilde kullanın.

## <a name="syntax"></a>Sözdizimi

```cpp
class SymbolName : public SimpleEvent
{
public:
    SymbolName(const RawEvent& event);

    const unsigned long long&  Key() const;
    const char*                Name() const;
};
```

## <a name="members"></a>Üyeler

[SimpleEvent](simple-event.md) temel sınıfından devralınan üyelerle birlikte `SymbolName` sınıfı aşağıdaki üyeleri içerir:

### <a name="constructors"></a>Oluşturucular

[SymbolName](#symbol-name)

### <a name="functions"></a>İşlevler

[Anahtar](#key)
[adı](#name)

## <a name="key"></a>Anahtar

```cpp
const unsigned long long& Key() const;
```

### <a name="return-value"></a>Dönüş Değeri

Bu simge tarafından temsil edilen tür için sayısal tanımlayıcı. Bu tanımlayıcı, bir derleyici ön ucu geçişi içinde benzersizdir.

## <a name="name"></a>Ada

```cpp
const char* Name() const;
```

### <a name="return-value"></a>Dönüş Değeri

UTF-8 ile kodlanmış, simgesiyle temsil edilen türün adı.

## <a name="symbol-name"></a>SymbolName

```cpp
SymbolName(const RawEvent& event);
```

### <a name="parameters"></a>Parametreler

*olay*\
[SYMBOL_NAME](../event-table.md#symbol-name) bir olay.

::: moniker-end