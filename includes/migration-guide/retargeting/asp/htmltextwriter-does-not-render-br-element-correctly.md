### <a name="htmltextwriter-does-not-render-br-element-correctly"></a><span data-ttu-id="1f1f6-101">HtmlTextWriter で `<br/>` 要素が正しく表示されない</span><span class="sxs-lookup"><span data-stu-id="1f1f6-101">HtmlTextWriter does not render `<br/>` element correctly</span></span>

|   |   |
|---|---|
|<span data-ttu-id="1f1f6-102">説明</span><span class="sxs-lookup"><span data-stu-id="1f1f6-102">Details</span></span>|<span data-ttu-id="1f1f6-103">.NET Framework 4.6 以降では、<xref:System.Web.UI.HtmlTextWriter.RenderBeginTag(System.String)> と <xref:System.Web.UI.HtmlTextWriter.RenderEndTag> を <code>&lt;BR /&gt;</code> 要素を指定して呼び出すと、<code>&lt;BR /&gt;</code> を 1 つだけ (2 つではなく) 正しく挿入します。</span><span class="sxs-lookup"><span data-stu-id="1f1f6-103">Beginning in the .NET Framework 4.6, calling <xref:System.Web.UI.HtmlTextWriter.RenderBeginTag(System.String)> and <xref:System.Web.UI.HtmlTextWriter.RenderEndTag> with a <code>&lt;BR /&gt;</code> element will correctly insert only one <code>&lt;BR /&gt;</code> (instead of two)</span></span>|
|<span data-ttu-id="1f1f6-104">提案される解決策</span><span class="sxs-lookup"><span data-stu-id="1f1f6-104">Suggestion</span></span>|<span data-ttu-id="1f1f6-105">アプリが余分な <code>&lt;BR /&gt;</code> タグに依存している場合は、<xref:System.Web.UI.HtmlTextWriter.RenderBeginTag(System.String)> をもう一度呼び出す必要があります。</span><span class="sxs-lookup"><span data-stu-id="1f1f6-105">If an app depended on the extra <code>&lt;BR /&gt;</code> tag, <xref:System.Web.UI.HtmlTextWriter.RenderBeginTag(System.String)> should be called a second time.</span></span> <span data-ttu-id="1f1f6-106">この動作の変更は、.NET Framework 4.6 以降を対象とするアプリにのみ影響するので、以前の動作を得るためには、以前のバージョンの .NET Framework を対象とするという方法もあります。</span><span class="sxs-lookup"><span data-stu-id="1f1f6-106">Note that this behavior change only affects apps that target the .NET Framework 4.6 or later, so another option is to target a previous version of the .NET Framework in order to get the old behavior.</span></span>|
|<span data-ttu-id="1f1f6-107">スコープ</span><span class="sxs-lookup"><span data-stu-id="1f1f6-107">Scope</span></span>|<span data-ttu-id="1f1f6-108">エッジ</span><span class="sxs-lookup"><span data-stu-id="1f1f6-108">Edge</span></span>|
|<span data-ttu-id="1f1f6-109">Version</span><span class="sxs-lookup"><span data-stu-id="1f1f6-109">Version</span></span>|<span data-ttu-id="1f1f6-110">4.6</span><span class="sxs-lookup"><span data-stu-id="1f1f6-110">4.6</span></span>|
|<span data-ttu-id="1f1f6-111">型</span><span class="sxs-lookup"><span data-stu-id="1f1f6-111">Type</span></span>|<span data-ttu-id="1f1f6-112">再ターゲット中</span><span class="sxs-lookup"><span data-stu-id="1f1f6-112">Retargeting</span></span>|
|<span data-ttu-id="1f1f6-113">影響を受ける API</span><span class="sxs-lookup"><span data-stu-id="1f1f6-113">Affected APIs</span></span>|<ul><li><xref:System.Web.UI.HtmlTextWriter.RenderBeginTag(System.String)?displayProperty=nameWithType></li><li><xref:System.Web.UI.HtmlTextWriter.RenderBeginTag(System.Web.UI.HtmlTextWriterTag)?displayProperty=nameWithType></li></ul>|
