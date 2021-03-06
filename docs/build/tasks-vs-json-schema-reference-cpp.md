---
title: Tasks. vs. JSON şema başvurusu (C++)
ms.date: 08/20/2019
helpviewer_keywords:
- tasks.vs.json file [C++]
ms.assetid: abd1985e-3717-4338-9e80-869db5435175
ms.openlocfilehash: cc6b2983d3cc3d40449357a554df5feee38c21d9
ms.sourcegitcommit: 6c1960089b92d007fc28c32af1e4bef0f85fdf0c
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/31/2019
ms.locfileid: "75556662"
---
# <a name="tasksvsjson-schema-reference-c"></a>Tasks. vs. JSON şema başvurusu (C++)

Visual Studio 'Yu açık bir klasör projesinde kaynak kodunuzu nasıl derleyeceğinizi söylemek için bir *Tasks. vs. JSON* dosyası ekleyin. Burada herhangi bir rastgele görevi tanımlayabilir ve ardından **Çözüm Gezgini** bağlam menüsünden çağırabilirsiniz. CMake projeleri, *Cmakelists. txt*dosyasında tüm derleme komutları belirtildiğinden bu dosyayı kullanmaz. CMake dışındaki derleme sistemlerinde, *Tasks. vs. JSON* , derleme komutlarını belirtebileceğiniz ve derleme betikleri çağırabileceğiniz yerdir. *Tasks. vs. JSON*kullanma hakkında genel bilgi için bkz. ["klasör açma" geliştirmesi için derleme ve hata ayıklama görevlerini özelleştirme](/visualstudio/ide/customize-build-and-debug-tasks-in-visual-studio).

Bir görev, dört `type` değerden birine sahip olabilecek bir özelliğe sahiptir `default`:, `launch`, `remote`veya. `msbuild` Birçok görev, uzak `launch` bir bağlantı gerekmiyorsa kullanılmalıdır.

## <a name="default-properties"></a>Varsayılan Özellikler

Tüm görev türlerinde varsayılan özellikler mevcuttur:

||||
|-|-|-|
|**Özellik**|**Tür**|**Açıklama**|
|`taskLabel`|string| (Gerekli.) Kullanıcı arabiriminde kullanılan görev etiketini belirtir.|
|`appliesTo`|string| (Gerekli.) Komutun hangi dosyalara uygulanabilir olduğunu belirtir. Joker karakter kullanımı desteklenir, örneğin: "*", "*. cpp", "/*. txt"|
|`contextType`|string| İzin verilen değerler: "özel", "derleme", "Temizle", "yeniden derle". Görevin bağlam menüsünde nerede görüneceğini belirler. Varsayılan "Custom" olarak belirlenmiştir.|
|`output`|string| Göreviniz için bir çıkış etiketi belirtir.|
|`inheritEnvironments`|array| Birden çok kaynaktan devralınan bir ortam değişkenleri kümesini belirtir. *Cmakesettings. JSON* veya *cppproperties. JSON* gibi dosyalardaki değişkenleri tanımlayabilir ve bunları görev bağlamı için kullanılabilir hale getirebilirsiniz. **Visual Studio 16,4:**: `env.VARIABLE_NAME` sözdizimini kullanarak görev başına temelinde ortam değişkenlerini belirtin. Bir değişkeni kaldırmak için, "null" olarak ayarlayın.|
|`passEnvVars`|boole| Görev bağlamına ek ortam değişkenlerinin eklenip eklenmeyeceğini belirtir. Bu değişkenler, `envVars` özelliği kullanılarak tanımlandıklarından farklıdır. Varsayılan değer "true" olarak belirlenmiştir.|

## <a name="launch-properties"></a>Başlatma özellikleri

Görev türü olduğunda `launch`, bu özellikler kullanılabilir:

||||
|-|-|-|
|**Özellik**|**Tür**|**Açıklama**|
|`command`|string| Başlatılacak işlemin veya betiğin tam yolunu belirtir.|
|`args`|array| Komuta geçirilen bağımsız değişkenlerin virgülle ayrılmış bir listesini belirtir.|
|`launchOption`|string| İzin verilen değerler: "none", "devam eden", "IgnoreError". Hatalar olduğunda komutla nasıl devam etmek istediğinizi belirtir.|
|`workingDirectory`|string| Komutun çalıştırılacağı dizini belirtir. Projenin geçerli çalışma dizinini varsayılan olarak belirler.|
|`customLaunchCommand`|string| Komutu yürütmeden önce uygulanacak genel kapsam özelleştirmesini belirtir. % PATH% gibi ortam değişkenlerini ayarlamak için faydalıdır.|
|`customLaunchCommandArgs`|string| CustomLaunchCommand için bağımsız değişkenleri belirtir. (Gerektirir `customLaunchCommand`.)|
 `env`| Özel ortam değişkenlerinin anahtar-değer listesini belirtir. Örneğin, "myEnv": "myVal"|
|`commands`|array| Sırayla çağrılacak komutların listesini belirtir.|

### <a name="example"></a>Örnek

