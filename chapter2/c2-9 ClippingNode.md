#ClippingNode

##工具
Tiled Map Editor

## code
```
auto bg = LayerColor::create(Color4B(255, 255, 255,255));
this->addChild(bg, -1);//1

auto stencil = Sprite::create("CloseNormal.png");
stencil->setScale(2);//2
auto clipper = ClippingNode::create();
clipper->setStencil(stencil);//设置裁剪模板 //3
clipper->setInverted(true);//设置底板可见
clipper->setAlphaThreshold(0);//设置绘制底板的Alpha值为0
this->addChild(clipper);//4

auto content = Sprite::create("HelloWorld.png");//被裁剪的内容
clipper->addChild(content);//5

clipper->setPosition(Vec2(visibleSize.width/2 + origin.x, visibleSize.height/2 + origin.y));
```



