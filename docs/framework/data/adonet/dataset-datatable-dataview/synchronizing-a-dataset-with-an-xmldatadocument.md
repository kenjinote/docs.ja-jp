---
title: DataSet と XmlDataDocument の同期
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: fbc96fa9-b5d1-4f97-b099-c89b0e14ce2c
ms.openlocfilehash: d026a425f7a38777fcb5bbb4b18816c39a99aa72
ms.sourcegitcommit: 11f11ca6cefe555972b3a5c99729d1a7523d8f50
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/03/2018
---
# <a name="synchronizing-a-dataset-with-an-xmldatadocument"></a>DataSet と XmlDataDocument の同期
このセクションでは、<xref:System.Data.DataSet> と同期され、厳密に型指定された <xref:System.Xml.XmlDataDocument> を使用して、注文書を処理する手順の 1 ステップを例に説明します。 次の例を作成、**データセット**ソース XML ドキュメントの一部だけに一致する最小限のスキーマとします。 例を使用して、 **XmlDataDocument**ソース XML ドキュメントの忠実性を保持するために有効にすると、**データセット**を使用して XML ドキュメントのサブセットを公開します。  
  
 注文書に関する情報 (顧客情報、発注品目、出荷情報など) をすべて含む XML ドキュメントの例を次に示します。  
  
```xml  
<?xml version="1.0" standalone="yes"?>  
<PurchaseOrder>  
  <Customers>  
    <CustomerID>CHOPS</CustomerID>  
    <Orders>  
      <OrderID>10966</OrderID>  
      <OrderDetails>  
        <OrderID>10966</OrderID>  
        <ProductID>37</ProductID>  
        <UnitPrice>26</UnitPrice>  
        <Quantity>8</Quantity>  
        <Discount>0</Discount>  
      </OrderDetails>  
      <OrderDetails>  
        <OrderID>10966</OrderID>  
        <ProductID>56</ProductID>  
        <UnitPrice>38</UnitPrice>  
        <Quantity>12</Quantity>  
        <Discount>0.15</Discount>  
      </OrderDetails>  
      <OrderDetails>  
        <OrderID>10966</OrderID>  
        <ProductID>62</ProductID>  
        <UnitPrice>49.3</UnitPrice>  
        <Quantity>12</Quantity>  
        <Discount>0.15</Discount>  
      </OrderDetails>  
      <CustomerID>CHOPS</CustomerID>  
      <EmployeeID>4</EmployeeID>  
      <OrderDate>1998-03-20T00:00:00.0000000</OrderDate>  
      <RequiredDate>1998-04-17T00:00:00.0000000</RequiredDate>  
      <ShippedDate>1998-04-08T00:00:00.0000000</ShippedDate>  
      <ShipVia>1</ShipVia>  
      <Freight>27.19</Freight>  
      <ShipName>Chop-suey Chinese</ShipName>  
      <ShipAddress>Hauptstr. 31</ShipAddress>  
      <ShipCity>Bern</ShipCity>  
      <ShipPostalCode>3012</ShipPostalCode>  
      <ShipCountry>Switzerland</ShipCountry>  
    </Orders>  
    <CompanyName>Chop-suey Chinese</CompanyName>  
    <ContactName>Yang Wang</ContactName>  
    <ContactTitle>Owner</ContactTitle>  
    <Address>Hauptstr. 29</Address>  
    <City>Bern</City>  
    <PostalCode>3012</PostalCode>  
    <Country>Switzerland</Country>  
    <Phone>0452-076545</Phone>  
  </Customers>  
  <Shippers>  
    <ShipperID>1</ShipperID>  
    <CompanyName>Speedy Express</CompanyName>  
    <Phone>(503) 555-0100</Phone>  
  </Shippers>  
  <Shippers>  
    <ShipperID>2</ShipperID>  
    <CompanyName>United Package</CompanyName>  
    <Phone>(503) 555-0101</Phone>  
  </Shippers>  
  <Shippers>  
    <ShipperID>3</ShipperID>  
    <CompanyName>Federal Shipping</CompanyName>  
    <Phone>(503) 555-0102</Phone>  
  </Shippers>  
  <Products>  
    <ProductID>37</ProductID>  
    <ProductName>Gravad lax</ProductName>  
    <QuantityPerUnit>12 - 500 g pkgs.</QuantityPerUnit>  
    <UnitsInStock>11</UnitsInStock>  
    <UnitsOnOrder>50</UnitsOnOrder>  
    <ReorderLevel>25</ReorderLevel>  
  </Products>  
  <Products>  
    <ProductID>56</ProductID>  
    <ProductName>Gnocchi di nonna Alice</ProductName>  
    <QuantityPerUnit>24 - 250 g pkgs.</QuantityPerUnit>  
    <UnitsInStock>21</UnitsInStock>  
    <UnitsOnOrder>10</UnitsOnOrder>  
    <ReorderLevel>30</ReorderLevel>  
  </Products>  
  <Products>  
    <ProductID>62</ProductID>  
    <ProductName>Tarte au sucre</ProductName>  
    <QuantityPerUnit>48 pies</QuantityPerUnit>  
    <UnitsInStock>17</UnitsInStock>  
    <UnitsOnOrder>0</UnitsOnOrder>  
    <ReorderLevel>0</ReorderLevel>  
  </Products>  
</PurchaseOrder>  
```  
  
 前述の XML ドキュメントに含まれている注文書の情報を処理する手順の 1 ステップとして、企業の現在の在庫のデータを使用してこの注文書が処理されます。 企業の倉庫で注文を処理する従業員は、注文書の内容をすべて確認する必要はありません。確認する必要がある情報は、注文書の製品情報だけです。 XML ドキュメントから製品情報のみを公開するには、厳密に型指定された作成**データセット**スキーマを持つ順序付けに製品と数量をマップする XML スキーマ定義言語 (XSD) スキーマとして記述します。 詳細については厳密に型指定された**データセット**、オブジェクトを参照してください[型指定されたデータセット](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/typed-datasets.md)です。  
  
 次のコードは、元のスキーマを示しています。 厳密に型指定**データセット**このサンプルの生成。  
  
