# README: Upgrade Certificate in .NET Installer Package

This document outlines the process for upgrading the certificate used by the component service installer built with the .NET Installer Projects.
---

## Steps to Build the Installer

### Prerequisites:
1. **.NET Framework 4.8** must be installed.
2. **Visual Studio Extension**: Ensure the following extension is installed:
   - [Microsoft Visual Studio Installer Projects](https://marketplace.visualstudio.com/items?itemName=VisualStudioClient.MicrosoftVisualStudio2022InstallerProjects)

### Build Instructions:
1. Open the `StixCloudComponentInstaller` project in Visual Studio.
2. Perform the following steps:
   - Clean the project: **Build > Clean Solution**
   - Build the project: **Build > Build Solution**
3. Locate the newly generated installer:
   ```
   StixComponentService\StixCloudComponentInstaller\Release\
   ```
4. Verify that the installer includes the updated certificate and versioning.

---

## Steps to Replace the Certificate

### 1. Replace the Certificate File
- Replace the file `stixdriver_marinabaysands_com.pfx` with the updated version received from **MBS** (contact Darrell or Shafie for the latest file).
- File Path:
  ```
  StixCloudComponentServices\certs\stixdriver_marinabaysands_com.pfx
  ```

### 2. Update Certificate Thumbprint
- Obtain the **new thumbprint** from the internal knowledge base URL:
  [Get the New CERT_THUMBPRINT_NEW from here](https://kb.sistic.com.sg/pages/viewpage.action?spaceKey=ITA&title=Removal+of+Existing+Old+Certificate+Installed+by+Component+Service)

- Update the thumbprint in the code:
  - Replace `CERT_THUMBPRINT_OLD` with the old value.
  - Replace `CERT_THUMBPRINT_NEW` with the new thumbprint.

#### Updated Code:
```csharp
public static readonly string CERT_THUMBPRINT_OLD = "08CFBD6DE9DF0C6F7A38A6FA1AE2E5BF13E66070";
public static readonly string CERT_THUMBPRINT_NEW = "37a39777c1e79c3a8f66e01f4225f18a3ed52087";
```

### 3. Upgrade Installer Configuration
- Open the `.NET Installer Package` project in Visual Studio.
- Update the following properties:
  - **Product Code**: Ensure its new ProductCode.
  - **RemovePreviousVersions**: Ensure this is set to `TRUE`.
  - **DetectNewerInstalledVersion**: Ensure this is set to `TRUE`.
- Update the **Version Number**:
  - Increment the version number (e.g., from `1.0.0` to `1.1.0`).

---

## Notes:
- **Testing**: Ensure the new installer upgrades the previous version correctly and validates the new certificate.
- **Troubleshooting**: If the installer fails, check the thumbprint and ensure the file paths are correct.

---

## Contact:
- For the certificate file: Darrell or Shafie (MBS)

---

End of Document.
