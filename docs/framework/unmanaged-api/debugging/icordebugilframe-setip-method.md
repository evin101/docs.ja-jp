---
title: ICorDebugILFrame::SetIP メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugILFrame.SetIP
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugILFrame::SetIP
helpviewer_keywords:
- SetIP method, ICorDebugILFrame interface [.NET Framework debugging]
- ICorDebugILFrame::SetIP method [.NET Framework debugging]
ms.assetid: 23f38dc1-85e4-4263-9235-2d05bbb6a833
topic_type:
- apiref
ms.openlocfilehash: 60273d7cf91be04c5fc3041260e4bb146ce9a45e
ms.sourcegitcommit: 559fcfbe4871636494870a8b716bf7325df34ac5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/30/2019
ms.locfileid: "73095431"
---
# <a name="icordebugilframesetip-method"></a>ICorDebugILFrame::SetIP メソッド
命令ポインターを Microsoft 中間言語 (MSIL) コード内の指定されたオフセット位置に設定します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT SetIP (  
    [in] ULONG32 nOffset  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `nOffset`  
 MSIL コード内のオフセット位置。  
  
## <a name="remarks"></a>Remarks  
 `SetIP` を呼び出すと、現在のスレッドのすべてのフレームとチェーンがすぐに無効になります。 `SetIP`の呼び出しの後にデバッガーがフレーム情報を必要とする場合は、新しいスタックトレースを実行する必要があります。  
  
 [ICorDebug](../../../../docs/framework/unmanaged-api/debugging/icordebug-interface.md)は、スタックフレームを有効な状態のままにします。 ただし、フレームが有効な状態であっても、初期化されていないローカル変数などの問題が発生する可能性があります。 呼び出し元は、実行中のプログラムの一貫性を確保する役割を担います。  
  
 64ビットプラットフォームでは、命令ポインターを `catch` または `finally` ブロックの外に移動することはできません。 64ビットプラットフォーム上でこのような移動を行うために `SetIP` を呼び出すと、失敗を示す HRESULT が返されます。  
  
## <a name="requirements"></a>［要件］  
 **:** 「[システム要件](../../../../docs/framework/get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
