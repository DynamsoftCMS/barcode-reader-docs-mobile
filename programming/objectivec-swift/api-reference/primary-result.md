---
layout: default-layout
title: Dynamsoft Barcode Reader Objective-C & Swift API Reference - Result Methods
description: This page shows Result methods of Dynamsoft Barcode Reader for iOS SDK.
keywords: getIntermediateResult, result methods, api reference, objective-c, oc, swift
needAutoGenerateSidebar: true
---

# Result Methods

  | Method               | Description |
  |----------------------|-------------|
  | [`getIntermediateResult`](#getintermediateresult) | Get intermediate results. |
  | [`enableResultVerification`](#enableresultverification) | Result will be verified before output. |
  | [`enableDuplicateFilter`](#enableduplicatefilter) | Duplicate results will be filtered and output only once for every 3 seconds |

  ---

## getIntermediateResult

Return intermediate results containing the original image, the color clustered image, the binarized image, contours, lines, text blocks, etc.

```objc
-(NSArray<iIntermediateResult*>* _Nullable)getIntermediateResult:(NSError* _Nullable *  _Nullable)error;
```

### Parameters

`[in,out] error` Input a pointer to an error object. If an error occurs, this pointer is set to an actual error object containing the error information. You may specify nil for this parameter if you do not want the error information.

### Return value

Returns intermediate result array.

### Code Snippet

Objective-C:

```objc
iPublicRuntimeSettings *settings;
NSError __autoreleasing * _Nullable error;
NSArray<iTextResult *> *result;
NSArray<iIntermediateResult *> *irResult;
DynamsoftBarcodeReader *barcodeReader;
iDMDLSConnectionParameters* dls = [[iDMDLSConnectionParameters alloc] init];
dls.organizationID = @"200001";
dls.sessionPassword = @"******";
barcodeReader = [[DynamsoftBarcodeReader alloc] initLicenseFromDLS:dls verificationDelegate:self];
- (void)DLSLicenseVerificationCallback:(bool)isSuccess error:(NSError * _Nullable)error
{
        //TODO add your code for license verification
}

[m_barcodeReader getRuntimeSettings:&error];
settings.intermediateResultTypes = EnumIntermediateResultTypeColourConvertedGrayScaleImage|EnumIntermediateResultTypeOriginalImage|EnumIntermediateResultTypeColourClusteredImage;
[m_barcodeReader updateRuntimeSettings:settings error:&error];
result = [m_barcodeReader decodeFileWithName:@"your file path" templateName:@"" error:&error];
irResult = [m_barcodeReader getIntermediateResult:&error];
```

Swift:

```Swift
let error: NSError? = NSError()
let dls = iDMDLSConnectionParameters()
dls.organizationID = "200001"
dls.sessionPassword = "******"
let barcodeReader = DynamsoftBarcodeReader(licenseFromDLS: dls, verificationDelegate: self)
func DLSLicenseVerificationCallback(_ isSuccess: Bool, error: Error?)
{
    print("isSucc : \(isSuccess) error : \(String(describing: error))")
}
let settings = barcodeReader.getRuntimeSettings(error: nil)
settings.intermediateResultTypes = EnumIntermediateResultType.ColourConvertedGrayScaleImage.rawValue | EnumIntermediateResultType.OriginalImage.rawValue | EnumIntermediateResultType.ColourClusteredImage.rawValue
barcodeReader.updateRuntimeSettings(settings:settings, error:nil)
let result = barcodeReader.decodeFileWithName(name:"your file path", templateName:"", error:nil)
let irResult = barcodeReader.getIntermediateResult(error: &error)
```

## enableResultVerification

The text results will be verified before output if the result verification is enabled.

Objective-C:

```objectivec
[barcodeReader enableResultVerification:true];
// To check the status of this mode
[barcodeReader getEnableResultVerification]
```

Swift:

```swift
barcodeReader.enableResultVerification = true
// To check the status of this mode
let x = barcodeReader.enableResultVerification
```

## enableDuplicateFilter

The duplicated text result will be filtered. The barcode reader will not output the result for the same barcode a second time in 3 seconds.

Objective-C:

```objectivec
[barcodeReader enableDuplicateFilter:true];
// To check the status of this mode
[barcodeReader getEnableDuplicateFilter]
```

Swift:

```swift
barcodeReader.enableDuplicateFilter = true
// To check the status of this mode
let x = barcodeReader.enableDuplicateFilter
```
