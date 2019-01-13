#6.Highest Scoring Word:
>Given a string of words, you need to find the highest scoring word.  
Each letter of a word scores points according to it's position in the alphabet: a = 1, b = 2, c = 3 etc.  
You need to return the highest scoring word as a string.If two words score the same, return the word that appears earliest in the original string.  
All letters will be lowercase and all inputs will be valid.

```cpp
#include <iostream>
#include <string>
#include <vector>
std::string highestScoringWord(const std::string &str)
{ int i=0;
  std::vector <std::string> v;
  std::vector <int> scorev;
  while(str[i]!='\0'){
      int score=0;
      std::string ret;
      while(str[i]!=' '&&str[i]!='\0'){
          char c = str[i];
          score+=(int(c)-96);
          ret+=str[i];
          i++;
      }
      v.push_back(ret);
      scorev.push_back(score);
	  if (str[i] != '\0') i++;
  }
  
  int max=scorev[0];
  int max_index=0;
  for(int n=1;n<scorev.size();n++){
      if(scorev[n]>max) {
      max=scorev[n];
      max_index=n;
      } 
  }
  return v[max_index];
}
```

方法二：

```cpp
//ostringstream ： 用于执行C风格字符串的输出操作。
//istringstream ： 用于执行C风格字符串的输入操作。
//stringstream ： 同时支持C风格字符串的输入输出操作。使用它们创建对象必须包含<sstream>头文件
#include <iostream>
#include <sstream>
#include <string>

std::string higheastScoringWord(const std::string &str)
{
    std::string mostScoredS;
    int mostScore=0;
 
    std::stringstream ss(str);
    std::string curr;
    
    while(ss>>curr){
        int score=0;
        for(char c:curr) score+=c-'a'+1;
        if(score>mostScore){
            mostScore=score;
            mostScoredS=curr;
        }
    }
    return mostScoredS;
}
```

方法三

```cpp
#include <iostream>
#include <string>
#include <sstream>
#include<iterator>
#include <vector>


std::string highestScoringWord(const std::string &text)
{
  int highest = 0;
  std::string answer;
  std::istringstream iss(text);
  std::vector<std::string> words(std::istream_iterator<std::string>{iss},
    std::istream_iterator<std::string>());
  
  for (auto word: words) {
    int score = 0;
    for (auto c: word) score += ((int) c) - 96;
    if (score > highest) {
      highest = score;
      answer = word;
    }
  }
  return answer;
}
```