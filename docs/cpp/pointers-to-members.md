---
title: Üye İşaretçileri
ms.date: 11/04/2016
helpviewer_keywords:
- declarations, pointers
- class members [C++], pointers to
- pointers, to members
- members [C++], pointers to
- pointers, declarations
ms.assetid: f42ddb79-9721-4e39-95b1-c56b55591f68
ms.openlocfilehash: 75bd29310d64b0309ac48be053aa43cc0084aa2d
ms.sourcegitcommit: 1a8fac06478da8bee1f6d70e25afbad94144af1a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/30/2020
ms.locfileid: "84226090"
---
# <a name="pointers-to-members"></a>Üye İşaretçileri

Üye işaretçilerin bildirimleri, işaretçi bildirimlerinin özel çalışmalardır.  Bunlar aşağıdaki sıra kullanılarak bildirilenler:

> *depolama sınıfı belirticileri*<sub>opt</sub> *CV-niteleyiciler*<sub>opt</sub> *tür belirleyicisi* *MS-değiştirici*<sub>opt</sub> *nitelikli adı* **`::*`** *CV-niteleyicileri*<sub>opt</sub> *tanımlayıcı tanımlayıcı* - *Başlatıcı*<sub>opt</sub>**`;`**

1. Bildirim belirleyicisi:

   - İsteğe bağlı bir depolama sınıfı Belirleyicisi.

   - İsteğe bağlı **const** ve **volatile** belirticileri.

   - Tür belirleyicisi: bir türün adı. Bu, sınıfa değil, işaret edilecek üyenin türüdür.

1. Bildirimci:

   - İsteğe bağlı Microsoft 'a özgü değiştirici. Daha fazla bilgi için bkz. [Microsoft 'A özgü değiştiriciler](../cpp/microsoft-specific-modifiers.md).

   - İşaret edilecek üyeleri içeren sınıfın tam adı.

   - __`::`__ İşleci.

   - __`*`__ İşleci.

   - İsteğe bağlı **const** ve **volatile** belirticileri.

   - Tanıtıcı, üyeye olan işaretçiyi adlandırma.

1. İsteğe bağlı bir işaretçiden üyeye başlatıcısı:

   - **`=`** İşleci.

   - **`&`** İşleci.

   - Sınıfın tam adı.

   - __`::`__ İşleci.

   - Uygun tür sınıfının statik olmayan bir üyesinin adı.

Her zaman olduğu gibi, tek bir bildirimde birden çok bildirimciye (ve ilişkili başlatıcılara) izin verilir. Üye işaretçisi, sınıfın statik bir üyesini, başvuru türü üyesini veya bir üyeyi işaret edebilir **`void`** .

Bir sınıfın üyesi için bir işaretçi normal işaretçiden farklıdır: üyenin türü ve üyenin ait olduğu sınıf için tür bilgilerine sahiptir. Normal bir işaretçi yalnızca bellekte tek bir nesne (adresini içerir) tanımlar. Bir sınıfın bir işaretçisi, bu üyeyi sınıfın herhangi bir örneğinde tanımlar. Aşağıdaki örnek, bir sınıfı, `Window` ve bazı üye verilerine yönelik işaretçileri bildirir.

```cpp
// pointers_to_members1.cpp
class Window
{
public:
   Window();                               // Default constructor.
   Window( int x1, int y1,                 // Constructor specifying
   int x2, int y2 );                       // Window size.
   bool SetCaption( const char *szTitle ); // Set window caption.
   const char *GetCaption();               // Get window caption.
   char *szWinCaption;                     // Window caption.
};

// Declare a pointer to the data member szWinCaption.
char * Window::* pwCaption = &Window::szWinCaption;
int main()
{
}
```

Yukarıdaki örnekte, `pwCaption` türünde olan sınıfın herhangi bir üyesine yönelik bir işaretçidir `Window` `char*` . Türü `pwCaption` `char * Window::*` . Sonraki kod parçası, `SetCaption` ve üye işlevlerine işaretçiler bildirir `GetCaption` .

```cpp
const char * (Window::* pfnwGC)() = &Window::GetCaption;
bool (Window::* pfnwSC)( const char * ) = &Window::SetCaption;
```

