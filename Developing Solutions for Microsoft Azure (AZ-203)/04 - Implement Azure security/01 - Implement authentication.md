# Implement authentication

## Implement authentication by using certificates, forms-based authentication, or tokens

### Concept

- [**Certificate-based authentication**](https://docs.microsoft.com/en-us/azure/active-directory/authentication/active-directory-certificate-based-authentication-get-started) enables you to be authenticated by Azure Active Directory with a client certificate on a Windows, Android, or iOS device when connecting your Exchange online account to:
    - Microsoft mobile applications such as Microsoft Outlook and Microsoft Word
    - Exchange ActiveSync (EAS) clients

- [**Legacy authentication methods**](https://docs.microsoft.com/en-us/azure/active-directory/authentication/howto-mfaserver-iis)

- [**Access tokens**](https://docs.microsoft.com/en-us/azure/active-directory/develop/access-tokens) enable clients to securely call protected APIs. Microsoft identity platform access tokens are JWTs, Base64 encoded JSON objects signed by Microsoft identity platform.

## Implement multi-factor or Windows authentication by using Azure AD

### Concept

- [**How it works: Azure Multi-Factor Authentication**](https://docs.microsoft.com/en-us/azure/active-directory/authentication/concept-mfa-howitworks)

### Resource

- [Plan an Azure Multi-Factor Authentication deployment](https://docs.microsoft.com/en-us/azure/active-directory/authentication/howto-mfa-getstarted)

## Implement OAuth2 authentication

### Concept

- [**Authorize access to web applications using OpenID Connect and Azure Active Directory**](https://docs.microsoft.com/en-us/azure/active-directory/azuread-dev/v1-protocols-openid-connect-code)

- The [**OAuth2 implicit grant**](https://docs.microsoft.com/en-us/azure/active-directory/azuread-dev/v1-oauth2-implicit-grant-flow) is notorious for being the grant with the longest list of security concerns in the OAuth2 specification.

- [**Authorize access to Azure Active Directory web applications using the OAuth 2.0 code grant flow**](https://docs.microsoft.com/en-us/azure/active-directory/azuread-dev/v1-protocols-oauth-code)

- The [**OAuth 2.0 Client Credentials**](https://docs.microsoft.com/en-us/azure/active-directory/azuread-dev/v1-oauth2-client-creds-grant-flow) Grant Flow permits a web service (confidential client) to use its own credentials instead of impersonating a user, to authenticate when calling another web service.

## Implement Managed identities/Service Principal authentication

### Concept

- [**What are managed identities for Azure resources?**](https://docs.microsoft.com/en-us/azure/active-directory/managed-identities-azure-resources/overview)

### Resource

- [Configure managed identities for Azure resources on an Azure VM using Azure CLI](https://docs.microsoft.com/en-us/azure/active-directory/managed-identities-azure-resources/qs-configure-cli-windows-vm)

- [How to use managed identities for Azure resources on an Azure VM to acquire an access token](https://docs.microsoft.com/en-us/azure/active-directory/managed-identities-azure-resources/how-to-use-vm-token)

- [Assign a managed identity access to a resource using Azure CLI](https://docs.microsoft.com/en-us/azure/active-directory/managed-identities-azure-resources/howto-assign-access-cli)

## Implement Microsoft identity platform

### Concept

- [**Microsoft identity platform**](https://docs.microsoft.com/en-us/azure/active-directory/develop/v2-overview) is an evolution of the Azure Active Directory (Azure AD) developer platform. It allows developers to build applications that sign in all Microsoft identities and get tokens to call Microsoft APIs, such as Microsoft Graph, or APIs that developers have built.

- [**Application types for Microsoft identity platform**](https://docs.microsoft.com/en-us/azure/active-directory/develop/v2-app-types)

- [**Application and service principal objects in Azure Active Directory**](https://docs.microsoft.com/en-us/azure/active-directory/develop/app-objects-and-service-principals)

- [**Permissions and consent in the Microsoft identity platform endpoint**](https://docs.microsoft.com/en-us/azure/active-directory/develop/v2-permissions-and-consent)

