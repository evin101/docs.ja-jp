---
title: イベントの概要 (Windows フォーム)
ms.date: 03/30/2017
helpviewer_keywords:
- Windows Forms, event handling
- events [Windows Forms], about events
- delegates [Windows Forms], multicast
- delegates [Windows Forms], events and
- multicast event delegates
- Windows Forms controls, events
ms.assetid: 814a6a43-a312-4791-88d8-f75f9a4f8c4c
ms.openlocfilehash: 4abcf20b851f349a2b5df78c1fe1d15f729a5462
ms.sourcegitcommit: 30a558d23e3ac5a52071121a52c305c85fe15726
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/25/2019
ms.locfileid: "75345003"
---
# <a name="events-overview-windows-forms"></a>イベントの概要 (Windows フォーム)
イベントとは、プログラマが応答できる、つまり、コードを使って "処理" できるアクションのことです。 イベントは、マウスのクリックやキーを押すなどのユーザー アクション、プログラム コードまたはシステムによって生成されます。

 イベント ドリブン アプリケーションでは、イベントに応答してコードが実行されます。 各フォームおよびコントロールは、定義済みのイベント セットを公開しており、プログラマはそれらに対応するプログラムを作成できます。 これらのイベントの 1 つが発生したときに、関連するイベント ハンドラーにコードがある場合は、そのコードが呼び出されます。

 オブジェクトが発生させるイベントにはさまざまな種類がありますが、その多くがほとんどのコントロールで共通です。 たとえば、<xref:System.Windows.Forms.Control.Click> イベントは、ほとんどのオブジェクトで処理されます。 ユーザーがフォームをクリックすると、フォームの <xref:System.Windows.Forms.Control.Click> イベント ハンドラー内のコードが実行されます。

> [!NOTE]
> イベントの多くは、他のイベントと共に発生します。 たとえば、<xref:System.Windows.Forms.Control.DoubleClick> イベントが発生する場合は、<xref:System.Windows.Forms.Control.MouseDown>、<xref:System.Windows.Forms.Control.MouseUp>、および <xref:System.Windows.Forms.Control.Click> の各イベントが発生します。

 イベントを発生させて使用する方法の詳細については、「 [Events](../../standard/events/index.md)」を参照してください。

## <a name="delegates-and-their-role"></a>デリゲートとその役割
 デリゲートは、イベント処理機構を構築するために .NET Framework 内で一般的に使用されるクラスです。 デリゲートは、通常、ビジュアルC++やその他のオブジェクト指向言語で使用される関数ポインターとほぼ同等です。 ただし、関数ポインターとは異なり、デリゲートはオブジェクト指向で、タイプ セーフで、安全です。 また、関数ポインターには特定の関数への参照だけが含まれていますが、デリゲートはオブジェクトへの参照、およびそのオブジェクト内の 1 つ以上のメソッドへの参照で構成されています。

 このイベントモデルでは、*デリゲート*を使用して、イベントを処理するために使用されるメソッドにイベントをバインドします。 デリゲートを使用すると、ハンドラーのメソッドを指定することにより、イベント通知のための他のクラスを登録できます。 イベントが発生すると、デリゲートは関連付けられたメソッドを呼び出します。 デリゲートを定義する方法の詳細については、「[イベント](../../standard/events/index.md)」を参照してください。

デリゲートは、単一のメソッドまたは複数のメソッドに関連付けることができます。後者は、マルチキャストと呼ばれます。 イベントのデリゲートを作成する場合、ユーザー (または Windows) は通常、マルチキャストイベントを作成します。 例外は、1 回のイベントで複数回実行されることが論理的にあり得ないような特定のプロシージャ (ダイアログ ボックスの表示など) を呼び出すイベントです。 マルチキャストデリゲートを作成する方法の詳細については、「[デリゲートを結合する方法 (マルチキャストデリゲート)](../../csharp/programming-guide/delegates/how-to-combine-delegates-multicast-delegates.md)」を参照してください。

 マルチキャスト デリゲートは、関連付けられたメソッドの呼び出しリストを保持します。 マルチキャスト デリゲートでは、呼び出しリストにメソッドを追加する <xref:System.Delegate.Combine%2A> メソッド、およびリストからメソッドを削除する <xref:System.Delegate.Remove%2A> メソッドがサポートされています。

 アプリケーションによってイベントが記録されると、コントロールは、そのイベント用のデリゲートを呼び出すことによってイベントを発生させます。 次に、デリゲートによって、関連付けられたメソッドが呼び出されます。 ほとんどの場合、デリゲート (通常はマルチキャスト デリゲート) では、呼び出しリストにある関連付けされた各メソッドが順番に呼び出されるため、一対多通知を実行できます。 この方法では、すべての登録と通知がデリゲートによって処理されるため、コントロールでは、イベント通知の対象となるオブジェクトのリストを保持する必要がありません。

 デリゲートでは、複数のイベントを同じメソッドに関連付けし、多対一通知を実行することもできます。 たとえば、ボタンとメニューコマンドのクリック イベントで、同じデリゲートを呼び出すことができます。呼び出されたデリゲートによって単一のメソッドが呼び出されるので、どちらのイベントも同じように処理されます。

 デリゲートと共に使用される関連付けの機構は動的です。デリゲートは、シグネチャがイベント ハンドラのシグネチャと一致する任意のメソッドに実行時に関連付けできます。 この機能によって、状況に応じて関連付けるメソッドを設定または変更したり、イベント ハンドラをコントロールに動的に関連付けることができます。

## <a name="see-also"></a>関連項目

- [Windows フォーム内でのイベント ハンドラーの作成](creating-event-handlers-in-windows-forms.md)
- [イベント ハンドラーの概要](event-handlers-overview-windows-forms.md)
