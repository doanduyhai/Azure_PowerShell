# User

Create new User

```powershell
$PasswordProfile = New-Object -TypeName Microsoft.Open.AzureAD.Model.PasswordProfile
$PasswordProfile.Password = "xxx"
$OtherMails = New-Object System.Collections.Generic.List[string]
$OtherMails.Add("testuser@yopmail.com")

New-AzureADUser -AccountEnabled $true -DisplayName "TestUser" `
    -UserPrincipalName "ddh@doanduyhaihotmail.onmicrosoft.com" -UserType "Member" `
    -OtherMails $OtherMails -PasswordPolicies "DisablePasswordExpiration" `
    -PasswordProfile $PasswordProfile -MailNickName "ddh"
    
```

Search for User

```powershell
Get-AzureADUser -Filter "userPrincipalName eq 'ddh@doanduyhaihotmail.onmicrosoft.com'"
Get-AzureADUser -ObjectId "ddh@doanduyhaihotmail.onmicrosoft.com"
```

Delete Existing User

```powershell
Remove-AzureADUser -ObjectId "ddh@doanduyhaihotmail.onmicrosoft.com"
```


