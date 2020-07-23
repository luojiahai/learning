## Implement Azure security (10-15%)

### Implement authentication
#### implement authentication by using certificates, forms-based authentication, or tokens
- [Get started with certificate-based authentication in Azure Active Directory](https://docs.microsoft.com/en-us/azure/active-directory/authentication/active-directory-certificate-based-authentication-get-started)
    - Configure the certificate authorities
        ```azurepowershell-interactive
        # Install Azure AD
        Install-Module -Name AzureAD –RequiredVersion 2.0.0.33

        # Connect
        Connect-AzureAD

        # Retrieve
        Get-AzureADTrustedCertificateAuthority

        # Add
        New-AzureADTrustedCertificateAuthority

        # Remove
        Remove-AzureADTrustedCertificateAuthority

        # Modify
        Set-AzureADTrustedCertificateAuthority
        ```
    - Configure revocation
        ```azurepowershell-interactive
        # Connect with admin credentials to the MSOL service:
        $msolcred = get-credential
        connect-msolservice -credential $msolcred

        # Retrieve the current StsRefreshTokensValidFrom value for a user:
        $user = Get-MsolUser -UserPrincipalName test@yourdomain.com`
        $user.StsRefreshTokensValidFrom

        # Configure a new StsRefreshTokensValidFrom value for the user equal to the current timestamp:
        Set-MsolUser -UserPrincipalName test@yourdomain.com -StsRefreshTokensValidFrom ("03/05/2016")
        ```
- [Configure Azure Multi-Factor Authentication Server for IIS web apps](https://docs.microsoft.com/en-us/azure/active-directory/authentication/howto-mfaserver-iis)
- [Microsoft identity platform access tokens](https://docs.microsoft.com/en-us/azure/active-directory/develop/access-tokens)
#### implement multi-factor or Windows authentication by using Azure AD
- [Plan an Azure Multi-Factor Authentication deployment](https://docs.microsoft.com/en-us/azure/active-directory/authentication/howto-mfa-getstarted)
#### implement OAuth2 authentication
- [OAuth 2.0 and OpenID Connect protocols on Microsoft identity platform](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-v2-protocols)
#### implement Managed identities/Service Principal authentication
- [Microsoft identity platform access tokens](https://docs.microsoft.com/en-us/azure/active-directory/develop/access-tokens)
#### implement Microsoft identity platform
- [Microsoft identity platform overview](https://docs.microsoft.com/en-us/azure/active-directory/develop/v2-overview)

---

### Implement access control
#### implement CBAC (Claims-Based Access Control) authorization
#### implement RBAC (Role-Based Access Control) authorization
- [Grant a user access to Azure resources using Azure PowerShell](https://docs.microsoft.com/en-us/azure/role-based-access-control/tutorial-role-assignments-user-powershell)
    ```azurepowershell-interactive
    # Create a user
    $PasswordProfile = New-Object -TypeName Microsoft.Open.AzureAD.Model.PasswordProfile
    $PasswordProfile.Password = "Password"
    New-AzureADUser -DisplayName "RBAC Tutorial User" -PasswordProfile $PasswordProfile `
        -UserPrincipalName "rbacuser@example.com" -AccountEnabled $true -MailNickName "rbacuser"

    # Create a resource group
    Get-AzLocation | select Location
    $location = "westus"
    New-AzResourceGroup -Name "rbac-tutorial-resource-group" -Location $location

    # Grant access
    Get-AzSubscription
    $subScope = "/subscriptions/00000000-0000-0000-0000-000000000000"
    New-AzRoleAssignment -SignInName rbacuser@example.com `
        -RoleDefinitionName "Reader" `
        -Scope $subScope
    New-AzRoleAssignment -SignInName rbacuser@example.com `
        -RoleDefinitionName "Contributor" `
        -ResourceGroupName "rbac-tutorial-resource-group"

    # List access
    Get-AzRoleAssignment -SignInName rbacuser@example.com -Scope $subScope
    Get-AzRoleAssignment -SignInName rbacuser@example.com -ResourceGroupName "rbac-tutorial-resource-group"

    # Remove access
    Remove-AzRoleAssignment -SignInName rbacuser@example.com `
        -RoleDefinitionName "Contributor" `
        -ResourceGroupName "rbac-tutorial-resource-group"
    Remove-AzRoleAssignment -SignInName rbacuser@example.com `
        -RoleDefinitionName "Reader" `
        -Scope $subScope

    # Clean up resources
    Remove-AzResourceGroup -Name "rbac-tutorial-resource-group"
    Remove-AzureADUser -ObjectId "rbacuser@example.com"
    ```
#### create shared access signatures
- [Grant limited access to Azure Storage resources using shared access signatures (SAS)](https://docs.microsoft.com/en-us/azure/storage/common/storage-sas-overview)

---

### Implement secure data solutions
#### encrypt and decrypt data at rest and in transit
- [Azure data security and encryption best practices](https://docs.microsoft.com/en-us/azure/security/fundamentals/data-encryption-best-practices)
#### create, read, update, and delete keys, secrets, and certificates by using the KeyVault API
- [Set and retrieve a secret from Azure Key Vault using PowerShell](https://docs.microsoft.com/en-us/azure/key-vault/secrets/quick-create-powershell)
    ```azurepowershell-interactive
    # Create a connection with Azure
    Login-AzAccount

    # Create a resource group
    New-AzResourceGroup -Name ContosoResourceGroup -Location EastUS

    # Create a Key Vault
    New-AzKeyVault -Name 'Contoso-Vault2' -ResourceGroupName 'ContosoResourceGroup' -Location 'East US'

    # Give your user account permissions to manage secrets in Key Vault
    Set-AzKeyVaultAccessPolicy -VaultName 'Contoso-Vault2' -UserPrincipalName 'user@domain.com' -PermissionsToSecrets get,set,delete

    # Adding a secret to Key Vault
    $secretvalue = ConvertTo-SecureString 'hVFkk965BuUv' -AsPlainText -Force
    $secret = Set-AzKeyVaultSecret -VaultName 'Contoso-Vault2' -Name 'ExamplePassword' -SecretValue $secretvalue
    (Get-AzKeyVaultSecret -vaultName "Contoso-Vault2" -name "ExamplePassword").SecretValueText

    # Clean up resources
    Remove-AzResourceGroup -Name ContosoResourceGroup
    ```
- [Set and retrieve a secret from Azure Key Vault using Azure CLI](https://docs.microsoft.com/en-us/azure/key-vault/secrets/quick-create-cli)
    ```azurecli
    # Create a connection with Azure
    az login

    # Create a resource group
    az group create --name "ContosoResourceGroup" --location eastus

    # Create a Key Vault
    az keyvault create --name "Contoso-Vault2" --resource-group "ContosoResourceGroup" --location eastus

    # Add a secret to Key Vault
    az keyvault secret set --vault-name "Contoso-Vault2" --name "ExamplePassword" --value "hVFkk965BuUv"
    az keyvault secret show --name "ExamplePassword" --vault-name "Contoso-Vault2

    # Clean up resources
    az group delete --name ContosoResourceGroup
    ```