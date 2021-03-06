---
title: Denetimi Web Sayfasına Koyma (ATL Eğitmeni, Bölüm 7)
ms.custom: get-started-article
ms.date: 05/06/2019
ms.assetid: 50dc4c95-c95b-4006-b88a-9826f7bdb222
ms.openlocfilehash: db6dcc57ff9f3748d802e76617ef18dea8f9506c
ms.sourcegitcommit: 6cf0c67acce633b07ff31b56cebd5de3218fd733
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/24/2019
ms.locfileid: "67344352"
---
# <a name="putting-the-control-on-a-web-page-atl-tutorial-part-7"></a>Denetimi Web Sayfasına Koyma (ATL Eğitmeni, Bölüm 7)

Denetiminiz artık tamamlandı. Denetim çalışmanızı gerçek durumda görmek için bir Web sayfasına koyun. Denetim tanımladığınızda, denetim içeren bir HTML dosyası oluşturuldu. Nden PolyCtl.htm dosyasını açın **Çözüm Gezgini**, denetiminizi Web sayfasında görebilirsiniz.

Bu adımda, denetime işlevsellik ekleme ve olaylara yanıt vermesi için Web sayfası betiği. Ayrıca, Internet Explorer'ın denetimin komut dosyası için güvenli olduğunu bilmesini sağlamak için denetimi değiştireceksiniz.

## <a name="adding-new-functionality"></a>Yeni işlevsellik ekleme

### <a name="to-add-control-features"></a>Denetim özellikleri eklemek için

1. PolyCtl.cpp açın ve aşağıdaki kodu değiştirin:

    ```cpp
    if (PtInRegion(hRgn, xPos, yPos))
        Fire_ClickIn(xPos, yPos);
    else
        Fire_ClickOut(xPos, yPos);
    ```

    örneklerini şununla değiştirin:

    ```cpp
    short temp = m_nSides;
    if (PtInRegion(hRgn, xPos, yPos))
    {
        Fire_ClickIn(xPos, yPos);
        put_Sides(++temp);
    }
    else
    {
        Fire_ClickOut(xPos, yPos);
        put_Sides(--temp);
    }
    ```

Şekil, şimdi ekleyin veya yüz erişebilen bağlı olarak kaldırın.

## <a name="scripting-the-web-page"></a>Web sayfası betiği oluşturma

Denetim bir şey henüz, dolayısıyla gönderdiğiniz olaylara yanıt vermek için Web sayfasını değiştirin.

### <a name="to-script-the-web-page"></a>Web sayfası betiği oluşturmak için

1. Polyctl.htm dosyasını açın ve HTML görünümü seçin. Aşağıdaki satırları HTML koduna ekleyin. Sonra eklenmelidir `</OBJECT>` önce `</BODY>`.

    ```html
    <SCRIPT LANGUAGE="VBScript">
    <!--
        Sub PolyCtl_ClickIn(x, y)
            MsgBox("Clicked (" & x & ", " & y & ") - adding side")
        End Sub
        Sub PolyCtl_ClickOut(x, y)
            MsgBox("Clicked (" & x & ", " & y & ") - removing side")
        End Sub
    -->
    </SCRIPT>
    ```

1. HTM dosyasını kaydedin.

Denetimden kenar özelliğini alır bazı VBScript kodlarını eklediniz. Denetimin içini tıkladığınızda bir kenar sayısını artırır. Denetimin dışına tıklarsanız, kenar sayısını birer birer azaltır.

## <a name="indicating-that-the-control-is-safe-for-scripting"></a>Denetim komut dosyası için güvenli olduğunu gösterme

Denetimi içeren Web sayfasını Internet Explorer'da yalnızca görüntüleyebilir. Diğer tarayıcılarda ActiveX denetimleri nedeniyle güvenlik zayıf artık desteklemiyor.

> [!NOTE]
> Denetim görünür durumda değilse bazı tarayıcılar ayarları düzeltmeleri ActiveX denetimlerini çalıştırmak için gerekli olduğunu bilirsiniz. ActiveX denetimleri etkinleştirme hakkında tarayıcının belgelerine bakın.

Geçerli Internet Explorer güvenlik ayarlarınıza göre bağlı olarak, bir güvenlik uyarısı iletişim kutusu alabilirsiniz. Denetimin betik oluşturmak için güvenli olmayabilir ve potansiyel olarak verebilir durumları zarar verebilir. Örneğin, ancak ayrıca bir dosya görüntüleyen bir denetiminizin yanında, bir `Delete` bir dosyayı silen yöntemi olacağını güvenli yalnızca bir sayfa üzerinde görüntülemeniz. Biri çağırabilirsiniz çünkü bu betik, ancak güvenli olmayacaktır `Delete` yöntemi.

> [!IMPORTANT]
> Bu öğretici için güvenli olarak işaretlenmemiş ActiveX denetimlerini çalıştırmak için Internet Explorer'da güvenlik ayarlarını değiştirebilirsiniz. Denetim Masası'nda tıklatın **Internet Özellikleri** tıklatıp **güvenlik** uygun ayarları değiştirmek için. Öğreticiyi tamamladıktan sonra güvenlik ayarlarınızı ilk durumuna değiştirin.

Ayrıca, bu belirli denetim için Güvenlik Uyarısı iletişim kutusunu görüntülemek gerekli olmayan Internet Explorer programlı olarak uyarabilir. Kullanarak bunu yapabilirsiniz `IObjectSafety` arabirimi. ATL sağlayan bir uygulama sınıfındaki bu arabirimin [Iobjectsafetyımpl](../atl/reference/iobjectsafetyimpl-class.md). Arabirimi denetiminize eklemek için Ekle `IObjectSafetyImpl` devralınan sınıflar listenize ve bunun için COM haritanıza bir giriş ekleyin.

### <a name="to-add-iobjectsafetyimpl-to-the-control"></a>Denetime Iobjectsafetyımpl eklemek için

1. PolyCtl.h içindeki devralınmış sınıflar listesinin sonuna aşağıdaki satırı ekleyin ve önceki satıra bir virgül ekleyin:

    [!code-cpp[NVC_ATL_Windowing#62](../atl/codesnippet/cpp/putting-the-control-on-a-web-page-atl-tutorial-part-7_1.h)]

1. PolyCtl.h içindeki COM eşlemesine aşağıdaki satırı ekleyin:

    [!code-cpp[NVC_ATL_Windowing#63](../atl/codesnippet/cpp/putting-the-control-on-a-web-page-atl-tutorial-part-7_2.h)]

## <a name="building-and-testing-the-control"></a>Derleme ve denetimini test etme

Denetimi oluşturun. Derleme tamamlandıktan sonra polyctl.htm dosyasını tarayıcı görünümünde yeniden açın. Bu kez Web sayfası doğrudan olmadan görüntülenmelidir **Güvenlik Uyarısı** iletişim kutusu. Çokgenin tıklarsanız, kenar sayısını birer birer artırır. Kenar sayısını azaltmak için çokgenin dışını tıklayın.

[6. adıma geri](../atl/adding-a-property-page-atl-tutorial-part-6.md)

## <a name="next-steps"></a>Sonraki Adımlar

Bu adım, ATL Öğreticisi burada sona eriyor. ATL hakkında daha fazla bilgi için bağlantılar için bkz: [ATL başlangıç sayfası](../atl/active-template-library-atl-concepts.md).

## <a name="see-also"></a>Ayrıca bkz.

[Öğretici](../atl/active-template-library-atl-tutorial.md)
