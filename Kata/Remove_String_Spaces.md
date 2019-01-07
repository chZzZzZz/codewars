#3. 返回删除字符串中的空格后的字符串(8kyu)  

```cpp
#include <iostream>

std::string no_space(std::string x)
{
    //your code here
    std::string result_str="";
    for(int i=0;i<x.size();i++)
    {if(x[i]!=' ')
        {result_str+=x[i];
        }
    }
    return result_str;
}
```  

方法二：

```cpp
#include <iostream>
#include <algorithm>
std::string no_space(std::string x)
{
    x.erase(std::remove(x.begin(), x.end(), ' '), x.end());//remove覆盖空格，erase删除后面多余没用的字符
    return x;
}
```