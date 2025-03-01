---
layout: default-layout
title: Dynamsoft Barcode Reader Android API Reference - BarcodeReader Parameter and Runtime Settings Advanced Methods
description: This page shows BarcodeReader advanced runtime settings methods of Dynamsoft Barcode Reader for Android SDK.
keywords: initRuntimeSettingsWithFile, initRuntimeSettingsWithString, appendTplFileToRuntimeSettings, appendTplStringToRuntimeSettings, getAllParameterTemplateNames, outputSettingsToFile, outputSettingsToString, parameter and runtime settings advanced methods, BarcodeReader, api reference, android
needAutoGenerateSidebar: true
needGenerateH3Content: false
---

# Parameter and Runtime Settings Advanced Methods

  | Method               | Description |
  |----------------------|-------------|
  | [`initRuntimeSettingsWithFile`](#initruntimesettingswithfile)  | Initialize runtime settings with the settings in a given JSON file. |
  | [`initRuntimeSettingsWithString`](#initruntimesettingswithstring) | Initialize runtime settings with the settings in a given JSON string. |
  | [`appendTplFileToRuntimeSettings`](#appendtplfiletoruntimesettings) | Append a new template file to the current runtime settings. |
  | [`appendTplStringToRuntimeSettings`](#appendtplstringtoruntimesettings) | Append a new template string to the current runtime settings. |
  | [`getAllParameterTemplateNames`](#getallparametertemplatenames) | Gets the parameter templates name array. |
  | [`outputSettingsToFile`](#outputsettingstofile) | Output runtime settings to a settings file (JSON file). |
  | [`outputSettingsToString`](#outputsettingstostring) | Output runtime settings to a string. |

  ---

## initRuntimeSettingsWithFile

Initialize runtime settings with the settings in a given JSON file.

```java
void com.dynamsoft.dbr.BarcodeReader.initRuntimeSettingsWithFile(String filePath, int enumConflictMode) throws BarcodeReaderException
```

### Parameters

- `filePath`: The path of the settings file.  
- `enumConflictMode`: The parameter setting mode, which decides whether to inherit parameters from previous template setting or to overwrite previous settings and replace with the new template.

### Exceptions

[`BarcodeReaderException`](auxiliary-BarcodeReaderException.md)

### Code Snippet

```java
BarcodeReader reader = new BarcodeReader();
DMDLSConnectionParameters info = new DMDLSConnectionParameters();
info.organizationID = "200001";
info.sessionPassword = "******";
reader.initLicenseFromDLS(info, new DBRDLSLicenseVerificationListener() {
   @Override
   public void DLSLicenseVerificationCallback(boolean b, Exception e) {
      if (!b && e != null) {
         e.printStackTrace();
      }
   }
});
reader.initRuntimeSettingsWithFile("your template file path", EnumConflictMode.CM_OVERWRITE);
reader.destroy();
```

## initRuntimeSettingsWithString

Initialize runtime settings with the settings in a given JSON string.

```java
void com.dynamsoft.dbr.BarcodeReader.initRuntimeSettingsWithString(String content, int enumConflictMode)throws BarcodeReaderException
```

### Parameters

- `content`: A JSON string that represents the content of the settings.
- `enumConflictMode`: The parameter setting mode, which decides whether to inherit parameters from previous template setting or to overwrite previous settings and replace with the new template.

### Exceptions

[`BarcodeReaderException`](auxiliary-BarcodeReaderException.md)

### Code Snippet

```java
BarcodeReader reader = new BarcodeReader();
DMDLSConnectionParameters info = new DMDLSConnectionParameters();
info.organizationID = "200001";
info.sessionPassword = "******";
reader.initLicenseFromDLS(info, new DBRDLSLicenseVerificationListener() {
   @Override
   public void DLSLicenseVerificationCallback(boolean b, Exception e) {
      if (!b && e != null) {
         e.printStackTrace();
      }
   }
});
reader.initRuntimeSettingsWithString("{\"Version\":\"3.0\", \"ImageParameter\":{\"Name\":\"IP1\", \"BarcodeFormatIds\":[\"BF_QR_CODE\"], \"ExpectedBarcodesCount\":10}}", EnumConflictMode.CM_OVERWRITE);
reader.destroy();
```

## appendTplFileToRuntimeSettings

Append a new template file to the current runtime settings.

```java
void com.dynamsoft.dbr.BarcodeReader.appendTplFileToRuntimeSettings(String filePath, int enumConflictMode) throws BarcodeReaderException
```

### Parameters

- `filePath`: The path of the settings file.  
- `enumConflictMode`: The parameter setting mode, which decides whether to inherit parameters from previous template setting or to overwrite previous settings with the new template. 

### Exceptions

[`BarcodeReaderException`](auxiliary-BarcodeReaderException.md)

### Code Snippet

```java
BarcodeReader reader = new BarcodeReader();
DMDLSConnectionParameters info = new DMDLSConnectionParameters();
info.organizationID = "200001";
info.sessionPassword = "******";
reader.initLicenseFromDLS(info, new DBRDLSLicenseVerificationListener() {
   @Override
   public void DLSLicenseVerificationCallback(boolean b, Exception e) {
      if (!b && e != null) {
         e.printStackTrace();
      }
   }
});
reader.appendTplFileToRuntimeSettings("your template file path", EnumConflictMode.CM_IGNORE);
reader.destroy();
```

## appendTplStringToRuntimeSettings

Append a new template string to the current runtime settings.

```java
void com.dynamsoft.dbr.BarcodeReader.appendTplStringToRuntimeSettings(String content, int enumConflictMode)	throws BarcodeReaderException
```

### Parameters

- `content`: A JSON string that represents the content of the settings.  
- `enumConflictMode`: The parameter setting mode, which decides whether to inherit parameters from previous template setting or to overwrite previous settings with the new template.  

### Exceptions

[`BarcodeReaderException`](auxiliary-BarcodeReaderException.md)

### Code Snippet

```java
BarcodeReader reader = new BarcodeReader();
DMDLSConnectionParameters info = new DMDLSConnectionParameters();
info.organizationID = "200001";
info.sessionPassword = "******";
reader.initLicenseFromDLS(info, new DBRDLSLicenseVerificationListener() {
   @Override
   public void DLSLicenseVerificationCallback(boolean b, Exception e) {
      if (!b && e != null) {
         e.printStackTrace();
      }
   }
});
reader.initRuntimeSettingsWithString("{\"Version\":\"3.0\", \"ImageParameter\":{\"Name\":\"IP1\", \"BarcodeFormatIds\":[\"BF_QR_CODE\"], \"ExpectedBarcodesCount\":10}}", EnumConflictMode.CM_OVERWRITE);
reader.appendTplStringToRuntimeSettings("{\"Version\":\"3.0\", \"ImageParameter\":{\"Name\":\"IP1\", \"BarcodeFormatIds\":[\"BF_OneD\"], \"ExpectedBarcodesCount\":20}}", EnumConflictMode.CM_IGNORE);
reader.destroy();
```

## getAllParameterTemplateNames

Gets the parameter templates name array.

```java
String [] com.dynamsoft.dbr.BarcodeReader.getAllParameterTemplateNames()
```

### Return value

The template name array.

### Exceptions

[`BarcodeReaderException`](auxiliary-BarcodeReaderException.md)

### Code Snippet

```java
BarcodeReader reader = new BarcodeReader();
DMDLSConnectionParameters info = new DMDLSConnectionParameters();
info.organizationID = "200001";
info.sessionPassword = "******";
reader.initLicenseFromDLS(info, new DBRDLSLicenseVerificationListener() {
   @Override
   public void DLSLicenseVerificationCallback(boolean b, Exception e) {
      if (!b && e != null) {
         e.printStackTrace();
      }
   }
});
String[] templateNames = reader.getAllParameterTemplateNames();
reader.destroy();
```

## outputSettingsToFile

Output runtime settings to a settings file (JSON file).

```java
void com.dynamsoft.dbr.BarcodeReader.outputSettingsToFile(String filePath, String settingsName) throws BarcodeReaderException
```

### Parameters

- `filePath`: The output file path which stores current settings.  
- `settingsName`: A unique name for declaring current runtime settings.

### Exceptions

[`BarcodeReaderException`](auxiliary-BarcodeReaderException.md)

### Code Snippet

```java
BarcodeReader reader = new BarcodeReader();
DMDLSConnectionParameters info = new DMDLSConnectionParameters();
info.organizationID = "200001";
info.sessionPassword = "******";
reader.initLicenseFromDLS(info, new DBRDLSLicenseVerificationListener() {
   @Override
   public void DLSLicenseVerificationCallback(boolean b, Exception e) {
      if (!b && e != null) {
         e.printStackTrace();
      }
   }
});
reader.outputSettingsToFile("your saving file path", "currentRuntimeSettings");
reader.destroy();
```

## outputSettingsToString

Output runtime settings to a string.

```java
String com.dynamsoft.dbr.BarcodeReader.outputSettingsToString(String settingsName) throws BarcodeReaderException
```

### Parameters 

`settingsName` A unique name for declaring current runtime settings.  

### Return value

The output string which stores the contents of current settings.

### Code Snippet

```java
BarcodeReader reader = new BarcodeReader();
DMDLSConnectionParameters info = new DMDLSConnectionParameters();
info.organizationID = "200001";
info.sessionPassword = "******";
reader.initLicenseFromDLS(info, new DBRDLSLicenseVerificationListener() {
   @Override
   public void DLSLicenseVerificationCallback(boolean b, Exception e) {
      if (!b && e != null) {
         e.printStackTrace();
      }
   }
});
String settingStr = reader.outputSettingsToString("currentRuntimeSettings");
reader.destroy();
```
