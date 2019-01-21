#12.Xbonacci 
If you have completed the Tribonacci sequence kata, you would know by now that mister Fibonacci has at least a bigger brother. If not, give it a quick look to get how things work.

Well, time to expand the family a little more: think of a Quadribonacci starting with a signature of 4 elements and each following element is the sum of the 4 previous, a Pentabonacci (well Cinquebonacci would probably sound a bit more italian, but it would also sound really awful) with a signature of 5 elements and each following element is the sum of the 5 previous, and so on.

Well, guess what? You have to build a Xbonacci function that takes a signature of X elements - and remember each next element is the sum of the last X elements - and returns the first n elements of the so seeded sequence.

Example:
>xbonacci {1,1,1,1} 10 = {1,1,1,1,4,7,13,25,49,94}  
xbonacci {0,0,0,0,1} 10 = {0,0,0,0,1,1,2,4,8,16}  
xbonacci {1,0,0,0,0,0,1} 10 = {1,0,0,0,0,0,1,2,3,6}  
xbonacci {1,1} produces the Fibonacci sequence

```cpp
std::vector<int> xbonacci(std::vector<int> signature, int n)
{
    // Your code here
    int X=signature.size();
    
    if(n<X){signature.resize(n);return signature;}
    else{
         
         for(int i=X;i<n;i++){
             int sum=0;
             for(int j=0;j<X;j++){
                 
                 sum+=signature[i-j-1];
             }
             signature.push_back(sum);
             }
         
         return signature;
    }
}
```
简化：

```cpp
std::vector<int> xbonacci(std::vector<int> signature, int n)
{
    int k = signature.size();
    signature.resize(n);
    
    for (int i = k; i < n; ++i)
      for (int j = 1; j <= k; ++j)
        signature[i] += signature[i-j];
    
    return signature;
}
```

方法二：

```cpp
#include <numeric>

std::vector<int> xbonacci(std::vector<int> sequence, int n)
{
    if (n > sequence.size())
    {
        std::size_t sumLength = sequence.size();

        sequence.push_back(std::accumulate(sequence.begin(), sequence.end(), 0));

        for (int i = sequence.size(); i < n; ++i)
        {
            // [n] = [n-1] + [n-2] + ... + [n-x]
            // [n-1] = [n-2] + ... + [n-x] + [n-x-1]
            // rearrange
            // [n-1] - [n-x-1] = [n-2] + ... + [n-x]
            // therefore
            // [n] = [n-1] + [n-1] - [n-x-1]
            // [n] = 2 * [n-1] - [n-x-1]
            sequence.push_back(2 * sequence[i - 1] - sequence[i - sumLength - 1]);
        }
    }
    else
    {
        sequence.resize(n);
    }

    return sequence;
}
```