İşaretçilerle `pfnwGC` `pfnwSC` `GetCaption` `SetCaption` , sırasıyla sınıfına ve üzerine gelin `Window` . Kod, üyeye yönelik işaretçiyi kullanarak bilgileri pencere açıklamalı yazısına doğrudan kopyalar `pwCaption` :

```cpp
Window  wMainWindow;
Window *pwChildWindow = new Window;
char   *szUntitled    = "Untitled -  ";
int     cUntitledLen  = strlen( szUntitled );

strcpy_s( wMainWindow.*pwCaption, cUntitledLen, szUntitled );
(wMainWindow.*pwCaption)[cUntitledLen - 1] = '1';     // same as
// wMainWindow.SzWinCaption [cUntitledLen - 1] = '1';
strcpy_s( pwChildWindow->*pwCaption, cUntitledLen, szUntitled );
(pwChildWindow->*pwCaption)[cUntitledLen - 1] = '2'; // same as
// pwChildWindow->szWinCaption[cUntitledLen - 1] = '2';
```

**`.*`** Ve **`->*`** işleçleri (üye işaretçisi işleçleri) arasındaki fark, işlecin bir **`.*`** nesne veya nesne başvurusu verilen üyeleri seçtiği, **`->*`** işlecin bir işaretçi aracılığıyla Üyeler seçtiği. Bu işleçler hakkında daha fazla bilgi için bkz. [üye Işaretçisi işleçleri olan ifadeler](../cpp/pointer-to-member-operators-dot-star-and-star.md).

Üye işaretçiden üyeye işleçlerinin sonucu üyenin türüdür. Bu durumda, `char *` .

Aşağıdaki kod parçası, üye işlevlerini çağırır `GetCaption` ve `SetCaption` üyelere işaretçiler kullanarak:

```cpp
// Allocate a buffer.
enum {
    sizeOfBuffer = 100
};
char szCaptionBase[sizeOfBuffer];

// Copy the main window caption into the buffer
//  and append " [View 1]".
strcpy_s( szCaptionBase, sizeOfBuffer, (wMainWindow.*pfnwGC)() );
strcat_s( szCaptionBase, sizeOfBuffer, " [View 1]" );
// Set the child window's caption.
(pwChildWindow->*pfnwSC)( szCaptionBase );
```

## <a name="restrictions-on-pointers-to-members"></a>Üye İşaretçileri Kısıtlamaları

Statik üyenin adresi bir üyeye işaretçi değildir. Bu, statik üyenin bir örneğine düzenli bir işaretçidir. Belirli bir sınıfın tüm nesneleri için bir statik üyenin yalnızca bir örneği bulunur. Bu, normal adres ( **&** ) ve başvuru () işleçlerini kullanabileceğiniz anlamına gelir <strong>\*</strong> .

## <a name="pointers-to-members-and-virtual-functions"></a>Üye ve Sanal İşlev İşaretçileri

Üye işaretçisi işlevi aracılığıyla sanal bir işlevi çağırmak, işlev doğrudan çağrılmış gibi çalışır. Doğru işlev v tablosunda aranır ve çağrılır.

Sanal işlevlerin çalışması, her zaman olduğu gibi bir temel sınıf işaretçisiyle çağrılmalarına bağlıdır. (Sanal işlevler hakkında daha fazla bilgi için bkz. [sanal işlevler](../cpp/virtual-functions.md).)

Aşağıdaki kodda, üye işaretçisi işleviyle sanal bir işlevin nasıl çağrılacağı gösterilmektedir:

```cpp
// virtual_functions.cpp
// compile with: /EHsc
#include <iostream>
using namespace std;

class Base
{
public:
    virtual void Print();
};
void (Base::* bfnPrint)() = &Base::Print;
void Base::Print()
{
    cout << "Print function for class Base" << endl;
}

class Derived : public Base
{
public:
    void Print();  // Print is still a virtual function.
};

void Derived::Print()
{
    cout << "Print function for class Derived" << endl;
}

int main()
{
    Base   *bPtr;
    Base    bObject;
    Derived dObject;
    bPtr = &bObject;    // Set pointer to address of bObject.
    (bPtr->*bfnPrint)();
    bPtr = &dObject;    // Set pointer to address of dObject.
    (bPtr->*bfnPrint)();
}

// Output:
// Print function for class Base
// Print function for class Derived
```
