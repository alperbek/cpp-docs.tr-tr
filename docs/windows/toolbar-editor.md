---
title: Araç Çubuğu DüzenleyicisiC++()
ms.date: 02/14/2019
f1_keywords:
- vc.editors.toolbar.F1
- vc.editors.toolbar
- vc.editors.newtoolbarresource
helpviewer_keywords:
- resource editors [C++], Toolbar editor
- editors, toolbars
- toolbars [C++], editing
- Toolbar editor
- toolbars [C++], creating
- Toolbar editor [C++], creating new toolbars
- Insert Resource
- bitmaps [C++], converting to toolbars
- Toolbar editor [C++], converting bitmaps
- toolbars [C++], converting bitmaps
- New Toolbar Resource dialog box [C++]
- buttons [C++], custom toolbars
- toolbar buttons [C++], editing
- buttons
- toolbar buttons [C++], creating
- Toolbar editor [C++], creating buttons
- toolbar buttons [C++], button image
- toolbar buttons [C++], creating
- toolbar buttons (in Toolbar editor)
- toolbar buttons [C++], moving
- Toolbar editor [C++], moving buttons
- Toolbar editor [C++], copying buttons
- toolbars [C++], copying buttons
- toolbar buttons [C++], copying
- toolbar buttons [C++], deleting
- Toolbar editor [C++], deleting buttons
- Toolbar editor [C++], spacing toolbar buttons
- toolbar buttons [C++], space between buttons
- toolbar controls [MFC], command ID
- toolbar buttons [C++], setting properties
- Toolbar editor [C++], toolbar button properties
- command IDs, toolbar buttons
- size, toolbar buttons
- toolbar buttons [C++], setting properties
- Toolbar editor [C++], toolbar button properties
- status bars [C++], active toolbar button text
- command IDs, toolbar buttons
- width, toolbar buttons
- tool tips [C++], adding to toolbar buttons
- "\n in tool tip"
- toolbar buttons [C++], tool tips
- buttons [C++], tool tips
- Toolbar editor [C++], creating tool tips
ms.assetid: aa9f0adf-60f6-4f79-ab05-bc330f15ec43
ms.openlocfilehash: 72c42a06da8276d118c6c204f838ed4b31d142b9
ms.sourcegitcommit: 389c559918d9bfaf303d262ee5430d787a662e92
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/25/2019
ms.locfileid: "69514684"
---
# <a name="toolbar-editor-c"></a>Araç Çubuğu DüzenleyicisiC++()

**Araç Çubuğu Düzenleyicisi** , araç çubuğu kaynakları oluşturmanızı ve bit eşlemleri araç çubuğu kaynaklarına dönüştürmenizi sağlar. **Araç Çubuğu Düzenleyicisi** , tamamlanmış bir uygulamada nasıl göründükleri yakından benzeyen bir araç çubuğu ve düğme göstermek için bir grafik görüntüler kullanır.

**Araç Çubuğu Düzenleyicisi** penceresi, **resim Düzenleyicisi** penceresiyle aynı olan bir düğme resminin iki görünümünü gösterir. Bölünmüş çubuk iki bölmeyi ayırır ve bölmelerin göreli boyutlarını değiştirmek için bölme çubuğunu yan yana sürükleyebilirsiniz. Etkin bölmede bir seçim kenarlığı görüntülenir ve görüntünün iki görünümünün üzerinde konu araç çubuğu bulunur.

![Araç Çubuğu Düzenleyicisi](../mfc/media/vctoolbareditor.gif "vctoolbareditor")<br/>
**Araç Çubuğu Düzenleyicisi**

**Araç Çubuğu Düzenleyicisi** , Işlevsellikten **Görüntü Düzenleyicisi** ile benzerdir ve ikisi arasındaki menü öğeleri, grafik araçları ve bit eşlem Kılavuzu aynıdır. **Araç Çubuğu Düzenleyicisi** ve **Görüntü Düzenleyicisi**arasında geçiş yapmak için **görüntü** menüsünde bir menü komutu vardır. **Grafik** araç çubuğunu, **renkler** paletini veya **görüntü** menüsünü kullanma hakkında daha fazla bilgi için bkz. [görüntü düzenleyici](../windows/image-editor-for-icons.md).

