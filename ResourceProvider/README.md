List available resource providers

```powershell
Get-AzureRmResourceProvider -ListAvailable | Where-Object ProviderNamespace -Eq "Microsoft.BotService"
Get-AzureRmResourceProvider -ListAvailable `
  | Where-Object RegistrationState -Eq "NotRegistered" `
  | Where-Object ProviderNamespace -Match "Microsoft." `
  | Select-Object ProviderNamespace
```

Register a resource provider

```powershell
$azureBluePrintResourceProvider = Get-AzureRmResourceProvider -ListAvailable | Where-Object ProviderNamespace -Eq "Microsoft.Blueprint"
Register-AzureRmResourceProvider -ProviderNamespace $azureBluePrintResourceProvider.ProviderNamespace -Confirm
```

Unregister a resource provider

```powershell
$azureBluePrintResourceProvider = Get-AzureRmResourceProvider -ListAvailable | Where-Object ProviderNamespace -Eq "Microsoft.Blueprint"
Unregister-AzureRmResourceProvider -ProviderNamespace $azureBluePrintResourceProvider.ProviderNamespace -Confirm
```
