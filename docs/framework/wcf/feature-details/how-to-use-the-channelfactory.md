---
title: '方法 : ChannelFactory を使用する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: d48f01b5-582b-4c8b-b547-8adddae7e371
ms.openlocfilehash: b407c76c86c7b4c988da5280d76c91969c155841
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/04/2018
---
# <a name="how-to-use-the-channelfactory"></a>方法 : ChannelFactory を使用する
<xref:System.ServiceModel.ChannelFactory%601> ジェネリック クラスは、複数チャネルの作成に使用できるチャネル ファクトリの作成を必要とする高度なシナリオで使用します。  
  
### <a name="to-create-and-use-the-channelfactory-class"></a>ChannelFactory クラスの作成方法と使用方法  
  
1.  ビルドして、Windows Communication Foundation (WCF) サービスを実行します。 詳細については、次を参照してください。 [Services の実装を設計および](../../../../docs/framework/wcf/designing-and-implementing-services.md)、[サービスを構成する](../../../../docs/framework/wcf/configuring-services.md)、および[ホスティング サービス](../../../../docs/framework/wcf/hosting-services.md)です。  
  
2.  使用して、 [ServiceModel メタデータ ユーティリティ ツール (Svcutil.exe)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md)をクライアントのコントラクト (インターフェイス) を生成します。  
  
3.  クライアント コード内で、<xref:System.ServiceModel.ChannelFactory%601> クラスを使用して複数のエンドポイント リスナーを作成します。  
  
## <a name="example"></a>例  
 [!code-csharp[c_HowToUseChannelFactory#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howtousechannelfactory/cs/source.cs#1)]
 [!code-vb[c_HowToUseChannelFactory#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howtousechannelfactory/vb/source.vb#1)]
