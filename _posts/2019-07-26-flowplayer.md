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
