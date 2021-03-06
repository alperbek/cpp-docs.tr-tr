---
title: Bir nesneye bağlantı noktaları ekleme
ms.date: 11/04/2016
helpviewer_keywords:
- connection points [C++], adding to ATL objects
- Implement Connection Point ATL wizard
ms.assetid: 843531be-4a36-4db0-9d54-e029b1a72a8b
ms.openlocfilehash: 7341e69852ed804122e0196b51d305f5af0c35b9
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62223525"
---
# <a name="adding-connection-points-to-an-object"></a>Bir nesneye bağlantı noktaları ekleme

[ATL öğretici](../atl/active-template-library-atl-tutorial.md) desteğiyle bağlantı noktaları için bir denetim oluşturma, olayları ekleme ve bağlantı noktası uygulamak nasıl gösterir. ATL bağlantı noktaları ile uygulayan [Iconnectionpointımpl](../atl/reference/iconnectionpointimpl-class.md) sınıfı.

Bir bağlantı noktası uygulamak için iki seçeneğiniz vardır:

- Giden kendi olay kaynağı, bir bağlantı noktası denetim veya nesne ekleyerek uygulayın.

- Başka bir tür kitaplığı içinde tanımlanmış bir bağlantı noktası arabirimi yeniden kullanın.

Her iki durumda da, bağlantı noktası Uygulama Sihirbazı, işlemini gerçekleştirmek için bir tür kitaplığını kullanır.

### <a name="to-add-a-connection-point-to-a-control-or-object"></a>Bir denetim veya nesne için bir bağlantı noktası eklemek için

1. .İdl dosyasının kitaplığı bloğunda bir dispinterface tanımlayın. ATL denetimi Sihirbazı'yla denetim oluşturduğunuzda bağlantı noktaları desteğini etkinleştirilirse, dispinterface zaten oluşturulur. Denetim oluşturduğunuzda bağlantı noktaları desteğini etkinleştirmediyseniz .idl dosyasına bir dispinterface el ile eklemeniz gerekir. Bir dispinterface örneği verilmiştir. Giden arabirimleri dağıtma arabirimleri olarak gerekli değildir, ancak bu, bu örnekte iki görüntü arabirimlerinde bunu VBScript ve JScript gibi pek çok komut dosyası dilleri gerektirir:

   [!code-cpp[NVC_ATL_Windowing#81](../atl/codesnippet/cpp/adding-connection-points-to-an-object_1.idl)]

   Bir GUID oluşturulacak uuidgen.exe veya guidgen.exe yardımcı programını kullanın.

2. Dispinterface olarak ekleme `[default,source]` nesnesinin projenin .idl dosyasındaki coclass'ı arabirimi. ATL Denetim Sihirbazı'nı denetim oluşturduğunuzda bağlantı noktaları desteğini etkinleştirilirse, yeniden oluşturur `[default,source`] giriş. Bu giriş el ile eklemek için satırın kalın olarak ekleyin:

   [!code-cpp[NVC_ATL_Windowing#82](../atl/codesnippet/cpp/adding-connection-points-to-an-object_2.idl)]

   .İdl dosyasına bakın [Dai](../overview/visual-cpp-samples.md) ATL örnek olarak.

3. Sınıf Görünümü, olay arabirimin yöntemlerini ve özelliklerini eklemek için kullanın. Sınıf Görünümü'nde sınıfı sağ tıklatın, **Ekle** kısayol menüsüne ve ardından şirket **bağlantı noktası Ekle**.

4. İçinde **kaynak arabirimleri** bağlantı noktası Uygulama Sihirbazı, select liste kutusunda **projesinin arabirimleri**. Tuşuna basın ve denetim için bir arabirimi seçerseniz **Tamam**, şunları yapacaksınız:

   - Olay için giden aramaları yapmadan kod uygulayan bir olay proxy sınıfı ile bir üstbilgi dosyası oluşturur.

   - Bağlantı noktası eşlemesi için bir giriş ekleyin.

   Ayrıca, bilgisayarınızda tüm tür kitaplıklarını bir listesini görürsünüz. Yalnızca bu diğer tür kitaplıklarında biri başka bir tür kitaplığında bulunan tam aynı giden arabirimini uygulamak istiyorsanız, bağlantı noktası tanımlamak için kullanmanız gerekir.

### <a name="to-reuse-a-connection-point-interface-defined-in-another-type-library"></a>Bir bağlantı noktası arabirimi yeniden kullanmak için başka bir tür kitaplığında tanımlanan

1. Sınıf Görünümü'nde sağ uygulayan bir sınıf bir **BEGIN_COM_MAP** makrosu, noktasına **Ekle** kısayol menüsüne ve ardından şirket **bağlantı noktası Ekle**.

2. Bağlantı noktası Uygulama Sihirbazı, tür kitaplığındaki tür kitaplığının ve arabirim seçin ve tıklayın **Ekle**.

3. .İdl dosyası ya da düzenleyin:

   - Olay kaynağı kullanılan nesne .idl dosyasındaki dispinterface kopyalayın.

   - Kullanım **importlib** bu tür kitaplığı yönerge.

## <a name="see-also"></a>Ayrıca bkz.

[Bağlantı noktası](../atl/atl-connection-points.md)
