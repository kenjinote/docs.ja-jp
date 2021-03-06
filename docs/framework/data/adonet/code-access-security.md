---
title: コード アクセス セキュリティと ADO.NET
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 93e099eb-daa1-4f1e-b031-c1e10a996f88
ms.openlocfilehash: ea5dbcc128f97ebbec72273378adb042bbe34e1e
ms.sourcegitcommit: 11f11ca6cefe555972b3a5c99729d1a7523d8f50
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/03/2018
---
# <a name="code-access-security-and-adonet"></a>コード アクセス セキュリティと ADO.NET
.NET Framework はコード アクセス セキュリティ (CAS) に加えてロール ベースのセキュリティを備えています。どちらも、共通言語ランタイム (CLR) が提供する共通のインフラストラクチャを使って実装されています。 アンマネージ コードの場合、ほとんどのアプリケーションはユーザーまたはプリンシパルの権限で実行されます。 そのため、悪意のあるソフトウェアやエラーを含むソフトウェアが、システム特権を持つユーザーによって実行された場合、コンピューター システムが被害を受けたり、機密データが改ざんされる可能性があります。  
  
 これに対し、.NET Framework で実行されるマネージ コードには、コードそのものに適用されるコード アクセス セキュリティが存在します。 コードの実行が許可されるかどうかは、プリンシパルの ID だけでなく、コードの作成元など、コードの ID を表す情報に依存します。 これにより、マネージ コードが誤用される可能性が低くなります。  
  
## <a name="code-access-permissions"></a>コード アクセス許可  
 コードは、実行されるときに、CLR のセキュリティ システムで評価される証拠を提示します。 通常、この証拠は、URL、サイト、ゾーン、アセンブリの ID を保証するデジタル署名などのコードの作成元に関する情報で構成されます。  
  
 CLR は、そのコードに許されている操作の範囲内で実行を許可します。 コードは権限を要求できますが、その要求は管理者が設定したセキュリティ ポリシーに基づいて受理されます。  
  
