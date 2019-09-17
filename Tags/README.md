List tags for a resource

```powershell
(Get-AzureRmResourceGroup -Name "Test-RG").Tags

```

Add tag for a resource
```powershell
$resourceGroup = Get-AzureRmResourceGroup -Name "Test-RG"
```
