---
title: パス マークアップ構文
ms.date: 03/30/2017
helpviewer_keywords:
- attribute usage in XAML [WPF]
- XAML [WPF], attribute usage
- graphics [WPF], PathGeometry class
- XAML [WPF], object element usage
ms.assetid: b8586241-a02d-486e-9223-e1e98e047f41
ms.openlocfilehash: 86901f357c43dc7c0c1402bf313e674603eaccbe
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/04/2018
---
# <a name="path-markup-syntax"></a>パス マークアップ構文
パスは、後ほど[図形と WPF の概要での基本的な描画](../../../../docs/framework/wpf/graphics-multimedia/shapes-and-basic-drawing-in-wpf-overview.md)と[ジオメトリの概要](../../../../docs/framework/wpf/graphics-multimedia/geometry-overview.md)、ただし、このトピックの詳細、強力で複雑なミニ言語の説明パスの指定に使用することができます使用してよりコンパクト ジオメトリ[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)]です。  
  
<a name="prerequisites"></a>   
## <a name="prerequisites"></a>必須コンポーネント  
 このトピックの内容を理解しておく必要がありますの基本的な機能を使い慣れて<xref:System.Windows.Media.Geometry>オブジェクト。 詳細については、次を参照してください。、[ジオメトリの概要](../../../../docs/framework/wpf/graphics-multimedia/geometry-overview.md)です。  
  
<a name="abouthisdocument"></a>   
## <a name="streamgeometry-and-pathfigurecollection-mini-languages"></a>StreamGeometry ミニ言語と PathFigureCollection ミニ言語  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 幾何学模様のパスを記述するためのミニ言語を提供する 2 つのクラスを提供します。<xref:System.Windows.Media.StreamGeometry>と<xref:System.Windows.Media.PathFigureCollection>です。  
  
