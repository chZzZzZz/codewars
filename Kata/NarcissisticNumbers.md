#1.判断一个数是不是Narcissistic number？（Does my number look big in this?）(8kyu)
方法一：

```cpp
#include<cmath>
bool narcissistic(int value)
{
    int n = value;
    int sum = 0;
    int digits = log10(value)+1;
    while(n)
    {
     sum+=pow(n%10,digits);
     n=n/10;
    }
    return sum==value;
}
```  

  
方法二

```cpp
#inclue<cmath>
bool narcissistic(int value)
{
    std::string a = std::to_string(value);
    int sum=0;
    for(i=0;i<a.size();i++)
    {
     sum+=pow(a[i]-48,a.size());
    }
    return sum==value;
}
```  

方法三  

```cpp
#include<cmath>
bool narcissistic(int value)
{
    int n =value;
    int sum = 0;
    std:vector<uint8_t> digits;
    do{
       digits.push_back(n%10);
       n/=10;
      }while(n!=0)
    for(auto digit:digits)
    {
     sum+=pow(digit,digits.size());
    }
    reutrn sum==value;
}
```