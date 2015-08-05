#类文件定义

## 头文件 ControlManager.h

```
#ifndef __ControlManager__
#define __ControlManager__

#include <iostream>
#include "cocos2d.h"
#include "SimpleaudioEngine.h"

using namespace std;
using namespace CocosDenshion;
USING_NS_CC;

enum menuType
{
    kBack = 100,    
    kMenu_bg,
};

class ControlManager
{
private:
    bool isOk;
public:
    static ControlManager* getInstance();

    void goHome();  
    
    ~ControlManager();
};

#endif
```

## 实现文件 ControlManager.cpp

```
#include "ControlManager.h"
#include "HomeScene.h"

const string ModelSound[] = {"Wow.mp3","Awesome.mp3"};

static ControlManager *instance = nullptr;

ControlManager* ControlManager::getInstance()
{
    if (!instance) {
        instance = new ControlManager();
        isOk = true;
    }
    return instance;
}

ControlManager::~ControlManager()
{
}

void ControlManager::goHome()
{
    #if CC_TARGET_PLATFORM == CC_PLATFORM_IOS
    Director::getInstance()->replaceScene(TransitionFade::create(1.0, Home::scene()));
    #else
    Director::getInstance()->replaceScene(Home::scene());
    #endif
    SimpleAudioEngine::getInstance()->playEffect(ModelSound[arc4random() % 2].c_str());


}

```

## 调用

```
ControlManager::getInstance()->goHome();
```



