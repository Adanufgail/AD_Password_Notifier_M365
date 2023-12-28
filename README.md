# AD_Password_Notifier_M365

Forked from https://github.com/bwya77/PowerShell/blob/master/Active%20Directory/PasswordExpiry.ps1
Updated to send email via M365 Azure/Entra App registration

This script will connect to an on-prem AD environment, pull all active users with password expirations under a threshold number of days, and then send each one an email notification via M365. It will then send a summary report to a given address containing the users meeting the criteria and how long until their password expires.


Setup: 
1. Create an Entra App Registration with the Microsoft Graph Application Mail.Send permisison. Grant it Admin Consent.
2. Create a self-signed certificate per Microsoft's guidelines here (https://learn.microsoft.com/en-us/powershell/exchange/app-only-auth-powershell-v2?view=exchange-ps) and attach it to the application.
3. Update the script configuration with the certificate thumbprint, Entra App ID, and your Entra Tenant ID.
4. Ensure the $FromEmail is a valid sender in your tenant. $TechEmail and $AlertEmail do not have to belong to your tenant (for MSP use)
5. Update any settings as you see fit, and customize the user message and the summary report message to your needs.
6. Set up a Scheduled Task on the same server possessing the self-signed certificate
7. Ensure server posessing script also has the Microsoft.Graph.Users.Actions module installed.

Placeholders:
There is a hash table (line 118 in the template) which contains a list of placeholder names that can be replaced per user with a valid name. Feel free to expand this with additonal variables (domain in a multi-domain Forest for example).
- The formatting is PLACEHOLDERTEXT = "VariableName"
- At present all used variables are in the hash table.
- You are unable to use variable attributes (ie $VARIABLE.count). To circumvent this, create a variable set to that attribute and use that (ie $COUNT=$VARIABLE.count; PLACEHOLDERCOUNT = "COUNT")
