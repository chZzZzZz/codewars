#13.Reverse Letter
Given a string str, reverse it omitting all non-alphabetic characters.
example:For str = "ultr53o?n", the output should be "nortlu".

```cpp
std::string reverse_letter(const std::string &str)
{
    std::string ret;
    for(int i=str.size()-1;i>=0;i--){
    if((str[i]>='a')&&(str[i]<='z')){
        ret+=str[i];
        }
    }
    return ret; //coding and coding..
}
```

方法二：

```cpp
std::string reverse_letter(const std::string &str)
{
    std::string copy(str.rbegin(), str.rend());
    copy.erase(std::remove_if(copy.begin(), copy.end(), [](char c) { return !isalpha(c); } ), copy.end());
    return copy;
}
```