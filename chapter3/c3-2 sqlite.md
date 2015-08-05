#Sqlite

## 导入sqlite文件
1. sqlite3.c sqlite3.h sqlite3ext.h
2. CppSQLite3.h CppSQLite3.cpp

## 创建DB
```
string dbname = FileUtils::getInstance()->getWritablePath() + kSQLITE_FILE_NAME1;
if (FileUtils::getInstance()->isFileExist(dbname)) {
    remove(dbname.c_str());
}

bool lCreateRes = DatabaseHelper::getInstance()->createDatabase(kSQLITE_FILE_NAME1);
assert(lCreateRes);
```

## 打开db
```
std::string filename = FileUtils::getInstance()->getWritablePath() + kSQLITE_FILE_NAME1;
CppSQLite3DB db;
db.open(filename.c_str());

```

## 查询
```
pageCount = DataManager::getInstance()->count("select max(pagenum) from spatool");

DataManager::getInstance()->update("update maketool set selectnum = 1");

Vector<Model*> DataManager::queryModel(string sql)
{
    CppSQLite3Query q = DbConn::getInstance()->db.execQuery("select * from spa");
    Vector<Model*> vec;
    while (!q.eof())
    {
        Model *ca = new Model;
        ca->setIid(q.getIntField("id"));
        ca->setName(q.getStringField("name"));
        vec.pushBack(ca);
        ca->release();
        q.nextRow();
    }
    return vec;
}
```
