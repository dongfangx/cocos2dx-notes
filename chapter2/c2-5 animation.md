#Animation

## eg1
```
auto animation = Animation::create();
for( int i=1;i<15;i++)
{
    char szName[100] = {0};
    sprintf(szName, "Images/grossini_dance_%02d.png", i);
    animation->addSpriteFrameWithFile(szName);
}
animation->setDelayPerUnit(2.8f / 14.0f);
animation->setRestoreOriginalFrame(true);

auto action = Animate::create(animation);
sprite1->runAction(Sequence::create(action, action->reverse(), nullptr));
```
## eg2
```
auto cache = AnimationCache::getInstance();
cache->addAnimationsWithFile("animations/animations-2.plist");
auto animation2 = cache->getAnimation("dance_1");

auto action2 = Animate::create(animation2);
sprite1->runAction(Sequence::create(action2, action2->reverse(), nullptr));
```

## remove
```
void releaseCaches()
{
    AnimationCache::destroyInstance();
    SpriteFrameCache::getInstance()->removeUnusedSpriteFrames();
    TextureCache::getInstance()->removeUnuserdTextures();
}
```



