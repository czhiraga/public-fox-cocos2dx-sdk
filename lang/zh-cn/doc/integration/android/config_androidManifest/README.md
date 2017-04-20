[TOP](../../../../README.md)　>　[Cocos2d-xplugin的导入步骤](../../README.md)　>　[Android项目设置](../README.md)　>　AndroidManifest 选项详情

---

## AndroidManifest.xml Metadata 设定项目详细

|参数名|必须|概要|
|:------|:------|:------|
|APPADFORCE_APP_ID|必须|请输入Force Operation X管理者通知的数值。|
|APPADFORCE_SERVER_URL|必须|请输入Force Operation X管理者通知的数值。|
|APPADFORCE_CRYPTO_SALT|必须|请输入Force Operation X管理者通知的数值。|
|ANALYTICS_APP_KEY|必须|请输入Force Operation X管理者通知的数值。|
|APPADFORCE_ID_DIR|任意|使用内(外)部储存时，可以指定任意保存目录名。<br>未指定时，默认使用包（package）名生成目录。|
|APPADFORCE_ID_FILE|任意|使用内(外)部储存时，可以指定任意保存文件名。<br>未指定时，文件名默认为”__FOX_XUNIQ__”。|
|APPADFORCE_USE_EXTERNAL_STORAGE|任意|指定为0时，不保存在内(外)部储存中。|

#### 使用内部及外部储存进行重复排查。
APP首次启动时，SDK生成的识别ID保存在本地储存或SD卡中，使用次ID可以在APP再次安装时进行重复判定。在<manifest>标签内设置往外部储存里读写文件的必要权限。本设置为任意项目，但为了提高APP再次安装时排除重复安装的精度，建议使用。

	<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />




	/mnt/shell/emulated/0/APP的Package名/__FOX_XUNIQ__

保存文件的目录名默认为package名，可以更改任意目录名及文件名。另外，本功能可以抑制文件生成。希望控制标识符文件的保存地点时，可以在<application>标签中添加以下设置。通常无需设置。<br>
指定任意目录名和文件名，会在Environment.getExternalStorageDirectory().getPath()返回值的路径下面创建出来。

	<meta-data android:name="APPADFORCE_ID_DIR" android:value="任意目录名" />
	<meta-data android:name="APPADFORCE_ID_FILE" android:value="任意文件名" />

<设置案例>

	<meta-data android:name="APPADFORCE_ID_DIR" android:value="fox_id_dir" />
	<meta-data android:name="APPADFORCE_ID_FILE" android:value="fox_id_file" />

<默认保存路径案例>

　(※根据终端及OS版本有所不同。)

	/mnt/shell/emulated/0/APP的package名/__FOX_XUNIQ__

> ※ Environment.getExternalStorageDirectory().getPath()返回值根据终端和OS版本有所不同。<br>
> ※ ”APPADFORCE_ID_DIR”(任意目录名)未指定，任意文件名已指定时，将在生成APP的package名目录中保存任意文件名。<br>
> ※ ”APPADFORCE_ID_FILE”(任意文件名)未指定，任意目录名已指定时，将在任意目录名中保存为”__XUNIQ__”文件。

####AndroidManifest.xml的设置案例

	<?xml version="1.0" encoding="utf-8"?>

	        <meta-data android:name="com.google.android.gms.version"
				android:value="@integer/google_play_services_version" />
③	必须设置meta-data<br>
④	不使用内(外)部储存保存功能设置：ON
⑤	项目中导入GooglePlayServices类库时必须设置
