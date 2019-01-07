#5 altERnaTIng cAsE <=> ALTerNAtiNG CaSe(8kyu)

```cpp
#include <iostream>
using namespace std;
string to_alternating_case(const string& str)
{
  string new_str=str;
  for(int i=0;i<str.size();i++)
  {
      if(new_str[i]>='a'&& new_str[i]<='z')
      {new_str[i]-=32;}
      else if(new_str[i]>='A'&& new_str[i]<='Z')
      {new_str[i]+=32;}
  }
	return new_str;
}
```

方法二：

```cpp
#include <iostream>
using namespace std;
string to_alternating_case(const string& str)
{
    string ret=str;
    for(char& c:ret){
        c=isupper(c)?tolower(c):toupper(c);    
    }
    return ret;
}
```

方法三：

```cpp
#include <iostream>
using namespace std;
string to_alternating_case(const string& str)
{
    string ret;
    for(char c:str){
        ret+=isupper(c)?tolower(c):toupper(c);    
    }
    return ret;
}
```