Bir bit eşlemi dönüştürerek bir C++ projede yeni bir araç çubuğu oluşturabilirsiniz. Bit eşlemdeki grafik, bir araç çubuğunun düğme görüntülerine dönüştürür. Genellikle bit eşlem, her düğme için bir görüntüyle tek bir bit eşlem üzerinde birkaç düğme görüntüsü içerir. Varsayılan değer 16 piksel genişliğinde ve görüntünün yüksekliği olacak şekilde görüntüler herhangi bir boyutta olabilir. **Görüntü Düzenleyicinizde** **resim** menüsünden **Araç Çubuğu Düzenleyicisi** ' ni seçtiğinizde, **Yeni araç çubuğu kaynağı** iletişim kutusunda düğme görüntülerinin boyutunu belirtebilirsiniz.

**Yeni araç çubuğu kaynağı** iletişim kutusu, C++ projedeki bir araç çubuğu kaynağına eklemekte olduğunuz düğmelerin genişlik ve yüksekliğini belirtmenize olanak tanır. Varsayılan değer 16 × 15 pikseldir.

Bir araç çubuğu oluşturmak için kullanılan bir bit eşlemin en yüksek genişliği 2048, bu nedenle **Düğme genişliğini** *512*olarak ayarlarsanız yalnızca dört düğme olabilir. Genişliği *513*olarak ayarlarsanız yalnızca üç düğme olabilir.

**Yeni araç çubuğu kaynağı** iletişim kutusu aşağıdaki özelliklere sahiptir:

|Özellik|Açıklama|
|---|---------------|
|**Düğme genişliği**|Bir bit eşlem kaynağından bir araç çubuğu kaynağına dönüştürdüğünüz araç çubuğu düğmelerinin genişliğini girebileceğiniz bir alan sağlar.|
|**Düğme yüksekliği**|Bir bit eşlem kaynağından bir araç çubuğu kaynağına dönüştürdüğünüz araç çubuğu düğmelerinin yüksekliğini girmeniz için bir alan sağlar.|

> [!NOTE]
> Görüntüler, belirtilen genişlik ve yüksekliğe kırpılır ve renkler standart araç çubuğu renklerini (16 renk) kullanacak şekilde ayarlanır.

Varsayılan olarak, araç çubuğunun sağ ucunda yeni veya boş bir düğme görüntülenir. Düzenlemeden önce bu düğmeyi taşıyabilirsiniz. Yeni bir düğme oluşturduğunuzda, düzenlenen düğmesinin sağında başka bir boş düğme belirir. Bir araç çubuğunu kaydettiğinizde boş düğme kaydedilmez.

Bir araç çubuğu düğmesi aşağıdaki özelliklere sahiptir:

|Özellik|Açıklama|
|--------------|-----------------|
|**ID**|Düğme için KIMLIĞI tanımlar. Açılan liste, ortak **kimlik** adları sağlar.|
|**Genişlik**|Düğmenin genişliğini ayarlar. 16 piksel önerilir.|
|**Yükseklik**|Düğmenin yüksekliğini ayarlar. Bir düğmenin yüksekliği, araç çubuğundaki tüm düğmelerin yüksekliğini değiştirir. 15 piksel önerilir.|
|**Sor**|Durum çubuğunda görünen iletiyi tanımlar. *\N* ve bir adı eklemek, bu araç çubuğu düğmesine bir araç **İpucu** ekler. Daha fazla bilgi için bkz. [araç Ipucu oluşturma](../windows/creating-a-tool-tip-for-a-toolbar-button.md).|

**Genişlik** ve **Yükseklik** tüm düğmelere uygulanır. Bir araç çubuğu oluşturmak için kullanılan bir bit eşlem maksimum 2048 genişliğine sahiptir, bu nedenle düğme genişliğini *512*olarak ayarlarsanız yalnızca dört düğme olabilir ve genişliği *513*olarak ayarlarsanız yalnızca üç düğme olabilir.

## <a name="how-to"></a>Nasıl Yapılır

**Araç Çubuğu Düzenleyicisi** şunları yapmanızı mümkün:

### <a name="to-create-new-toolbars"></a>Yeni araç çubukları oluşturmak için

1. **Kaynak görünümü**, *. RC* dosyanıza sağ tıklayıp **Kaynak Ekle**' yi seçin. *. RC* dosyanızda mevcut bir araç çubuğağınız varsa, **araç** çubuğu klasörüne sağ tıklayıp **Ekle araç çubuğu**' nu seçebilirsiniz.

