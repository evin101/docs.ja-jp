---
title: .Net を使用してC# JSON をシリアル化および逆シリアル化する
ms.date: 01/10/2020
helpviewer_keywords:
- JSON serialization
- serializing objects
- serialization
- objects, serializing
ms.openlocfilehash: c05783963ba521109fb542f247ec9e62fdb5c2d9
ms.sourcegitcommit: dfad244ba549702b649bfef3bb057e33f24a8fb2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/12/2020
ms.locfileid: "75904640"
---
# <a name="json-serialization-and-deserialization-marshalling-and-unmarshalling-in-net---overview"></a>.NET での JSON のシリアル化と逆シリアル化 (マーシャリングとアンマーシャリング)-概要

`System.Text.Json` 名前空間は、JavaScript Object Notation (JSON) にシリアル化および逆シリアル化する機能を提供します。

ライブラリの設計では、高度な機能セットに対する高パフォーマンスと低メモリ割り当てが強調されています。 組み込みの UTF-8 サポートは、UTF-8 としてエンコードされた JSON テキストの読み取りと書き込みのプロセスを最適化します。これは、web 上のデータおよびディスク上のファイルのための最も一般的なエンコードです。

ライブラリには、メモリ内のドキュメントオブジェクトモデル (DOM) を操作するためのクラスも用意されています。 この機能により、JSON ファイルまたは文字列内の要素に対する読み取り専用のランダムアクセスが可能になります。 

## <a name="how-to-get-the-library"></a>ライブラリを取得する方法

* このライブラリは、 [.Net Core 3.0](https://aka.ms/netcore3download)共有フレームワークの一部として組み込まれています。
* その他のターゲットフレームワークの場合[は、System.string NuGet パッケージ](https://www.nuget.org/packages/System.Text.Json)をインストールします。 パッケージは次をサポートします。
  * .NET Standard 2.0 以降のバージョン
  * 4\.7.2 以降のバージョンの .NET Framework
  * .NET Core 2.0、2.1、および2.2

## <a name="additional-resources"></a>その他の技術情報

* [ライブラリの使用方法](system-text-json-how-to.md)
* [Newtonsoft. Json から移行する方法](system-text-json-migrate-from-newtonsoft-how-to.md)
* [方法 (コンバーターを記述する)](system-text-json-converters-how-to.md)
* [System.string のソースコード](https://github.com/dotnet/runtime/tree/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/libraries/System.Text.Json)
* [System.string API リファレンス](xref:System.Text.Json)
* [Text. Json. Serialization API リファレンス](xref:System.Text.Json.Serialization)
<!-- * [Roadmap](https://github.com/dotnet/runtime/blob/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/libraries/System.Text.Json/roadmap/README.md)-->
