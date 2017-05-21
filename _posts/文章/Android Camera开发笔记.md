---
layout: post
title: Android Camera 开发笔记
categories: 文章
tags: [安卓, Camera]
comments: true
---

## android.hardware.camera2

![camera2流程示意图](https://wx1.sinaimg.cn/mw690/006zFO3ggy1ffpielw6p0j30go0bs0t5.jpg)

管道的概念：英文pipeline，简单的讲就是一个进程的输出作为下一个进程的输入。

![管道](https://wx2.sinaimg.cn/mw690/006zFO3ggy1ffsukpyf3gj30fk0es3zm.jpg)

>引用了管道的概念将安卓设备和摄像头联通起来，系统向摄像头发送`CaptureRequest`请求，摄像头返回`CameraMetadata`元数据。这一切建立在一个叫做`CameraCaptureSession`的会话当中。

重要的类：
- `CameraManager`，用来打开摄像头，`openCamera`方法
- `CameraDevice`，摄像头对象，有一个内部类`StateCallback`用来在打开摄像头的时候回调，`createCaptureRequest`方法，用来创建捕获请求，传递给CaptureRequest.Builder对象，`createCaptureSession`方法，用来创建捕获会话（三个参数，List<Surface>，表示摄像头传过来的数据放入哪个Surface对象中，CaptureRequestSession对象，这个类有两个内部类：StateCallback和CaptureCallback都是用来回调，这里用CameraCaptureSession.StateCallback，最后一个是线程对象，表示哪个线程处理这个会话）。
- `CaptureRequest.Builder`对象，它接受的是CameraDevice.createCaptureRequest()返回的对象，可以设置各种具体的事项，如：自动对焦，自动打开闪光灯，设置摄像头传回来的数据的接受目标

### 打开摄像头

利用CameraManager获取摄像头管理

```java
//获取系统服务
mCameraManager = (CameraManager) getSystemService(Context.CAMERA_SERVICE);
//CameraException，这个IDE会有提示叫你加上
try{
    if(ActivityCompat.checkSelfPermission(this, Manifest.permission.CAMERA) != PackageManager.PERMISSION_GRANTED){
        return;
    }
    //打开摄像头，注意参数：摄像头ID（String，'0'或者'1'，分别代表前后摄像头），stateCallback是一个回调对象，mainHandler是线程处理对象（也就是说把这个打开过程交给哪个线程）
    mCameraManager.openCamera(mCameraID, stateCallback, mainHandler);
} catch(CameraException e){
    e.printStackTrace();
}
```

### 获取摄像头实时预览画面

openCamera的stateCallback（摄像头回调），CameraDevice.StateCallback类（CameraDevice本身是一个类，StateCallback是它的内部类）

```java
private CameraDevice.StateCallback stateCallback = new CameraDevice.StateCallback(){
    //需要重写类中的方法，onOpened，onDisconnected，onError。
    @Override
    public void onOpened(CameraDevice camera){
        mCameraDevice = camera;
        //开启预览，在摄像头回调方法中调用预览方法，也就是说一旦开启摄像头就开始预览
        startPreview();
    }
    @Override
    public void onDisconnected(CameraDevice camera){
        if(null != mCameraDevice){
            mCameraDevice.close();
            MainActivity.this.mCameraDevice = null;
        }
    }
    @Override
    public void onError(CameraDevice camera, int error){
        Toast.makeText(MainActivity.this, "摄像头开启失败", Toast.LENGTH_SHORT).show();
    }
}
```

### 开启预览的方法

```java
private void startPreview(){
    try{
        //创建一个CaptureRequest.Builder实例对象，传入CameraDevice的TEMPLATE_PREVIEW参数（用于获取实时画面预览，其他的几个属性比如：TEMPLATE_STILL_CAPTURE，是用来获取照片；TEMPLATE_RECORD，是用来获取录像）
        final CaptureRequest.Builder previewRequestBuilder = mCameraDevice.createCaptureRequest(CameraDevice.TEMPLATE_PREVIEW);
        //将SurfaceView作为CaptureRequest.Builder的目标输出容器
        previewRequestBuilder.addTarget(mSurfaceHolder.getSurface());
        //创建CameraCaptureSession会话，该对象负责管理预览请求和拍照请求
        mCameraDevice.createCaptureSession(Arrays.asList(mSurfaceHolder.getSurface(), mImageReader.getSurface()), new CameraCaptureSession.StateCallback(){
            @Override
            public void onConfigured(CameraCaptureSession cameraCaptureSession){
                if(null == mCameraDevice)return;
                //当摄像头已经准备好时，开始显示预览
                mCameraCaptureSession = cameraCaptureSession;
                try{
                    //自动对焦，AF的意思：Auto Focus
                    previewRequestBuilder.set(CaptureRequest.CONTROL_AF_MODE,CaptureRequest.CONTROL_AF_MODE_CONTINUOUS_PICTURE);
                    //打开闪光灯，AE的意思：Auto Exposure
                    previewRequestBuilder.set(CaptureRequest.CONTROL_AE_MODE, CaptureRequest.CONTROL_AE_MODE_ON_AUTO_FLASH);
                    mCameraCaptureSession.setRepeatingRequest(previewRequestBuilder.build(), null, childHandler);
                } catch(CameraAccessException e){
                    e.printStackTrace();
                }
            }
            @Override
            public void onConfigureFailed(CameraCaptureSession cameraCaptureSession){
                Toast.makeText(MainActivity.this, "会话建立失败", Toast.LENGTH_SHORT).show();
            }
        }, childHandler);
    } catch(CameraException e){
        e.printStackTrace();
    }
}
```
