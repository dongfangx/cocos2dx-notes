#Event

## eg

```
auto listener1 = EventListenerTouchOneByOne::create();
listener1->onTouchBegan = [=](Touch* touch, Event* event){    
    Vec2 p1 = this->convertToNodeSpace(touch->getLocation());
    this->onSelect(p1);
    return true;
};
listener1->onTouchMoved = [](Touch* touch, Event* event){
};

listener1->onTouchEnded = [=](Touch* touch, Event* event){
};
listener1->setSwallowTouches(true);
_eventDispatcher->addEventListenerWithSceneGraphPriority(listener1, this);

```



