# Windows Network File Shares

Steeltoe's `WindowsNetworkFileShare` provides a simplified experience for interacting with SMB file shares by making [P/Invoke calls](https://docs.microsoft.com/en-us/cpp/dotnet/how-to-call-native-dlls-from-managed-code-using-pinvoke) to underlying Windows APIs, specifically to `mpr.dll`. For more background on SMB, see [Microsoft's SMB documentation](https://docs.microsoft.com/en-us/windows/desktop/fileio/microsoft-smb-protocol-and-cifs-protocol-overview)

Network shares are not the most cloud-native way to deal with files. For new development, consider exploring message queues, caches, blob stores, and NoSQL stores. The alternatives offer greater resiliency and decoupling from backing services. That said, sometimes the alternatives are n0t viable. For .NET applications deployed to Microsoft Windows Servers, Steeltoe provides a stepping stone towards cloud-native in the form of the `WindowsNetworkFileShare`. For applications deployed to Linux hosts on Pivotal Cloud Foundry, [volume services](https://docs.pivotal.io/pivotalcf/opsguide/enable-vol-services.html) are available.