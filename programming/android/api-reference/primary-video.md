---
layout: default-layout
title: Dynamsoft Barcode Reader Android API Reference - BarcodeReader Video Methods
description: This page shows BarcodeReader video methods of Dynamsoft Barcode Reader for Android SDK.
keywords: startFrameDecoding, startFrameDecodingEx, appendFrame, stopFrameDecoding, initFrameDecodingParameters, setErrorCallback, setTextResultCallback, setIntermediateResultCallback, getLengthOfFrameQueue, video methods, BarcodeReader, api reference, android
needAutoGenerateSidebar: true
needGenerateH3Content: false
---

# Video Methods

- Decode

   | Method               | Description |
   |----------------------|-------------|
   | [`startFrameDecoding`](#startframedecoding) | Decode barcodes from inner frame queue. |
   | [`startFrameDecodingEx`](#startframedecodingex) | Decode barcodes from inner frame queue. |
   | [`appendFrame`](#appendframe) | Append a frame image buffer to the inner frame queue. |
   | [`stopFrameDecoding`](#stopframedecoding) | Stop thread used for frame decoding. |

- Parameter

   | Method               | Description |
   |----------------------|-------------|
   | [`initFrameDecodingParameters`](#initframedecodingparameters) | Initialize frame decoding parameter. |

- Callback

   | Method               | Description |
   |----------------------|-------------|
   | [`setErrorCallback`](#seterrorcallback) | Set callback interface to process errors generated during frame decoding. |
   | [`setTextResultCallback`](#settextresultcallback) | Set callback interface to process text results generated during frame decoding. |
   | [`setIntermediateResultCallback`](#setintermediateresultcallback) | Set callback interface to process intermediate results generated during frame decoding. |

- Status retrieval

   | Method               | Description |
   |----------------------|-------------|
   | [`getLengthOfFrameQueue`](#getlengthofframequeue) | Get length of current inner frame queue. |

  ---

## startFrameDecoding

Start a new thread to decode barcodes from the inner frame queue with specific frame decoding setting passed in.

```java
void com.dynamsoft.dbr.BarcodeReader.startFrameDecoding (final int maxQueueLength, final int maxResultQueueLength, final int width, final int height, final int stride, final int enumImagePixelFormat, final String templateName) throws BarcodeReaderException
```

### Parameters

- `maxQueueLength`: The max number of frames waiting for decoding.  
- `maxResultQueueLength`: The max number of frames whose results (text result/localization result) will be kept.  
- `width`: The width of the frame image in pixels.  
- `height`: The height of the frame image in pixels.  
- `stride`: The stride (or scan width) of the frame image.  
- `format`: The image pixel format used in the image byte array.  
- `templateName`: The template name.  

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
reader.setErrorCallback(new ErrorCallback() {
    @Override
    public void errorCallback(int frameId, int errorCode, Object userData) {
        //TODO add your code for using error code
    }
}, null);
reader.startFrameDecoding(2, 10, 1024, 720, 1024, EnumImagePixelFormat.IPF_GRAYSCALED, "");
```

## startFrameDecodingEx

Start a new thread to decode barcodes from the inner frame queue with specific frame decoding setting defined in [`FrameDecodingParameters`](auxiliary-FrameDecodingParameters.md) struct.

```java
void com.dynamsoft.dbr.BarcodeReader.startFrameDecodingEx(FrameDecodingParameters parameters, String templateName) throws BarcodeReaderException
```

### Parameters

- `parameters`: The frame decoding parameters.
- `templateName`: The template name.

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
FrameDecodingParameters parameters = reader.initFrameDecodingParameters();
parameters.maxQueueLength = 2;
parameters.maxResultQueueLength = 10;
parameters.width = 1024;
parameters.height = 720;
parameters.stride = 1024;
parameters.imagePixelFormat = EnumImagePixelFormat.IPF_GRAYSCALED;
reader.setErrorCallback(new ErrorCallback() {
    @Override
    public void errorCallback(int frameId, int errorCode, Object userData) {
        //TODO add your code for using error code
    }
}, null);
reader.startFrameDecodingEx(parameters, "");
reader.destroy();
```

## appendFrame

Append a frame image buffer to the inner frame queue.  

```java
int com.dynamsoft.dbr.BarcodeReader.appendFrame(byte[] bufferBytes)
```

### Parameters

`bufferBytes`: The array of bytes which contain the image data.

### Return value

Returns the ID of the appended frame.

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
reader.startFrameDecoding(2, 10, 1024, 720, 1024, EnumImagePixelFormat.IPF_GRAYSCALED, "");
int frameId = reader.appendFrame(bufferBytes);
reader.destroy();
```

## stopFrameDecoding

Stop the frame decoding thread created by [`StartFrameDecoding`](#startframedecoding) or [`StartFrameDecodingEx`](#startframedecodingex).

```java
void com.dynamsoft.dbr.BarcodeReader.stopFrameDecoding() throws BarcodeReaderException
```  

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
reader.startFrameDecoding(2, 10, 1024, 720, 1024, EnumImagePixelFormat.IPF_GRAYSCALED, "");
reader.stopFrameDecoding();
reader.destroy();
```

## initFrameDecodingParameters

Initialize frame decoding parameters with default values.

```java
FrameDecodingParameters com.dynamsoft.dbr.BarcodeReader.initFrameDecodingParameters() throws BarcodeReaderException
```

### Return value

The frame decoding parameters.

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
FrameDecodingParameters parameters = reader.initFrameDecodingParameters();
reader.destroy();
```

## setErrorCallback

Set callback interface to process errors generated during frame decoding.

```java
void com.dynamsoft.dbr.BarcodeReader.setErrorCallback(ErrorCallback errorCallback, Object userData) throws BarcodeReaderException
```

### Parameters

- `errorCallback`: Callback interface.
- `userData`: Customized arguments passed to your function.

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
reader.setErrorCallback(new ErrorCallback() {
    @Override
    public void errorCallback(int frameId, int errorCode, Object userData) {
        //TODO add your code for using error code
    }
}, null);
reader.startFrameDecoding(2, 10, 1024, 720, 1024, EnumImagePixelFormat.IPF_GRAYSCALED, "");
```

## setTextResultCallback

Set callback interface to process text results generated during frame decoding.

```java
void com.dynamsoft.dbr.BarcodeReader.setTextResultCallback(TextResultCallback textResultCallback, Object userData) throws BarcodeReaderException	
```

### Parameters

- `textResultCallback`: Callback interface.
- `userData`: Customized arguments passed to your function.

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
reader.setTextResultCallback(new TextResultCallback() {
    @Override
    public void textResultCallback(int frameId, TextResult[] results, Object userData) {
        //TODO add your code for using text results
    }
}, null);
reader.startFrameDecoding(2, 10, 1024, 720, 1024, EnumImagePixelFormat.IPF_GRAYSCALED, "");
```

## setIntermediateResultCallback

Set callback interface to process intermediate results generated during frame decoding.

```java
void com.dynamsoft.dbr.BarcodeReader.setIntermediateResultCallback(IntermediateResultCallback intermediateResultCallback, Object userData} throws BarcodeReaderException
```

### Parameters

- `intermediateResultCallback`: Callback interface.
- `userData`: Customized arguments passed to your function.

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
PublicRuntimeSettings settings = reader.getRuntimeSettings();
settings.intermediateResultTypes = EnumIntermediateResultType.IRT_ORIGINAL_IMAGE | EnumIntermediateResultType.IRT_COLOUR_CLUSTERED_IMAGE | EnumIntermediateResultType.IRT_COLOUR_CONVERTED_GRAYSCALE_IMAGE;
reader.updateRuntimeSettings(settings);
reader.setIntermediateResultCallback(new IntermediateResultCallback() {
    @Override
    public void intermediateResultCallback(int frameId, IntermediateResult[] results, Object userData) {
        //TODO add your code for using intermediate results
    }
}, null);
reader.startFrameDecoding(2, 10, 1024, 720, 1024, EnumImagePixelFormat.IPF_GRAYSCALED, "");
```

## getLengthOfFrameQueue

Get length of current inner frame queue.

```java
int com.dynamsoft.dbr.BarcodeReader.getLengthOfFrameQueue()	
```

### Return value

Returns length of current inner frame queue.

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
int length = reader.getLengthOfFrameQueue();
reader.destroy();
```
