---
title: DataGridView コントロールの概要 (Windows フォーム)
ms.date: 03/30/2017
f1_keywords:
- DataGridView
helpviewer_keywords:
- DataGridView control [Windows Forms], about DataGridView control
- grid controls [Windows Forms]
- tables [Windows Forms], displaying in DataGridView control
- tables [Windows Forms], binding to DataGridView control
- columns [Windows Forms], DataGridView control
- bound controls [Windows Forms], dataGridView control
- datasets [Windows Forms], binding to DataGridView control
- data grids [Windows Forms], about data grids
- data [Windows Forms], resorting
- data [Windows Forms], navigating
- grids [Windows Forms]
- data binding [Windows Forms], DataGridView control
- data sources [Windows Forms], binding to DataGridView control
- DataGridView control [Windows Forms], data binding
ms.assetid: 0a45c661-89dc-4390-9cc6-c47eee501488
ms.openlocfilehash: 992bf57642c955a87cd7675e0bbe7c52131e8039
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/22/2019
ms.locfileid: "69969151"
---
# <a name="datagridview-control-overview-windows-forms"></a>DataGridView コントロールの概要 (Windows フォーム)
> [!NOTE]
> <xref:System.Windows.Forms.DataGridView> コントロールは、<xref:System.Windows.Forms.DataGrid> コントロールに代わると共に追加の機能を提供します。ただし、<xref:System.Windows.Forms.DataGrid> コントロールは、下位互換性を保つ目的および将来使用する目的で保持されます。 詳細については、「[Windows フォームの DataGridView コントロールと DataGrid コントロールの違いについて](differences-between-the-windows-forms-datagridview-and-datagrid-controls.md)」を参照してください。  
  
 <xref:System.Windows.Forms.DataGridView>コントロールを使用すると、さまざまな種類のデータソースの表形式データを表示および編集できます。  
  
 コントロールへの<xref:System.Windows.Forms.DataGridView>データのバインドは、簡単かつ直感的に行うことができ、多くの場合、 <xref:System.Windows.Forms.DataGridView.DataSource%2A>プロパティを設定するのと同じくらい簡単です。 複数のリストまたはテーブルを含むデータソースにバインドする場合は、 <xref:System.Windows.Forms.DataGridView.DataMember%2A>バインド先のリストまたはテーブルを指定する文字列にプロパティを設定します。  
  
 コントロール<xref:System.Windows.Forms.DataGridView>は標準の Windows フォームデータバインディングモデルをサポートするため、次の一覧に示すクラスのインスタンスにバインドされます。  
  
- <xref:System.Collections.IList>インターフェイスを実装する任意のクラス (1 次元配列を含む)。  
  
- クラス<xref:System.ComponentModel.IListSource> <xref:System.Data.DataTable>やクラス<xref:System.Data.DataSet>など、インターフェイスを実装する任意のクラス。  
  
- <xref:System.ComponentModel.IBindingList>インターフェイスを実装するクラス ( <xref:System.ComponentModel.BindingList%601>クラスなど)。  
  
