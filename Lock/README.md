Lock types:

1. **CanNotDelete**: read & update allowed, delete forbidden.
2. **ReadOnly**: read allowed, update & delete forbidden.

List locks on a resource group

```powershell
Get-AzureRmResourceLock -ResourceGroupName "Test-RG"
Get-AzureRmResourceLock -Scope (Get-AzureRmResourceGroup -Name "Test-RG").ResourceId
```

Add lock on a resource group

```powershell
Set-AzureRmResourceLock -ResourceGroupName "Test-RG" -LockName "READ_ONLY" -LockLevel ReadOnly -Force

//Try to update tags
Set-AzureRmResourceGroup -Name "Test-RG" -Tag @{"key"="value"}
```

Update lock on a resource group
```powershell
Remove-AzureRmResourceLock -ResourceGroupName "Test-RG" -LockName "READ_ONLY" -Force
Set-AzureRmResourceLock -ResourceGroupName "Test-RG" -LockName "DO_NOT_DELETE" -LockLevel CanNotDelete -Force

Set-AzureRmResourceGroup -Name "Test-RG" -Tag @{"key"="value"}
```
