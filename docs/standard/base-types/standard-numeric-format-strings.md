---
title: "標準の数値書式指定文字列 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "書式指定子, 数値"
  - "書式指定子, 標準の数値書式指定文字列"
  - "書式指定文字列"
  - "書式指定 [.NET Framework], 数"
  - "書式指定 (数値の) [.NET Framework]"
  - "数値 [.NET Framework], 書式指定"
  - "数値書式指定文字列 [.NET Framework]"
  - "標準の書式指定文字列, 数値"
  - "標準の数値書式指定文字列"
ms.assetid: 580e57eb-ac47-4ffd-bccd-3a1637c2f467
caps.latest.revision: 99
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 95
---
# 標準の数値書式指定文字列
一般的な数値型を書式設定するには、標準の数値書式指定文字列を使用します。 標準の数値書式指定文字列の形式は `Axx` です。  
  
-   `A` は *書式指定子* です。これは 1 文字の英文字です。 空白を含む複数の英文字で構成される数値書式指定文字列は、カスタム数値書式指定文字列として解釈されます。 詳細については、「[カスタム数値書式指定文字列](../../../docs/standard/base-types/custom-numeric-format-strings.md)」を参照してください。  
  
-   `xx` は *精度指定子* です。これは省略可能な整数値です。 精度指定子は 0 ～ 99 の範囲で指定され、結果の桁数に影響します。 精度指定子は、文字列形式の数値の桁数を制御することに注意してください。 精度指定子では、数値を丸めません。 丸め操作を実行するには、<xref:System.Math.Ceiling%2A?displayProperty=fullName>、<xref:System.Math.Floor%2A?displayProperty=fullName>、または <xref:System.Math.Round%2A?displayProperty=fullName> の各メソッドを使用します。  
  
     *精度指定子*が結果文字列内の小数部の桁数を制御する際、結果文字列は、ゼロから離れる方向に丸められる数を反映します \(つまり、<xref:System.MidpointRounding?displayProperty=fullName> を使用します\)。  
  
 標準の数値書式指定文字列は、すべての数値型の `ToString` メソッドの一部のオーバーロードでサポートされています。 たとえば、<xref:System.Int32.ToString%28System.String%29> 型の <xref:System.Int32.ToString%28System.String%2CSystem.IFormatProvider%29> メソッドおよび <xref:System.Int32> メソッドに数値書式指定文字列を指定できます。 標準の数値書式指定文字列は、.NET Framework の[複合書式指定機能](../../../docs/standard/base-types/composite-formatting.md)でもサポートされています。この機能を使用するメソッドには、`Write` クラスおよび `WriteLine` クラスの一部の <xref:System.Console> メソッドと <xref:System.IO.StreamWriter> メソッド、<xref:System.String.Format%2A?displayProperty=fullName> メソッド、および <xref:System.Text.StringBuilder.AppendFormat%2A?displayProperty=fullName> メソッドがあります。 複合書式指定機能により、複数のデータ項目の文字列表現を 1 つの文字列にまとめ、フィールド幅を指定し、フィールドの数値の位置を揃えることができます。 詳細については、「[複合書式指定](../../../docs/standard/base-types/composite-formatting.md)」を参照してください。  
  