> [!NOTE]
>  CLR で実行されるコード自体に、アクセス許可を与えることはできません。 たとえば、コードから要求できる権限は、セキュリティ ポリシーによって許可されたレベルよりも低い権限だけであり、それを超える権限が付与されることはありません。 権限を付与する場合は、まず、権限をまったく付与しない状態から始め、その後で、実行しようとする特定のタスクに必要な最小限の権限を追加してゆくようにします。 すべての権限を与えてから、不要なものを 1 つずつ拒否していく方法では、アプリケーションを危険にさらす結果となります。必要以上の権限を付与することによって意図しないセキュリティ ホールを招く可能性があります。 詳細については、次を参照してください。 [NIB: セキュリティ ポリシーを構成する](http://msdn.microsoft.com/library/0f130bcd-1bba-4346-b231-0bcca7dab1a4)と[NIB: セキュリティ ポリシーの管理](http://msdn.microsoft.com/library/d754e05d-29dc-4d3a-a2c2-95eaaf1b82b9)です。  
  
 コードのアクセス権限には、次の 3 種類があります。  
  
-   `Code access permissions`。<xref:System.Security.CodeAccessPermission> クラスから派生します。 ファイルや環境変数などの保護されたリソースにアクセスして、保護された操作 (アンマネージ コードへのアクセスなど) を実行するには権限が必要です。  
  
-   `Identity permissions`。アセンブリを識別する特性を表します。 アセンブリには証拠に基づいて権限が付与されます。証拠には、デジタル署名やコードの作成元などの情報が含まれます。 ID 権限も <xref:System.Security.CodeAccessPermission> 基本クラスから派生します。  
  
-   `Role-based security permissions`。プリンシパルが、指定された ID を持っているか、または、指定されたロールに属しているかどうかに基づきます。 <xref:System.Security.Permissions.PrincipalPermission> クラスにより、アクティブなプリンシパルに対する宣言型および命令型の権限チェックが可能となります。  
  
 ランタイムのセキュリティ システムは、特定のリソースへのアクセスまたは特定の操作の実行がコードに許されているかどうかを判断するため、呼び出し履歴をたどりながら、各呼び出し元に付与されている権限と、要求されている権限とを比較します。 呼び出し履歴に、要求された権限を持たない呼び出し元が 1 つでも見つかった場合、<xref:System.Security.SecurityException> がスローされてアクセスが拒否されます。  
  
### <a name="requesting-permissions"></a>権限の要求  
 権限を要求する目的は、そのアプリケーションを実行するために必要な権限をランタイムに伝えると共に、実際に必要な権限以外は付与されないようにすることです。 たとえば、ローカル ディスクにデータを書き込むアプリケーションは <xref:System.Security.Permissions.FileIOPermission> を必要とします。 この権限が付与されていない場合、アプリケーションがディスクへの書き込みを試行した時点で実行に失敗します。 ただし、アプリケーションから `FileIOPermission` を要求した場合、その権限が付与されなければ、最初の段階で例外が生成され、アプリケーションが読み込まれることはありません。  
  
 ディスクからのデータの読み取りだけを必要とするアプリケーションでは、書き込み権限が決して付与されないように要求できます。 バグが存在していたり、悪意のある攻撃を受けたとしても、操作の対象となるデータに損害を与えることはありません。 詳細については、次を参照してください。 [NIB: アクセス許可の要求](http://msdn.microsoft.com/library/0447c49d-8cba-45e4-862c-ff0b59bebdc2)です。  
  
## <a name="role-based-security-and-cas"></a>ロール ベースのセキュリティと CAS  
 ロール ベースのセキュリティとコード アクセス セキュリティ (CAS) の両方を実装することで、アプリケーションの全体的なセキュリティを高めることができます。 ロール ベースのセキュリティには、Windows アカウントまたはカスタム ID を使用できます。セキュリティ プリンシパルに関する情報には、現在のスレッドからアクセスできます。 また、ユーザーによって指定された資格情報に基づいて、データやリソースへのアクセスを提供するアプリケーションも少なくありません。 このようなアプリケーションは、通常、ユーザーのロールを調べ、そのロールに基づいてリソースへのアクセスを許可します。  
  
 ロール ベースのセキュリティを使用することで、コンポーネントが、現在のユーザーおよびそのユーザーに関連付けられているロールを実行時に特定できるようになります。 この情報を CAS ポリシーを使ってマッピングすることによって、一連の権限が実行時に判別されます。 特定のアプリケーション ドメインでは、ホストが既定のロール ベース セキュリティ ポリシーを変更し、ユーザーおよびそのユーザーに関連付けられたロールを表す既定のセキュリティ プリンシパルを設定できます。  
  
 CLR にはマネージ コードに制限を適用するためのメカニズムが、権限を使用することによって実装されています。 ロール ベースのセキュリティ権限により、ユーザー (またはユーザーのために行動するエージェント) が特定の ID を持っているかどうか、または特定のロールに所属しているかどうかを検出するメカニズムが実現されます。 詳細については、次を参照してください。[セキュリティのアクセス許可](http://msdn.microsoft.com/library/b03757b4-e926-4196-b738-3733ced2bda0)です。  
  
 開発しているアプリケーションの種類によっては、データベースに対するロール ベースの権限の実装も考慮する必要があります。 SQL Server でのロールベースのセキュリティの詳細については、次を参照してください。 [SQL Server のセキュリティ](../../../../docs/framework/data/adonet/sql/sql-server-security.md)です。  
  
## <a name="assemblies"></a>アセンブリ  
 アセンブリは、.NET Framework アプリケーションの配置、バージョン管理、再利用、アクティベーション スコープ、およびセキュリティ権限の基本単位です。 アセンブリは、互いに連携して動作するように作成された一連の型やリソースを提供し、"機能" の論理上の単位を成すものです。 CLR から見て、型がアセンブリのコンテキスト外に存在することはありません。 作成して、アセンブリの展開の詳細については、次を参照してください。[アセンブリを使用したプログラミング](../../../../docs/framework/app-domains/programming-with-assemblies.md)です。  
  
### <a name="strong-naming-assemblies"></a>厳密な名前付きアセンブリ  
 厳密な名前 (デジタル署名) は、アセンブリの ID (単純なテキスト名、バージョン番号、および使用可能な場合はカルチャ情報) と、公開キーおよびデジタル署名で構成されます。 このデジタル署名は、対応する秘密キーを使用してアセンブリ ファイルから生成されます。 アセンブリ ファイルにはアセンブリ マニフェストが格納されており、そこに、アセンブリを構成するすべてのファイルの名前とハッシュが含まれます。  
  
 アセンブリに厳密な名前を付けることで、アプリケーションやコンポーネントに一意の ID が与えられます。他のソフトウェアは、その ID を使用することで、対応するアプリケーションまたはコンポーネントを明示的に参照できます。 アセンブリに厳密な名前を付けると、悪意のあるコードを含むアセンブリのなりすましから保護することができます。 また、異なるバージョンのコンポーネント間でバージョンの整合性をとることもできます。 グローバル アセンブリ キャッシュ (GAC) に展開されるアセンブリには、厳密な名前を付ける必要があります。 詳しくは、「[厳密な名前付きアセンブリの作成と使用](../../../../docs/framework/app-domains/create-and-use-strong-named-assemblies.md)」をご覧ください。  
  
## <a name="partial-trust-in-adonet-20"></a>ADO.NET 2.0 での Partial Trust (部分信頼)  
 ADO.NET 2.0 では、.NET Framework Data Provider for SQL Server、.NET Framework Data Provider for OLE DB、.NET Framework Data Provider for ODBC、および .NET Framework Data Provider for Oracle のすべてが、部分的に信頼された環境でも実行できるようになりました。 .NET Framework の以前のリリースでは、信頼性のレベルが full-trust よりも低いアプリケーションでは <xref:System.Data.SqlClient> のみがサポートされていました。  
  
 SQL Server プロバイダーを使用する部分的に信頼できるアプリケーションは、少なくとも、Execution アクセス許可と <xref:System.Data.SqlClient.SqlClientPermission> アクセス許可が必要です。  
  
### <a name="permission-attribute-properties-for-partial-trust"></a>Partial Trust (部分信頼) のアクセス許可属性プロパティ  
 部分信頼のシナリオでは、<xref:System.Data.SqlClient.SqlClientPermissionAttribute> メンバーを使用して、.NET Framework Data Provider for SQL Server が使用できる機能をさらに制限することができます。  
  
 使用可能な <xref:System.Data.SqlClient.SqlClientPermissionAttribute> プロパティとその説明を次の表に示します。  
  
|アクセス許可属性プロパティ|説明|  
|-----------------------------------|-----------------|  
|`Action`|セキュリティ アクションを取得または設定します。 このプロパティは、<xref:System.Security.Permissions.SecurityAttribute> から継承されています。|  
|`AllowBlankPassword`|接続文字列内で空白のパスワードの使用を許可または禁止します。 有効な値は、空白のパスワードの使用を許可する `true` および空白のパスワードの使用を禁止する `false` です。 このプロパティは、<xref:System.Data.Common.DBDataPermissionAttribute> から継承されています。|  
|`ConnectionString`|使用できる接続文字列を指定します。 複数の接続文字列を指定できます。 **注:** 接続文字列でユーザー ID またはパスワードを含まれません。 このリリースでは、.NET Framework 構成ツールを使用して接続文字列制限を変更することはできません。 <br /><br /> このプロパティは、<xref:System.Data.Common.DBDataPermissionAttribute> から継承されています。|  
|`KeyRestrictions`|許可または禁止する接続文字列パラメーターを指定します。 接続文字列パラメーターが、フォームで識別される*\<パラメーター名 > =* です。 セミコロン (;) で区切って、複数のパラメーターを指定できます。 **注:** を指定しない場合`KeyRestrictions`、設定するが、`KeyRestrictionBehavior`プロパティを`AllowOnly`または`PreventUsage`、追加の接続文字列パラメーターは許可されていません。 このプロパティは、<xref:System.Data.Common.DBDataPermissionAttribute> から継承されています。|  
|`KeyRestrictionBehavior`|接続文字列パラメーターが、追加を許可された唯一の接続文字列パラメーター (`AllowOnly`) か、または追加を禁止された接続文字列パラメーター (`PreventUsage`) かを指定します。 `AllowOnly` が既定値です。 このプロパティは、<xref:System.Data.Common.DBDataPermissionAttribute> から継承されています。|  
|`TypeID`|派生クラスで実装すると、この属性の一意の識別子を取得します。 このプロパティは、<xref:System.Attribute> から継承されています。|  
|`Unrestricted`|このリソースに対する無制限のアクセス許可が宣言されているかどうかを示します。 このプロパティは、<xref:System.Security.Permissions.SecurityAttribute> から継承されています。|  
  
#### <a name="connectionstring-syntax"></a>ConnectionString の構文  
 次の例では、特定の接続文字列のみ使用できるようにするために、構成ファイルの `connectionStrings` 要素を使用する方法を示しています。 参照してください[接続文字列](../../../../docs/framework/data/adonet/connection-strings.md)について詳細を格納して、構成ファイルから接続文字列を取得します。  
  
```xml  
<connectionStrings>  
  <add name="DatabaseConnection"   
    connectionString="Data Source=(local);Initial   
    Catalog=Northwind;Integrated Security=true;" />  
</connectionStrings>  
```  
  
#### <a name="keyrestrictions-syntax"></a>KeyRestrictions の構文  
 次の例の同じ接続文字列、使用できるように、`Encrypt`と`Packet``Size`接続文字列のいずれかのオプションが他の接続文字列オプションの使用を制限します。  
  
```xml  
<connectionStrings>  
  <add name="DatabaseConnection"   
    connectionString="Data Source=(local);Initial   
    Catalog=Northwind;Integrated Security=true;"  
    KeyRestrictions="Encrypt=;Packet Size=;"  
    KeyRestrictionBehavior="AllowOnly" />  
</connectionStrings>  
```  
  
#### <a name="keyrestrictionbehavior-with-preventusage-syntax"></a>KeyRestrictionBehavior を PreventUsage に設定する場合の構文  
 上述の接続文字列の使用を許可し、`User Id`、`Password`、および `Persist Security Info` を除く他のすべての接続パラメーターを許可する例を次に示します。  
  
```xml  
<connectionStrings>  
  <add name="DatabaseConnection"   
    connectionString="Data Source=(local);Initial   
    Catalog=Northwind;Integrated Security=true;"  
    KeyRestrictions="User Id=;Password=;Persist Security Info=;"  
    KeyRestrictionBehavior="PreventUsage" />  
</connectionStrings>  
```  
  
#### <a name="keyrestrictionbehavior-with-allowonly-syntax"></a>KeyRestrictionBehavior を AllowOnly に設定する場合の構文  
 `Initial Catalog`、`Connection Timeout`、`Encrypt`、および `Packet Size` パラメーターも含まれる 2 つの接続文字列の使用を許可する例を次に示します。 その他の接続文字列パラメーターは、すべて制限されます。  
  
```xml  
<connectionStrings>  
  <add name="DatabaseConnection"   
    connectionString="Data Source=(local);Initial   
    Catalog=Northwind;Integrated Security=true;"  
    KeyRestrictions="Initial Catalog;Connection Timeout=;  
       Encrypt=;Packet Size=;"   
    KeyRestrictionBehavior="AllowOnly" />  
  
  <add name="DatabaseConnection2"   
    connectionString="Data Source=SqlServer2;Initial   
    Catalog=Northwind2;Integrated Security=true;"  
    KeyRestrictions="Initial Catalog;Connection Timeout=;  
       Encrypt=;Packet Size=;"   
    KeyRestrictionBehavior="AllowOnly" />  
</connectionStrings>  
```  
  
### <a name="enabling-partial-trust-with-a-custom-permission-set"></a>カスタム アクセス許可セットを使用した Partial Trust の有効化  
 特定のゾーンに対して <xref:System.Data.SqlClient> アクセス許可を有効にするには、システム管理者がカスタム アクセス許可セットを作成して、目的のゾーンに指定する必要があります。 `LocalIntranet` などの既定のアクセス許可セットは変更できません。 例については、含める<xref:System.Data.SqlClient>がコードのアクセス許可、<xref:System.Security.Policy.Zone>の`LocalIntranet`、システム管理者の権限セットをコピーでした`LocalIntranet`、"CustomLocalIntranet"に名前を変更、追加、<xref:System.Data.SqlClient>権限、インポートCustomLocalIntranet アクセス許可セットを使用して、 [Caspol.exe (コード アクセス セキュリティ ポリシー ツール)](../../../../docs/framework/tools/caspol-exe-code-access-security-policy-tool.md)の権限のセットを設定および`LocalIntranet_Zone`CustomLocalIntranet にします。  
  
### <a name="sample-permission-set"></a>サンプル アクセス許可セット  
 部分信頼のシナリオでの、.NET Framework Data Provider for SQL Server 用アクセス許可セットの例を次に示します。 カスタム権限セットを作成する方法については、次を参照してください。 [NIB: を構成するアクセス許可設定を使用して Caspol.exe](http://msdn.microsoft.com/library/94e2625e-21ad-4038-af36-6d1f9df40a57)です。  
  
```xml  
<PermissionSet class="System.Security.NamedPermissionSet"  
  version="1"  
  Name="CustomLocalIntranet"  
  Description="Custom permission set given to applications on  
    the local intranet">  
  
<IPermission class="System.Data.SqlClient.SqlClientPermission, System.Data, Version=2.0.0000.0, Culture=neutral, PublicKeyToken=b77a5c561934e089"  
version="1"  
AllowBlankPassword="False">  
<add ConnectionString="Data Source=(local);Integrated Security=true;"  
 KeyRestrictions="Initial Catalog=;Connection Timeout=;  
   Encrypt=;Packet Size=;"   
 KeyRestrictionBehavior="AllowOnly" />  
 </IPermission>  
</PermissionSet>  
```  
  
## <a name="verifying-adonet-code-access-using-security-permissions"></a>セキュリティ アクセス許可を使用した ADO.NET コード アクセスの検証  
 部分信頼のシナリオでは、<xref:System.Data.SqlClient.SqlClientPermissionAttribute> を指定することによって、コード内の特定のメソッドに対する CAS 特権を要求できます。 制限されたセキュリティ ポリシーによって、実際にはその特権が許可されていない場合は、そのコードを実行する前に例外がスローされます。 セキュリティ ポリシーの詳細については、次を参照してください。 [NIB: セキュリティ ポリシーの管理](http://msdn.microsoft.com/library/d754e05d-29dc-4d3a-a2c2-95eaaf1b82b9)と[NIB: セキュリティ ポリシーのベスト プラクティス](http://msdn.microsoft.com/library/d49bc4d5-efb7-4caa-a2fe-e4d3cec63c05)です。  
  
### <a name="example"></a>例  
 次のサンプルは、特定の接続文字列を必要とするコードの作成方法を示しています。 このサンプルは、<xref:System.Data.SqlClient> に対する無制限の権限を拒否する機能をシミュレートします。この機能は、実際には、システム管理者が、CAS ポリシーを使用して実装します。  
  
> [!IMPORTANT]
>  ADO.NET の CAS 権限を定義する場合、最も制限の厳しいケース (権限なし) から開始し、その後で、コードが実行する特定のタスクに必要な特定の権限を追加するというのが、適切なパターンです。 逆に、すべての権限を与えてから特定の権限を拒否してゆく方法は、安全ではありません。同じ接続文字列を表現する方法が多数あるためです。 たとえば、すべての権限を与えた後で接続文字列 "server=someserver" の使用を拒否しても、"server=someserver.mycompany.com" という接続文字列は使用可能です。 常に権限をまったく与えない状態から開始することで、権限セットのセキュリティ ホールを減らすことができます。  
  
 `SqlClient` でセキュリティ確認要求を実行する方法を、次のコードに示します。CAS の権限が適切に設定されていない場合、<xref:System.Security.SecurityException> がスローされます。 <xref:System.Security.SecurityException> の出力は、コンソール ウィンドウに表示されます。  
  
 [!code-csharp[DataWorks SqlClient.CAS#1](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SqlClient.CAS/CS/source.cs#1)]
 [!code-vb[DataWorks SqlClient.CAS#1](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SqlClient.CAS/VB/source.vb#1)]  
  
 コンソール ウィンドウに表示される出力の例を次に示します。  
  
```  
Failed, as expected: <IPermission class="System.Data.SqlClient.  
SqlClientPermission, System.Data, Version=2.0.0.0,   
  Culture=neutral, PublicKeyToken=b77a5c561934e089" version="1"  
  AllowBlankPassword="False">  
<add ConnectionString="Data Source=(local);Initial Catalog=  
  Northwind;Integrated Security=SSPI" KeyRestrictions=""  
KeyRestrictionBehavior="AllowOnly"/>  
</IPermission>  
  
Connection opened, as expected.  
Failed, as expected: Request failed.  
```  
  
## <a name="interoperability-with-unmanaged-code"></a>アンマネージ コードとの相互運用性  
 CLR の外部で実行されるコードはアンマネージ コードと呼ばれます。 したがって、CAS などのセキュリティ メカニズムをアンマネージ コードに適用することはできません。 アンマネージ コードの例としては、COM コンポーネント、ActiveX インターフェイス、Win32 API 関数があります。 アンマネージ コードを実行する場合は、アプリケーションの全体的なセキュリティが損なわれないよう特別な考慮をする必要があります。 詳細については、「[アンマネージ コードとの相互運用](../../../../docs/framework/interop/index.md)」を参照してください。  
  
 .NET Framework は、COM 相互運用機能を介したアクセスを提供することによって、既存の COM コンポーネントとの下位互換性をサポートしています。 COM 相互運用ツールを使って適切な COM 型をインポートすることにより、.NET Framework アプリケーションに COM コンポーネントを組み込むことができます。 インポートが完了すると、COM 型を使用できるようになります。 アセンブリのメタデータをタイプ ライブラリにエクスポートし、マネージ コンポーネントを COM コンポーネントとして登録することで、COM クライアントからマネージ コードにアクセスすることもできます。 詳細については、次を参照してください。[高度な COM 相互運用性](http://msdn.microsoft.com/library/3ada36e5-2390-4d70-b490-6ad8de92f2fb)です。  
  
## <a name="see-also"></a>関連項目  
 [ADO.NET アプリケーションのセキュリティ保護](../../../../docs/framework/data/adonet/securing-ado-net-applications.md)  
 [ネイティブ コードと .NET Framework コードのセキュリティ](http://msdn.microsoft.com/library/bd61be84-c143-409a-a75a-44253724f784)  
 [コード アクセス セキュリティ](http://msdn.microsoft.com/library/23a20143-241d-4fe5-9d9f-3933fd594c03)  
 [ロール ベースのセキュリティ](http://msdn.microsoft.com/library/239442e3-5be4-4203-b7fd-793baffea803)  
 [ADO.NET のマネージ プロバイダーと DataSet デベロッパー センター](http://go.microsoft.com/fwlink/?LinkId=217917)