-   使用する、<xref:System.Windows.Media.StreamGeometry>型のプロパティを設定するときに、ミニ言語<xref:System.Windows.Media.Geometry>、ように、<xref:System.Windows.UIElement.Clip%2A>のプロパティ、<xref:System.Windows.UIElement>または<xref:System.Windows.Shapes.Path.Data%2A>のプロパティ、<xref:System.Windows.Shapes.Path>要素。 次の例では、属性の構文を使用して、作成、<xref:System.Windows.Media.StreamGeometry>です。  
  
     [!code-xaml[GeometrySample_snip_XAML#GraphicsMMStreamGeometryAttributeSyntaxInline](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GeometrySample_snip_XAML/CS/MiniLanguageExample.xaml#graphicsmmstreamgeometryattributesyntaxinline)]  
  
-   使用する、<xref:System.Windows.Media.PathFigureCollection>ミニ言語を設定する場合、<xref:System.Windows.Media.PathGeometry.Figures%2A>のプロパティ、<xref:System.Windows.Media.PathGeometry>です。 次の例では、属性の構文を使用して、作成、<xref:System.Windows.Media.PathFigureCollection>の<xref:System.Windows.Media.PathGeometry>です。  
  
     [!code-xaml[GeometrySample_snip_XAML#GraphicsMMPathFigureCollectionAttributeSyntaxInline](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GeometrySample_snip_XAML/CS/MiniLanguageExample.xaml#graphicsmmpathfigurecollectionattributesyntaxinline)]  
  
 前の例からわかるように、2 つのミニ言語はほとんど同じです。 使用することは常に、<xref:System.Windows.Media.PathGeometry>を使用する場合、状況、<xref:System.Windows.Media.StreamGeometry>以外の場合はそのうち、どれを使用する必要がありますか。 使用して、<xref:System.Windows.Media.StreamGeometry>作成後にパスを変更する必要はないときを使用して、<xref:System.Windows.Media.PathGeometry>は、パスを変更する必要がある場合。  
  
 間の相違点の詳細については<xref:System.Windows.Media.PathGeometry>と<xref:System.Windows.Media.StreamGeometry>、オブジェクトを参照してください、[ジオメトリの概要](../../../../docs/framework/wpf/graphics-multimedia/geometry-overview.md)です。  
  
### <a name="a-note-about-white-space"></a>空白についてのメモ  
 簡潔にするために、この後のセクションで示す構文には 1 つの空白が使用されていますが、1 つの空白を使用できるところでは、常に複数の空白スペースも許容されます。  
  
 2 つの数値は、実際にはコンマまたは空白で区切る必要はありませんが、これは結果の文字列があいまいにならない場合にのみ実行できます。 たとえば、`2..3`が実際には 2 つの数値:「2」 と ".3" ) です。 同様に、`2-3`は、「2」および「-3」です。 どちらの場合も、コマンドの前後に空白は必要ありません。  
  
### <a name="syntax"></a>構文  
 [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)]属性の使用法の構文、<xref:System.Windows.Media.StreamGeometry>は省略可能なので構成されて<xref:System.Windows.Media.FillRule>値と 1 つ以上の説明を図します。  
  
|StreamGeometry XAML 属性使用構文|  
|-----------------------------------------|  
|`<` *object* *property* `="`[ `fillRule`] `figureDescription`[ `figureDescription`]* `" ... />`|  
  
 [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)]属性の使用法の構文、<xref:System.Windows.Media.PathFigureCollection>は 1 つまたは複数の図の説明で構成されます。  
  
|PathFigureCollection XAML 属性使用構文|  
|-----------------------------------------------|  
|`<` *object* *property* `="` `figureDescription`[ `figureDescription`]* `" ... />`|  
  
|用語|説明|  
|----------|-----------------|  
|*fillRule*|<xref:System.Windows.Media.FillRule?displayProperty=nameWithType><br /><br /> 指定するかどうか、<xref:System.Windows.Media.StreamGeometry>を使用して、<xref:System.Windows.Media.FillRule.EvenOdd>または<xref:System.Windows.Media.FillRule.Nonzero><xref:System.Windows.Media.PathGeometry.FillRule%2A>です。<br /><br /> -   `F0` 指定します、<xref:System.Windows.Media.FillRule.EvenOdd>塗りつぶしルール。<br />-   `F1` 指定します、<xref:System.Windows.Media.FillRule.Nonzero>塗りつぶしルール。<br /><br /> このコマンドを省略した場合、サブパスが既定の動作を使用<xref:System.Windows.Media.FillRule.EvenOdd>です。 このコマンドを指定する場合は、先頭に配置する必要があります。|  
|*figureDescription*|移動コマンドと描画コマンド (および省略可能な閉じるコマンド) で構成される図形。<br /><br /> `moveCommand` `drawCommands`  `[` `closeCommand` `]`|  
|*moveCommand*|図形の開始位置を指定する移動コマンド。 参照してください、[移動コマンド](#themovecommand)セクションです。|  
|*drawCommands*|図の内容を記述する 1 つまたは複数の描画コマンド。 参照してください、[描画コマンド](#drawcommands)セクションです。|  
|*closeCommand*|図形を閉じるコマンド (省略可能)。 参照してください、[閉じるコマンド](#closecommand)セクションです。|  
  
<a name="themovecommand"></a>   
## <a name="move-command"></a>移動コマンド  
 新しい図形の始点を指定します。  
  
|構文|  
|------------|  
|`M` *startPoint*<br /><br /> または<br /><br /> `m` *startPoint*|  
  
|用語|説明|  
|----------|-----------------|  
|*startPoint*|<xref:System.Windows.Point?displayProperty=nameWithType><br /><br /> 新しい図形の始点。|  
  
 大文字`M`ことを示します`startPoint`絶対値; 小文字`m`ことを示します`startPoint`を過去の時点のオフセットです (0, 0) が存在しない場合、または。 移動コマンドの後ろに複数の点を指定した場合は、直線コマンドを指定した場合でも、これらの点を結ぶ線が描画されます。  
  
<a name="drawcommands"></a>   
## <a name="draw-commands"></a>描画コマンド  
 描画コマンドは、さまざまな図形コマンドで構成できます。 次の図形のコマンドを使用できます。直線、水平線、垂直線、3 次ベジエ曲線、2 次ベジエ曲線、スムーズ 3 次ベジエ曲線、スムーズ 2 次ベジエ曲線、および楕円の円弧。  
  
 各コマンドは、大文字または小文字で入力します。大文字は絶対値を、小文字は相対値を表し、そのセグメントの制御点は、前の例の終点を基準とします。 順番に同じ型の 1 つ以上のコマンドを入力する、ときに、重複するコマンドの入力を省略できます。たとえば、`L 100,200 300,400`は等価`L 100,200 L 300,400`です。 次の表、**移動**と**描画**コマンド。  
  
### <a name="line-command"></a>直線コマンド  
 現在の点と指定された終点の間に直線を作成します。 `l 20 30` および`L 20,30`の有効な例については、**行**コマンド。  
  
|構文|  
|------------|  
|`L` *endPoint*<br /><br /> または<br /><br /> `l` *endPoint*|  
  
|用語|説明|  
|----------|-----------------|  
|*endPoint*|<xref:System.Windows.Point?displayProperty=nameWithType><br /><br /> 線の終点。|  

大文字`L`ことを示します`endPoint`絶対値; 小文字`l`ことを示します`endPoint`を過去の時点のオフセットです (0, 0) が存在しない場合、または。

### <a name="horizontal-line-command"></a>水平線コマンド  
 現在の点と指定された x 座標の間に水平線を作成します。 `H 90` は、有効な水平線コマンドの例です。

  
|構文|  
|------------|  
|`H`  *x*<br /><br /> または<br /><br /> `h`  *x*|  
  
|用語|説明|  
|----------|-----------------|  
|*x*|<xref:System.Double?displayProperty=nameWithType><br /><br /> 直線の終点の x 座標。|  
  
大文字`H`ことを示します`x`絶対値; 小文字`h`ことを示します`x`を過去の時点のオフセットです (0, 0) が存在しない場合、または。
  
### <a name="vertical-line-command"></a>垂直線コマンド  
 現在の点と指定された y 座標の間に垂直線を作成します。 `v 90` は、有効な垂直線コマンドの例です。

  
|構文|  
|------------|  
|`V`  *y*<br /><br /> または<br /><br /> `v`  *y*|  
  
|用語|説明|  
|----------|-----------------|  
|*y*|<xref:System.Double?displayProperty=nameWithType><br /><br /> 直線の終点の y 座標。|  

大文字`V`ことを示します`y`絶対値; 小文字`v`ことを示します`y`を過去の時点のオフセットです (0, 0) が存在しない場合、または。  
    
### <a name="cubic-bezier-curve-command"></a>3 次ベジエ曲線コマンド  
 2 つの指定されたコントロール ポイントを使用して、現在のポイントと指定したエンドポイントの間で 3 次ベジエ曲線を作成 (`controlPoint`1 と`controlPoint`2)。 `C 100,200 200,400 300,200` は、有効な曲線コマンドの例です。  
  
|構文|  
|------------|  
|`C` `controlPoint`1`controlPoint`2`endPoint`<br /><br /> または<br /><br /> `c` `controlPoint`1`controlPoint`2`endPoint`|  
  
|用語|説明|  
|----------|-----------------|  
|`controlPoint`1|<xref:System.Windows.Point?displayProperty=nameWithType><br /><br /> 曲線の 1 つ目の制御点。曲線の前半の接線を決定します。|  
|`controlPoint`2|<xref:System.Windows.Point?displayProperty=nameWithType><br /><br /> 曲線の 2 つ目の制御点。曲線の後半の接線を決定します。|  
|`endPoint`|<xref:System.Windows.Point?displayProperty=nameWithType><br /><br /> 曲線が描画される点。|  
  
### <a name="quadratic-bezier-curve-command"></a>2 次ベジエ曲線コマンド  
 指定されたコントロール ポイントを使用して、現在のポイントと指定したエンドポイントの間で 2 次ベジエ曲線を作成 (`controlPoint`)。 `q 100,200 300,200` は、有効な 2 次ベジエ曲線コマンドの例です。  
  
|構文|  
|------------|  
|`Q` `controlPoint` `endPoint`<br /><br /> または<br /><br /> `q` `controlPoint` `endPoint`|  
  
|用語|説明|  
|----------|-----------------|  
|`controlPoint`|<xref:System.Windows.Point?displayProperty=nameWithType><br /><br /> 曲線の制御点。曲線の前半と後半の接線を決定します。|  
|`endPoint`|<xref:System.Windows.Point?displayProperty=nameWithType><br /><br /> 曲線が描画される点。|  
  
### <a name="smooth-cubic-bezier-curve-command"></a>スムーズ 3 次ベジエ曲線コマンド  
 現在の点と指定された終点の間に 3 次ベジエ曲線を作成します。 1 つ目の制御点は、現在の点に対する前のコマンドの 2 つ目の制御点のリフレクションと見なされます。 前のコマンドが存在しない場合、または前のコマンドが 3 次ベジエ曲線コマンドまたはスムーズ 3 次ベジエ曲線コマンドでなかった場合、1 つ目の制御点は、現在の点と一致するとみなされます。 曲線の最後のコントロール ポイントは、2 つ目のコントロール ポイントで指定された`controlPoint`2 です。 たとえば、`S 100,200 200,300`有効な smooth 3 次ベジエ曲線コマンドします。  
  
|構文|  
|------------|  
|`S` `controlPoint`2`endPoint`<br /><br /> または<br /><br /> `s` `controlPoint`2`endPoint`|  
  
|用語|説明|  
|----------|-----------------|  
|`controlPoint`2|<xref:System.Windows.Point?displayProperty=nameWithType><br /><br /> 曲線の制御点。曲線の後半の接線を決定します。|  
|`endPoint`|<xref:System.Windows.Point?displayProperty=nameWithType><br /><br /> 曲線が描画される点。|  
  
### <a name="smooth-quadratic-bezier-curve-command"></a>スムーズ 2 次ベジエ曲線コマンド  
 現在の点と指定された終点の間に 2 次ベジエ曲線を作成します。 制御点は、現在の点に対する前のコマンドの制御点のリフレクションと見なされます。 前のコマンドが存在しない場合、または前のコマンドが 2 次ベジエ曲線コマンドまたはスムーズ 2 次ベジエ曲線コマンドでなかった場合、制御点は、現在の点と一致するとみなされます。  
  
|構文|  
|------------|  
|`T` `controlPoint` `endPoint`<br /><br /> または<br /><br /> `t` `controlPoint` `endPoint`|  
  
|用語|説明|  
|----------|-----------------|  
|`controlPoint`|<xref:System.Windows.Point?displayProperty=nameWithType><br /><br /> 曲線の制御点。曲線の前半の接線を決定します。|  
|`endPoint`|<xref:System.Windows.Point?displayProperty=nameWithType><br /><br /> 曲線が描画される点。|  
  
### <a name="elliptical-arc-command"></a>楕円の円弧コマンド  
 現在の点と指定された終点の間に楕円の円弧を作成します。  
  
|構文|  
|------------|  
|`A` `size` `rotationAngle` `isLargeArcFlag` `sweepDirectionFlag` `endPoint`<br /><br /> または<br /><br /> `a` `size` `rotationAngle` `isLargeArcFlag` `sweepDirectionFlag` `endPoint`|  
  
|用語|説明|  
|----------|-----------------|  
|`size`|<xref:System.Windows.Size?displayProperty=nameWithType><br /><br /> 円弧の x 半径と y 半径。|  
|`rotationAngle`|<xref:System.Double?displayProperty=nameWithType><br /><br /> 楕円の回転 (度単位)。|  
|`isLargeArcFlag`|円弧の角度を 180 度以上にする場合は 1 に設定します。それ以外の場合は 0 に設定します。|  
|`sweepDirectionFlag`|円弧が正の角度の方向に描画される場合は 1 に設定します。それ以外の場合は 0 に設定します。|  
|`endPoint`|<xref:System.Windows.Point?displayProperty=nameWithType><br /><br /> 円弧が描画される点。|  
  
<a name="closecommand"></a>   
## <a name="the-close-command"></a>閉じるコマンド  
 現在の図形を終了し、現在の点と図の開始点を結ぶ線を作成します。 このコマンドは、図形の最初のセグメントと最後のセグメントの間に線結合 (コーナー) を作成します。  
  
|構文|  
|------------|  
|`Z`<br /><br /> または<br /><br /> `z`|  

<a name="pointsyntax"></a>   
## <a name="point-syntax"></a>点の構文  
 ポイントの x 座標と y 座標をについて説明します。 ここで (0, 0) は、左上隅です。
  
|構文|  
|------------|  
|`x` `,` `y`<br /><br /> または<br /><br /> `x` `y`|  
  
|用語|説明|  
|----------|-----------------|  
|`x`|<xref:System.Double?displayProperty=nameWithType><br /><br /> 点の x 座標。|  
|`y`|<xref:System.Double?displayProperty=nameWithType><br /><br /> 点の y 座標。|  
  
<a name="specialvalues"></a>   
## <a name="special-values"></a>特殊な値  
 標準的な数値ではなく、次の特殊な値を使用することもできます。 これらの値では、大文字と小文字が区別されます。  
  
 Infinity  
 表す<xref:System.Double.PositiveInfinity?displayProperty=nameWithType>です。  
  
 -Infinity  
 表す<xref:System.Double.NegativeInfinity?displayProperty=nameWithType>です。  
  
 NaN  
 表す<xref:System.Double.NaN?displayProperty=nameWithType>です。  
  
 指数表記を使用することもできます。 たとえば、`+1.e17`有効な値です。  
  
## <a name="see-also"></a>関連項目  
 <xref:System.Windows.Shapes.Path>  
 <xref:System.Windows.Media.StreamGeometry>  
 <xref:System.Windows.Media.PathGeometry>  
 <xref:System.Windows.Media.PathFigureCollection>  
 [WPF での図形と基本描画の概要](../../../../docs/framework/wpf/graphics-multimedia/shapes-and-basic-drawing-in-wpf-overview.md)  
 [ジオメトリの概要](../../../../docs/framework/wpf/graphics-multimedia/geometry-overview.md)  
 [方法トピック](../../../../docs/framework/wpf/graphics-multimedia/geometries-how-to-topics.md)