Aşağıdaki görevler, klasöründe bir derleme görevleri dosyası sağlandığında ve `Mingw64` bu ortam cppproperties. JSON içinde tanımlanmışsa, [cppproperties. JSON Şema başvurusunda](cppproperties-schema-reference.md#user_defined_environments)gösterildiği gibi *Make. exe* ' yi çağırır: *CppProperties.json*

```json
 {
  "version": "0.2.1",
  "tasks": [
    {
      "taskLabel": "gcc make",
      "appliesTo": "*.cpp",
      "type": "launch",
      "contextType": "custom",
      "inheritEnvironments": [
        "Mingw64"
      ],
      "command": "make"
    },
    {
      "taskLabel": "gcc clean",
      "appliesTo": "*.cpp",
      "type": "launch",
      "contextType": "custom",
      "inheritEnvironments": [
        "Mingw64"
      ],
      "command": "make",
      "args": ["clean"]
    }
  ]
}
```

Bu görevler, **Çözüm Gezgini**bir *. cpp* dosyasına sağ tıkladığınızda bağlam menüsünden çağrılabilir.

## <a name="remote-properties"></a>Uzak Özellikler

C++ iş yüküyle Linux geliştirmeyi yüklediğinizde ve Visual Studio bağlantı Yöneticisi 'Ni kullanarak uzak makineye bir bağlantı eklediğinizde uzak görevler etkinleştirilir. Uzak bir görev, uzak bir sistemde komutlar çalıştırır ve ayrıca dosyaları buna kopyalayabilir.

Görev türü olduğunda `remote`, bu özellikler kullanılabilir:

||||
|-|-|-|
|**Özellik**|**Tür**|**Açıklama**|
|`remoteMachineName`|string|Uzak makinenin adı. **Bağlantı yöneticisinde**bir makine adıyla eşleşmelidir.|
|`command`|string|Uzak makineye gönderme komutu. Varsayılan olarak komutlar, uzak sistemdeki $HOME dizininde yürütülür.|
|`remoteWorkingDirectory`|string|Uzak makinedeki geçerli çalışma dizini.|
|`localCopyDirectory`|string|Uzak makineye kopyalanacak yerel dizin. Geçerli çalışma dizinini varsayılan olarak belirler.|
|`remoteCopyDirectory`|string|İçine kopyalanmış olan `localCopyDirectory` uzak makinedeki dizin.|
|`remoteCopyMethod`|string| Kopyalama için kullanılacak yöntem. İzin verilen değerler: "none", "SFTP", "rsync". büyük projeler için rsync önerilir.|
|`remoteCopySourcesOutputVerbosity`|string| İzin verilen değerler: "normal", "verbose", "Tanılama".|
|`rsyncCommandArgs`|string|Varsayılan olarak "-t--Delete" olarak belirlenmiştir.|
|`remoteCopyExclusionList`|array|Kopyalama işlemlerinden hariç tutulacak dosyaların `localCopyDirectory` virgülle ayrılmış listesi.|

### <a name="example"></a>Örnek

**Çözüm Gezgini**'de *Main. cpp* öğesine sağ tıkladığınızda, bağlam menüsünde aşağıdaki görev görüntülenir. `ubuntu` **Bağlantı Yöneticisi**'nde çağrılan uzak makineye bağlıdır. Görev, Visual Studio 'daki geçerli açık klasörü uzak makinedeki `sample` dizine kopyalar ve ardından programı derlemek için g + + çağırır.

```json
{
  "version": "0.2.1",
  "tasks": [
    {
      "taskLabel": "Build",
      "appliesTo": "main.cpp",
      "type": "remote",
      "contextType": "build",
      "command": "g++ main.cpp",
      "remoteMachineName": "ubuntu",
      "remoteCopyDirectory": "~/sample",
      "remoteCopyMethod": "sftp",
      "remoteWorkingDirectory": "~/sample/hello",
      "remoteCopySourcesOutputVerbosity": "Verbose"
    }
  ]
}
```

## <a name="msbuild-properties"></a>MSBuild özellikleri

Görev türü olduğunda `msbuild`, bu özellikler kullanılabilir:

||||
|-|-|-|
|**Özellik**|**Tür**|**Açıklama**|
|`verbosity`|string| MSBuild proje derlemesi çıkış verbosityAllowed değerlerini belirtir: "sessiz", "minimal", "normal", "ayrıntılı", "Tanılama".|
|`toolsVersion`|string| Projeyi derlemek için araç takımı sürümünü belirtir, örneğin "2,0", "3,5", "4,0", "Current". Varsayılan olarak "geçerli" olur.|
|`globalProperties`|object|Projeye geçirilecek genel özelliklerin anahtar-değer listesini belirtir, örneğin, "yapılandırma": "yayın"|
|`properties`|object| Yalnızca ek proje özelliklerinin anahtar-değer listesini belirtir.|
|`targets`|array| Üzerinde çağrılacak hedeflerin listesini proje üzerinde belirtir. Hiçbiri belirtilmemişse projenin varsayılan hedefi kullanılır.|
