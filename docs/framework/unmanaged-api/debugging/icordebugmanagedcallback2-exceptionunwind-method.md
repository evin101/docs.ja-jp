---
title: ICorDebugManagedCallback2::ExceptionUnwind メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugManagedCallback2.ExceptionUnwind
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugManagedCallback2::ExceptionUnwind
helpviewer_keywords:
- ICorDebugManagedCallback2::ExceptionUnwind method [.NET Framework debugging]
- ExceptionUnwind method [.NET Framework debugging]
ms.assetid: aaf5938d-179c-4eaa-8d35-8523a4fadded
topic_type:
- apiref
ms.openlocfilehash: fa317e1217ac0a9ca46bfeb312446534b1fca63a
ms.sourcegitcommit: 559fcfbe4871636494870a8b716bf7325df34ac5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/30/2019
ms.locfileid: "73131564"
---
# <a name="icordebugmanagedcallback2exceptionunwind-method"></a>ICorDebugManagedCallback2::ExceptionUnwind メソッド
例外アンワインド処理中の状態通知を提供します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT ExceptionUnwind (  
    [in] ICorDebugAppDomain                  *pAppDomain,  
    [in] ICorDebugThread                     *pThread,  
    [in] CorDebugExceptionUnwindCallbackType  dwEventType,  
    [in] DWORD                                dwFlags  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `pAppDomain`  
 から例外がスローされたスレッドを含むアプリケーションドメインを表す、のオブジェクトへのポインター。  
  
 `pThread`  
 から例外がスローされたスレッドを表す、スレッドオブジェクトへのポインター。  
  
 `dwEventType`  
 からアンワインドフェーズ中にコールバックによって通知されるイベントを指定する CorDebugExceptionUnwindCallbackType 列挙体の値。  
  
 `dwFlags`  
 から例外に関する追加情報を指定する[Cordebugexceptionflags](../../../../docs/framework/unmanaged-api/debugging/cordebugexceptionflags-enumeration.md)列挙体の値。  
  
## <a name="remarks"></a>Remarks  
 `ExceptionUnwind` は、例外処理プロセスのアンワインドフェーズ中にさまざまなポイントで呼び出されます。 1つの例外のアンワインド中に、`ExceptionUnwind` を複数回呼び出すことができます。  
  
 `dwEventType` = DEBUG_EXCEPTION_INTERCEPTED の場合、命令ポインターは、例外の原因となった命令の前 (これは複数の命令になることがあります) に、スレッドのリーフフレームに配置されます。  
  
## <a name="requirements"></a>［要件］  
 **:** 「[システム要件](../../../../docs/framework/get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICorDebugManagedCallback2 インターフェイス](../../../../docs/framework/unmanaged-api/debugging/icordebugmanagedcallback2-interface.md)
- [ICorDebugManagedCallback インターフェイス](../../../../docs/framework/unmanaged-api/debugging/icordebugmanagedcallback-interface.md)
