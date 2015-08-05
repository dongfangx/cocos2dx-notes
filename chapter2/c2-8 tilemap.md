#ParticleSystemQuad

##工具
Tiled Map Editor

## code
```
 auto map = cocos2d::experimental::TMXTiledMap::create("TileMaps/iso-test-bug787.tmx");
//TMXTiledMap *map = TMXTiledMap::create("bg.tmx");
addChild(map, 0);

Vector<Node*> pChildrenArray = map->getChildren();
SpriteBatchNode* child = NULL;
Ref* pObject = NULL;
for (Vector<Node*>::iterator it = pChildrenArray.begin(); it != pChildrenArray.end(); it++) {
    pObject = *it;
    child = (SpriteBatchNode*)pObject;
}

TMXLayer* layer = map->getLayer("layer0");
Sprite* tile0 = layer->getTileAt(Point(1, 15));
layer->removeTileAt(Point(1, 15));

TMXObjectGroup* objectGroup = map->getObjectGroup("center");
ValueVector object = objectGroup->getObjects();
for (ValueVector::iterator it = object.begin(); it != object.end(); it++) {
    Value obj = *it;
    ValueMap map = obj.asValueMap();
    log("x = %d y = %d", map.at("x").asInt(), map.at("y").asInt());
}
```



