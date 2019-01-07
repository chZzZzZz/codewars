#2.取出字符串的中间部分（字符串为奇数个就取出中间的1个字符，字符串为偶数就取出中间的两个字符）(8kyu)
方法一：  

```cpp
std::string get_middle(std::string input)
{
  return input.substr((input.size()-1)/2,(input.size()-1)%2+1);
}
```  
方法二：

```cpp
std::string get_middle(std::string input) 
{
  int i = input.length();

  if ((i % 2) == 0) 
    return input.substr(i/2 - 1, 2);
    
  else
    return input.substr(i/2, 1);
}
```