#10 isograms
An isogram is a word that has no repeating letters, consecutive or non-consecutive. Implement a function that determines whether a string that contains only letters is an isogram. Assume the empty string is an isogram. Ignore letter case.
>isIsogram "Dermatoglyphics" == true  
isIsogram "moose" == false  
isIsogram "aba" == false

```cpp
bool is_isogram(std::string str) {
    
    for(int a=0;a<str.size();a++){str[a]=std::tolower(str[a]);}
    if(str=="") {return true;}
    for(int i =0;i<str.size()-1;i++){
        for(int j=i+1;j<str.size();j++){
            if(str[j]==str[i]) {return false;}
        }
    }
    return true;
}
```

方法二

```cpp
#include <cctype>
#include <unordered_set>

bool is_isogram(std::string str)
{
    std::unordered_set<char> char_set;
    for (const auto &c : str) {
        auto c_lower = std::tolower(c);
        if (char_set.count(c_lower) == 0) char_set.insert(c_lower);
        else return false;
    }
    return true;
}
```

方法三

```cpp
#include <string>
#include <set>
#include <algorithm>
using namespace std; 

bool is_isogram(string str) 
{
if (str.length() == 0) {return true;}
transform(str.begin(),str.end(),str.begin(),::tolower);
set <char> iso (str.begin(),str.end());
if (iso.size() == str.length()) {return true;} else {return false;} 
}
```

方法四

```cpp
bool is_isogram(std::string str) {

  for(auto &i: str) i = tolower(i);
  
  std::string temp = str;
  
  sort(temp.begin(), temp.end());
  sort(str.begin(), str.end());
  temp.erase(unique(temp.begin(), temp.end()), temp.end());
  
  return str == temp;
}
```