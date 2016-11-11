---
title: TLS (Scahannel SSP)
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
ms.assetid: ebd3c40c-b4c0-4f6d-a00c-f90eda4691df
manager: alanth
author: justinha
ms.technology: security-authentication
ms.date: 11/09/2016
---

# TLS (Schannel SSP) changes in Windows 10 and Windows Server 2016

>Applies To: Windows Server 2016 and Windows 10

## Cipher Suite Changes

Windows 10, version 1511 and Windows Server 2016 add support for configuration of cipher suite order using Mobile Device Management (MDM).

For cipher suite priority order changes, see [Cipher Suites in Schannel](https://msdn.microsoft.com/library/windows/desktop/aa374757.aspx).

Added support for the following cipher suites:

- TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256 (RFC 5289) in Windows 10, version 1507 and Windows Server 2016
- TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384 (RFC 5289) in Windows 10, version 1507 and Windows Server 2016

Starting with Windows 10, version 1507 and Windows Server 2016, SHA 512 certificates are supported by default.

### RSA key changes

Windows 10, version 1507 and Windows Server 2016 add registry configuration options for client RSA key sizes.

Registry path: 

HKLM\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\KeyExchangeAlgorithms\PKCS
 
To specify a minimum supported range of RSA key bit length for the TLS client, create a **ClientMinKeyBitLength** entry. 
This entry does not exist in the registry by default. 
After you have created the entry, change the DWORD value to the desired bit length. 
If not configured, 1024 bits will be the minimum. 
 
To specify a maximum supported range of RSA key bit length for the TLS client, create a **ClientMaxKeyBitLength** entry. 
This entry does not exist in the registry by default. 
After you have created the entry, change the DWORD value to the desired bit length. 
If not configured, then a maximum is not enforced. 

### Diffie-Hellman key changes

Windows 10, version 1507 and Windows Server 2016 add registry configuration options for Diffie-Hellman key sizes.

Registry path: 

HKLM\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\KeyExchangeAlgorithms\Diffie-Hellman
 
To specify a minimum supported range of Diffie-Helman key bit length for the TLS client, create a **ClientMinKeyBitLength** entry. 
This entry does not exist in the registry by default. 
After you have created the entry, change the DWORD value to the desired bit length. 
If not configured, 1024 bits will be the minimum. 
 
To specify a maximum supported range of Diffie-Helman key bit length for the TLS client, create a **ClientMaxKeyBitLength** entry. 
This entry does not exist in the registry by default. 
After you have created the entry, change the DWORD value to the desired bit length. 
If not configured, then a maximum is not enforced. 
 
To specify the Diffie-Helman key bit length for the TLS server default, create a **ServerMinKeyBitLength** entry. 
This entry does not exist in the registry by default. 
After you have created the entry, change the DWORD value to the desired bit length. 
If not configured, 2048 bits will be the default. 

### SCH_USE_STRONG_CRYPTO option changes

With Windows 10, version 1507 and Windows Server 2016, [SCH_USE_STRONG_CRYPTO](https://msdn.microsoft.com/library/windows/desktop/aa379810.aspx) option now disables NULL, MD5, DES, and export ciphers.

## Elliptical Curve changes

Windows 10, version 1507 and Windows Server 2016 add Group Policy configuration for elliptical curves under Computer Configuration > Administrative Templates > Network > SSL Configuration Settings. 
The ECC Curve Order list specifies the order in which elliptical curves are preferred as well as enables supported curves which are not enabled. 
 
Added support for the following elliptical curves:

- BrainpoolP256r1 (RFC 7027) in Windows 10, version 1507 and Windows Server 2016
- BrainpoolP384r1 (RFC 7027) in Windows 10, version 1507 and Windows Server 2016 
- BrainpoolP512r1 (RFC 7027) in Windows 10, version 1507 and Windows Server 2016
- Curve25519 (RFC draft-ietf-tls-curve25519) in Windows 10, version 1607 and Windows Server 2016

## Dispatch level support for SealMessage & UnsealMessage

Windows 10, version 1507 and Windows Server 2016 add support for SealMessage/UnsealMessage at dispatch level.

## DTLS 1.2

Windows 10, version 1607 and Windows Server 2016 add support for DTLS 1.2 (RFC 6347).

## HTTP.SYS thread pool 

Windows 10, version 1607 and Windows Server 2016 add registry configuration of the size of the thread pool used to handle TLS handshakes for HTTP.SYS.

Registry path: 

HKLM\SYSTEM\CurrentControlSet\Control\LSA

To specify a maximum thread pool size per CPU core, create a **MaxAsyncWorkerThreadsPerCpu** entry. 
This entry does not exist in the registry by default. 
After you have created the entry, change the DWORD value to the desired size. 
If not configured, then the maximum is 2 threads per CPU core.

## Pre-Shared Key (PSK)

Windows 10, version 1607 and Windows Server 2016 add support for PSK key exchange algorithm (RFC 4279).

Added support for the following PSK cipher suites:

- TLS_PSK_WITH_AES_128_CBC_SHA256 (RFC 5487) in Windows 10, version 1607 and Windows Server 2016
- TLS_PSK_WITH_AES_256_CBC_SHA384(RFC 5487) in Windows 10, version 1607 and Windows Server 2016
- TLS_PSK_WITH_NULL_SHA256 (RFC 5487) in Windows 10, version 1607 and Windows Server 2016
- TLS_PSK_WITH_NULL_SHA384 (RFC 5487) in Windows 10, version 1607 and Windows Server 2016
- TLS_PSK_WITH_AES_128_GCM_SHA256 (RFC 5487) in Windows 10, version 1607 and Windows Server 2016
- TLS_PSK_WITH_AES_256_GCM_SHA384 (RFC 5487) in Windows 10, version 1607 and Windows Server 2016

## Session Resumption without Server-Side State server-side performance improvements

Windows 10, version 1507 and Windows Server 2016 provide 30% more session resumptions per second with session tickets compared to Windows Server 2012.

## Session Hash and Extended Master Secret Extension

Windows 10, version 1507 and Windows Server 2016 add support for RFC 7627: Transport Layer Security (TLS) Session Hash and Extended Master Secret Extension.

Due to this change, Windows 10 and Windows Server 2016 requires 3rd party [CNG SSL provider](https://msdn.microsoft.com/library/windows/desktop/ff468652.aspx) updates to support NCRYPT_SSL_INTERFACE_VERSION_3, and to describe this new interface.


## SSL support

Beginning with Windows 10, version 1607 and Windows Server 2016, the TLS client and server SSL 3.0 is disabled by default. 
This means that unless the application or service specifically requests SSL 3.0 via the SSPI, the client will never offer or accept SSL 3.0 and the server will never select SSL 3.0.

Beginning with Windows 10 version 1607 and Windows Server 2016, SSL 2.0 has been removed and is no longer supported.
