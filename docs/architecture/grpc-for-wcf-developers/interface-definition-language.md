---
title: インターフェイス定義言語-WCF 開発者向け gRPC
description: プロトコルバッファー IDL の概要を紹介します。
ms.date: 09/02/2019
ms.openlocfilehash: 1f304502bd0091f753a3d2f7854298f4bbf983f1
ms.sourcegitcommit: f348c84443380a1959294cdf12babcb804cfa987
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/12/2019
ms.locfileid: "73967625"
---
# <a name="interface-definition-language"></a>インターフェイス定義言語

WCF では、サービスは Web サービス定義言語 (WSDL) を使用して記述メタデータを公開できます。 WSDL は、実行時に .NET リフレクションを使用して動的に生成されます。 開発者は、このメタデータを使用して、これらのサービスのクライアントを生成できます。 SOAP over HTTP などのプラットフォームに依存しないバインディングが使用されている場合は、他の言語のクライアントを生成できます。

gRPC は、プロトコルバッファーからインターフェイス定義言語 (IDL) を使用します。 プロトコルバッファー IDL は、オープンな仕様を持つ、プラットフォームに依存しないカスタム言語です。 開発者は、サービスを入力および出力と共に記述するために、ファイルを手動でコーディング `.proto` ます。 これらの `.proto` ファイルを使用して、クライアントとサーバーの言語またはプラットフォーム固有のスタブを生成し、複数の異なるプラットフォームが通信できるようにすることができます。 `.proto` ファイルを共有することにより、コードの依存関係を取らずに、他のサービスを使用するコードを生成できます。

Protobuf IDL の利点の1つは、カスタム言語として、gRPC を完全な言語とプラットフォームに依存しないようにすることです。これにより、他のテクノロジを優先することはできません。

Protobuf IDL は、人間が読み取りと書き込みの両方を行うように設計されています。一方、WSDL は、機械で読み取り可能な形式であることを意図しています。 通常、WCF サービスの WSDL を変更するには、サービスを実行し、サーバーから WSDL ファイルを再生成する必要があります。 これに対し、`.proto` ファイルでは、変更をテキストエディターで簡単に適用し、生成されたコードを自動的にフローすることができます。 Visual Studio 2019 では、保存時に `.proto` ファイルがバックグラウンドでビルドされます。VS Code などの他のエディターを使用する場合は、プロジェクトのビルド時に変更が適用されます。

XML (特に SOAP) と比較すると、Protobuf を使用してエンコードされたメッセージには多くの利点があります。 Protobuf メッセージは、SOAP XML としてシリアル化されるのと同じデータよりも小さくなる傾向があります。また、エンコード、デコード、ネットワーク経由での転送が高速になる可能性があります。

SOAP と比較した場合の Protobuf の潜在的な欠点は、メッセージが人間が判読できないため、メッセージの内容をデバッグするために追加のツールが必要になることです。

> [!TIP]
> gRPC*は*、プリコンパイルされたスタブを使用せずに動的にサービスにアクセスするためのサーバーリフレクションをサポートしています。ただし、アプリケーション固有のクライアントよりも汎用ツールの方が適しています。 GRPC サーバーリフレクションの詳細については、GitHub の「 [grpc/grpc](https://github.com/grpc/grpc/blob/master/doc/server-reflection.md)リポジトリ」を参照してください。

> [!NOTE]
> NetTCP バインドと共に使用される WCF のバイナリ形式は、コンパクトさもとパフォーマンスの点で Protobuf に非常に近いものですが、NetTCP は .NET クライアントとサーバーの間でのみ使用できます。一方、Protobuf はクロスプラットフォームソリューションです。

>[!div class="step-by-step"]
>[前へ](approach.md)
>[次へ](network-protocols.md)
