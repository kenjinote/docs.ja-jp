---
title: XslTransform への XmlDocument の入力
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
ms.assetid: 97115892-410a-4657-ab47-1e14dfba73f8
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 3179425597173e09a8c1ef1fbdfc582f8f4538e7
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/04/2018
---
# <a name="xmldocument-input-to-xsltransform"></a>XslTransform への XmlDocument の入力
<xref:System.Xml.XmlDocument> クラスは、XML ドキュメントの編集機能を持っています。 XML を <xref:System.Xml.Xsl.XslTransform.Transform%2A> メソッドに送信する前に編集または変更する必要がある場合は、XML を <xref:System.Xml.XmlDocument> に読み込み、編集し、<xref:System.Xml.Xsl.XslTransform> に送信します。  
  
> [!NOTE]
>  <xref:System.Xml.Xsl.XslTransform> では、[!INCLUDE[dnprdnext](../../../../includes/dnprdnext-md.md)] クラスが廃止されています。 <xref:System.Xml.Xsl.XslCompiledTransform> クラスを使用して XSLT (Extensible Stylesheet Language for Transformations) 変換を実行できます。 詳しくは、「[XslCompiledTransform クラスの使用](../../../../docs/standard/data/xml/using-the-xslcompiledtransform-class.md)」および「[XslTransform クラスからの移行](../../../../docs/standard/data/xml/migrating-from-the-xsltransform-class.md)」をご覧ください。  
  
 <xref:System.Xml.XmlDocument> は <xref:System.Xml.XPath.IXPathNavigable> インターフェイスを実装しているため、ドキュメントを編集した後で <xref:System.Xml.Xsl.XslTransform.Transform%2A> メソッドに渡すことができます。  
  
 <xref:System.Xml.XmlDocument> は編集機能を持っているのに対して、<xref:System.Xml.XmlDocument> は内部ストレージを利用して XPath (XML Path Language) クエリに最適化されているため、<xref:System.Xml.XPath.XPathDocument> クラスを変換への入力として使用する方法は、<xref:System.Xml.XPath.XPathDocument> を XSLT (Extensible Stylesheet Language for Transformations) 変換に使用する方法より動作が遅くなります。  
  
## <a name="example"></a>例  
 <xref:System.Xml.XmlDocument> を <xref:System.Xml.Xsl.XslTransform> に渡し、出力を <xref:System.Xml.XmlReader> に送信するコード サンプルを次に示します。  
  
```vb  
Dim doc as XmlDocument = new XmlDocument()  
doc.Load("books.xml")  
Dim trans As XslTransform = new XslTransform()  
trans.Load("book.xsl")  
Dim rdr As XmlReader = trans.Transform(doc, Nothing, Nothing)  
while (rdr.Read())  
end while  
```  
  
```csharp  
XmlDocument doc = new XmlDocument();  
doc.Load("books.xml");  
XslTransform trans = new XslTransform();  
trans.Load("book.xsl");  
XmlReader rdr = trans.Transform(doc, null, null);  
while (rdr.Read()) {}  
```  
  
## <a name="see-also"></a>参照  
 <xref:System.Xml.XmlDocument>  
 [XslTransform クラスを使用した XSLT 変換](../../../../docs/standard/data/xml/xslt-transformations-with-the-xsltransform-class.md)  
 [XslTransform クラスによる XSLT プロセッサの実装](../../../../docs/standard/data/xml/xsltransform-class-implements-the-xslt-processor.md)  
 [変換における XPathNavigator](../../../../docs/standard/data/xml/xpathnavigator-in-transformations.md)  
 [変換における XPathNodeIterator](../../../../docs/standard/data/xml/xpathnodeiterator-in-transformations.md)  
 [XslTransform への XPathDocument の入力](../../../../docs/standard/data/xml/xpathdocument-input-to-xsltransform.md)  
 [XslTransform への XmlDataDocument の入力](../../../../docs/standard/data/xml/xmldatadocument-input-to-xsltransform.md)
