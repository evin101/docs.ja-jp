---
title: ICorDebugVariableHomeEnum インターフェイス
ms.date: 03/30/2017
api_name:
- ICorDebugVariableHomeEnum
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugVariableHomeEnum
helpviewer_keywords:
- ICorDebugVariableHomeEnum interface [.NET Framework debugging]
ms.assetid: c312ae6d-c8dc-48d6-9f1e-ead515c88fdf
topic_type:
- apiref
ms.openlocfilehash: a9b65449747fde42f9cd770e33741ef34d33fbb8
ms.sourcegitcommit: 559fcfbe4871636494870a8b716bf7325df34ac5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/30/2019
ms.locfileid: "73121030"
---
# <a name="icordebugvariablehomeenum-interface"></a>ICorDebugVariableHomeEnum インターフェイス
関数のローカル変数および引数に列挙子を提供します。  
  
## <a name="methods"></a>メソッド  
  
|メソッド|説明|  
|------------|-----------------|  
|[Next メソッド](../../../../docs/framework/unmanaged-api/debugging/icordebugvariablehomeenum-next-method.md)|関数内のローカル変数および引数に関する情報を格納している指定された数の表示変数[home](../../../../docs/framework/unmanaged-api/debugging/icordebugvariablehome-interface.md)インスタンスを取得します。|  
  
## <a name="remarks"></a>Remarks  
 `ICorDebugVariableHomeEnum` インターフェイスは、ICorDebugEnum インターフェイスを実装します。  
  
 [ICorDebugCode4:: EnumerateVariableHomes](../../../../docs/framework/unmanaged-api/debugging/icordebugcode4-enumeratevariablehomes-method.md)メソッドを呼び出すことによって、`ICorDebugVariableHomeEnum` インスタンスには、表示[変数 home](../../../../docs/framework/unmanaged-api/debugging/icordebugvariablehome-interface.md)インスタンスが設定されます。 コレクション内[の各は](../../../../docs/framework/unmanaged-api/debugging/icordebugvariablehome-interface.md)、関数のローカル変数または引数を表します。 コレクション内[のオブジェクトを](../../../../docs/framework/unmanaged-api/debugging/icordebugvariablehome-interface.md)列挙するには、[次](../../../../docs/framework/unmanaged-api/debugging/icordebugvariablehomeenum-next-method.md)のように指定します。  
  
## <a name="requirements"></a>［要件］  
 **:** 「[システム要件](../../../../docs/framework/get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:** [!INCLUDE[net_current_v462plus](../../../../includes/net-current-v462plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICorDebugVariableHome インターフェイス](../../../../docs/framework/unmanaged-api/debugging/icordebugvariablehome-interface.md)
- [デバッグ インターフェイス](../../../../docs/framework/unmanaged-api/debugging/debugging-interfaces.md)