```xml  
<?xml version="1.0" standalone="yes"?>  
<xs:schema id="OrderDetail" xmlns=""   
                            xmlns:xs="http://www.w3.org/2001/XMLSchema"   
                            xmlns:codegen="urn:schemas-microsoft-com:xml-msprop"   
                            xmlns:msdata="urn:schemas-microsoft-com:xml-msdata">  
  <xs:element name="OrderDetail" msdata:IsDataSet="true">  
    <xs:complexType>  
      <xs:choice maxOccurs="unbounded">  
        <xs:element name="OrderDetails" codegen:typedName="LineItem" codegen:typedPlural="LineItems">  
          <xs:complexType>  
            <xs:sequence>  
              <xs:element name="OrderID" type="xs:int" minOccurs="0" codegen:typedName="OrderID"/>  
              <xs:element name="Quantity" type="xs:short" minOccurs="0" codegen:typedName="Quantity"/>  
              <xs:element name="ProductID" type="xs:int" minOccurs="0" codegen:typedName="ProductID"/>  
            </xs:sequence>  
          </xs:complexType>  
        </xs:element>  
        <xs:element name="Products" codegen:typedName="Product" codegen:typedPlural="Products">  
          <xs:complexType>  
            <xs:sequence>  
              <xs:element name="ProductID" type="xs:int" minOccurs="0" codegen:typedName="ProductID"/>  
              <xs:element name="ProductName" type="xs:string" minOccurs="0" codegen:typedName="ProductName"/>  
              <xs:element name="QuantityPerUnit" type="xs:string" minOccurs="0" codegen:typedName="QuantityPerUnit"/>  
              <xs:element name="UnitsInStock" type="xs:short" minOccurs="0" codegen:typedName="UnitsInStock"/>  
              <xs:element name="UnitsOnOrder" type="xs:short" minOccurs="0" codegen:typedName="UnitsOnOrder"/>  
              <xs:element name="ReorderLevel" type="xs:short" minOccurs="0" codegen:typedName="ReorderLevel"/>  
            </xs:sequence>  
          </xs:complexType>  
        </xs:element>  
      </xs:choice>  
    </xs:complexType>  
    <xs:unique name="Constraint1">  
      <xs:selector xpath=".//Products" />  
      <xs:field xpath="ProductID" />  
    </xs:unique>  
    <xs:keyref name="Relation1" refer="Constraint1" codegen:typedChildren="GetLineItems" codegen:typedParent="Product">  
      <xs:selector xpath=".//OrderDetails" />  
      <xs:field xpath="ProductID" />  
    </xs:keyref>  
  </xs:element>  
</xs:schema>  
```  
  
 その唯一の情報に注意してください、 **OrderDetails**と**製品**のスキーマで、元の XML ドキュメントの要素が含まれている、**データセット**です。 同期、**データセット**で、 **XmlDataDocument**に含まれていない要素により、**データセット**XML ドキュメントに保持されます。  
  
 厳密に型指定と**データセット**XML スキーマから生成された (の名前空間を持つ**Northwind.FillOrder**)、同期することによって、元の XML ドキュメントの一部を公開することができます、 **データセット**で、 **XmlDataDocument**ソース XML ドキュメントから読み込まれます。 注意して、**データセット**から生成されたスキーマには、構造体がないデータが含まれています。 XML を読み込むときに、データが入力、 **XmlDataDocument**です。 読み込もうとした場合、 **XmlDataDocument**と同期されている、**データセット**データが含まれている、例外がスローされます。  
  
 後に、**データセット**(および**XmlDataDocument**) が更新された、 **XmlDataDocument**書き出すことができますし、変更された XML ドキュメントによって無視された要素で、**データセット**そのまま次のようにします。 注文書の処理手順では、注文品目の入力後に、変更された XML ドキュメントが注文処理の次のステップ (社内の出荷部門) に渡されます。  
  
