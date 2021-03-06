---
title: '方法: FTP を使用してファイルをアップロードする'
ms.date: 03/30/2017
ms.assetid: e40f17c5-dd12-4c62-9dbf-00ab491382dc
author: mcleblanc
ms.author: markl
manager: markl
ms.openlocfilehash: d032c171188f8a9536276c3cfe46392f90567bb3
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/04/2018
---
# <a name="how-to-upload-files-with-ftp"></a>方法: FTP を使用してファイルをアップロードする
このサンプルでは、FTP サーバーにファイルをアップロードする方法を示します。  
  
## <a name="example"></a>例  
  
```csharp  
using System;  
using System.IO;  
using System.Net;  
using System.Text;  
  
namespace Examples.System.Net  
{  
    public class WebRequestGetExample  
    {  
        public static void Main ()  
        {  
            // Get the object used to communicate with the server.  
            FtpWebRequest request = (FtpWebRequest)WebRequest.Create("ftp://www.contoso.com/test.htm");
            request.Method = WebRequestMethods.Ftp.UploadFile;

            // This example assumes the FTP site uses anonymous logon.  
            request.Credentials = new NetworkCredential("anonymous", "janeDoe@contoso.com");

            // Copy the contents of the file to the request stream.  
            byte[] fileContents;
            using (StreamReader sourceStream = new StreamReader("testfile.txt"))
            {
                fileContents = Encoding.UTF8.GetBytes(sourceStream.ReadToEnd());
            }
            
            request.ContentLength = fileContents.Length;

            using (Stream requestStream = request.GetRequestStream())
            {
                requestStream.Write(fileContents, 0, fileContents.Length);
            }

            using (FtpWebResponse response = (FtpWebResponse)request.GetResponse())
            {
                Console.WriteLine("Upload File Complete, status {0}", response.StatusDescription);
            }
        }  
    }  
}  
```  
  
## <a name="compiling-the-code"></a>コードのコンパイル  
 この例で必要な要素は次のとおりです。  
  
-   **System.Net** 名前空間への参照。  
  
## <a name="robust-programming"></a>信頼性の高いプログラミング  
  
## <a name="net-framework-security"></a>.NET Framework セキュリティ
