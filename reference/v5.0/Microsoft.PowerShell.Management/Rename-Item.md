---
external help file: PSITPro5_Management.xml
online version: http://go.microsoft.com/fwlink/p/?linkid=293901
schema: 2.0.0
---

# Rename-Item
## SYNOPSIS
Renames an item in a Windows PowerShell provider namespace.

## SYNTAX

### UNNAMED_PARAMETER_SET_1
```
Rename-Item [-Path] <String> [-NewName] <String> [-Credential <PSCredential>] [-Force] [-PassThru] [-Confirm]
 [-WhatIf] [-UseTransaction]
```

### UNNAMED_PARAMETER_SET_2
```
Rename-Item [-NewName] <String> [-Credential <PSCredential>] [-Force] [-PassThru] -LiteralPath <String>
 [-Confirm] [-WhatIf] [-UseTransaction]
```

## DESCRIPTION
The Rename-Item cmdlet changes the name of a specified item.
This cmdlet does not affect the content of the item being renamed.

You cannot use Rename-Item to move an item, such as by specifying a path together with the new name.
To move and rename an item, use the Move-Item cmdlet.

## EXAMPLES

### Example 1: Rename a file
```
PS C:\>Rename-Item -Path "c:\logfiles\daily_file.txt" -NewName "monday_file.txt"
```

This command renames the file daily_file.txt to monday_file.txt.

### Example 2: Rename and move an item
```
The first command attempts to rename the project.txt file in the current directory to old-project.txt in the D:\Archive directory. The result is the error shown in the output.
PS C:\>Rename-Item -Path "project.txt" -NewName "d:\archive\old-project.txt"
Rename-Item : Cannot rename because the target specified represents a path or device name. 
At line:1 char:12
+ rename-item <<<<  -path project.txt -newname d:\archive\old-project.txt
+ CategoryInfo          : InvalidArgument: (:) [Rename-Item], PSArgumentException
+ FullyQualifiedErrorId : Argument,Microsoft.PowerShell.Commands.RenameItemCommand

The second command shows the correct way to move and rename a file by using Move-Item. The Move-Item cmdlet lets you specify both a new path and a new name in the value of its Destination parameter.
PS C:\>Move-Item -Path "project.txt" -Destination "d:\archive\old-project.txt"
```

This example shows that you cannot use Rename-Item to both rename and move an item.
Specifically, you cannot supply a path for the value of the NewName parameter, unless the path is identical to the path specified in the Path parameter.
Otherwise, only a new name is permitted.

### Example 3: Rename a registry key
```
PS C:\>Rename-Item -Path "HKLM:\Software\MyCompany\Advertising" -NewName "Marketing"
```

This command renames a registry key from Advertising to Marketing.
When the command is complete, the key is renamed, but the registry entries in the key are unchanged.

### Example 4: Rename multiple files
```
PS C:\>Get-ChildItem *.txt | Rename-Item -NewName { $_.name -Replace '\.txt','.log' }
```

This example shows how to use the Replace operator to rename multiple files, even though the NewName parameter does not accept wildcard characters.

This command renames all of the .txt files in the current directory to .log.

The command uses the Get-ChildItem cmdlet to get all of the files in the current folder that have a .txt file name extension.
Then, it uses the pipeline operator (|) to send those files to Rename-Item.

The value of NewName is a script block that runs before the value is submitted to the NewName parameter.

In the script block, the $_ automatic variable represents each file object as it comes to the command through the pipeline.
The command uses the dot format (.) to get the Name property of each file object.
The Replace operator replaces the .txt file name extension of each file with .log.

Because the Replace operator works with regular expressions, the dot in front of txt is interpreted to match any character.
To make sure that it matches only a dot (.), it is escaped with a backslash character (\\).
The backslash character is not required in .log because it is a string, not a regular expression.

## PARAMETERS

### -Credential
Specifies a user account that has permission to perform this action.
The default is the current user.

Type a user name, such as User01 or Domain01\User01, or enter a PSCredential object, such as one generated by the Get-Credential cmdlet.
If you type a user name, this cmdlet prompts you for a password.

This parameter is not supported by any providers installed with Windows PowerShell.

```yaml
Type: PSCredential
Parameter Sets: (All)
Aliases: 

Required: False
Position: Named
Default value: None
Accept pipeline input: True (ByPropertyName)
Accept wildcard characters: False
```

