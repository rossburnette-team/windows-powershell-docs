---
description: Use this topic to help manage Windows and Windows Server technologies with Windows PowerShell.
external help file: Microsoft.ActiveDirectory.Management.dll-Help.xml
Module Name: ActiveDirectory
ms.date: 12/27/2016
online version: https://docs.microsoft.com/powershell/module/activedirectory/revoke-adauthenticationpolicysiloaccess?view=windowsserver2019-ps&wt.mc_id=ps-gethelp
schema: 2.0.0
title: Revoke-ADAuthenticationPolicySiloAccess
---

# Revoke-ADAuthenticationPolicySiloAccess

## SYNOPSIS
Revokes membership in an authentication policy silo for the specified account.

## SYNTAX

```
Revoke-ADAuthenticationPolicySiloAccess [-WhatIf] [-Confirm] [-Account] <ADAccount> [-AuthType <ADAuthType>]
 [-Credential <PSCredential>] [-Identity] <ADAuthenticationPolicySilo> [-PassThru] [-Server <String>]
 [<CommonParameters>]
```

## DESCRIPTION
The **Revoke-ADAuthenticationPolicySiloAccess** cmdlet revokes the membership in an authentication policy silo for one or more accounts in Active Directory® Domain Services.

The *Identity* parameter specifies the Active Directory Domain Services authentication policy silo that contains the user accounts to remove.
You can identify an authentication policy silo by its distinguished name, GUID or name.
You can also use the *Identity* parameter to specify a variable that contains an authentication policy silo object, or you can use the pipeline operator to pass an authentication policy object to the *Identity* parameter.

The *Account* parameter specifies the users, computers and service accounts to remove from the authentication policy silo specified by the *Identity* parameter.
You can identify a user, computer or service account by its distinguished name, GUID, security identifier (SID), or Security Accounts Manager (SAM) account name.
You can also use the *Account* parameter to specify a variable that contains user, computer, and service account objects.

## EXAMPLES

### Example 1: Revoke access to an authentication policy silo
```
PS C:\> Revoke-ADAuthenticationPolicySiloAccess -Identity AuthenticationPolicySilo01 -Account User01 -Confirm:$False
```

This command revokes access to the authentication policy silo named AuthenticationPolicySilo01 for the user account named User01.
Because the *Confirm* parameter is set to $False, no confirmation message appears.

### Example 2: Revoke access to an authentication policy silo for filter matches
```
PS C:\> Get-ADComputer -Filter 'Name -like "newComputer*"' | Revoke-ADAuthenticationPolicySiloAccess -Identity AuthenticationPolicySilo02
Confirm
Are you sure you want to perform this action? 
Performing the operation "Set" on target "CN=Silo,CN=AuthN Silos,CN=AuthN PolicyConfiguration,CN=Services,CN=Configuration,DC=DC01,DC=Contoso,DC=com".
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "Y"): A
```

This command first uses the **Get-ADComputer** cmdlet to get a list of computers that match the filter specified by the Filter parameter.
The output is then passed to the **Revoke-ADAuthenticationPolicySiloAccess** to remove access to the authentication policy silo named AuthenticationPolicySilo02.
Because the *Confirm* parameter is not specified, a confirmation message appears.

## PARAMETERS

### -Account
Specifies the account to remove from the authentication policy silo.
Specify the account in one of the following formats: 

- A distinguished name
- GUID 
- security identifier 
- SAM account name

The cmdlet searches the default naming context or partition to find the object.
If two or more objects are found, the cmdlet returns a non-terminating error.

You can also use this parameter to specify a variable that contains user, computer, and service account objects.

```yaml
Type: ADAccount
Parameter Sets: (All)
Aliases: 

Required: True
Position: 1
Default value: None
Accept pipeline input: True (ByValue)
Accept wildcard characters: False
```

### -AuthType
Specifies the authentication method to use.
The acceptable values for this parameter are:

- Negotiate or 0
- Basic or 1

The default authentication method is Negotiate.
A Secure Sockets Layer (SSL) connection is required for the Basic authentication method.

```yaml
Type: ADAuthType
Parameter Sets: (All)
Aliases: 
Accepted values: Negotiate, Basic

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Confirm
Prompts you for confirmation before running the cmdlet.

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases: cf

Required: False
Position: Named
Default value: False
Accept pipeline input: False
Accept wildcard characters: False
```

### -Credential
Specifies a user account that has permission to perform the task.
The default is the current user.
Type a user name, such as User01 or Domain01\User01, or enter a **PSCredential** object, such as one generated by the **Get-Credential** cmdlet.

By default, the cmdlet uses the credentials of the currently logged on user unless the cmdlet is run from an Active Directory Domain Services Windows PowerShell provider drive.
If you run the cmdlet in a provider drive, the account associated with the drive is the default.

If you specify credentials that do not have permission to perform the task, the cmdlet returns an error.

```yaml
Type: PSCredential
Parameter Sets: (All)
Aliases: 

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Identity
Specifies an **ADAuthenticationPolicySilo** object.
Specify the authentication policy silo object in one of the following formats: 

- A distinguished name
- A GUID
- A name

This parameter can also get this object through the pipeline or you can set this parameter to an object instance.

The cmdlet searches the default naming context or partition to find the object.
If the cmdlet finds two or more objects, the cmdlet returns a non-terminating error.

```yaml
Type: ADAuthenticationPolicySilo
Parameter Sets: (All)
Aliases: 

Required: True
Position: 0
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -PassThru
Returns an object representing the item with which you are working.
By default, this cmdlet does not generate any output.

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases: 

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Server
Specifies the Active Directory Domain Services instance to which to connect, by providing one of the following values for a corresponding domain name or directory server.
The service may be any of the following:  Active Directory Lightweight Domain Services, Active Directory Domain Services or Active Directory snapshot instance.

Specify the Active Directory Domain Services instance in one of the following ways:  

Domain name values: 

- Fully qualified domain name
- NetBIOS name

Directory server values:  

- Fully qualified directory server name
- NetBIOS name
- Fully qualified directory server name and port

The default value for this parameter is determined by one of the following methods in the order that they are listed:

- By using the *Server* value from objects passed through the pipeline
- By using the server information associated with the Active Directory Domain Services Windows PowerShell provider drive, when the cmdlet runs in that drive
- By using the domain of the computer running Windows PowerShell

```yaml
Type: String
Parameter Sets: (All)
Aliases: 

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -WhatIf
Shows what would happen if the cmdlet runs.
The cmdlet is not run.

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases: wi

Required: False
Position: Named
Default value: False
Accept pipeline input: False
Accept wildcard characters: False
```

### CommonParameters
This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable. For more information, see [about_CommonParameters](https://go.microsoft.com/fwlink/?LinkID=113216).

## INPUTS

### None or Microsoft.ActiveDirectory.Management.ADAuthenticationPolicySilo
This cmdlet accepts an authentication policy silo object.

## OUTPUTS

### None or Microsoft.ActiveDirectory.Management.ADAuthenticationPolicySilo
This cmdlet returns the modified authentication policy silo object when the *PassThru* parameter is specified.
By default, this cmdlet does not generate any output.

## NOTES

## RELATED LINKS

[Grant-ADAuthenticationPolicySiloAccess](./Grant-ADAuthenticationPolicySiloAccess.md)

[AD DS Administration Cmdlets in Windows PowerShell](./activedirectory.md)
