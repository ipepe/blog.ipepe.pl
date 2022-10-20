---
title: "Setting default service version for Azure Blob Storage"
categories: ["paperclip", "azure"]
---

If you are sharing plain text files with url pointing directly to Azure Blob Storage you will notice that the browser will try to display file content instead of downloading it. 

This is because of two things:
1. You didn't set content disposition property when creating blob file
2. Azure Blob Storage by default uses `x-ms-version: 2009-09-19` service version. This version of the service does not support `Content-Disposition` property on files. To fix this you need to set the default service version to `2013-08-15` or higher.

Let's focus on point number 2 - Because we are sharing direct blob storage url, we cannot specify version through request headers so let's change this setting globally for whole blob storage.

Using Azure Portal launch Cloud Shell with PowerShell and run the following commands:

```powershell
Install-Module -Name AzureRM -AllowClobber

$ctx = New-AzureStorageContext -StorageAccountName <account-name>
Update-AzureStorageServiceProperty -ServiceType Blob -DefaultServiceVersion 2017-07-29 -Context $ctx
```

Sources:
 * <https://webcache.googleusercontent.com/search?q=cache:RKFTs1qIY_YJ:https://www.devtrends.co.uk/blog/fixing-azure-blob-storage-content-disposition&cd=1&hl=pl&ct=clnk&gl=pl>
 * <https://stackoverflow.com/questions/43335176/change-default-service-version-of-microsoft-azure-blob-php>