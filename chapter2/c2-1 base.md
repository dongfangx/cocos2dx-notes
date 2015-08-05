#基础

## 框架图
![](img/frame.png)

## Director
```
Director::getInstance();

```
## eg
```
auto scene = Scene::create();
auto layer = HelloWorld::create();
scene->addChild(layer);
auto sprite = Sprite::create("HelloWorld.png");
layer->addChild(sprite, 0);
Director::getInstance()->runWithScene(scene);

```