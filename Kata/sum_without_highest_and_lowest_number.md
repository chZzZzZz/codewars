#4 sum without highest and lowest number(8kyu)
方法一：

```cpp
#include<vector>
using namespace std;

int sum(vector<int> numbers)
{
    if (numbers.size() <= 1)
      return 0;
      
    int max = numbers[0], min = max, sum = 0;
    for (auto n : numbers) {
      if (n > max) max = n;
      if (n < min) min = n;
      sum += n;
    }
    
    return sum - (min + max);
}
```  

方法二：

```cpp
#include <vector>
#include<algorithm>
int sum(vector<int> numbers)
{
    std::sort(numbers.begin(),numbers.end());
    int sum=0;

    for(int i=1;i<(number.size()-1);i++)
        sum+=numbers[i];

    return sum;
}
```