#11.Tribonacci Sequence
Tribonacci  works basically like a Fibonacci, but summing the last 3 (instead of 2) numbers of the sequence to generate the next.
Given a Signature contain 3 numbers which is a fibnacci array and n .You should return the first n elements of a Tribonacci array including signature.
example:

```cpp
std::vector<int> tribonacci(std::vector<int> signature, int n)
{
    if(n<3){
       signature.resize(n);
    }
    for(unsigned int i = 3; i<n;i++){
      signature.push_back(signature[i-3]+signature[i-2]+signature[i-1]);
    }
    return signature;
}
```