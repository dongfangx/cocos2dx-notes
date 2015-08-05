#类文件定义

## 头文件 ControlManager.h

```
#ifndef __ControlManager__
#define __ControlManager__

#include <iostream>
#include "cocos2d.h"

using namespace std;
USING_NS_CC;

class ControlManager
{
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

static ControlManager *instance = nullptr;

ControlManager* ControlManager::getInstance()
{
    if (!instance) {
        instance = new ControlManager();
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
}

```

## 调用

```
ControlManager::getInstance()->goHome();
```



