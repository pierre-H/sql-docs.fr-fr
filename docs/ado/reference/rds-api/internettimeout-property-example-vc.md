---
title: Exemple de propriété InternetTimeout (VC ++) | Documents Microsoft
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- InternetTimeout property [ADO], VC++ example
ms.assetid: 88b6d05c-d4eb-4ab1-bbe2-95d146237f94
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b6ea81924a976b47cae193acb8e57d94476cfd23
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
---
# <a name="internettimeout-property-example-vc"></a>Exemple de propriété InternetTimeout (VC ++)
> [!IMPORTANT]
>  À compter de Windows 8 et Windows Server 2012, les composants de serveur Services Bureau à distance ne sont plus inclus dans le système d’exploitation Windows (consultez Windows 8 et [Cookbook de compatibilité de Windows Server 2012](https://www.microsoft.com/en-us/download/details.aspx?id=27416) pour plus de détails). Composants du client Bureau à distance seront supprimées dans une future version de Windows. Évitez d'utiliser cette fonctionnalité dans de nouveaux travaux de développement, et prévoyez de modifier les applications qui utilisent actuellement cette fonctionnalité. La migration vers les applications qui utilisent des services Bureau à distance [Service de données WCF](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
 Cet exemple illustre la [InternetTimeout](../../../ado/reference/rds-api/internettimeout-property-rds.md) propriété qui existe sur le [DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) et [DataSpace](../../../ado/reference/rds-api/dataspace-object-rds.md) objets. Dans ce cas, le **InternetTimeout** propriété est présentée sur la **DataControl** objet et le délai d’attente est défini sur 20 secondes.  
  
```  
// BeginInternetTimeoutCpp  
#import "c:\Program Files\Common Files\System\ADO\msado15.dll" \  
    no_namespace rename("EOF", "EndOfFile")  
#import "C:\Program Files\Common Files\System\MSADC\msadco.dll"  
  
#include <ole2.h>  
#include <stdio.h>  
#include <conio.h>  
  
// Function declarations  
inline void TESTHR(HRESULT x) {if FAILED(x) _com_issue_error(x);};  
void InternetTimeOutX(void);  
void PrintProviderError(_ConnectionPtr pConnection);  
void PrintComError(_com_error &e);  
  
//////////////////////////////////////////////////////////  
//                                                      //  
//    Main Function                                     //  
//                                                      //  
//////////////////////////////////////////////////////////  
  
void main()  
{  
    if(FAILED(::CoInitialize(NULL)))  
        return;  
  
    InternetTimeOutX();  
  
    ::CoUninitialize();  
}  
  
//////////////////////////////////////////////////////////  
//                                                      //  
//         InternetTimeOutX Function                    //  
//                                                      //  
//////////////////////////////////////////////////////////  
  
void InternetTimeOutX(void)   
{  
    HRESULT hr = S_OK;  
  
    // Define ADO object pointers.  
    // Initialize pointers on define.  
    // These are in the ADODB::  namespace.  
    _RecordsetPtr  pRst = NULL;  
  
    //Define RDS object pointers  
    RDS::IBindMgrPtr dc ;  
  
    try  
    {  
        TESTHR(dc.CreateInstance(__uuidof(RDS::DataControl)));  
        dc->Server = "http://MyServer";  
        dc->Connect = "Data Source='AuthorDatabase'";  
        dc->SQL = "SELECT * FROM Authors";  
  
        // Wait at least 20 seconds.  
        dc->InternetTimeout = 20000;  
        dc->Refresh();  
  
        // Use another Recordset as a convenience  
        pRst = dc->GetRecordset();  
        while(!(pRst->EndOfFile))  
        {  
            printf("%s %s",(LPSTR) (_bstr_t) pRst->Fields->  
                GetItem("au_fname")->Value,  
               (LPSTR) (_bstr_t) pRst->Fields->  
                GetItem("au_lname")->Value);  
  
            pRst->MoveNext();  
        }  
        pRst->Close();  
    }  
  
    catch (_com_error &e)  
    {  
        PrintProviderError(pRst->GetActiveConnection());  
        PrintComError(e);  
    }  
}  
  
//////////////////////////////////////////////////////////  
//                                                      //  
//     PrintProviderError Function                      //  
//                                                      //  
//////////////////////////////////////////////////////////  
  
void PrintProviderError(_ConnectionPtr pConnection)  
{  
    // Print Provider Errors from Connection object.  
    // pErr is a record object in the Connection's Error collection.  
    ErrorPtr  pErr  = NULL;  
  
    if( (pConnection->Errors->Count) > 0)  
    {  
        long nCount = pConnection->Errors->Count;  
        // Collection ranges from 0 to nCount -1.  
        for(long i = 0; i < nCount; i++)  
        {  
            pErr = pConnection->Errors->GetItem(i);  
            printf("\t Error number: %x\t%s", pErr->Number,   
                pErr->Description);  
        }  
    }  
}  
  
//////////////////////////////////////////////////////////  
//                                                      //  
//     PrintComError Function                           //  
//                                                      //  
//////////////////////////////////////////////////////////  
  
void PrintComError(_com_error &e)  
{  
    _bstr_t bstrSource(e.Source());  
    _bstr_t bstrDescription(e.Description());  
  
    // Print Com errors.    
    printf("Error\n");  
    printf("\tCode = %08lx\n", e.Error());  
    printf("\tCode meaning = %s\n", e.ErrorMessage());  
    printf("\tSource = %s\n", (LPCSTR) bstrSource);  
    printf("\tDescription = %s\n", (LPCSTR) bstrDescription);  
}  
// EndInternetTimeoutCpp  
```  
  
## <a name="see-also"></a>Voir aussi  
 [InternetTimeout, propriété (RDS)](../../../ado/reference/rds-api/internettimeout-property-rds.md)


