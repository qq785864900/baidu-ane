百度ane是一个方便flash as3开发人员在flex，flash air 移动应用中添加百度移动广告联盟广告的ane插件，
支持flash air ios和flash air android，支持百度广告联盟全屏广告和banner广告
百度广告联盟网站：http://munion.baidu.com/
版本号：1.0
构建于：adobe air sdk 4.0，百度移动推广sdk android 3.42 ，百度移动应用广告ios sdk3.4.7
iphone4/ios7,iphone5/ios7,小米/android 4测试都ok

使用：
1.在百度广告联盟网站创建应用，获取广告id和计费id
2.添加baidu1.0.ane到flex air项目或者flash android ，flash ios项目中。具体怎么在flex air项目中加ane可以在网上找
3.书写下面代码,正式上传应用到商店时把debug改成在百度网站获得的广告id和计费ID
if(BaiDu.getInstance().supportDevice){
	BaiDu.getInstance().setKeys("debug","debug");//	BaiDu.getInstance().setKeys("appsid","计费id");
	BaiDu.getInstance().showBanner(BaiDu.BANNER,RelationPosition.BOTTOM_CENTER);
}
4.确认xxx-app.xml中已经有ane的id代码
 <extensionID>com.baidu.mobads</extensionID>
5.ios只需要上门4步，android版本需要比ios多出此步骤
     a.给应用添加相关权限，确认在xxx-app.xml中添加下面的权限代码
            <uses-permission android:name="android.permission.INTERNET"/>
	    <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
	    <uses-permission android:name="android.permission.READ_PHONE_STATE"/>
	    <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
	    <uses-permission android:name="android.permission.ACCESS_WIFI_STATE"/>
	    <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>
     b.代码中添加广告的Activity，提交给百度审核时需要加俩meta-data，值是百度申请到的ID，提交到市场的时候可以删除
        <application>
    	<meta-data android:name="BaiduMobAd_APP_ID" android:value="debug" /> 
	<meta-data android:name="BaiduMobAd_APP_SEC" android:value="debug" />
  	 <activity android:name="com.baidu.mobads.AppActivity" android:configChanges="keyboard|keyboardHidden|orientation"/> 
	</application>
     c.打包出apk，把extra目录拖进apk中。可以用apktool做，也可以用winrar做，打开方式选择winrar，然后把extra目录拖进去，就可以了,拖进去后apk目录结构可以看截图
     d.给修改后的apk签名，可以用命令行的方式给apk签名（做法可以百度 给apk签名，专业做法），也可以用用"APK签名工具.exe"签名(简单菜鸟的做法)
6.apk或者ipa打包出来后需要提交到百度广告联盟审核，提交申请前记得把debug都换成应用的appsid和计费id

ane其他api:
缓存加载百度全屏广告
public function cacheInterstitial():void
展示广告，展示前先需要缓存好
public function showInterstitial():void
检测百度移动全屏广告是否缓存好了
public function isInterstitialReady():Boolean
相对位置，展示百度移动应用banner广告
public function showBanner(adSize:BaiDuSize, position:int):void
绝对定位展示百度应用广告
public function showBannerAbsolute(adSize:BaiDuSize, x:Number, y:Number):void
隐藏banner广告
public function hideBanner():void

ane支持广告相关的各种事件在BaiDuAdEvent中的常量
广告隐藏
public static const onBannerDismiss:String = "onBannerDismiss";
广告加载失败
public static const onBannerFailedReceive:String = "onBannerFailedReceive";
点击广告离开应用
public static const onBannerLeaveApplication:String = "onBannerLeaveApplication";
展示广告
public static const onBannerPresent:String = "onBannerPresent";
接收到广告
public static const onBannerReceive:String = "onBannerReceive";
全屏广告关闭
public static const onInterstitialDismiss:String = "onInterstitialDismiss";
全屏广告加载失败
public static const onInterstitialFailedReceive:String = "onInterstitialFailedReceive";
点击了全屏广告跳出应用
public static const onInterstitialLeaveApplication:String = "onInterstitialLeaveApplication";
全屏广告将展示
public static const onInterstitialPresent:String = "onInterstitialPresent";
全屏广告加载成功
public static const onInterstitialReceive:String = "onInterstitialReceive";
