# QuickFaceAnalyzer

This project is a sample Android Application to show the power of HMS MLKit Face recognition feature
integrated with Android CameraX

![Demo](https://github.com/joaobiriba/QuickFaceAnalyzer/blob/master/face.gif)


## Important bits

In the [AndroidManifest.xml](https://github.com/joaobiriba/QuickFaceAnalyzer/blob/master/app/src/main/AndroidManifest.xml) is enabled the dependency of the face model for HMS ML Kit with

```xml
 <meta-data
        android:name="com.huawei.hms.ml.DEPENDENCY"
        android:value="face" />
 ```

In the [FaceDetectorProcessor.kt](https://github.com/joaobiriba/QuickFaceAnalyzer/blob/master/app/src/main/java/com/huawei/quickfaceanalyzer/processor/face/FaceDetectorProcessor.kt) there is the creation of the Face Analyzer responsible to detect the faces in an image

```kotlin
        detector = MLAnalyzerFactory.getInstance().getFaceAnalyzer(options)
 ```

The option passed as argument can have multiple statements
```kotlin
    val faceDetectorOptions = MLFaceAnalyzerSetting.Factory()
                .setFeatureType(MLFaceAnalyzerSetting.TYPE_FEATURE_OPENCLOSEEYE)
                .setFeatureType(MLFaceAnalyzerSetting.TYPE_FEATURE_EMOTION)
                .setFeatureType(MLFaceAnalyzerSetting.TYPE_KEYPOINTS)
                .setShapeType(MLFaceAnalyzerSetting.TYPE_SHAPES)
                .allowTracing(MLFaceAnalyzerSetting.MODE_TRACING_FAST)
                .create()
 ```
feel free to check the [documentation](https://developer.huawei.com/consumer/en/doc/development/HMSCore-References-V5/mlfaceanalyzersetting-0000001050169395-V5)
for more options

Every time the detector detects one or more faces these will be returned in the onSuccess
```kotlin
   override fun onSuccess(faces: List<MLFace>, graphicOverlay: GraphicOverlay) {
        for (face in faces) {
            graphicOverlay.add(FaceGraphic(graphicOverlay, face))
            logExtrasForTesting(face)
        }
    }
```
From a MLFace object You will be able to get 

[Emotions](https://developer.huawei.com/consumer/en/doc/development/HMSCore-References-V5/mlfaceemotion-0000001050169397-V5)

[Face Features](https://developer.huawei.com/consumer/en/doc/development/HMSCore-References-V5/mlfacefeature-0000001050167444-V5)

[Feature Key Points](https://developer.huawei.com/consumer/en/doc/development/HMSCore-References-V5/mlfacekeypoint-0000001050169399-V5)

[Face feature contour](https://developer.huawei.com/consumer/en/doc/development/HMSCore-References-V5/mlfaceshape-0000001050167446-V5)

Also check [FaceGraphic.kt](https://github.com/joaobiriba/QuickFaceAnalyzer/blob/master/app/src/main/java/com/huawei/quickfaceanalyzer/graphic/face/FaceGraphic.kt) for a sample to check how to display the info you want on the canvas

In the [OnSwipeTouchListener.kt](https://github.com/joaobiriba/QuickFaceAnalyzer/blob/master/app/src/main/java/com/huawei/quickfaceanalyzer/utils/OnSwipeTouchListener.kt) there is the code to handle the Top to Bottom swype down gesture to change the camera
## Usage

Open the project with Android Studio 4.0 and run it or alternatively use gradle directly

Enable the permissions asked by the system

Point the camera to a face 

Swype down from top to bottom on the screen to change camera

## Use it!

You are encouraged to try it out and study and hack every parts to achieve your own target