> [!TIP]
>  [書式指定ユーティリティ](http://code.msdn.microsoft.com/NET-Framework-4-Formatting-9c4dae8d)をダウンロードできます。このアプリケーションを使用すると、書式指定文字列を数値または日付と時刻の値に適用して、結果の文字列を表示できます。  
  
<a name="table"></a> 次の表に、標準数値書式指定子の説明および書式指定子ごとのサンプル出力を示します。 標準の数値書式指定文字列の使用方法については、「[メモ](#NotesStandardFormatting)」を参照してください。それらを使用する包括的な例については、「[例](#example)」を参照してください。  
  
|書式指定子|名前|説明|例|  
|-----------|--------|--------|-------|  
|"C" または "c"|通貨|結果: 通貨値。<br /><br /> サポート: すべての数値型。<br /><br /> 精度指定子: 小数部の桁数。<br /><br /> 既定の精度指定子: <xref:System.Globalization.NumberFormatInfo.CurrencyDecimalDigits%2A?displayProperty=fullName> によって定義されます。<br /><br /> 詳細については、「[通貨 \("C"\) 書式指定子](#CFormatString)」を参照してください。|123.456 \("C", en\-US\) \-\> $123.46<br /><br /> 123.456 \("C", fr\-FR\) \-\> 123,46 €<br /><br /> 123.456 \("C", ja\-JP\) \-\> ¥123<br /><br /> \-123.456 \("C3", en\-US\) \-\> \($123.456\)<br /><br /> \-123.456 \("C3", fr\-FR\) \-\> \-123,456 €<br /><br /> \-123.456 \("C3", ja\-JP\) \-\> \-¥123.456|  
|"D" または "d"|Decimal \(10 進数型\)|結果: 必要に応じて負の符号が付く整数。<br /><br /> サポート: 整数型のみ。<br /><br /> 精度指定子: 最小桁数。<br /><br /> 既定の精度指定子: 必要な最小桁数。<br /><br /> 詳細については、「[10 進数 \("D"\) 書式指定子](#DFormatString)」を参照してください。|1234 \("D"\) \-\> 1234<br /><br /> \-1234 \("D6"\) \-\> \-001234|  
|"E" または "e"|指数|結果: 指数表記。<br /><br /> サポート: すべての数値型。<br /><br /> 精度指定子: 小数部の桁数。<br /><br /> 既定の精度指定子: 6。<br /><br /> 詳細については、「[指数 \("E"\) 書式指定子](#EFormatString)」を参照してください。|1052.0329112756 \("E", en\-US\) \-\> 1.052033E\+003<br /><br /> 1052.0329112756 \("e", fr\-FR\) \-\> 1,052033e\+003<br /><br /> \-1052.0329112756 \("e2", en\-US\) \-\> \-1.05e\+003<br /><br /> \-1052.0329112756 \("E2", fr\_FR\) \-\> \-1,05E\+003|  
|"F" または "f"|固定小数点|結果: 必要に応じて負の符号が付く整数と小数。<br /><br /> サポート: すべての数値型。<br /><br /> 精度指定子: 小数部の桁数。<br /><br /> 既定の精度指定子: <xref:System.Globalization.NumberFormatInfo.NumberDecimalDigits%2A?displayProperty=fullName> によって定義されます。<br /><br /> 詳細については、「[固定小数点 \("F"\) 書式指定子](#FFormatString)」を参照してください。|1234.567 \("F", en\-US\) \-\> 1234.57<br /><br /> 1234.567 \("F", de\-DE\) \-\> 1234,57<br /><br /> 1234 \("F1", en\-US\) \-\> 1234.0<br /><br /> 1234 \("F1", de\-DE\) \-\> 1234,0<br /><br /> \-1234.56 \("F4", en\-US\) \-\> \-1234.5600<br /><br /> \-1234.56 \("F4", de\-DE\) \-\> \-1234,5600|  
|"G" または "g"|全般|結果: 固定小数点表記または指数表記のいずれかの最も簡潔な形式。<br /><br /> サポート: すべての数値型。<br /><br /> 精度指定子: 有効桁数。<br /><br /> 既定の精度指定子: 数値型によって異なります。<br /><br /> 詳細については、「[一般 \("G"\) 書式指定子](#GFormatString)」を参照してください。|\-123.456 \("G", en\-US\) \-\> \-123.456<br /><br /> \-123.456 \("G", sv\-SE\) \-\> \-123,456<br /><br /> 123.4546 \("G4", en\-US\) \-\> 123.5<br /><br /> 123.4546 \("G4", sv\-SE\) \-\> 123,5<br /><br /> \-1.234567890e\-25 \("G", en\-US\) \-\> \-1.23456789E\-25<br /><br /> \-1.234567890e\-25 \("G", sv\-SE\) \-\> \-1,23456789E\-25|  
|"N" または "n"|Number|結果: 必要に応じて負の符号が付く整数と小数、桁区切り記号、および小数点記号。<br /><br /> サポート: すべての数値型。<br /><br /> 精度指定子: 小数部の桁数。<br /><br /> 既定の精度指定子: <xref:System.Globalization.NumberFormatInfo.NumberDecimalDigits%2A?displayProperty=fullName> によって定義されます。<br /><br /> 詳細については、「[数値 \("N"\) 書式指定子](#NFormatString)」を参照してください。|1234.567 \("N", en\-US\) \-\> 1,234.57<br /><br /> 1234.567 \("N", ru\-RU\) \-\> 1 234,57<br /><br /> 1234 \("N1", en\-US\) \-\> 1,234.0<br /><br /> 1234 \("N1", ru\-RU\) \-\> 1 234,0<br /><br /> \-1234.56 \("N3", en\-US\) \-\> \-1,234.560<br /><br /> \-1234.56 \("N3", ru\-RU\) \-\> \-1 234,560|  
|"P" または "p"|パーセント|結果: 数値に 100 を掛けて、パーセント記号を付けて表示します。<br /><br /> サポート: すべての数値型。<br /><br /> 精度指定子: 小数部の桁数。<br /><br /> 既定の精度指定子: <xref:System.Globalization.NumberFormatInfo.PercentDecimalDigits%2A?displayProperty=fullName> によって定義されます。<br /><br /> 詳細については、「[パーセント \("P"\) 書式指定子](#PFormatString)」を参照してください。|1 \("P", en\-US\) \-\> 100.00 %<br /><br /> 1 \("P", fr\-FR\) \-\> 100,00 %<br /><br /> \-0.39678 \("P1", en\-US\) \-\> \-39.7 %<br /><br /> \-0.39678 \("P1", fr\-FR\) \-\> \-39,7 %|  
|"R" または "r"|ラウンドトリップ|結果: 同じ数値にラウンドトリップできる文字列。<br /><br /> サポート: <xref:System.Single>、<xref:System.Double>、および <xref:System.Numerics.BigInteger>。<br /><br /> 精度指定子: 無視されます。<br /><br /> 詳細については、「[ラウンドトリップ \("R"\) 書式指定子](#RFormatString)」を参照してください。|123456789.12345678 \("R"\) \-\> 123456789.12345678<br /><br /> \-1234567890.12345678 \("R"\) \-\> \-1234567890.1234567|  
|"X" または "x"|16 進数|結果: 16 進数文字列。<br /><br /> サポート: 整数型のみ。<br /><br /> 精度指定子: 結果文字列の桁数。<br /><br /> 詳細については、「[16 進数 \("X"\) 書式指定子](#XFormatString)」を参照してください。|255 \("X"\) \-\> FF<br /><br /> \-1 \("x"\) \-\> ff<br /><br /> 255 \("x4"\) \-\> 00ff<br /><br /> \-1 \("X4"\) \-\> 00FF|  
|その他の 1 文字|未定義の指定子|結果: 実行時に <xref:System.FormatException> をスローします。||  
  
<a name="Using"></a>   
## 標準の数値書式指定文字列の使用  
 標準の数値書式指定文字列を使用すると、次のいずれかの方法で数値の書式を定義できます。  
  
-   `ToString` パラメーターを持つ `format` メソッドのオーバーロードに渡す。 次の例では、数値の書式を現在のカルチャ \(ここでは en\-US\) の通貨文字列に設定しています。  
  
     [!code-cpp[Formatting.Numeric.Standard#10](../../../samples/snippets/cpp/VS_Snippets_CLR/Formatting.Numeric.Standard/cpp/standardusage1.cpp#10)]
     [!code-csharp[Formatting.Numeric.Standard#10](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.Numeric.Standard/cs/standardusage1.cs#10)]
     [!code-vb[Formatting.Numeric.Standard#10](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.Numeric.Standard/vb/standardusage1.vb#10)]  
  
-   <xref:System.String.Format%2A?displayProperty=fullName>、<xref:System.Console.WriteLine%2A?displayProperty=fullName>、<xref:System.Text.StringBuilder.AppendFormat%2A?displayProperty=fullName> などのメソッドで使用される書式指定項目の `formatString` 引数として渡す。 詳細については、「[複合書式指定](../../../docs/standard/base-types/composite-formatting.md)」を参照してください。 次の例では、書式指定項目を使用して文字列に通貨値を挿入しています。  
  
     [!code-cpp[Formatting.Numeric.Standard#11](../../../samples/snippets/cpp/VS_Snippets_CLR/Formatting.Numeric.Standard/cpp/standardusage1.cpp#11)]
     [!code-csharp[Formatting.Numeric.Standard#11](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.Numeric.Standard/cs/standardusage1.cs#11)]
     [!code-vb[Formatting.Numeric.Standard#11](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.Numeric.Standard/vb/standardusage1.vb#11)]  
  
     オプションで、`alignment` 引数を渡して数値フィールドの幅と、その値を右揃えまたは左揃えにするかどうかを指定します。 次の例では、通貨の値が 28 文字フィールドでは左揃えになっており、14 文字フィールドでは右揃えになっています。  
  
     [!code-cpp[Formatting.Numeric.Standard#12](../../../samples/snippets/cpp/VS_Snippets_CLR/Formatting.Numeric.Standard/cpp/standardusage1.cpp#12)]
     [!code-csharp[Formatting.Numeric.Standard#12](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.Numeric.Standard/cs/standardusage1.cs#12)]
     [!code-vb[Formatting.Numeric.Standard#12](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.Numeric.Standard/vb/standardusage1.vb#12)]  
  
 以降では、それぞれの標準の数値書式指定文字列について詳しく説明します。  
  
<a name="CFormatString"></a>   
## 通貨 \("C"\) 書式指定子  
 "C" \(通貨\) 書式指定子は、金額を表す文字列に数値を変換します。 精度指定子は、結果文字列の小数部の桁数を示します。 精度指定子を省略すると、<xref:System.Globalization.NumberFormatInfo.CurrencyDecimalDigits%2A?displayProperty=fullName> プロパティによって既定の桁数が定義されます。  
  
 書式指定される値が指定または既定の小数部の桁数を超えている場合、小数値は結果文字列で丸められます。 指定した小数部の桁数の右側にある値が 5 以上の場合、結果文字列の最後の桁はゼロから離れる方向に丸められます。  
  
 結果文字列は、現在の <xref:System.Globalization.NumberFormatInfo> オブジェクトの書式情報に影響されます。 返される文字列の書式を制御する <xref:System.Globalization.NumberFormatInfo> のプロパティの一覧を次の表に示します。  
  
|NumberFormatInfo のプロパティ|説明|  
|-----------------------------|--------|  
|<xref:System.Globalization.NumberFormatInfo.CurrencyPositivePattern%2A>|正の値の通貨記号の位置を定義します。|  
|<xref:System.Globalization.NumberFormatInfo.CurrencyNegativePattern%2A>|負の値の通貨記号の位置を定義し、かっこと <xref:System.Globalization.NumberFormatInfo.NegativeSign%2A> プロパティのどちらによって負の符号が表されるかを指定します。|  
|<xref:System.Globalization.NumberFormatInfo.NegativeSign%2A>|<xref:System.Globalization.NumberFormatInfo.CurrencyNegativePattern%2A> でかっこを使用しないように示されている場合に使用される負の符号を定義します。|  
|<xref:System.Globalization.NumberFormatInfo.CurrencySymbol%2A>|通貨記号を定義します。|  
|<xref:System.Globalization.NumberFormatInfo.CurrencyDecimalDigits%2A>|通貨値の既定の小数点以下桁数を定義します。 この値は、精度指定子を使用してオーバーライドできます。|  
|<xref:System.Globalization.NumberFormatInfo.CurrencyDecimalSeparator%2A>|整数部と小数部を区切る文字列を定義します。|  
|<xref:System.Globalization.NumberFormatInfo.CurrencyGroupSeparator%2A>|整数の桁を区切る文字列を定義します。|  
|<xref:System.Globalization.NumberFormatInfo.CurrencyGroupSizes%2A>|桁を何桁ごとに区切るかを定義します。|  
  
 次の例では、通貨書式指定子を使って <xref:System.Double> 値の書式を設定します。  
  
 [!code-cpp[Formatting.Numeric.Standard#1](../../../samples/snippets/cpp/VS_Snippets_CLR/Formatting.Numeric.Standard/cpp/Standard.cpp#1)]
 [!code-csharp[Formatting.Numeric.Standard#1](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.Numeric.Standard/cs/Standard.cs#1)]
 [!code-vb[Formatting.Numeric.Standard#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.Numeric.Standard/vb/Standard.vb#1)]  
  
 [表のトップへ](#table)  
  
<a name="DFormatString"></a>   
## 10 進数 \("D"\) 書式指定子  
 "D" \(10 進数\) 書式指定子は、0 ～ 9 の数字から成る文字列に数値を変換します。負の数値の場合は、文字列の先頭にマイナス記号が挿入されます。 この書式指定は整数型でだけサポートされています。  
  
 精度指定子は、変換後の文字列の最小桁数を示します。 必要に応じて、精度指定子によって指定された桁数に達するまで、数値の左側にゼロが埋め込まれます。 精度指定子が指定されていない場合の既定値は、先行するゼロを含めずに整数を表すために必要な最小値です。  
  
 結果文字列は、現在の <xref:System.Globalization.NumberFormatInfo> オブジェクトの書式情報に影響されます。 次の表に示すように、結果文字列の書式に影響を与えるプロパティは 1 つです。  
  
|NumberFormatInfo のプロパティ|説明|  
|-----------------------------|--------|  
|<xref:System.Globalization.NumberFormatInfo.NegativeSign%2A>|数値が負であることを示す文字列を定義します。|  
  
 次の例では、10 進数の書式指定子を使って <xref:System.Int32> 値の書式を設定します。  
  
 [!code-cpp[Formatting.Numeric.Standard#2](../../../samples/snippets/cpp/VS_Snippets_CLR/Formatting.Numeric.Standard/cpp/Standard.cpp#2)]
 [!code-csharp[Formatting.Numeric.Standard#2](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.Numeric.Standard/cs/Standard.cs#2)]
 [!code-vb[Formatting.Numeric.Standard#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.Numeric.Standard/vb/Standard.vb#2)]  
  
 [表のトップへ](#table)  
  
<a name="EFormatString"></a>   
## 指数 \("E"\) 書式指定子  
 指数 \("E"\) 書式指定子は、"\-d.ddd…E\+ddd" または "\-d.ddd…e\+ddd" という形式の文字列に数値を変換します。この "d" は 0 ～ 9 の 1 桁の数字を示します。 負の数値の場合、変換後の文字列の先頭にマイナス記号が挿入されます。 小数点の前には 1 桁の数字が必ず示されます。  
  
 精度指定子は、小数部の桁数を示します。 精度指定子を省略すると、小数部の桁数として既定の 6 桁が使用されます。  
  
 書式指定子が大文字の場合は指数部の前に "E" が挿入され、小文字の場合は "e" が挿入されます。 指数部は常に、プラス記号またはマイナス記号のいずれかと、3 桁以上の桁で構成されます。 指数部の桁数が最小桁数の 3 桁よりも少ない場合には、3 桁になるようにゼロが埋め込まれます。  
  
 結果文字列は、現在の <xref:System.Globalization.NumberFormatInfo> オブジェクトの書式情報に影響されます。 返される文字列の書式を制御する <xref:System.Globalization.NumberFormatInfo> のプロパティの一覧を次の表に示します。  
  
|NumberFormatInfo のプロパティ|説明|  
|-----------------------------|--------|  
|<xref:System.Globalization.NumberFormatInfo.NegativeSign%2A>|係数と指数部の両方で数値が負であることを示す文字列を定義します。|  
|<xref:System.Globalization.NumberFormatInfo.NumberDecimalSeparator%2A>|係数の整数部と小数部を区切る文字列を定義します。|  
|<xref:System.Globalization.NumberFormatInfo.PositiveSign%2A>|指数部が正であることを示す文字列を定義します。|  
  
 次の例では、指数書式指定子を使って <xref:System.Double> 値の書式を設定します。  
  
 [!code-cpp[Formatting.Numeric.Standard#3](../../../samples/snippets/cpp/VS_Snippets_CLR/Formatting.Numeric.Standard/cpp/Standard.cpp#3)]
 [!code-csharp[Formatting.Numeric.Standard#3](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.Numeric.Standard/cs/Standard.cs#3)]
 [!code-vb[Formatting.Numeric.Standard#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.Numeric.Standard/vb/Standard.vb#3)]  
  
 [表のトップへ](#table)  
  
<a name="FFormatString"></a>   
## 固定小数点 \("F"\) 書式指定子  
 固定小数点 \("F\) 書式指定子は、"\-ddd.ddd…" という形式の文字列に数値を変換します。 この "d" は 0 ～ 9 の 1 桁の数字を示します。 負の数値の場合、変換後の文字列の先頭にマイナス記号が挿入されます。  
  
 精度指定子は、小数部の桁数を示します。 精度指定子を省略すると、現在の <xref:System.Globalization.NumberFormatInfo.NumberDecimalDigits%2A?displayProperty=fullName> プロパティによって桁数が指定されます。  
  
 結果文字列は、現在の <xref:System.Globalization.NumberFormatInfo> オブジェクトの書式情報に影響されます。 結果文字列の書式を制御する <xref:System.Globalization.NumberFormatInfo> オブジェクトのプロパティの一覧を次の表に示します。  
  
|NumberFormatInfo のプロパティ|説明|  
|-----------------------------|--------|  
|<xref:System.Globalization.NumberFormatInfo.NegativeSign%2A>|数値が負であることを示す文字列を定義します。|  
|<xref:System.Globalization.NumberFormatInfo.NumberDecimalSeparator%2A>|整数部と小数部を区切る文字列を定義します。|  
|<xref:System.Globalization.NumberFormatInfo.NumberDecimalDigits%2A>|既定の小数点以下桁数を定義します。 この値は、精度指定子を使用してオーバーライドできます。|  
  
 次の例では、固定小数点の書式指定子を使って <xref:System.Double> および <xref:System.Int32> 値の書式を設定します。  
  
 [!code-cpp[Formatting.Numeric.Standard#4](../../../samples/snippets/cpp/VS_Snippets_CLR/Formatting.Numeric.Standard/cpp/Standard.cpp#4)]
 [!code-csharp[Formatting.Numeric.Standard#4](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.Numeric.Standard/cs/Standard.cs#4)]
 [!code-vb[Formatting.Numeric.Standard#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.Numeric.Standard/vb/Standard.vb#4)]  
  
 [表のトップへ](#table)  
  
<a name="GFormatString"></a>   
## 一般 \("G"\) 書式指定子  
 一般 \("G"\) 書式指定子は、数値の型や、精度指定子が指定されているかどうかに応じて、固定小数点表記または指数表記のいずれかの最も簡潔な形式に数値を変換します。 精度指定子は、結果文字列の有効桁数の最大値を定義します。 精度指定子が省略されている場合や、0 である場合は、次の表に示すように、数値の型によって既定の精度が決定されます。  
  
|数値型|既定の精度|  
|---------|-----------|  
|<xref:System.Byte> または <xref:System.SByte>|3 桁|  
|<xref:System.Int16> または <xref:System.UInt16>|5 桁|  
|<xref:System.Int32> または <xref:System.UInt32>|10 桁|  
|<xref:System.Int64>|19 桁|  
|<xref:System.UInt64>|20 桁|  
|<xref:System.Numerics.BigInteger>|50 桁|  
|<xref:System.Single>|7 桁|  
|<xref:System.Double>|15 桁|  
|<xref:System.Decimal>|29 桁|  
  
 数値を指数表記で表した結果の指数部が \-5 よりも大きく、精度指定子よりも小さい場合は、固定小数点表記が使用されます。それ以外の場合は、指数表記が使用されます。 結果には必要に応じて小数点が含まれ、小数点の後続のゼロは省略されます。 精度指定子が存在し、指定された精度を結果の有効桁数が超える場合は、超過した桁は丸められ削除されます。  
  
 ただし、数値が <xref:System.Decimal> で、精度指定子が省略されている場合は、常に固定小数点表記が使用され、後続のゼロは保持されます。  
  
 指数表記が使用される場合、結果の指数部には、書式指定子が "G" のときには "E"、書式指定子が "g" のときには "e" というプレフィックスが付きます。 指数部には少なくとも 2 桁が含まれます。 これは、指数部に少なくとも 3 桁が含まれる、指数書式指定子によって生成される指数表記の書式とは異なります。  
  
 結果文字列は、現在の <xref:System.Globalization.NumberFormatInfo> オブジェクトの書式情報に影響されます。 結果文字列の書式を制御する <xref:System.Globalization.NumberFormatInfo> のプロパティの一覧を次の表に示します。  
  
|NumberFormatInfo のプロパティ|説明|  
|-----------------------------|--------|  
|<xref:System.Globalization.NumberFormatInfo.NegativeSign%2A>|数値が負であることを示す文字列を定義します。|  
|<xref:System.Globalization.NumberFormatInfo.NumberDecimalSeparator%2A>|整数部と小数部を区切る文字列を定義します。|  
|<xref:System.Globalization.NumberFormatInfo.PositiveSign%2A>|指数部が正であることを示す文字列を定義します。|  
  
 次の例では、一般書式指定子を使って、さまざまな浮動小数点値の書式を設定します。  
  
 [!code-cpp[Formatting.Numeric.Standard#5](../../../samples/snippets/cpp/VS_Snippets_CLR/Formatting.Numeric.Standard/cpp/Standard.cpp#5)]
 [!code-csharp[Formatting.Numeric.Standard#5](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.Numeric.Standard/cs/Standard.cs#5)]
 [!code-vb[Formatting.Numeric.Standard#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.Numeric.Standard/vb/Standard.vb#5)]  
  
 [表のトップへ](#table)  
  
<a name="NFormatString"></a>   
## 数値 \("N"\) 書式指定子  
 "N" \(Numeric: 数値\) は、数値を "\-d,ddd,ddd.ddd…" という形式の文字列に変換する書式指定子です。"\-" は負数記号を示し \(必要な場合\)、"d" は数字 \(0 ～ 9\) を示し、"," は桁区切り記号を示し、"." は小数点記号を示します。 精度指定子は、小数部の桁数を示します。 精度指定子を省略すると、現在の <xref:System.Globalization.NumberFormatInfo.NumberDecimalDigits%2A?displayProperty=fullName> プロパティによって小数部の桁数が定義されます。  
  
 結果文字列は、現在の <xref:System.Globalization.NumberFormatInfo> オブジェクトの書式情報に影響されます。 結果文字列の書式を制御する <xref:System.Globalization.NumberFormatInfo> のプロパティの一覧を次の表に示します。  
  
|NumberFormatInfo のプロパティ|説明|  
|-----------------------------|--------|  
|<xref:System.Globalization.NumberFormatInfo.NegativeSign%2A>|数値が負であることを示す文字列を定義します。|  
|<xref:System.Globalization.NumberFormatInfo.NumberNegativePattern%2A>|負の値の書式を定義し、かっこと <xref:System.Globalization.NumberFormatInfo.NegativeSign%2A> プロパティのどちらによって負の符号が表されるかを指定します。|  
|<xref:System.Globalization.NumberFormatInfo.NumberGroupSizes%2A>|桁区切り記号の間の桁数を定義します。|  
|<xref:System.Globalization.NumberFormatInfo.NumberGroupSeparator%2A>|整数の桁を区切る文字列を定義します。|  
|<xref:System.Globalization.NumberFormatInfo.NumberDecimalSeparator%2A>|整数部と小数部を区切る文字列を定義します。|  
|<xref:System.Globalization.NumberFormatInfo.NumberDecimalDigits%2A>|既定の小数点以下桁数を定義します。 この値は、精度指定子を使用してオーバーライドできます。|  
  
 次の例では、数値書式指定子を使って、さまざまな浮動小数点値の書式を設定します。  
  
 [!code-cpp[Formatting.Numeric.Standard#6](../../../samples/snippets/cpp/VS_Snippets_CLR/Formatting.Numeric.Standard/cpp/Standard.cpp#6)]
 [!code-csharp[Formatting.Numeric.Standard#6](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.Numeric.Standard/cs/Standard.cs#6)]
 [!code-vb[Formatting.Numeric.Standard#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.Numeric.Standard/vb/Standard.vb#6)]  
  
 [表のトップへ](#table)  
  
<a name="PFormatString"></a>   
## パーセント \("P"\) 書式指定子  
 パーセント \("P"\) 書式指定子は、数値に 100 を掛けて、パーセントを表す文字列に変換します。 精度指定子は、小数部の桁数を示します。 精度指定子を省略すると、現在の <xref:System.Globalization.NumberFormatInfo.PercentDecimalDigits%2A> プロパティによって指定される既定の桁数が使用されます。  
  
 返される文字列の書式を制御する <xref:System.Globalization.NumberFormatInfo> のプロパティの一覧を次の表に示します。  
  
|NumberFormatInfo のプロパティ|説明|  
|-----------------------------|--------|  
|<xref:System.Globalization.NumberFormatInfo.PercentPositivePattern%2A>|正の値のパーセント記号の位置を定義します。|  
|<xref:System.Globalization.NumberFormatInfo.PercentNegativePattern%2A>|負の値のパーセント記号と負の符号の位置を定義します。|  
|<xref:System.Globalization.NumberFormatInfo.NegativeSign%2A>|数値が負であることを示す文字列を定義します。|  
|<xref:System.Globalization.NumberFormatInfo.PercentSymbol%2A>|パーセント記号を定義します。|  
|<xref:System.Globalization.NumberFormatInfo.PercentDecimalDigits%2A>|パーセント値の既定の小数点以下桁数を定義します。 この値は、精度指定子を使用してオーバーライドできます。|  
|<xref:System.Globalization.NumberFormatInfo.PercentDecimalSeparator%2A>|整数部と小数部を区切る文字列を定義します。|  
|<xref:System.Globalization.NumberFormatInfo.PercentGroupSeparator%2A>|整数の桁を区切る文字列を定義します。|  
|<xref:System.Globalization.NumberFormatInfo.PercentGroupSizes%2A>|桁を何桁ごとに区切るかを定義します。|  
  
 次の例では、パーセント書式指定子を使って、浮動小数点値の書式を設定します。  
  
 [!code-cpp[Formatting.Numeric.Standard#7](../../../samples/snippets/cpp/VS_Snippets_CLR/Formatting.Numeric.Standard/cpp/Standard.cpp#7)]
 [!code-csharp[Formatting.Numeric.Standard#7](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.Numeric.Standard/cs/Standard.cs#7)]
 [!code-vb[Formatting.Numeric.Standard#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.Numeric.Standard/vb/Standard.vb#7)]  
  
 [表のトップへ](#table)  
  
<a name="RFormatString"></a>   
## ラウンドトリップ \("R"\) 書式指定子  
 ラウンドトリップ \("R"\) 書式指定子は、数値の変換後の文字列が、変換前と同じ数値へ戻るように解析されること確認するために使用されます。 この書式指定は、<xref:System.Single> 型、<xref:System.Double> 型、および <xref:System.Numerics.BigInteger> 型でだけサポートされています。  
  
 この指定子を使用して <xref:System.Numerics.BigInteger> 値の書式を設定すると、その文字列形式に <xref:System.Numerics.BigInteger> 値の有効桁数がすべて含まれます。 この指定子を使用して <xref:System.Single> 値または <xref:System.Double> 値の書式を設定すると、最初に一般書式を使用して数値がテストされます。このとき、<xref:System.Double> の場合は 15 桁、<xref:System.Single> の場合は 7 桁の有効桁数が使用されます。 変換後の文字列を解析して変換前の数値へ戻った場合には、一般書式指定子を使用してこの数値の書式が設定されます。 変換後の文字列が解析によって変換前の数値に戻らなかった場合、<xref:System.Double> は 17 桁、<xref:System.Single> は 9 桁の有効桁数でこの値の形式が設定されます。  
  
 精度指定子は、指定できますが無視されます。 ラウンドトリップ指定子と精度指定子の両方を指定すると、ラウンドトリップ指定子が優先されます。  
  
 結果文字列は、現在の <xref:System.Globalization.NumberFormatInfo> オブジェクトの書式情報に影響されます。 結果文字列の書式を制御する <xref:System.Globalization.NumberFormatInfo> のプロパティの一覧を次の表に示します。  
  
|NumberFormatInfo のプロパティ|説明|  
|-----------------------------|--------|  
|<xref:System.Globalization.NumberFormatInfo.NegativeSign%2A>|数値が負であることを示す文字列を定義します。|  
|<xref:System.Globalization.NumberFormatInfo.NumberDecimalSeparator%2A>|整数部と小数部を区切る文字列を定義します。|  
|<xref:System.Globalization.NumberFormatInfo.PositiveSign%2A>|指数部が正であることを示す文字列を定義します。|  
  
 次の例では、ラウンドトリップ書式指定子を使って <xref:System.Double> 値の書式を設定します。  
  
 [!code-cpp[Formatting.Numeric.Standard#8](../../../samples/snippets/cpp/VS_Snippets_CLR/Formatting.Numeric.Standard/cpp/Standard.cpp#8)]
 [!code-csharp[Formatting.Numeric.Standard#8](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.Numeric.Standard/cs/Standard.cs#8)]
 [!code-vb[Formatting.Numeric.Standard#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.Numeric.Standard/vb/Standard.vb#8)]  
  
> [!IMPORTANT]
>  場合によっては、`/platform:x64` スイッチまたは `/platform:anycpu` スイッチを使用してコンパイルして 64 ビット システムで実行すると、"R" 標準の数値書式指定文字列で書式設定される <xref:System.Double> 値のラウンドトリップに失敗することがあります。 詳細については、次の段落を参照してください。  
  
 `/platform:x64` スイッチまたは `/platform:anycpu` スイッチを使用してコンパイルして 64 ビット システムで実行すると、「R」標準の数値書式指定文字列を使用して書式設定される <xref:System.Double> 値のラウンドトリップが失敗するという問題を回避するために、<xref:System.Double> 値を「G17」標準の数値書式指定文字列を使用して書式設定することができます。 次の例では、ラウンドトリップに失敗する <xref:System.Double> 値を持つ "R" 書式指定文字列を使用しています。元の値のラウンドトリップに成功する "G17" 書式指定文字列も使用しています。  
  
 [!code-csharp[System.Double.ToString#5](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.Double.ToString/cs/roundtripex1.cs#5)]
 [!code-vb[System.Double.ToString#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.Double.ToString/vb/roundtripex1.vb#5)]  
  
 [表のトップへ](#table)  
  
<a name="XFormatString"></a>   
## 16 進数 \("X"\) 書式指定子  
 16 進数 \("X"\) 書式指定子は、16 進数文字列に数値を変換します。 書式指定子の大文字と小文字によって、9 よりも大きい 16 進数値を示すアルファベット文字が大文字と小文字のどちらで表示されるかが決まります。 たとえば、"X" を指定すると "ABCDEF" となり、"x" を指定すると "abcdef" となります。 この書式指定は整数型でだけサポートされています。  
  
 精度指定子は、変換後の文字列の最小桁数を示します。 必要に応じて、精度指定子によって指定された桁数に達するまで、数値の左側にゼロが埋め込まれます。  
  
 結果文字列は、現在の <xref:System.Globalization.NumberFormatInfo> オブジェクトの書式情報に影響されません。  
  
 次の例では、16 進数の書式指定子を使って <xref:System.Int32> 値の書式を設定します。  
  
 [!code-cpp[Formatting.Numeric.Standard#9](../../../samples/snippets/cpp/VS_Snippets_CLR/Formatting.Numeric.Standard/cpp/Standard.cpp#9)]
 [!code-csharp[Formatting.Numeric.Standard#9](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.Numeric.Standard/cs/Standard.cs#9)]
 [!code-vb[Formatting.Numeric.Standard#9](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.Numeric.Standard/vb/Standard.vb#9)]  
  
 [表のトップへ](#table)  
  
<a name="NotesStandardFormatting"></a>   
## ノート  
  
### コントロール パネルの設定  
 コントロール パネルの **\[地域と言語のオプション\]** での設定は、書式設定操作によって生成される結果の文字列に影響します。 これらの設定は、書式設定の制御に使用される値を提供する現在のスレッド カルチャに関連付けられた <xref:System.Globalization.NumberFormatInfo> オブジェクトを初期化するために使用されます。 コンピューターで使用する設定が異なる場合は、生成される文字列も異なります。  
  
 また、<xref:System.Globalization.CultureInfo.%23ctor%28System.String%29?displayProperty=fullName> コンストラクターを使用して、現在のシステム カルチャと同じカルチャを表す新しい <xref:System.Globalization.CultureInfo> オブジェクトをインスタンス化した場合、コントロール パネルの **\[地域と言語のオプション\]** 項目で設定されたカスタマイズが新しい <xref:System.Globalization.CultureInfo> オブジェクトに適用されます。<xref:System.Globalization.CultureInfo.%23ctor%28System.String%2CSystem.Boolean%29?displayProperty=fullName> コンストラクターを使用すると、システムに対するカスタマイズが反映されない <xref:System.Globalization.CultureInfo> オブジェクトを作成できます。  
  
### NumberFormatInfo のプロパティ  
 書式設定は、現在の <xref:System.Globalization.NumberFormatInfo> オブジェクトのプロパティの影響を受けます。このオブジェクトは、現在のスレッド カルチャによって暗黙的に指定されるか、または書式設定を実行するメソッドの <xref:System.IFormatProvider> パラメーターによって明示的に指定されます。 このパラメーターには、<xref:System.Globalization.NumberFormatInfo> オブジェクトまたは <xref:System.Globalization.CultureInfo> オブジェクトを指定してください。  
  
> [!NOTE]
>  数値の書式設定に使用するパターンまたは文字列のカスタマイズの詳細については、<xref:System.Globalization.NumberFormatInfo> クラスに関するトピックを参照してください。  
  
### 整数数値型と浮動小数点数値型  
 標準の数値書式指定子の記述で、整数数値型または浮動小数点数値型が参照されている場合があります。 整数数値型には、<xref:System.Byte>、<xref:System.SByte>、<xref:System.Int16>、<xref:System.Int32>、<xref:System.Int64>、<xref:System.UInt16>、<xref:System.UInt32>、<xref:System.UInt64>、および <xref:System.Numerics.BigInteger> があります。 浮動小数点数値型には、<xref:System.Decimal>、<xref:System.Single>、および <xref:System.Double> があります。  
  
### 浮動小数点の無限大値と NaN \(非数\) 値  
 <xref:System.Single> の浮動小数点型または <xref:System.Double> の浮動小数点型が正の無限大、負の無限大、または NaN \(非数\) である場合は、書式指定文字列とは関係なく、現在適用可能な <xref:System.Globalization.NumberFormatInfo.PositiveInfinitySymbol%2A> オブジェクトによって指定される <xref:System.Globalization.NumberFormatInfo.NegativeInfinitySymbol%2A>、<xref:System.Globalization.NumberFormatInfo.NaNSymbol%2A>、または <xref:System.Globalization.NumberFormatInfo> の各プロパティの値は、書式設定された文字列となります。  
  
<a name="example"></a>   
## 例  
 次の例では、en\-US カルチャおよびすべての標準数値書式指定子を使用して、整数値と浮動小数点数値を書式設定します。 この例では 2 つの特定の数値型 \(<xref:System.Double> および <xref:System.Int32>\) を使用していますが、他の数値基本型 \(<xref:System.Byte>、<xref:System.SByte>、<xref:System.Int16>、<xref:System.Int32>、<xref:System.Int64>、<xref:System.UInt16>、<xref:System.UInt32>、<xref:System.UInt64><xref:System.Numerics.BigInteger>、<xref:System.Decimal>、および <xref:System.Single>\) でも類似した結果が得られます。  
  
 [!code-csharp[system.x.tostring-and-culture#1](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.X.ToString-and-Culture/cs/xts.cs#1)]
 [!code-vb[system.x.tostring-and-culture#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.X.ToString-and-Culture/vb/xts.vb#1)]  
  
## 参照  
 <xref:System.Globalization.NumberFormatInfo>   
 [カスタム数値書式指定文字列](../../../docs/standard/base-types/custom-numeric-format-strings.md)   
 [型の書式設定](../../../docs/standard/base-types/formatting-types.md)   
 [方法: 数値に先行するゼロを埋め込む](../../../docs/standard/base-types/how-to-pad-a-number-with-leading-zeros.md)   
 [サンプル: .NET Framework 4 の書式設定ユーティリティ](http://code.msdn.microsoft.com/NET-Framework-4-Formatting-9c4dae8d)   
 [複合書式指定](../../../docs/standard/base-types/composite-formatting.md)