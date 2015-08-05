#Bone

##工具
1. Spine
2. coco studio

## Spine eg1
```
#include <spine/spine-cocos2dx.h>
#include "spine/spine.h"
using namespace spine;

auto skeletonNode = new SkeletonAnimation("enemy.json", "enemy.atlas");
skeletonNode->setMix("walk", "attack", 0.2f);
skeletonNode->setMix("attack", "walk", 0.4f);

skeletonNode->setAnimation(0, "walk", false);
skeletonNode->setAnimation(0, "attact", false);
skeletonNode->addAnimation(0, "walk", false);
skeletonNode->addAnimation(0, "attact", true);

skeletonNode->debugBones = true;

Size windowSize = Director::getInstance()->getWinSize();
skeletonNode->setPosition(Point(windowSize.width / 2, windowSize.height / 2));
addChild(skeletonNode);
```

## CocoStudio1.6
```
string armName = "animation/BHUG1052_SPA.ExportJson";
ArmatureDataManager::getInstance()->addArmatureFileInfo(armName);
arm8 = Armature::create("BHUG1052_SPA");
arm8->setPosition(DESIGN_W /2,450);
spaLayer->addChild(arm8);
arm8->getAnimation()->playWithIndex(0);
```


