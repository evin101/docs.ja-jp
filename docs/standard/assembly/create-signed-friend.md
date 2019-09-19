---
title: '方法: 署名されたフレンド アセンブリを作成する'
ms.date: 08/19/2019
ms.assetid: bab62063-61e6-453f-905f-77673df9534e
dev_langs:
- csharp
- vb
ms.openlocfilehash: 19c301c6b96e1070447401af9105fba2e0f0837f
ms.sourcegitcommit: 7b1ce327e8c84f115f007be4728d29a89efe11ef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/13/2019
ms.locfileid: "70972811"
---
# <a name="how-to-create-signed-friend-assemblies"></a><span data-ttu-id="a6abd-102">方法: 署名されたフレンド アセンブリを作成する</span><span class="sxs-lookup"><span data-stu-id="a6abd-102">How to: Create signed friend assemblies</span></span>
<span data-ttu-id="a6abd-103">この例では、厳密な名前を持つアセンブリと共にフレンド アセンブリを使用する方法を示します。</span><span class="sxs-lookup"><span data-stu-id="a6abd-103">This example shows how to use friend assemblies with assemblies that have strong names.</span></span> <span data-ttu-id="a6abd-104">両方のアセンブリに厳密な名前が付けられている必要があります。</span><span class="sxs-lookup"><span data-stu-id="a6abd-104">Both assemblies must be strong named.</span></span> <span data-ttu-id="a6abd-105">この例のアセンブリは両方とも同じキーを使用していますが、2 つのアセンブリそれぞれが別々のキーを使用することもできます。</span><span class="sxs-lookup"><span data-stu-id="a6abd-105">Although both assemblies in this example use the same keys, you could use different keys for two assemblies.</span></span>  
  
## <a name="create-a-signed-assembly-and-a-friend-assembly"></a><span data-ttu-id="a6abd-106">署名付きアセンブリとフレンド アセンブリを作成する</span><span class="sxs-lookup"><span data-stu-id="a6abd-106">Create a signed assembly and a friend assembly</span></span>  
  
1. <span data-ttu-id="a6abd-107">コマンド プロンプトを開きます。</span><span class="sxs-lookup"><span data-stu-id="a6abd-107">Open a command prompt.</span></span>  
  
