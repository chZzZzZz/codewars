#19Complete The Pattern #8 - Number Pyramid
###Task:

You have to write a function pattern which creates the following Pattern(See Examples) upto n(parameter) number of rows.

####Rules/Note:

    If the Argument is 0 or a Negative Integer then it should return "" i.e. empty string.
    All the lines in the pattern have same length i.e equal to the number of characters in the last line.
    Range of n is (-∞,100]

###Examples:

pattern(5):

    1    
   121   
  12321  
 1234321 
123454321

```cpp
#include <iostream>
#include <vector>
#include <string>

std::string reverse_str(std::string strng){
    std::string res;
    for (int i = strng.size() - 1; i >= 0;i--){
        res += strng[i];
    }
    return res;
}

std::string pattern(int n)
{
    std::string restr;
    std::vector<std::string> v={"1","2","3","4","5","6","7","8","9","0"};
    if(n<=0){return "";}
    else{
        for (int i = 1; i <= n;i++){
            std::string lhalf;
            std::string mid = std::to_string(i % 10);
            std::string space= std::string(n-i, ' ');
            for (int j = 1;j<i;j++){
                lhalf += v[(j-1)% 10];
            }
            std::string rhalf = reverse_str(lhalf);
            restr += space+lhalf + mid + rhalf + space+'\n';

        }
        return restr.substr(0, restr.size() - 1);
    }
}
```

简化：

```cpp
#include <algorithm>
#include <string>

std::string pattern(int n)
{
    std::string result;

    if (n <= 0)
    {
        return result;
    }
    
    for(int i = 1; i <= n; i++)
    {
        std::string spaces = std::string(n - i, ' ');

        std::string leftNums;
        std::string rightNums;
        for(int j = 1; j <= i - 1; j++)
        {
            leftNums += std::to_string(j%10);
            rightNums += std::to_string(j%10);
        }
        std::reverse(rightNums.begin(),rightNums.end());
        
        result += spaces + leftNums + std::to_string(i%10) + rightNums + spaces;
        
        if (i != n)
        {
            result += '\n';
        }
    }

    return result;
```