1. **Kaynak Ekle** Iletişim kutusunda **kaynak türü** listesinden **araç çubuğu** ' nu seçin ve ardından **Yeni**' yi seçin.

   **Araç çubuğu** kaynak türünün yanında bir artı işareti ( **+** ) görünürse, araç çubuğu şablonlarının kullanılabildiği anlamına gelir. Şablon listesini genişletmek için artı işaretini seçin, bir şablon seçin ve **Yeni**' yi seçin.

### <a name="to-convert-bitmaps-to-toolbar-resources"></a>Bit eşlemleri araç çubuğu kaynaklarına dönüştürmek için

1. [Görüntü düzenleyicisinde](../windows/image-editor-for-icons.md)varolan bir bit eşlem kaynağını açın. Bit eşlem zaten *. RC* dosyanızda yoksa, *. RC* dosyasına sağ tıklayın ve **içeri aktar**' ı seçin, ardından *. RC* dosyanıza eklemek istediğiniz bit eşlem 'e gidin ve **Aç**' ı seçin.

1. Menü **resmi** > **Araç Çubuğu Düzenleyicisi**' ne gidin.

   **Yeni araç çubuğu kaynağı** iletişim kutusu görüntülenir. Simge görüntülerinin genişliğini ve yüksekliğini bit eşlemle eşleşecek şekilde değiştirebilirsiniz. Araç çubuğu görüntüsü daha sonra **araç çubuğu düzenleyicisinde**görüntülenir.

1. Dönüştürme işleminin tamamlanabilmesi için, [Özellikler penceresi](/visualstudio/ide/reference/properties-window)kullanarak düğmenin komut **kimliğini** değiştirin. Yeni *kimliği* yazın veya açılan listeden bir **kimlik** seçin.

   > [!TIP]
   > **Özellikler** penceresi, başlık çubuğunda bir raptiye düğmesi içerir ve bu pencere Için **Otomatik gizlemeyi** etkinleştirilir veya devre dışı bırakır. Tek bir özellik pencerelerini yeniden açmak zorunda kalmadan tüm araç çubuğu düğmesi özellikleri arasında geçiş yapmak için, **Özellikler** penceresinin sabit kalmasını sağlamak üzere **otomatik gizleme** ' yi kapatın.

   Ayrıca, yeni araç çubuğundaki düğmelerin komut kimliklerini [Özellikler penceresi](/visualstudio/ide/reference/properties-window)kullanarak değiştirebilirsiniz.

### <a name="to-manage-toolbar-buttons"></a>Araç çubuğu düğmelerini yönetmek için

#### <a name="to-create-a-new-toolbar-button"></a>Yeni bir araç çubuğu düğmesi oluşturmak için