2. <span data-ttu-id="a6abd-108">厳密な名前ツールで次のコマンド シーケンスを使用して、キー ファイルを生成し、公開鍵を表示します。</span><span class="sxs-lookup"><span data-stu-id="a6abd-108">Use the following sequence of commands with the Strong Name tool to generate a keyfile and to display its public key.</span></span> <span data-ttu-id="a6abd-109">詳細については、「[Sn.exe (厳密名ツール)](../../framework/tools/sn-exe-strong-name-tool.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="a6abd-109">For more information, see [Sn.exe (Strong Name tool)](../../framework/tools/sn-exe-strong-name-tool.md).</span></span>  
  
    1. <span data-ttu-id="a6abd-110">この例で使用する厳密な名前キーを生成し、*FriendAssemblies.snk* ファイルに格納します。</span><span class="sxs-lookup"><span data-stu-id="a6abd-110">Generate a strong-name key for this example and store it in the file *FriendAssemblies.snk*:</span></span>  
  
         `sn -k FriendAssemblies.snk`  
  
    2. <span data-ttu-id="a6abd-111">*FriendAssemblies.snk* から公開鍵を抽出し、*FriendAssemblies.publickey* に追加します。</span><span class="sxs-lookup"><span data-stu-id="a6abd-111">Extract the public key from *FriendAssemblies.snk* and put it into *FriendAssemblies.publickey*:</span></span>  
  
         `sn -p FriendAssemblies.snk FriendAssemblies.publickey`  
  
    3. <span data-ttu-id="a6abd-112">*FriendAssemblies.publickey* ファイルに格納されている公開鍵を表示します。</span><span class="sxs-lookup"><span data-stu-id="a6abd-112">Display the public key stored in the file *FriendAssemblies.publickey*:</span></span>  
  
         `sn -tp FriendAssemblies.publickey`  
  
3. <span data-ttu-id="a6abd-113">次のコードを含む、*friend_signed_A* という名前の C# または Visual Basic ファイルを作成します。</span><span class="sxs-lookup"><span data-stu-id="a6abd-113">Create a C# or Visual Basic file named *friend_signed_A* that contains the following code.</span></span> <span data-ttu-id="a6abd-114">コードでは <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute> 属性を使用して、フレンド アセンブリとして *friend_signed_B* を宣言します。</span><span class="sxs-lookup"><span data-stu-id="a6abd-114">The code uses the <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute> attribute to declare *friend_signed_B* as a friend assembly.</span></span>  
   
   <span data-ttu-id="a6abd-115">厳密な名前ツールは、実行するごとに新しい公開鍵を生成します。</span><span class="sxs-lookup"><span data-stu-id="a6abd-115">The Strong Name tool generates a new public key every time it runs.</span></span> <span data-ttu-id="a6abd-116">このため、次の例に示すコード内の公開鍵を、ここで生成した公開鍵に置き換える必要があります。</span><span class="sxs-lookup"><span data-stu-id="a6abd-116">Therefore, you must replace the public key in the following code with the public key you just generated, as shown in the following example.</span></span>  
   
   ```csharp  
   // friend_signed_A.cs  
   // Compile with:   
   // csc /target:library /keyfile:FriendAssemblies.snk friend_signed_A.cs  
   using System.Runtime.CompilerServices;  
   
   [assembly: InternalsVisibleTo("friend_signed_B, PublicKey=0024000004800000940000000602000000240000525341310004000001000100e3aedce99b7e10823920206f8e46cd5558b4ec7345bd1a5b201ffe71660625dcb8f9a08687d881c8f65a0dcf042f81475d2e88f3e3e273c8311ee40f952db306c02fbfc5d8bc6ee1e924e6ec8fe8c01932e0648a0d3e5695134af3bb7fab370d3012d083fa6b83179dd3d031053f72fc1f7da8459140b0af5afc4d2804deccb6")]  
   class Class1  
   {  
       public void Test()  
       {  
           System.Console.WriteLine("Class1.Test");  
           System.Console.ReadLine();  
       }  
   }  
   ```  
   
   ```vb  
   ' friend_signed_A.vb  
   ' Compile with:   
   ' Vbc -target:library -keyfile:FriendAssemblies.snk friend_signed_A.vb  
   Imports System.Runtime.CompilerServices  
   
   <Assembly: InternalsVisibleTo("friend_signed_B, PublicKey=0024000004800000940000000602000000240000525341310004000001000100e3aedce99b7e10823920206f8e46cd5558b4ec7345bd1a5b201ffe71660625dcb8f9a08687d881c8f65a0dcf042f81475d2e88f3e3e273c8311ee40f952db306c02fbfc5d8bc6ee1e924e6ec8fe8c01932e0648a0d3e5695134af3bb7fab370d3012d083fa6b83179dd3d031053f72fc1f7da8459140b0af5afc4d2804deccb6")>   
   Public Class Class1  
       Public Sub Test()  
           System.Console.WriteLine("Class1.Test")  
           System.Console.ReadLine()  
       End Sub  
   End Class  
   ```  
   
4. <span data-ttu-id="a6abd-117">次のコマンドを使用して *friend_signed_A* をコンパイルして署名します。</span><span class="sxs-lookup"><span data-stu-id="a6abd-117">Compile and sign *friend_signed_A* by using the following command.</span></span>  
   
   ```csharp
   csc /target:library /keyfile:FriendAssemblies.snk friend_signed_A.cs  
   ```  
   
   ```vb
   Vbc -target:library -keyfile:FriendAssemblies.snk friend_signed_A.vb  
   ```  
   
5. <span data-ttu-id="a6abd-118">次のコードを含む、*friend_signed_B* という名前の C# または Visual Basic ファイルを作成します。</span><span class="sxs-lookup"><span data-stu-id="a6abd-118">Create a C# or Visual Basic file named *friend_signed_B* that contains the following code.</span></span> <span data-ttu-id="a6abd-119">*friend_signed_A* で *friend_signed_B* がフレンド アセンブリとして指定されているため、*friend_signed_B* 内のコードは、*friend_signed_A* の `internal` (C#) または `Friend` (Visual Basic) 型とメンバーにアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="a6abd-119">Because *friend_signed_A* specifies *friend_signed_B* as a friend assembly, the code in *friend_signed_B* can access `internal` (C#) or `Friend` (Visual Basic) types and members from *friend_signed_A*.</span></span> <span data-ttu-id="a6abd-120">このファイルには、次のコードが含まれています。</span><span class="sxs-lookup"><span data-stu-id="a6abd-120">The file contains the following code.</span></span>  
   
   ```csharp  
   // friend_signed_B.cs  
   // Compile with:   
   // csc /keyfile:FriendAssemblies.snk /r:friend_signed_A.dll /out:friend_signed_B.exe friend_signed_B.cs  
   public class Program  
   {  
       static void Main()  
       {  
           Class1 inst = new Class1();  
           inst.Test();  
       }  
   }  
   ```  
   
   ```vb  
   ' friend_signed_B.vb  
   ' Compile with:   
   ' Vbc -keyfile:FriendAssemblies.snk -r:friend_signed_A.dll friend_signed_B.vb  
   Module Sample  
       Public Sub Main()  
           Dim inst As New Class1  
           inst.Test()  
       End Sub  
   End Module  
   ```  
   
6. <span data-ttu-id="a6abd-121">次のコマンドを使用して *friend_signed_B* をコンパイルして署名します。</span><span class="sxs-lookup"><span data-stu-id="a6abd-121">Compile and sign *friend_signed_B* by using the following command.</span></span>  
   
   ```csharp
   csc /keyfile:FriendAssemblies.snk /r:friend_signed_A.dll /out:friend_signed_B.exe friend_signed_B.cs  
   ```  
   
   ```vb
   vbc -keyfile:FriendAssemblies.snk -r:friend_signed_A.dll friend_signed_B.vb  
   ```  
   
   <span data-ttu-id="a6abd-122">コンパイラによって生成されたアセンブリの名前は、<xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute> 属性に渡されたフレンド アセンブリ名と一致している必要があります。</span><span class="sxs-lookup"><span data-stu-id="a6abd-122">The name of the assembly generated by the compiler must match the friend assembly name passed to the <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute> attribute.</span></span> <span data-ttu-id="a6abd-123">`/out` コンパイラ オプションを使用して、出力アセンブリ ( *.exe* または *.dll*) の名前を明示的に指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a6abd-123">You must explicitly specify the name of the output assembly (*.exe* or *.dll*) by using the `/out` compiler option.</span></span> <span data-ttu-id="a6abd-124">詳細については、「[/out (C# コンパイラ オプション)](../../csharp/language-reference/compiler-options/out-compiler-option.md)」または「[-out (Visual Basic)](../../visual-basic/reference/command-line-compiler/out.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="a6abd-124">For more information, see [/out (C# compiler options)](../../csharp/language-reference/compiler-options/out-compiler-option.md) or [-out (Visual Basic)](../../visual-basic/reference/command-line-compiler/out.md).</span></span>  
   
7. <span data-ttu-id="a6abd-125">*friend_signed_B.exe* ファイルを実行します。</span><span class="sxs-lookup"><span data-stu-id="a6abd-125">Run the *friend_signed_B.exe* file.</span></span>  
   
   <span data-ttu-id="a6abd-126">そのプログラムでは、**Class1.Test** という文字列が出力されます。</span><span class="sxs-lookup"><span data-stu-id="a6abd-126">The program outputs the string **Class1.Test**.</span></span>  
  
## <a name="net-security"></a><span data-ttu-id="a6abd-127">.NET セキュリティ</span><span class="sxs-lookup"><span data-stu-id="a6abd-127">.NET security</span></span>  
 <span data-ttu-id="a6abd-128"><xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute> 属性と <xref:System.Security.Permissions.StrongNameIdentityPermission> クラスには類似点があります。</span><span class="sxs-lookup"><span data-stu-id="a6abd-128">There are similarities between the <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute> attribute and the <xref:System.Security.Permissions.StrongNameIdentityPermission> class.</span></span> <span data-ttu-id="a6abd-129">主な違いは、<xref:System.Security.Permissions.StrongNameIdentityPermission> ではセキュリティ アクセス許可を要求することで特定のコード セクションを実行できますが、<xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute> 属性では `internal` (C#) または `Friend` (Visual Basic) 型とメンバーの参照可能範囲が制御されることです。</span><span class="sxs-lookup"><span data-stu-id="a6abd-129">The main difference is that <xref:System.Security.Permissions.StrongNameIdentityPermission> can demand security permissions to run a particular section of code, whereas the <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute> attribute controls the visibility of `internal` (C#) or `Friend` (Visual Basic) types and members.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="a6abd-130">関連項目</span><span class="sxs-lookup"><span data-stu-id="a6abd-130">See also</span></span>

- <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute>
- [<span data-ttu-id="a6abd-131">.NET のアセンブリ</span><span class="sxs-lookup"><span data-stu-id="a6abd-131">Assemblies in .NET</span></span>](index.md)
- [<span data-ttu-id="a6abd-132">フレンド アセンブリ</span><span class="sxs-lookup"><span data-stu-id="a6abd-132">Friend assemblies</span></span>](friend.md)
- [<span data-ttu-id="a6abd-133">方法: 署名のないフレンド アセンブリを作成する</span><span class="sxs-lookup"><span data-stu-id="a6abd-133">How to: Create unsigned friend assemblies</span></span>](create-unsigned-friend.md)
- [<span data-ttu-id="a6abd-134">/keyfile (C#)</span><span class="sxs-lookup"><span data-stu-id="a6abd-134">/keyfile (C#)</span></span>](../../csharp/language-reference/compiler-options/keyfile-compiler-option.md)
- [<span data-ttu-id="a6abd-135">-keyfile (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="a6abd-135">-keyfile (Visual Basic)</span></span>](../../visual-basic/reference/command-line-compiler/keyfile.md)
- [<span data-ttu-id="a6abd-136">Sn.exe (厳密名ツール)</span><span class="sxs-lookup"><span data-stu-id="a6abd-136">Sn.exe (Strong Name tool)</span></span>](../../framework/tools/sn-exe-strong-name-tool.md)
- [<span data-ttu-id="a6abd-137">厳密な名前付きアセンブリの作成と使用</span><span class="sxs-lookup"><span data-stu-id="a6abd-137">Create and use strong-named assemblies</span></span>](create-use-strong-named.md)
- [<span data-ttu-id="a6abd-138">C# プログラミング ガイド</span><span class="sxs-lookup"><span data-stu-id="a6abd-138">C# programming guide</span></span>](../../csharp/programming-guide/index.md)
- [<span data-ttu-id="a6abd-139">プログラミングの概念 (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="a6abd-139">Programming concepts (Visual Basic)</span></span>](../../visual-basic/programming-guide/concepts/index.md)