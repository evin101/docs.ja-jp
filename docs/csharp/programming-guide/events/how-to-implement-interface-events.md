---
title: '方法: インターフェイス イベントを実装する - C# プログラミング ガイド'
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords:
- interfaces [C#], event implementation in classes
- events [C#], in interfaces
ms.assetid: 63527447-9535-4880-8e95-35e2075827df
ms.openlocfilehash: 574ea9927a22c24c356d84652fd29692c519247b
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/19/2019
ms.locfileid: "69590508"
---
# <a name="how-to-implement-interface-events-c-programming-guide"></a>方法: インターフェイス イベントを実装する (C# プログラミング ガイド)
[インターフェイス](../../language-reference/keywords/interface.md)では[イベント](../../language-reference/keywords/event.md)を宣言できます。 次の例では、クラス内にインターフェイス イベントを実装する方法について説明します。 基本的な原則は、インターフェイスのメソッドやプロパティを実装する場合と同じです。  
  
## <a name="to-implement-interface-events-in-a-class"></a>クラス内でインターフェイス イベントを実装するには  
  
クラス内でイベントを宣言してから、適切な領域でそのイベントを呼び出します。  
  
```csharp
namespace ImplementInterfaceEvents  
{  
    public interface IDrawingObject  
    {  
        event EventHandler ShapeChanged;  
    }  
    public class MyEventArgs : EventArgs   
    {  
        // class members  
    }  
    public class Shape : IDrawingObject  
    {  
        public event EventHandler ShapeChanged;  
        void ChangeShape()  
        {  
            // Do something here before the event…  

            OnShapeChanged(new MyEventArgs(/*arguments*/));  

            // or do something here after the event.   
        }  
        protected virtual void OnShapeChanged(MyEventArgs e)  
        {  
            ShapeChanged?.Invoke(this, e);  
        }  
    }  

}  
```  
  
## <a name="example"></a>例  
次の例では、同じ名前のイベント名がある 2 つ以上のインターフェイスからクラスを継承するという、あまり一般的でない状況の対処方法を示します。 このような場合は、1 つ以上のイベントに対して明示的なインターフェイスの実装を指定する必要があります。 イベントに対する明示的なインターフェイスの実装を記述する場合、`add` および `remove` の各イベント アクセサーも記述する必要があります。 通常ではこれらのアクセサーはコンパイラで指定しますが、この例ではコンパイラで指定することはできません。  
  
独自のアクセサーを指定することで、2 つのイベントがクラス内の同一イベントと別々のイベントのどちらによって表されるかを指定できます。 たとえば、インターフェイスの仕様上、イベントを複数回発生させる必要がある場合は、各イベントをクラス内の別々の実装に関連付けます。 次の例では、サブスクライバーで `IShape` または `IDrawingObject` のいずれかに図形参照をキャストして、どちらの `OnDraw` イベントを受信するかを決定しています。  
  
 [!code-csharp[csProgGuideEvents#10](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideEvents/CS/Events.cs#10)]
  
## <a name="see-also"></a>関連項目

- [C# プログラミング ガイド](../index.md)
- [イベント](./index.md)
- [デリゲート](../delegates/index.md)
- [明示的なインターフェイスの実装](../interfaces/explicit-interface-implementation.md)
- [方法: 派生クラスから基本クラス イベントを発生させる](./how-to-raise-base-class-events-in-derived-classes.md)
