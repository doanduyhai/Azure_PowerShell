
List logs

```powershell
Get-AzureRmLog -StartTime (Get-Date).AddDays(-7) | Where-Object {$_.Authorization.Action -Match 'role'} 

Get-AzureRmLog -StartTime (Get-Date).AddDays(-7) -ResourceProvider 'Microsoft.Authorization'

```
