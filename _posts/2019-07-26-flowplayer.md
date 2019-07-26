---
layout: post
title: Plowpayer
---


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
