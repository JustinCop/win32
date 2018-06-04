---
Description: Context requirements are expressed as a combination of bit flags passed to either the InitializeSecurityContext (General) or AcceptSecurityContext (General) function.
ms.assetid: 4a44b829-4202-46c0-b17e-04943fa067ab
title: Context Requirements
ms.technology: desktop
ms.prod: windows
ms.author: windowssdkdev
ms.topic: article
ms.date: 05/31/2018
---

# Context Requirements

Context requirements are expressed as a combination of bit flags passed to either the [**InitializeSecurityContext (General)**](/windows/desktop/api/Sspi/) or [**AcceptSecurityContext (General)**](/windows/desktop/api/Sspi/) function. These flags affect the [*context*](https://msdn.microsoft.com/library/windows/desktop/ms721572#-security-context-gly) in a number of ways. Not all flags apply to all contexts. Some are valid only for the server, others only for the client.

The caller uses the *fContextReq* parameter of the [**InitializeSecurityContext (General)**](/windows/desktop/api/Sspi/) or [**AcceptSecurityContext (General)**](/windows/desktop/api/Sspi/) call to specify a set of flags that indicate the required capabilities. When the function returns, the *pfContextAttr* parameter indicates the attributes of the established context. The caller determines whether the final context attributes are acceptable.

Flags requested from or returned by [**InitializeSecurityContext (General)**](/windows/desktop/api/Sspi/) are prefixed by ISC. Those requested from or returned by [**AcceptSecurityContext (General)**](/windows/desktop/api/Sspi/) are prefixed by ASC. Flags passed into a function include REQ, while returned flags include RET. For example, a request flag for mutual authentication passed to **InitializeSecurityContext (General)** is ISC\_REQ\_MUTUAL\_AUTH. A server requesting mutual authentication passes ASC\_REQ\_MUTUAL\_AUTH to **AcceptSecurityContext (General)**. If mutual authentication is achieved, **InitializeSecurityContext (General)** returns ISC\_RET\_MUTUAL\_AUTH and **AcceptSecurityContext (General)** returns ASC\_RET\_MUTUAL\_AUTH. If the caller requests mutual authentication, but the [*security package*](https://msdn.microsoft.com/library/windows/desktop/ms721625#-security-security-package-gly) indicates that it cannot be performed, the caller must decide whether to cancel the context or continue.

The following table describes the various context requirement flags.



| Flag                             | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
|----------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| DELEGATE<br/>              | The server in the transport application can build new security contexts impersonating the client that will be accepted by other servers as the client's contexts. Delegate works only if MUTUAL\_AUTH is set. DELEGATE is currently supported only by [*Kerberos*](https://msdn.microsoft.com/library/windows/desktop/ms721590#-security-kerberos-protocol-gly). Further, Kerberos will delegate only to a server that has the flag TRUSTED\_FOR\_DELEGATION. Do not use this flag for [*constrained delegation*](https://msdn.microsoft.com/library/windows/desktop/ms721572#-security-constrained-delegation-gly).<br/> |
| MUTUAL\_AUTH<br/>          | The communicating parties must authenticate their identities to each other. Without MUTUAL\_AUTH, the client authenticates its identity to the server. With MUTUAL\_AUTH, the server also must authenticate its identity to the client.<br/> When using the [*Schannel*](https://msdn.microsoft.com/library/windows/desktop/ms721625#-security-schannel-gly) security package, the server sets the **ASC\_RET\_MUTUAL\_AUTH** constant only in the last call to [**AcceptSecurityContext (Negotiate)**](/windows/desktop/api/Sspi/), after certificate mapping has successfully completed.<br/>           |
| REPLAY\_DETECT<br/>        | The [*security package*](https://msdn.microsoft.com/library/windows/desktop/ms721625#-security-security-package-gly) detects replayed packets and notifies the caller if a packet has been replayed. The use of this flag implies all of the conditions specified by the INTEGRITY flag.<br/>                                                                                                                                                                                                                                                                                                                      |
| SEQUENCE\_DETECT<br/>      | The context must be allowed to detect out-of-order delivery of packets later through the message support functions. Use of this flag implies all of the conditions specified by the INTEGRITY flag.<br/>                                                                                                                                                                                                                                                                                                                                                                                             |
| CONFIDENTIALITY<br/>       | The context can protect data while in transit using the [**EncryptMessage (General)**](/windows/desktop/api/Sspi/) and [**DecryptMessage (General)**](/windows/desktop/api/Sspi/) functions. The CONFIDENTIALITY flag does not work if the generated context is for the Guest account.<br/>                                                                                                                                                                                                                                                                                                      |
| USE\_SESSION\_KEY<br/>     | A new [*session key*](https://msdn.microsoft.com/library/windows/desktop/ms721625#-security-session-key-gly) must be negotiated.<br/>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| PROMPT\_FOR\_CREDS<br/>    | If the client is an interactive user, the security package must, if possible, prompt the user for the appropriate [*credentials*](https://msdn.microsoft.com/library/windows/desktop/ms721572#-security-credentials-gly).<br/>                                                                                                                                                                                                                                                                                                                                                                                          |
| USE\_SUPPLIED\_CREDS<br/>  | Package-specific credential information is available in the input buffer. The security package can use these [*credentials*](https://msdn.microsoft.com/library/windows/desktop/ms721572#-security-credentials-gly) to authenticate the connection.<br/>                                                                                                                                                                                                                                                                                                                                                                |
| SAVE\_SUPPLIED\_CREDS<br/> | The supplied credentials should be cached with the supplemental credentials.<br/>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| ALLOCATE\_MEMORY<br/>      | The [*security package*](https://msdn.microsoft.com/library/windows/desktop/ms721625#-security-security-package-gly) must allocate memory. The caller must eventually call the [**FreeContextBuffer**](/windows/desktop/api/Sspi/nf-sspi-freecontextbuffer) function to free memory allocated by the security package.<br/>                                                                                                                                                                                                                                                                                                                      |
| USE\_DCE\_STYLE<br/>       | The caller expects a three-leg authentication [*transaction*](https://msdn.microsoft.com/library/windows/desktop/ms721627#-security-transaction-gly).<br/>                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| DATAGRAM<br/>              | [*Datagram*](https://msdn.microsoft.com/library/windows/desktop/ms721573#-security-datagram-gly) semantics must be used. For more information, see [Datagram Contexts](datagram-contexts.md).<br/>                                                                                                                                                                                                                                                                                                                                                                                                                        |
| CONNECTION<br/>            | Connection semantics must be used. For more information, see [Connection-Oriented Contexts](connection-oriented-contexts.md).<br/>                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| STREAM<br/>                | Stream semantics must be used. For more information, see [Stream Contexts](stream-contexts.md).<br/>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| EXTENDED\_ERROR<br/>       | Error reply messages for the peer must be generated if the context fails.<br/>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| INTEGRITY<br/>             | Buffer integrity can be verified but no sequencing or reply detection is enabled.<br/>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| NO\_INTEGRITY<br/>         | The **INTEGRITY** requirement is ignored.<br/>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| IDENTIFY<br/>              | When a server impersonates a context that has this flag set, that impersonation yields extremely limited access. Impersonation with IDENTIFY set is used to verify the client's identity.<br/>                                                                                                                                                                                                                                                                                                                                                                                                       |



 

 

 



