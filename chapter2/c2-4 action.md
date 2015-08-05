#Action

## 继承图
![](img/action.png)

## schedulerUpdate
```
bool HelloWorld::init()
{
    scheduleUpdate();
    return true;
}

void HelloWorld::update(float dt)
{
    log("update");
}
```
## schedule
```
bool HelloWorld::init()
{
    schedule(schedule_selector(HelloWorld::updateCustom), 1.0f, kRepeatForever, 0);
    return true;
}

void HelloWorld::updateCustom(float dt)
{
    log("Custom");
}
```

## scheduleOnce
```
bool HelloWorld::init()
{
    scheduleOnce(schedule_selector(HelloWorld::updateOnce), 0.1f);
    return true;
}

void HelloWorld::updateOnce(float dt)
{
    log("Once");
}
```



