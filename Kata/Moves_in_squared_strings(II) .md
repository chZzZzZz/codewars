#16 Moves in squared strings (II)(6kyu)
You are given a string of n lines, each substring being n characters long: For example:

>s = "abcd\nefgh\nijkl\nmnop"

We will study some transformations of this square of strings.

   Clock rotation 180 degrees: rot

>rot(s) => "ponm\nlkji\nhgfe\ndcba"

   selfie_and_rot(s) (or selfieAndRot or selfie-and-rot) It is initial string + string obtained by clock rotation 180 degrees with dots interspersed in order (hopefully) to better show the rotation when printed.

>s = "abcd\nefgh\nijkl\nmnop" --> 
 "abcd....\nefgh....\nijkl....\nmnop....\n....ponm\n....lkji\n....hgfe\n....dcba"


Task:

>Write these two functions rotand selfie_and_rot

and

 >high-order function oper(fct, s) where
        fct is the function of one variable f to apply to the string s (fct will be one of rot, selfie_and_rot)  

#Examples:

>s = "abcd\nefgh\nijkl\nmnop"
oper(rot, s) => "ponm\nlkji\nhgfe\ndcba"
oper(selfie_and_rot, s) => "abcd....\nefgh....\nijkl....\nmnop....\n....ponm\n....lkji\n....hgfe\n....dcba"


```cpp
#include <iostream>
#include <string>
#include <sstream>

class Opstrings1
{

public:
    static std::string rot(const std::string &strng);
    static std::string selfieAndRot(const std::string &strng);
    // ... complete oper
    template<typename Func>
    static std::string oper(Func func, const std::string &s);
};

std::string Opstrings1::rot(const std::string &strng){
    std::string ret;
    for (int i = strng.size() - 1; i >= 0;i--){
        ret += strng[i];
    }
    return ret;
    //return std::string(strng.rbegin(),strng.rend());
}

std::string Opstrings1::selfieAndRot(const std::string &strng){
    std::string ret;
    std::string temp;
    std::string res;
    std::stringstream ss(strng);

    int n;
    
    while(ss>>temp){
        n = temp.size();
        ret = ret + temp + std::string(n,'.') + "\n";  //std::string(n,'.')构造多个重复字符
    }
    res = Opstrings1::rot(ret);
    res = ret.substr(0, ret.size() - 1)+res;
    return res;
}
template<typename Func>
std::string Opstrings1::oper(Func func, const std::string &s){
        return func(s);
} 
```