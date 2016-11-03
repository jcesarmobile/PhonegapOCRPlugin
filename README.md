PhonegapOCRPlugin iOS
=================

***This plugin is deprecated and it's not maintained. But I've created a new plugin cordova-plugin-tesseract-ocr (https://github.com/jcesarmobile/cordova-plugin-tesseract-ocr). It's still a work in progress***

ocr plugin for phonegap iOS using tesseract

HOW TO USE:

drag the tessdata folder to your phonegap project in Xcode
mark the checkbox "copy items into destination group"
Choose the radio-button "Create folder references for any added folders"
The tessdata contains a trained data for english language. 
If you want to use other language download the language file from http://code.google.com/p/tesseract-ocr/downloads/list if available and change the "eng"
to the language code in this line inside the init function in claseAuxiliar.mm
tesseract->Init([dataPath cStringUsingEncoding:NSUTF8StringEncoding], "eng");

drag the dependencies folder to your phonegap project in Xcode
mark the checkbox "copy items into destination group"
Choose the radio-button "Created groups for any added folders" 

drag OCRPlugin.h, OCRPlugin.m, claseAuxiliar.h and claseAuxiliar.mm to your project in Xcode

drag OCRPlugin.js to your www folder (open the www folder in finder and drag there)

Add the plugin to Cordova.plist with this values

com.jcesarmobile.OCRPlugin   OCRPlugin

If you use a newer version that uses config.xml instead Codova.plist add a new plugin line into the plugins section with this values


name="com.jcesarmobile.OCRPlugin" value="OCRPlugin"




Thanks to suzuki for compiling tesseract in this post
http://tinsuke.wordpress.com/2011/11/01/how-to-compile-and-use-tesseract-3-01-on-ios-sdk-5

I have included an index.html with an example.

It uses the camera function with destinationType.FILE_URI (IMPORTANT!!!)


            // A button will call this function
            //
            function capturePhoto() {
                // Take picture using device camera and retrieve image as base64-encoded string
                navigator.camera.getPicture(onPhotoURISuccess, onFail, { quality: 100,
                                            destinationType: destinationType.FILE_URI });
            }
            
            // Call the plugin when a photo is successfully retrieved
            //
            function onPhotoURISuccess(imageURI) {
                callNativePlugin({url_imagen: imageURI});
            }
            

            function callNativePlugin( returnSuccess ) { 
                OCRPlugin.callNativeFunction( nativePluginResultHandler, nativePluginErrorHandler, returnSuccess ); 
            } 
            
            function nativePluginResultHandler (result) { 
                alert("ok: "+result);
            } 
            
            function nativePluginErrorHandler (error) { 
                alert("error: "+error);
            }



