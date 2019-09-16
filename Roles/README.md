# Role Assignment

Search built-in roles

```powershell

Get-AzureRmRoleDefinition | Where-Object Name -Match 'Reader' | Select Name, Id
Get-AzureRmRoleDefinition | Where-Object Name -Eq 'Reader' | Select Name, Id
```

Assign role to a principal on a scope

```powershell
$userObjectId = (Get-AzureADUser -ObjectId "ddh@doanduyhaihotmail.onmicrosoft.com").ObjectId
$roleName = (Get-AzureRmRoleDefinition | Where-Object Name -Eq 'Reader').Name
$currentSubscriptionId = "/subscriptions/" + (Get-AzureRmContext).Subscription.Id

New-AzureRmRoleAssignment -ObjectId $userObjectId `
    -Scope $currentSubscriptionId `
    -RoleDefinitionName $roleName
```

List role assignments on scope

```powershell
$currentSubscriptionId = "/subscriptions/" + (Get-AzureRmContext).Subscription.Id
Get-AzureRmRoleAssignment -Scope $currentSubscriptionId | Select RoleDefinitionName,ObjectId,ObjectType
```

Remove role assignment on scope
```powershell
$userObjectId = (Get-AzureADUser -ObjectId "ddh@doanduyhaihotmail.onmicrosoft.com").ObjectId
$roleName = (Get-AzureRmRoleDefinition | Where-Object Name -Eq 'Reader').Name
$currentSubscriptionId = "/subscriptions/" + (Get-AzureRmContext).Subscription.Id

Remove-AzureRmRoleAssignment -ObjectId $userObjectId `
    -Scope $currentSubscriptionId `
    -RoleDefinitionName $roleName 
```

Create custom role

```powershell
$currentSubscriptionId = "/subscriptions/" + (Get-AzureRmContext).Subscription.Id

$customRole = Get-AzureRmRoleDefinition -Name "Reader"
$customRole.Id = $null
$customRole.Name = "MyCustomRole"
$customRole.Description = "Custom role with read actions only on resource groups"
$customRole.Actions = New-Object System.Collections.Generic.List[string]
//$customRole.Actions.RemoveRange(0,$role.Actions.Count)
$customRole.Actions.Add("Microsoft.Resources/subscriptions/resourceGroups/*")
$customRole.AssignableScopes = New-Object System.Collections.Generic.List[string]
$customRole.AssignableScopes.Add($currentSubscriptionId)

New-AzureRmRoleDefinition -Role $customRole
```

List custom role

```powershell
Get-AzureRmRoleDefinition -Custom | Where-Object Name -Match 'My'
```

Delete custom role

```powershell
Remove-AzureRmRoleDefinition -Id (Get-AzureRmRoleDefinition -Custom | Where-Object Name -Match 'My').Id
```
