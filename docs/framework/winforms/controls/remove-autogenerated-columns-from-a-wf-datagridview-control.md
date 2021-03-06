---
title: '方法: Windows フォーム DataGridView コントロールから自動生成された列を削除する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- DataGridView control [Windows Forms], removing columns
- columns [Windows Forms], removing
ms.assetid: 92e28d98-95a3-446c-9150-41b7c7e5be15
ms.openlocfilehash: 95a39b22f3317e1721fa9f77e874a11431d35625
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2019
ms.locfileid: "64614712"
---
# <a name="how-to-remove-autogenerated-columns-from-a-windows-forms-datagridview-control"></a>方法: Windows フォーム DataGridView コントロールから自動生成された列を削除する
ときに、<xref:System.Windows.Forms.DataGridView>コントロールはその列のデータ ソースからデータに基づく自動生成を設定、特定の列を選択的に省略できます。 呼び出すことによってこれを行う、<xref:System.Windows.Forms.DataGridViewColumnCollection.Remove%2A>メソッドを<xref:System.Windows.Forms.DataGridView.Columns%2A>コレクション。 設定によってビューから列を非表示にする代わりに、<xref:System.Windows.Forms.DataGridViewColumn.Visible%2A>プロパティを`false`します。 この手法は、特定の条件に非表示の列を表示する場合、または列のデータを表示せずにアクセスする必要がある場合に便利です。  
  
### <a name="to-remove-autogenerated-columns"></a>自動生成された列を削除するには  
  
- 呼び出す、<xref:System.Windows.Forms.DataGridViewColumnCollection.Remove%2A>メソッドを<xref:System.Windows.Forms.DataGridView.Columns%2A>コレクション。  
  
     [!code-csharp[System.Windows.Forms.DataGridViewMisc#111](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/CS/datagridviewmisc.cs#111)]
     [!code-vb[System.Windows.Forms.DataGridViewMisc#111](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/VB/datagridviewmisc.vb#111)]  
  
### <a name="to-hide-autogenerated-columns"></a>自動生成された列を非表示にするには  
  
- セットの列の<xref:System.Windows.Forms.DataGridViewColumn.Visible%2A>プロパティを`false`します。  
  
     [!code-csharp[System.Windows.Forms.DataGridViewMisc#112](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/CS/datagridviewmisc.cs#112)]
     [!code-vb[System.Windows.Forms.DataGridViewMisc#112](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/VB/datagridviewmisc.vb#112)]  
  
## <a name="example"></a>例  
 [!code-csharp[System.Windows.Forms.DataGridViewMisc#110](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/CS/datagridviewmisc.cs#110)]
 [!code-vb[System.Windows.Forms.DataGridViewMisc#110](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/VB/datagridviewmisc.vb#110)]  
  
## <a name="compiling-the-code"></a>コードのコンパイル  
 この例で必要な要素は次のとおりです。  
  
- A<xref:System.Windows.Forms.DataGridView>という名前のコントロール`dataGridView1`を含むテーブルにバインドされている`Fax`と`CustomerID`列など、 `Customers` Northwind サンプル データベース内のテーブル。  
  
- <xref:System?displayProperty=nameWithType> アセンブリおよび <xref:System.Windows.Forms?displayProperty=nameWithType> アセンブリへの参照。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Forms.DataGridView>
- <xref:System.Windows.Forms.DataGridView.AutoGenerateColumns%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridView.Columns%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridViewColumnCollection.Remove%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridViewColumn.Visible%2A?displayProperty=nameWithType>
- [Windows フォーム DataGridView コントロールでのデータの表示](displaying-data-in-the-windows-forms-datagridview-control.md)
