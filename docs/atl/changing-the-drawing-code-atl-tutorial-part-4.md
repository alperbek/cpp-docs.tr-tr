---
title: Çizim Kodunu değiştirme (ATL Eğitmeni, Bölüm 4)
ms.custom: get-started-article
ms.date: 09/26/2018
helpviewer_keywords:
- _ATL_MIN_CRT macro
ms.assetid: 08ff14e8-aa49-4139-a110-5d071939cf1e
ms.openlocfilehash: 319a27b55c394349de751546457b0741c0799cfc
ms.sourcegitcommit: 2bc15c5b36372ab01fa21e9bcf718fa22705814f
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/27/2020
ms.locfileid: "82167649"
---
# <a name="changing-the-drawing-code-atl-tutorial-part-4"></a>Çizim Kodunu değiştirme (ATL Eğitmeni, Bölüm 4)

Varsayılan olarak, denetimin çizim kodu bir kare ve **PolyCtl**metnini görüntüler. Bu adımda, kodu daha ilgi çekici bir şekilde görüntüleyecek şekilde değiştirirsiniz. Aşağıdaki görevler yer alır:

- Üst bilgi dosyasını değiştirme

- `OnDraw` İşlevi değiştirme

- Çokgen noktalarını hesaplamak için bir yöntem ekleme

- Fill rengini başlatma

## <a name="modifying-the-header-file"></a>Üst bilgi dosyasını değiştirme

Math işlevleri `sin` için destek ekleyerek ve `cos`Çokgen noktalarını hesaplamak için ve konumları depolamak için bir dizi oluşturarak başlayın.

### <a name="to-modify-the-header-file"></a>Üst bilgi dosyasını değiştirmek için

