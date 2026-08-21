# HelloID-Conn-SA-Full-Exchange-On-Premises-Mailcontact-Delete

| :information_source: Information                                                                                                                                                                                                                                                                                                                                                          |
| :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| This repository contains the connector and configuration code only. The implementer is responsible for acquiring the connection details such as username, password, certificate, etc. You might even need to sign a contract or agreement with the supplier before implementing this connector. Please contact the client's application manager to coordinate the connector requirements. |

## Description

_HelloID-Conn-SA-Full-Exchange-On-Premises-Mailcontact-Delete_ is a template designed for use with HelloID Service Automation (SA) Delegated Forms. It can be imported into HelloID and customized according to your requirements.

This delegated form provides functionality to delete Exchange On-Premises mail contacts. The following workflow is available:

1.  Search for mail contacts by entering a search term (name, alias, or email address)
2.  Select the mail contact to delete from the search results grid
3.  The selected mail contact is validated and retrieved from Exchange
4.  The mail contact is permanently deleted from Exchange On-Premises
5.  All actions are logged to HelloID audit logs with detailed information

## Getting started

### Requirements

- **Exchange On-Premises Environment**:<br>
  A working Exchange On-Premises environment with remote PowerShell access enabled. The connector uses remote PowerShell sessions to connect to Exchange.
- **HelloID Service Automation Agent** (if not using cloud execution):<br>
  A HelloID Service Automation agent must be installed and configured if the tasks are not set to run in the cloud. The agent must have network access to the Exchange server.
- **PowerShell Remoting**:<br>
  PowerShell remoting must be enabled on the Exchange server. The connection URI should be accessible from the HelloID agent or cloud environment.

### Connection settings

The following user-defined variables are used by the connector.

| Setting               | Description                                               | Mandatory |
| --------------------- | --------------------------------------------------------- | --------- |
| ExchangeConnectionUri | The URI to the Exchange PowerShell endpoint               | Yes       |
| ExchangeAdminUsername | The username of an account with Exchange admin privileges | Yes       |
| ExchangeAdminPassword | The password of the Exchange admin account                | Yes       |

## Remarks

### Server-Side Filtering for Performance

- **Filter Parameter**: The datasource uses the `-Filter` parameter with `Get-Recipient` to perform server-side filtering. This significantly improves performance when searching through large mail contact collections by reducing the amount of data transferred over the network.

### Authentication Method

- **Default Authentication**: The connector uses `Default` authentication which allows for flexible authentication methods including NTLM and Kerberos. This provides broader compatibility across different Exchange environments compared to specifying a single authentication method.

### Session Security Options

- **Certificate Validation Enabled**: The connector has certificate validation enabled (`SkipCACheck`, `SkipCNCheck`, and `SkipRevocationCheck` are all set to `$false`). This ensures secure connections to Exchange servers. If you encounter certificate-related connection issues, verify that your Exchange server has a valid SSL certificate.

### Resource Cleanup

- **Guaranteed Session Cleanup**: The connector uses a `finally` block to ensure that Exchange PowerShell sessions are always cleaned up, even if errors occur during execution. This prevents resource leaks and session exhaustion.

### Wildcard Search Support

- **Flexible Search**: The search functionality supports wildcard matching across multiple attributes (Name, Alias, PrimarySmtpAddress). When a user enters a search term, it's automatically wrapped with wildcards to find partial matches.

### Error Handling and Logging

- **Detailed Audit Logs**: All operations including connection, deletion, and disconnection are logged to HelloID audit logs with detailed information including the action performed, target display name, and target identifier.
- **Contextual Error Messages**: Error messages include script line numbers and context to aid in troubleshooting.

## Development resources

### PowerShell cmdlets

The following Exchange PowerShell cmdlets are used by the connector:

| Cmdlet             | Description                                      |
| ------------------ | ------------------------------------------------ |
| Get-Recipient      | Retrieves mail contact information from Exchange |
| Remove-MailContact | Deletes a mail contact from Exchange             |

### API documentation

- [Exchange Server PowerShell Documentation](https://learn.microsoft.com/en-us/powershell/exchange/exchange-management-shell)
- [Connect to Exchange Servers using Remote PowerShell](https://learn.microsoft.com/en-us/powershell/exchange/connect-to-exchange-servers-using-remote-powershell)
- [Get-Recipient Cmdlet](https://learn.microsoft.com/en-us/powershell/module/exchange/get-recipient)
- [Remove-MailContact Cmdlet](https://learn.microsoft.com/en-us/powershell/module/exchange/remove-mailcontact)

## Getting help

> :bulb: **Tip:**  
> _For more information on Delegated Forms, please refer to our [documentation](https://docs.helloid.com/en/service-automation/delegated-forms.html) pages_.

## HelloID docs

The official HelloID documentation can be found at: https://docs.helloid.com/
