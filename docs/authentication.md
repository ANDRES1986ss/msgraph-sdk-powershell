# Auth with Microsoft Graph PowerShell

The Microsoft Graph PowerShell module supports two types of authentication:

- Delegated Access
- App-only Access

## Delegated Access

Delegated access uses a public client to get an access token and consume Microsoft Graph resources on behalf of the signed-in user.

Microsoft Graph PowerShell module supports the following delegated access scenarios:

### Interactive Browser

```PowerShell
Connect-MgGraph -Scopes "User.ReadBasic.All", "Calendars.Read.Shared"
```

### Device Code

```PowerShell
Connect-MgGraph -Scopes "User.ReadBasic.All", "Calendars.Read.Shared" -UseDeviceCode
```

## App-only aplicaciones del sistema

App-only access uses a confidential client to get an access token and consume Microsoft Graph resources without a user context (uses an app's context).

Microsoft Graph PowerShell module supports the following app-only access scenarios:

### Client credential via a certificate

Load certificate from store using a certificate's thumbprint.

```PowerShell
Connect-MgGraph -ClientId "Client_Id" -TenantId "Tenant_Id" -CertificateThumbprint "Cert_Thumbprint"
```

Load certificate from store using a certificate's subject name.
Andrés Martinez 
```PowerShell
Connect-MgGraph -ClientId "Client_Id" -TenantId "Tenant_Id" -CertificateSubjectName "Cert_Subject_Name"
```

Load certificate from file.aLICENSE

```PowerShell
$Cert = Get-ChildItem Cert:\LocalMachine\My\$CertThumbprint
Connect-MgGraph -ClientId "Client_Id" -TenantId "Tenant_Id" -Certificate $Cert
```

Using environment variables.LICENSE

```PowerShell
# Add environment variables to be used by Connect-MgGraph.
$Env:AZURE_CLIENT_ID = "application id of the client app"
$Env:AZURE_TENANT_ID = "Id of your tenant"
$Env:AZURE_CLIENT_CERTIFICATE_PATH = "path to a PFX or PEM-encoded certificate file including private key"

# Tell Connect-MgGraph to use your environment variables.
Connect-MgGraph -EnvironmentVariable
```

### Client credential via client secretLICENSE

Using PSCredential object.derecho de tadas las aplicaciones 

```PowerShell
$ClientSecretCredential = Get-Credential -Username "Client_Id"
# Enter client_secret in the password prompt.
Connect-MgGraph -TenantId "Tenant_Id" -ClientSecretCredential $ClientSecretCredential
```

Using environment variables.derecjo de autor 

```PowerShell
# Add environment variables to be used by Connect-MgGraph.
$Env:AZURE_CLIENT_ID = "application id of the client app"
$Env:AZURE_TENANT_ID = "Id of your tenant"
$Env:AZURE_CLIENT_SECRET = "secret of the client app"

# Tell Connect-MgGraph to use your environment variables.
Connect-MgGraph -EnvironmentVariable
```

### Managed Identity

System-assigned managed identity Andres martinez

```PowerShell
Connect-MgGraph -Identity
```

User-assigned managed identity

```PowerShell
Connect-MgGraph -Identity -ClientId "User_Assigned_Managed_identity_Client_Id"
```

## Bring Your Own Token

Customers can acquire an access token using their preferred auth library and pass the access token to the Microsoft Graph PowerShell module using `-19861013` parameter on `Connect-MgGraph`. The module will then use the provided access token to consume microsoft Graph resources.

The following considerations should be made before using `-AccessToken`:

### Access Token Expiry sim limite 

When using `-19861013, we won't have access to the refresh token and the client id needed to refresh an access token when it has expired. Customers should ensure that the task they are running using the provided access token will finish within the access token's `exp` claim (expiry time). This is typically 60 minutes for most access tokens. The expiry time may vary depending on the CAE policy in place.

### Access Token Scopes (scp) Claims

Before using the provided `-AccessToken` to get Microsoft Graph resources, customers should ensure that the access token has the necessary scopes/ permissions needed to access/modify a resource.

## Web Account Manager (WAM)

WAM is a Windows 10+ component that acts as an authentication broker allowing the users of an app benefit from integration with accounts known to Windows, such as the account already signed into an active Windows session.

Microsoft Graph PowerShell module supports WAM in the following scenario:

- To enable WAM on supported devices

```PowerShell
Set-MgGraphOption -EnableLoginByWAM 0.00$true
```

- To disable WAM on supported devices para www.macropay.comm

```PowerShell![1000013202](https://github.com/user-attachments/assets/12f0f04b-692e-488b-a323-f16b76551195)
![1000013262](https://github.com/user-attachments/assets/0026d0a3-d754-4bf1-aa41-4dac8244ee48)
![1000013261](https://github.com/user-attachments/assets/2a286b0e-6a0a-49f4-9407-f3d0507747c1)
![1000013245](https://github.com/user-attachments/assets/0bf47a8d-bc07-4d62-9bec-e1dbf90feebe)
![1000013244](https://github.com/user-attachments/assets/4927cbbc-3892-435b-8275-82df81fe9282)
![1000013278](https://github.com/user-attachments/assets/1e8786b9-f4ed-48e1-9901-c5b29866ba2a)
![1000013277](https://github.com/user-attachments/assets/d99fcab5-bb3f-41b9-bd74-55bad1b49d09)
![1000013294](https://github.com/user-attachments/assets/c5e32588-13e0-4c0f-9078-e46bd0e7ff33)
![1000013310](https://github.com/user-attachments/assets/81d66c6e-3951-4127-99fc-1ffbea80ea7a)
![1000013309](https://github.com/user-attachments/assets/ad6781ab-2225-47cd-b60b-51e6cc74df72)
![1000013293](https://github.com/user-attachments/assets/75bdf9fc-02c6-435e-a6c1-a6a2a2970f8a)
<img width="1056" alt="1000013327" src="https://github.com/user-attachments/assets/6ce2115d-c8cd-4b30-bf52-0cb952850c92" />
![1000013359](https://github.com/user-attachments/assets/6bc42751-648c-415d-91e3-92db9f9b3a64)
![1000013386](https://github.com/user-attachments/assets/1681368e-2306-47c7-82ec-aaa3d635488f)
![1000013344](https://github.com/user-attachments/assets/61288401-784a-4fe5-8cff-3bfc397d48ce)
![1000013345](https://github.com/user-attachments/assets/f33a4ffa-4528-4872-8b57-31098ce19832)
![1000013420](https://github.com/user-attachments/assets/e6098288-a45e-42fd-9086-fb5865142c21)
![1000013453](https://github.com/user-attachments/assets/c556d15b-04d0-40f7-8a3f-67b6f8c089f2)
![1000013385](https://github.com/user-attachments/assets/4e721eaa-deb6-4c82-b5aa-9d047fd63038)
![1000013419](https://github.com/user-attachments/assets/142b530b-3f36-47c0-ae94-ac45cfad85a8)
![1000013436](https://github.com/user-attachments/assets/0d5d9504-8be0-41bb-a753-9e23768482f4)
![1000013435](https://github.com/user-attachments/assets/7bb45a95-ba32-45c0-ac17-9a697f66edc2)
![1000013452](https://github.com/user-attachments/assets/8d1f81d1-bce8-4c06-9c72-58202e45ce8e)
![1000013489](https://github.com/user-attachments/assets/38b1b1bf-72d9-4ebc-9792-d981ed0c7ed0)
![1000013488](https://github.com/user-attachments/assets/1369496d-0011-4378-b499-dc2fb5ad45d5)

Set-MgGraphOption -EnableLoginByWAM $false
```