1. Çizgiyi `#include <math.h>` PolyCtl. h ' nin üstüne ekleyin. Dosyanın en üstü şöyle görünmelidir:

    [!code-cpp[NVC_ATL_Windowing#47](../atl/codesnippet/cpp/changing-the-drawing-code-atl-tutorial-part-4_1.cpp)]

1. PolyCtl `IProvideClassInfo` . h ' ye aşağıdaki kodu ekleyerek denetim için yöntem bilgilerini sağlamak üzere arabirimini uygulayın. `CPolyCtl` Sınıfında, şu satırı değiştirin:

    ```cpp
    public CComControl<CPolyCtl>
    ```

    örneklerini şununla değiştirin:

    ```cpp
    public CComControl<CPolyCtl>,
    public IProvideClassInfo2Impl<&CLSID_PolyCtl, &DIID__IPolyCtlEvents, &LIBID_PolygonLib>
    ```

    ve içinde `BEGIN_COM_MAP(CPolyCtl)`, satırları ekleyin:

    ```cpp
    COM_INTERFACE_ENTRY(IProvideClassInfo)
    COM_INTERFACE_ENTRY(IProvideClassInfo2)
    ```

1. Çokgen noktaları hesaplandıktan sonra, bunlar türünde `POINT`bir dizide saklanır, bu nedenle PolyCtl. h içindeki tanım ifadesinden `short m_nSides;` sonra diziyi ekleyin:

    [!code-cpp[NVC_ATL_Windowing#48](../atl/codesnippet/cpp/changing-the-drawing-code-atl-tutorial-part-4_2.h)]

## <a name="modifying-the-ondraw-method"></a>OnDraw metodunu değiştirme

Artık PolyCtl. h `OnDraw` içindeki yöntemi değiştirmelisiniz. Ekleyeceğiniz kod, çokgeni çizecek yeni bir kalem ve fırça oluşturur ve sonra gerçek çizimi gerçekleştirmek için `Ellipse` ve `Polygon` Win32 API işlevlerini çağırır.

### <a name="to-modify-the-ondraw-function"></a>OnDraw işlevini değiştirmek için

1. PolyCtl. `OnDraw` h içindeki mevcut yöntemi şu kodla değiştirin:

    [!code-cpp[NVC_ATL_Windowing#49](../atl/codesnippet/cpp/changing-the-drawing-code-atl-tutorial-part-4_3.cpp)]

## <a name="adding-a-method-to-calculate-the-polygon-points"></a>Çokgen noktalarını hesaplamak için bir yöntem ekleme

Poligonun çevresi oluşturan noktaların `CalcPoints`koordinatlarını hesaplayacak adlı bir yöntem ekleyin. Bu hesaplamalar, işleve geçirilen RECT değişkenine göre belirlenir.

### <a name="to-add-the-calcpoints-method"></a>CalcPoints metodunu eklemek için

1. Öğesinin `CalcPoints` bildirimini PolyCtl. h `IPolyCtl` içindeki `CPolyCtl` sınıfın genel bölümüne ekleyin:

    [!code-cpp[NVC_ATL_Windowing#50](../atl/codesnippet/cpp/changing-the-drawing-code-atl-tutorial-part-4_4.h)]

    `CPolyCtl` Sınıfının genel bölümünün son bölümü şöyle görünür:

    [!code-cpp[NVC_ATL_Windowing#51](../atl/codesnippet/cpp/changing-the-drawing-code-atl-tutorial-part-4_5.h)]

1. `CalcPoints` İşlevin bu uygulamasını PolyCtl. cpp sonuna ekleyin:

    [!code-cpp[NVC_ATL_Windowing#52](../atl/codesnippet/cpp/changing-the-drawing-code-atl-tutorial-part-4_6.cpp)]

## <a name="initializing-the-fill-color"></a>Fill rengini başlatma

Varsayılan `m_clrFillColor` renkle başlatın.

### <a name="to-initialize-the-fill-color"></a>Fill rengini başlatmak için

1. Bu satırı PolyCtl. h içindeki `CPolyCtl` oluşturucuya ekleyerek varsayılan renk olarak yeşil kullanın:

    [!code-cpp[NVC_ATL_Windowing#53](../atl/codesnippet/cpp/changing-the-drawing-code-atl-tutorial-part-4_7.h)]

Oluşturucu artık şuna benzer:

[!code-cpp[NVC_ATL_Windowing#54](../atl/codesnippet/cpp/changing-the-drawing-code-atl-tutorial-part-4_8.h)]

## <a name="building-and-testing-the-control"></a>Denetim oluşturma ve test etme

Denetimi yeniden derleyin. Hala açıksa PolyCtl. htm dosyasının kapalı olduğundan emin olun ve ardından **Yapı** menüsünde **Çokgen oluştur** ' a tıklayın. PolyCtl. htm sayfasından bir kez denetim görüntüleyebilirsiniz, ancak bu kez ActiveX denetimi test kapsayıcısını kullanır.

### <a name="to-use-the-activex-control-test-container"></a>ActiveX denetimi test kapsayıcısını kullanmak için

1. ActiveX denetimi test kapsayıcısını derleyin ve başlatın. [Tstcon örneği: ActiveX denetimi test kapsayıcısı](https://github.com/Microsoft/VCSamples/tree/master/VC2010Samples/MFC/ole/TstCon) GitHub 'da bulunabilir.

    > [!NOTE]
    > Script. cpp `ATL::CW2AEX`ile ilgili hatalar `TRACE( "XActiveScriptSite::GetItemInfo( %s )\n", pszNameT );` için, satır `TRACE( "XActiveScriptSite::GetItemInfo( %s )\n", pszNameT.m_psz );`ve satır `TRACE( "Source Text: %s\n", COLE2CT( bstrSourceLineText ) );` ile değiştirin. `TRACE( "Source Text: %s\n", bstrSourceLineText );`<br/>
    > İle ilgili `HMONITOR`hatalar için, `TCProps` projede stdadfx. h ' yi açın ve değiştirin:
    >
    > ```cpp
    > #ifndef WINVER
    > #define WINVER 0x0400
    > #endif
    > ```
    >
    > örneklerini şununla değiştirin:
    >
    > ```cpp
    > #ifndef WINVER
    > #define WINVER 0x0500
    > #define _WIN32_WINNT 0x0500
    > #endif
    > ```

1. **Test kapsayıcısında**, **Düzenle** menüsünde **Yeni Denetim Ekle**' ye tıklayın.

1. Çağrılacak `PolyCtl class`denetimi bulun ve **Tamam**' a tıklayın. Daire içinde yeşil bir üçgen görürsünüz.

Sonraki yordamı izleyerek kenar sayısını değiştirmeyi deneyin. **Test kapsayıcısından**çift bir arabirimdeki özellikleri değiştirmek Için **Invoke metotları**kullanın.

### <a name="to-modify-a-controls-property-from-within-the-test-container"></a>Test kapsayıcısının içinden bir denetimin özelliğini değiştirmek için

1. **Test kapsayıcısında**, **Denetim** menüsünde **yöntemleri çağır** ' a tıklayın.

    **Yöntemi çağır** iletişim kutusu görüntülenir.

1. **Yöntem adı** açılan liste kutusundan **yüzler** özelliğinin **propput** sürümünü seçin.

1. `5` **Parametre değeri** kutusuna yazın, **değer ayarla**' ya tıklayın ve **çağır**' a tıklayın.

Denetimin değişmediğini unutmayın. `m_nSides` Değişkeni ayarlayarak yan yana olan yüz sayısını değiştirseniz de, bu, denetimin yeniden oluşturulmasına neden olmadı. Başka bir uygulamaya geçip **Test kapsayıcısına**geri geçerseniz, denetimin yeniden boyandiğini ve doğru sayıda yüzü olduğunu görürsünüz.

Bu sorunu düzeltmek için, kenar sayısını ayarladıktan sonra ' `FireViewChange` de `IViewObjectExImpl`tanımlanan işleve bir çağrı ekleyin. Denetim kendi penceresinde çalışıyorsa, `FireViewChange` `InvalidateRect` yöntemi doğrudan çağıracaktır. Denetim penceresiz çalıştırıyorsa, `InvalidateRect` yöntemi kapsayıcının site arabiriminde çağrılır. Bu, denetimi kendisini yeniden çizmeyi zorlar.

### <a name="to-add-a-call-to-fireviewchange"></a>FireViewChange çağrısı eklemek için

1. `put_Sides` Yöntemine yapılan çağrıyı `FireViewChange` ekleyerek PolyCtl. cpp ' i güncelleştirin. İşiniz bittiğinde, `put_Sides` yöntemin şöyle görünmesi gerekir:

    [!code-cpp[NVC_ATL_Windowing#55](../atl/codesnippet/cpp/changing-the-drawing-code-atl-tutorial-part-4_9.cpp)]

Ekledikten sonra `FireViewChange`, ActiveX denetimi test kapsayıcısında denetimi yeniden oluşturun ve yeniden deneyin. Bu kez, kenar sayısını değiştirirken ve öğesini tıklattığınızda `Invoke`, denetim değişikliğini hemen görmeniz gerekir.

Sonraki adımda bir olay ekleyeceksiniz.

Adım 3 ' e [geri döndüğünüzde](../atl/adding-a-property-to-the-control-atl-tutorial-part-3.md) [5. adım](../atl/adding-an-event-atl-tutorial-part-5.md) &#124;

## <a name="see-also"></a>Ayrıca bkz.

[Eğitmen](../atl/active-template-library-atl-tutorial.md)<br/>
[Test Kapsayıcısı ile Özellikleri ve Olayları Test Etme](../mfc/testing-properties-and-events-with-test-container.md)