### -Force
Forces the cmdlet to rename items that cannot otherwise be changed, such as hidden or read-only files or read-only aliases or variables.
The cmdlet cannot change constant aliases or variables.
Implementation varies from provider to provider.
For more information, see about_Providers.

Even using the Force parameter, the cmdlet cannot override security restrictions.

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

### -LiteralPath
Specifies the path of the item to rename.

Unlike the Path parameter, the value of LiteralPath is used exactly as it is typed.
No characters are interpreted as wildcard characters.
If the path includes escape characters, enclose it in single quotation marks.
Single quotation marks tell Windows PowerShell not to interpret any characters as escape sequences.

```yaml
Type: String
Parameter Sets: UNNAMED_PARAMETER_SET_2
Aliases: PSPath

Required: True
Position: Named
Default value: None
Accept pipeline input: True (ByPropertyName)
Accept wildcard characters: False
```

### -NewName
Specifies the new name of the item.
Enter only a name, not a path and name.
If you enter a path that differs from the path that is specified in the Path parameter, Rename-Item generates an error.
To rename and move an item, use Move-Item.

You cannot use wildcard characters in the value of the NewName parameter.
To specify a name for multiple files, use the Replace operator in a regular expression.
For more information about the Replace operator, see about_Comparison_Operators.

```yaml
Type: String
Parameter Sets: (All)
Aliases: 

Required: True
Position: 2
Default value: None
Accept pipeline input: True (ByPropertyName)
Accept wildcard characters: False
```

### -PassThru
Returns an object that represents the item to the pipeline.
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

### -Path
Specifies the path of the item to rename.

```yaml
Type: String
Parameter Sets: UNNAMED_PARAMETER_SET_1
Aliases: 

Required: True
Position: 1
Default value: None
Accept pipeline input: True (ByValue, ByPropertyName)
Accept wildcard characters: False
```

### -Confirm
Prompts you for confirmation before running the cmdlet.Prompts you for confirmation before running the cmdlet.

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases: 

Required: False
Position: Named
Default value: False
Accept pipeline input: False
Accept wildcard characters: False
```

### -WhatIf
Shows what would happen if the cmdlet runs.
The cmdlet is not run.Shows what would happen if the cmdlet runs.
The cmdlet is not run.

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases: 

Required: False
Position: Named
Default value: False
Accept pipeline input: False
Accept wildcard characters: False
```

### -UseTransaction
Includes the command in the active transaction.
This parameter is valid only when a transaction is in progress.
For more information, see Includes the command in the active transaction.
This parameter is valid only when a transaction is in progress.
For more information, see

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases: 

Required: False
Position: Named
Default value: False
Accept pipeline input: False
Accept wildcard characters: False
```

## INPUTS

### System.String
You can pipe a string that contains a path to this cmdlet.

## OUTPUTS

### None or an object that represents the renamed item.
This cmdlet generates an object that represents the renamed item, if you specify the PassThru parameter.
Otherwise, this cmdlet does not generate any output.

## NOTES
* Rename-Item is designed to work with the data exposed by any provider. To list the providers available in your session, type Get-PsProvider. For more information, see about_Providers.

*

## RELATED LINKS

[Clear-Item](e78220a3-d720-4347-bdbe-8f15f77f3aa1)

[Copy-Item](60a19812-67ab-4b58-a6f5-34640edafbb0)

[Get-ChildItem](75cf79bb-4db6-4a67-8c36-3d20754e2190)

[Get-Item](4ed2b1e1-fde4-4425-90a0-87774477fefa)

[Invoke-Item](61bc0652-39d8-44fe-9ff4-476ae75c38c8)

[Move-Item](de1b4217-de99-45cd-a12c-35e87b0c8466)

[New-Item](67038d02-6598-49c6-b5bd-77b59d445abe)

[Remove-Item](0fe3ff11-a1f7-43b9-8c85-f92d52641395)

[Rename-ItemProperty](07be82e9-597b-4a41-b9b8-1b192c5f0322)

[Set-Item](704c03fc-6fdd-46d6-9da6-6d3a2196918c)

[about_Providers](55e2974f-3314-48d2-8b1b-abdea6b303cb)