- <xref:System.ComponentModel.IBindingListView>インターフェイスを実装するクラス ( <xref:System.Windows.Forms.BindingSource>クラスなど)。  
  
 コントロール<xref:System.Windows.Forms.DataGridView>は、これらのインターフェイスによって返されるオブジェクトのパブリックプロパティへのデータバインディング、または返され<xref:System.ComponentModel.ICustomTypeDescriptor>たオブジェクトに実装されている場合はインターフェイスによって返される properties コレクションへのデータバインディングをサポートします。  
  
 通常は、 <xref:System.Windows.Forms.BindingSource>コンポーネントにバインドし、 <xref:System.Windows.Forms.BindingSource>コンポーネントを別のデータソースにバインドするか、ビジネスオブジェクトを設定します。 <xref:System.Windows.Forms.BindingSource>コンポーネントは、さまざまなデータソースにバインドできるため、データバインディングに関する多くの問題を自動的に解決できるため、推奨されるデータソースです。 詳細については、「 [BindingSource コンポーネント](bindingsource-component.md)」を参照してください。  
  
 コントロール<xref:System.Windows.Forms.DataGridView>は、基になるデータストアを使用せずに、*非バインド*モードで使用することもできます。 バインド<xref:System.Windows.Forms.DataGridView>されていないコントロールを使用するコード[例については、「チュートリアル:非バインド Windows フォーム DataGridView コントロール](walkthrough-creating-an-unbound-windows-forms-datagridview-control.md)を作成する。  
  
 <xref:System.Windows.Forms.DataGridView>コントロールは、高度な構成と拡張が可能で、外観と動作をカスタマイズするための多数のプロパティ、メソッド、およびイベントが用意されています。 Windows フォームアプリケーションで表形式のデータを表示する場合は、他<xref:System.Windows.Forms.DataGridView>のコントロールの前にコントロールを<xref:System.Windows.Forms.DataGrid>使用することを検討してください (たとえば、)。 読み取り専用の値を持つ小さいグリッドを表示する場合や、ユーザーが何百万ものレコード<xref:System.Windows.Forms.DataGridView>を含むテーブルを編集できるようにする場合は、コントロールを使用すると、簡単にプログラミング可能なメモリ効率の高いソリューションが提供されます。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [DataGridView コントロール テクノロジの概要](datagridview-control-technology-summary-windows-forms.md)  
 コントロール<xref:System.Windows.Forms.DataGridView>の概念と関連クラスの使用について概要を説明します。  
  
 [DataGridView コントロールのアーキテクチャ](datagridview-control-architecture-windows-forms.md)  
 型階層と継承構造<xref:System.Windows.Forms.DataGridView>を説明するコントロールのアーキテクチャについて説明します。  
  
 [DataGridView コントロールのシナリオ](datagridview-control-scenarios-windows-forms.md)  
 <xref:System.Windows.Forms.DataGridView>コントロールが使用される最も一般的なシナリオについて説明します。  
  
 [DataGridView コントロールのコード ディレクトリ](datagridview-control-code-directory-windows-forms.md)  
 さまざまな<xref:System.Windows.Forms.DataGridView>タスクに関するドキュメントのコード例へのリンクを示します。 コード例はタスクの種類ごとに分類されています。  
  
## <a name="related-sections"></a>関連項目  
 [Windows フォーム DataGridView コントロールの列型](column-types-in-the-windows-forms-datagridview-control.md)  
 情報を表示し、ユーザーが<xref:System.Windows.Forms.DataGridView>情報を変更または追加できるようにするために使用される、Windows フォームコントロール内の列の型について説明します。  
  
 [Windows フォーム DataGridView コントロールでのデータの表示](displaying-data-in-the-windows-forms-datagridview-control.md)  
 コントロールに手動でデータを組み込む方法と、外部データ ソースからデータを取得する方法について説明するトピックを示します。  
  
 [Windows フォーム DataGridView コントロールのカスタマイズ](customizing-the-windows-forms-datagridview-control.md)  
 <xref:System.Windows.Forms.DataGridView> のセルおよび行のカスタム描画と、セル、列、および行の派生型の作成について説明するトピックを示します。  
  
 [Windows フォーム DataGridView コントロールでのパフォーマンス チューニング](performance-tuning-in-the-windows-forms-datagridview-control.md)  
 大量のデータを扱うときのパフォーマンスの問題を避けるために、このコントロールを効率的に使用する方法について説明するトピックを示します。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Forms.DataGridView>
- <xref:System.Windows.Forms.BindingSource>
- [DataGridView コントロール](datagridview-control-windows-forms.md)
- [Windows フォーム DataGridView コントロールの既定の機能](default-functionality-in-the-windows-forms-datagridview-control.md)
- [Windows フォーム DataGridView コントロールの既定のキーボード処理とマウス処理](default-keyboard-and-mouse-handling-in-the-windows-forms-datagridview-control.md)
