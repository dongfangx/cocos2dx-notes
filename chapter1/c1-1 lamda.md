#Lamda

## eg1

```
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

template<typename T>
class print
{
public:
    void operator()(T n)
    {
        cout<<n <<" ";
    }
};

int main()
{
    vector<int> vec;
    for(int i=0; i<10; i++)
        vec.push_back(i);
    cout<<"print from lambda:";
    for_each(vec.begin(), vec.end(), [](int n){cout<<n<<" ";});
    
    cout<<endl<<"print from function object:";
    print<int> p;
    for_each(vec.begin(), vec.end(), p); 
    cout<<endl;
    return 0;
}

```

## 主动调用

```
int num = [](int num)->int{return ++num;}(10);  
cout<<num<<endl; 

auto lambda = [](int num)
{
    cout<<++num<<endl;
};
lambda(10);

```

## 调用
```
[],[=],[&],[var],[&var]
```