```vb  
Imports System  
Imports System.Data  
Imports System.Xml  
Imports Northwind.FillOrder  
  
Public class Sample  
  Public Shared Sub Main()  
  
    Dim orderDS As OrderDetail = New OrderDetail  
  
    Dim xmlDocument As XmlDataDocument = New XmlDataDocument(orderDS)   
  
    xmlDocument.Load("Order.xml")  
  
    Dim orderItem As OrderDetail.LineItem  
    Dim product As OrderDetail.Product  
  
    For Each orderItem In orderDS.LineItems  
      product = orderItem.Product  
  
      ' Remove quantity from the current stock.  
      product.UnitsInStock = CType(product.UnitsInStock - orderItem.Quantity, Short)  
  
      ' If the remaining stock is less than the reorder level, order more.  
      If ((product.UnitsInStock + product.UnitsOnOrder) < product.ReorderLevel) Then  
        product.UnitsOnOrder = CType(product.UnitsOnOrder + product.ReorderLevel, Short)  
      End If  
    Next  
  
    xmlDocument.Save("Order_out.xml")  
  End Sub  
End Class  
```  
  
```csharp  
using System;  
using System.Data;  
using System.Xml;  
using Northwind.FillOrder;  
  
public class Sample  
{  
  public static void Main()  
  {  
    OrderDetail orderDS = new OrderDetail();   
  
    XmlDataDocument xmlDocument = new XmlDataDocument(orderDS);   
  
    xmlDocument.Load("Order.xml");  
  
    foreach (OrderDetail.LineItem orderItem in orderDS.LineItems)  
    {  
      OrderDetail.Product product = orderItem.Product;  
  
      // Remove quantity from the current stock.  
      product.UnitsInStock = (short)(product.UnitsInStock - orderItem.Quantity);  
  
      // If the remaining stock is less than the reorder level, order more.  
      if ((product.UnitsInStock + product.UnitsOnOrder) < product.ReorderLevel)  
        product.UnitsOnOrder = (short)(product.UnitsOnOrder + product.ReorderLevel);  
    }  
  
    xmlDocument.Save("Order_out.xml");  
  }  
}  
```  
  
## <a name="see-also"></a>関連項目  
 [DataSet と XmlDataDocument の同期](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/dataset-and-xmldatadocument-synchronization.md)  
 [ADO.NET のマネージ プロバイダーと DataSet デベロッパー センター](http://go.microsoft.com/fwlink/?LinkId=217917)