1. [Kaynak görünümü](how-to-create-a-resource-script-file.md#create-resources) kaynak klasörünü genişletin (örneğin, *Project1. RC*).

1. **Araç çubuğu** klasörünü genişletin ve düzenlemek üzere bir araç çubuğu seçin, sonra aşağıdakilerden birini yapın:

   - Araç çubuğunun sağ ucundaki boş düğmeye bir KIMLIK atayın. Bunu, [Özellikler penceresinde](/visualstudio/ide/reference/properties-window) **ID** özelliğini düzenleyerek yapabilirsiniz. Örneğin, bir menü seçeneği olarak aynı KIMLIĞE bir araç çubuğu düğmesi vermek isteyebilirsiniz. Bu durumda, menü seçeneğinin **kimliğini** seçmek için açılan liste kutusunu kullanın.

   - **Araç çubuğu görünüm** bölmesinde araç çubuğunun sağ ucundaki boş düğmesini seçin ve çizim ' i başlatın. Varsayılan düğme komut KIMLIĞI atanır (ID_BUTTON\<n >).

#### <a name="to-add-an-image-to-a-toolbar-as-a-button"></a>Bir araç çubuğuna düğme olarak görüntü eklemek için

1. [Kaynak görünümü](how-to-create-a-resource-script-file.md#create-resources)' de, araç çubuğunu çift tıklayarak açın.

1. Ardından, araç çubuğuna eklemek istediğiniz görüntüyü açın.

   > [!NOTE]
   > Görüntüyü Visual Studio 'da açarsanız, **görüntü düzenleyicide**açılır. Görüntüyü diğer grafik programlarında da açabilirsiniz.

1. Menü **düzenle** > **Kopyala**' ya gidin.

1. Kaynak pencerenin üst kısmındaki sekmesini seçerek araç çubuğa geçiş yapın.

1. Menü **düzenle** > **Yapıştır**'a gidin.

   Görüntü, araç çubuğunda yeni bir düğme olarak görünür.

#### <a name="to-move-a-toolbar-button"></a>Bir araç çubuğu düğmesini taşımak için

**Araç çubuğu görünüm** bölmesinde, taşımak istediğiniz düğmeyi araç çubuğunda yeni konumuna sürükleyin.

- Bir araç çubuğundan düğme kopyalamak için **CTRL** tuşunu basılı tutun ve **araç çubuğu görünüm** bölmesinde düğmeyi araç çubuğundaki yeni konumuna veya başka bir araç çubuğunda yer alan bir konuma sürükleyin.

- Bir araç çubuğu düğmesini silmek için araç çubuğu düğmesini seçin ve araç çubuğundan sürükleyin.

- Araç çubuğundaki düğmeler arasına boşluk eklemek veya kaldırmak için, araç çubuğunda bir diğerine veya bir diğerine doğru sürükleyin.

|Eylem|Adım|
|------|------|
|Arkasından bir boşluk gelen bir düğmeden önce boşluk eklemek için|Alt yarısında ilgili sonraki düğmeyle örtüşene kadar düğmeyi sağa veya aşağı sürükleyin.|
|Bir düğmeden önce bir boşluk gelen ve sondaki boşluğu tutan bir düğmeden önce boşluk eklemek için|Sağ veya alt kenar, ileri düğmesine dokunana kadar veya yalnızca onunla örtüşene kadar düğmeyi sürükleyin.|
|Bir düğmeden önce bir boşluk gelen bir boşluk eklemek ve aşağıdaki alanı kapatmak için|Alt yarısında ilgili sonraki düğmeyle örtüşene kadar düğmeyi sağa veya aşağı sürükleyin.|
|Araç çubuğundaki düğmeler arasındaki boşluğu kaldırmak için|Kenarı, üst yarısında ilgili bir sonraki düğmeyle çıkana kadar alanın diğer tarafındaki düğmeye doğru sürükleyerek düğmeyi sürükleyin.|

> [!NOTE]
> Düğmenin üzerine sürüklediğiniz bir boşluk yoksa ve düğmeyi bitişik düğmeden daha uzun bir yere sürüklerseniz **Araç Çubuğu Düzenleyicisi** , sürüklediğiniz düğmenin zıt tarafına bir boşluk ekler...

#### <a name="to-change-the-properties-of-a-toolbar-button"></a>Bir araç çubuğu düğmesinin özelliklerini değiştirmek için

1. Bir C++ projede araç çubuğu düğmesini seçin.

1. Yeni kimliği [Özellikler penceresinde](/visualstudio/ide/reference/properties-window) **kimlik** özelliğine yazın veya açılan listeyi kullanarak yeni bir **kimlik**seçin.

#### <a name="to-create-a-tool-tip-for-a-toolbar-button"></a>Bir araç çubuğu düğmesi için araç ipucu oluşturmak için

1. Araç çubuğu düğmesini seçin.

1. [Özellikler penceresinde](/visualstudio/ide/reference/properties-window), **istem** alanında, durum çubuğu için bir açıklama ve ileti sonra `\n` ekleyin ve araç ipucu adını ekleyin.

Örneğin, **WordPad**'de **Yazdır** düğmesine ait araç ipucunu görmek için:

1. **WordPad 'i**açın.

1. Fare işaretçinizi **Yazdır** araç çubuğu düğmesinin üzerine getirin ve şimdi `Print` kelimesinin fare işaretçiniz altında olduğuna dikkat edin.

1. **WordPad** penceresinin altındaki durum çubuğuna bakın ve şimdi `Prints the active document`metin gösterdiğini unutmayın.

`Print` araç ipucu adıdır ve `Prints the active document` durum çubuğu düğmesinin açıklamasıdır.

Bu etkiyi **araç çubuğu düzenleyicisini**kullanarak Istiyorsanız, **Prompt** özelliğini `Prints the active document\nPrint`olarak ayarlayın.

## <a name="requirements"></a>Gereksinimler

MFC veya ATL

## <a name="see-also"></a>Ayrıca bkz.

[Kaynak düzenleyicileri](../windows/resource-editors.md)
[menüler ve diğer kaynaklar](/windows/win32/menurc/resources)<br/>
[Araç Çubuğu Düğmesi Özellikleri](../windows/toolbar-button-properties.md)<br/>
