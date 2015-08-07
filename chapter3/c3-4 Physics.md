#物理引擎

## eg
```
PhysicsBody *body = PhysicsBody::create();
body->addShape(PhysicsShapeCircle::create(BIRD_RADIUS));
body->setDynamic(true);
body->setLinearDamping(0.0f);
body->setGravityEnable(false);
body->setCategoryBitmask(0x01);					//我是谁
body->setCollisionBitmask(0x02 | 0x03);			//和谁碰撞
body->setContactTestBitmask(0x02 | 0x03);		//碰撞了通知我
this->bird->setPhysicsBody(body);

body2->setCategoryBitmask(0x02);
body2->setCollisionBitmask(0x01);
body2->setContactTestBitmask(0x01);

body3->setCategoryBitmask(0x03);
body3->setCollisionBitmask(0x01);
body3->setContactTestBitmask(0x01);

```

## 备注:
![物理引擎文档](http://cn.cocos2d-x.org/tutorial/show?id=2564)
