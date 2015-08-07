#Mongodb

## 下载
![地址](https://www.mongodb.org/downloads)

## 解压启动
1. cd到mongodb bin目录下
2. 命名模式: mongod.exe --dbpath=c:\data
3. 测试:	http://localhost:27017
4. 启动客户端: 命名模式: mongo.exe

## 操作
1. insert: db.person.insert({"name":"zhongwei","age":20})
2. find: db.person.find()
3. update: db.person.update({"name":"zhongwei"},{"name":"zhongwei","age":30})
4. remove: db.person.remove({"name":"zhongwei"})

## 服务管理
1. mongod --dbpath=c:\data --logpath=c:\log\mongolog.txt --port 2322 --install
2. mongod --dbpath=c:\data --logpath=c:\log\mongolog.txt --port 2322 --remove

## C#调用
```
using System.Collections.Generic;
using System.Threading.Tasks;
using MongoDB.Bson;
using MongoDB.Driver;

namespace MongodbDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            var mongodbHelper =new MongodbHelper();
            //var updateTask = mongodbHelper.Update(new Person() { Name = "LearninghardUpdate", Age = 25 });
            //updateTask.Wait();

            var taskAdd = mongodbHelper.Add(new Person() { Id = ObjectId.GenerateNewId().ToString(), Name = "Learninghard2", Age = 25 });
            taskAdd.Wait();
            foreach (var person in mongodbHelper.SelectAll())
            {
                Console.WriteLine("Name: {0}, Age: {1}", person.Name, person.Age);
            }

            Console.Read();
        }
    }

    public class MongodbHelper
    {
        private const string Conn = "mongodb://localhost:2322";

        private const string DbName = "test";

        private const string TbName = "person";

        private readonly MongoClient client;
        private readonly IMongoDatabase dbDatabase;

        public MongodbHelper()
        {
            // 创建数据连接
            client = new MongoClient(Conn);
            
            // 获取指定数据库
            dbDatabase = client.GetDatabase(DbName);
        }

        public async Task Add(Person p)
        {
            // 获取表
            var collection = dbDatabase.GetCollection<Person>(TbName);

            // 插入
            await collection.InsertOneAsync(p);
        }

        public async Task Delete(string name)
        {
            var collection = dbDatabase.GetCollection<Person>(TbName);
            var filter = Builders<Person>.Filter.Eq("Name", name);

            await collection.DeleteOneAsync(filter);
        }

        public async Task Update(Person p)
        {
            //获取表
            var col = dbDatabase.GetCollection<Person>(TbName);

            var filter = Builders<Person>.Filter.Eq("Age", p.Age);
            var update = Builders<Person>.Update.Set("Name", p.Name); 
            
            await col.UpdateManyAsync(filter, update);
        }

        public Person SelectOne(string name)
        {
            var collection = dbDatabase.GetCollection<Person>(TbName);

            var filter = Builders<Person>.Filter.Eq("Name", name);

            var person = collection.Find(filter).FirstAsync().Result;

            return person;
        }

        public IEnumerable<Person> SelectAll()
        {
            var persons =new List<Person>();

            var collection = dbDatabase.GetCollection<Person>(TbName);
            var result = collection.Find(p => true).ToListAsync();
            result.Wait();
            persons.AddRange(result.Result);

            return persons;
        }
    }

    public class Person
    {
        public string Id { get; set; }

        public string Name { get; set; }

        public int Age { get; set; }
    }
}
```

## 备注
1. 工具: MongoVUE


