#9Printer Errors
given a string of which the letters is from 'a' to 'm',the Printer may print wrong char,please write code to return the print error rate(the num of wrong chars/the length of the string)

```cpp
#include <iostream>
#include <algorithm>
class Printer
{
public:
    static std::string printerError(const std::string &s);
};
std::string Printer::printerError(const std::string &s){
    int errsum = 0;
    std::string str = s;
    std::string result ="";
    for(char& c:str){
        if(c>'m') {errsum+=1;}
    }
    result = result+std::to_string(errsum)+"/"+std::to_string(s.size());
    return result;
}
```

方法二

```cpp
#include <iostream>
#include <algorithm>
class Printer
{
public:
    static std::string printerError(const std::string &s);
};

std::string Printer::printerError(const std::string &s){
    return std::to_string(std::count_if(s.cbegin(), s.cend(), [](char c) { return c > 'm'; }))+"/"+std::to_string(s.size());
}
```
