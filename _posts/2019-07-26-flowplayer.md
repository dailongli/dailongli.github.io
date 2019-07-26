---
layout: post
title: Plowpayer
---


```
wget http://download.macromedia.com/pub/flex/sdk/flex_sdk_4.6.zip
mkdir /opt/flowplayer
mkdir /opt/flowplayer/flex3sdk
unzip ~/Downloads/flex_sdk_4.6.zip -d /opt/flowplayer/flex3sdk

apt install ant


git clone https://github.com/flowplayer/flash.git
git clone https://github.com/flowplayer/flash-build.git
git clone https://github.com/flowplayer/tld.git
git clone https://github.com/mangui/flashls.git

cd flash-build
ant build-debug
ant

cd flashls/build
FLEXPATH=/opt/flowplayer/flex3sdk sh ./build.sh
```




```
import mx.core.UIComponent;
public class FlowplayerComponent extends UIComponent {
    private var _launcher:Launcher;
}
```



```
html 通过 flashvars 传递参数给flash
<object id="video_api" name="video_api" data="flowplayer.swf" type="application/x-shockwave-flash">
    <param name="flashvars" value="config={...}">
</object>

flash 通过 root.loaderInfo.parameters 获取传进来的参数
```


```
public class Launcher extends StyleableSprite implements ErrorHandler {
    public function Launcher() {
        addEventListener(Event.ADDED_TO_STAGE, onAddedToStage);
    }
    private function onAddedToStage(e:Event):void {
        callAndHandleError(createFlashVarsConfig, PlayerError.INIT_FAILED);
    }
    private function createFlashVarsConfig():void {
        var configStr:String = Preloader(root).injectedConfig || root.loaderInfo.parameters["config"];
        var configObj:Object = configStr && configStr.indexOf("{") == 0 ? ConfigParser.parse(configStr) : {};
    }
}
```


```
public function Config(config:Object, builtInConfig:Object, playerSwfUrl:String, controlsVersion:String, audioVersion:String) {
    this._configObject = createConfigObject(config, builtInConfig);
    _playlistBuilder = new PlaylistBuilder(playerId, this._configObject.playlist, this._configObject.clip);
    _config = ConfigParser.parseConfig(configObj, BuiltInConfig.config, loaderInfo.url, VersionInfo.controlsVersion, VersionInfo.audioVersion);
    callAndHandleError(initPhase1, PlayerError.INIT_FAILED);
}
```

```
public class ConfigParser {
    var configObj:Object = config is String ? com.adobe.serialization.json.JSONforFP.decode(config as String) : config;
    return new Config(configObj, builtInConfig, playerSwfUrl, controlsVersion, audioVersion);
}
```



```
public class Config { 
    public function Config(config:Object, builtInConfig:Object, playerSwfUrl:String, controlsVersion:String, audioVersion:String) {
        this._configObject = createConfigObject(config, builtInConfig);
        _playlistBuilder = new PlaylistBuilder(playerId, this._configObject.playlist, this._configObject.clip);
    }
}
```


```
class PlaylistBuilder {
    public function PlaylistBuilder(playerId:String, playlist:Object, commonClip:Object) {
        _commonClipObject = commonClip;
        if (playlist is Array) {
            _clipObjects = playlist as Array;
        }
    }
}
```
