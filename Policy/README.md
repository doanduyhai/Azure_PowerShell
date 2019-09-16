Create custom policy

```powershell
$policyJson = @' 
{
  "if": { 
    "anyOf": [
      {
        "field": "tags['creator']",
        "exists": "false"
      },
      {
        "field": "tags['Creator']",
        "exists": "false"
      },
      {
        "field": "tags['CREATOR']",
        "exists": "false"
      }
   ]
  },
  "then": {
    "effect": "deny"
  }
}  
'@
New-AzPolicyDefinition `
   -Name "MandatoryCreatorTagPolicy" `
   -Description "All resources should have mandatory 'creator' tag" `
   -Policy $policyJson `
   -Mode All
   
```   

Assign custom policy to a scope

```powershell
$currentSubscription = "/subscriptions/" + (Get-AzureRmContext).Subscription.Id
$customPolicy = Get-AzPolicyDefinition -Name "MandatoryCreatorTagPolicy"

New-AzPolicyAssignment -Name "MandatoryCreatorTag" `
    -PolicyDefinition $customPolicy `
    -Scope $currentSubscription

```

Remove policy assignment

```powershell
$customPolicy = Get-AzPolicyDefinition -Name "MandatoryCreatorTagPolicy"
$policyAssignment = Get-AzPolicyAssignment -PolicyDefinitionId $customPolicy.PolicyDefinitionId
Remove-AzPolicyAssignment -Id $policyAssignment.PolicyAssignmentId
```

Remove custom policy

```powershell
$customPolicy = Get-AzPolicyDefinition -Name "MandatoryCreatorTagPolicy"
Remove-AzPolicyDefinition -Id $customPolicy.PolicyDefinitionId
```

List all custom policies

```powershell
Get-AzPolicyDefinition -Custom
```
