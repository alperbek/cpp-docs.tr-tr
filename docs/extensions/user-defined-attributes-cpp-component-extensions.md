---
title: Kullanıcı tanımlı öznitelikler (C++/CLI ve C++/CX)
ms.date: 10/12/2018
ms.topic: reference
helpviewer_keywords:
- metadata, extending
- custom attributes, extending metadata
ms.assetid: 98b29048-a3ea-4698-8441-f149cdaec9fb
ms.openlocfilehash: aed36ac7fed7eb1f16f8648f7bcd7efb37f43a75
ms.sourcegitcommit: 857fa6b530224fa6c18675138043aba9aa0619fb
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/24/2020
ms.locfileid: "80171898"
---
# <a name="user-defined-attributes--ccli-and-ccx"></a>Kullanıcı tanımlı öznitelikler (C++/CLI ve C++/CX)

C++/CLı ve C++/CX, bir arabirimin, sınıfın veya yapının, yöntemin, parametrenin veya numaralandırmanın meta verilerini genişleten platforma özel öznitelikler oluşturmanızı sağlar. Bu öznitelikler [Standart C++ özniteliklerden](../cpp/attributes.md)farklıdır.

## <a name="windows-runtime"></a>Windows Çalışma Zamanı

Özellikler 'e/CX C++özniteliklerini uygulayabilir, ancak oluşturuculara veya yöntemlere uygulanmaz.

### <a name="requirements"></a>Gereksinimler

Derleyici seçeneği: `/ZW`

## <a name="common-language-runtime"></a>Ortak Dil Çalışma Zamanı

Bu konuda sunulan bilgiler ve söz dizimi, [özniteliğinde](../windows/attributes/attribute.md)sunulan bilgilerin yerini almak için tasarlanmıştır.

Bir tür tanımlayarak <xref:System.Attribute> ve isteğe bağlı olarak <xref:System.AttributeUsageAttribute> özniteliğini uygulayarak özel bir öznitelik tanımlayabilirsiniz.

Daha fazla bilgi için bkz.

- [Öznitelik Hedefleri](attribute-targets-cpp-component-extensions.md)

- [Öznitelik Parametre Türleri](attribute-parameter-types-cpp-component-extensions.md)

Derlemeleri görsel C++olarak imzalama hakkında daha fazla bilgi için bkz. [tanımlayıcı ad derlemeleri (derleme imzalamaC++) (/CLI)](../dotnet/strong-name-assemblies-assembly-signing-cpp-cli.md).

### <a name="requirements"></a>Gereksinimler

Derleyici seçeneği: `/clr`

### <a name="examples"></a>Örnekler

Aşağıdaki örnek, nasıl özel bir öznitelik tanımlanacağını göstermektedir.

```cpp
// user_defined_attributes.cpp
// compile with: /clr /c
using namespace System;

[AttributeUsage(AttributeTargets::All)]
ref struct Attr : public Attribute {
   Attr(bool i){}
   Attr(){}
};

[Attr]
ref class MyClass {};
```

Aşağıdaki örnek özel özniteliklerin bazı önemli özelliklerini gösterir. Örneğin, bu örnek özel özniteliklerin ortak kullanımını gösterir: kendisini istemcilere tam olarak betimleyen bir sunucu örneği oluşturma.

```cpp
// extending_metadata_b.cpp
// compile with: /clr
using namespace System;
using namespace System::Reflection;

public enum class Access { Read, Write, Execute };

// Defining the Job attribute:
[AttributeUsage(AttributeTargets::Class, AllowMultiple=true )]
public ref class Job : Attribute {
public:
   property int Priority {
      void set( int value ) { m_Priority = value; }
      int get() { return m_Priority; }
   }

   // You can overload constructors to specify Job attribute in different ways
   Job() { m_Access = Access::Read; }
   Job( Access a ) { m_Access = a; }
   Access m_Access;

protected:
   int m_Priority;
};

interface struct IService {
   void Run();
};

   // Using the Job attribute:
   // Here we specify that QueryService is to be read only with a priority of 2.
   // To prevent namespace collisions, all custom attributes implicitly
   // end with "Attribute".

[Job( Access::Read, Priority=2 )]
ref struct QueryService : public IService {
   virtual void Run() {}
};

// Because we said AllowMultiple=true, we can add multiple attributes
[Job(Access::Read, Priority=1)]
[Job(Access::Write, Priority=3)]
ref struct StatsGenerator : public IService {
   virtual void Run( ) {}
};

int main() {
   IService ^ pIS;
   QueryService ^ pQS = gcnew QueryService;
   StatsGenerator ^ pSG = gcnew StatsGenerator;

   //  use QueryService
   pIS = safe_cast<IService ^>( pQS );

   // use StatsGenerator
   pIS = safe_cast<IService ^>( pSG );

   // Reflection
   MemberInfo ^ pMI = pIS->GetType();
   array <Object ^ > ^ pObjs = pMI->GetCustomAttributes(false);

   // We can now quickly and easily view custom attributes for an
   // Object through Reflection */
   for( int i = 0; i < pObjs->Length; i++ ) {
      Console::Write("Service Priority = ");
      Console::WriteLine(static_cast<Job^>(pObjs[i])->Priority);
      Console::Write("Service Access = ");
      Console::WriteLine(static_cast<Job^>(pObjs[i])->m_Access);
   }
}
```

```Output
Service Priority = 0

Service Access = Write

Service Priority = 3

Service Access = Write

Service Priority = 1

Service Access = Read
```

`Object^` türü, VARIANT veri türünün yerini alır. Aşağıdaki örnek, `Object^` dizisini parametre olarak alan özel bir özniteliği tanımlar.

Öznitelik bağımsız değişkenleri derleme zamanı sabitleri olmalıdır; Çoğu durumda, sabit değişmez değer olmalıdır.

Özel öznitelik bloğundan System:: Type değeri döndürme hakkında bilgi için bkz. [TypeId](typeid-cpp-component-extensions.md) .

```cpp
// extending_metadata_e.cpp
// compile with: /clr /c
using namespace System;
[AttributeUsage(AttributeTargets::Class | AttributeTargets::Method)]
public ref class AnotherAttr : public Attribute {
public:
   AnotherAttr(array<Object^>^) {}
   array<Object^>^ var1;
};

// applying the attribute
[ AnotherAttr( gcnew array<Object ^> { 3.14159, "pi" }, var1 = gcnew array<Object ^> { "a", "b" } ) ]
public ref class SomeClass {};
```

Çalışma zamanı, özel öznitelik sınıfının ortak bölümünün seri hale getirilebilir olması gerekir.  Özel öznitelikler yazarken, özel özniteleyebileceğiniz adlandırılmış bağımsız değişkenler derleme zamanı sabitleri ile sınırlıdır.  (Meta verilerde sınıf düzeninize eklenen bir bit dizisi olarak düşünün.)

```cpp
// extending_metadata_f.cpp
// compile with: /clr /c
using namespace System;
ref struct abc {};

[AttributeUsage( AttributeTargets::All )]
ref struct A : Attribute {
   A( Type^ ) {}
   A( String ^ ) {}
   A( int ) {}
};

[A( abc::typeid )]
ref struct B {};
```

## <a name="see-also"></a>Ayrıca bkz.

[.NET ve UWP İçin Bileşen Uzantıları](component-extensions-for-runtime-platforms.md)
