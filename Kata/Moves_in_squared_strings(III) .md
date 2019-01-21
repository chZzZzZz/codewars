#17.Moves in squared strings (III)
You are given a string of n lines, each substring being n characters long: For example:

s = "abcd\nefgh\nijkl\nmnop"

We will study some transformations of this square of strings.

Symmetry with respect to the main diagonal: diag_1_sym (or diag1Sym or diag-1-sym)

   >diag_1_sym(s) => "aeim\nbfjn\ncgko\ndhlp"

Clockwise rotation 90 degrees: rot_90_clock (or rot90Clock or rot-90-clock)

>rot_90_clock(s) => "miea\nnjfb\nokgc\nplhd"

   selfie_and_diag1(s) (or selfieAndDiag1 or selfie-and-diag1) It is initial string + string obtained by symmetry with respect to the main diagonal.

>s = "abcd\nefgh\nijkl\nmnop" --> 
    "abcd|aeim\nefgh|bfjn\nijkl|cgko\nmnop|dhlp"

   or printed for the last:
>selfie_and_diag1  
abcd|aeim  
efgh|bfjn  
ijkl|cgko   
mnop|dhlp  

#Task:

>Write these functions diag_1_sym, rot_90_clock, selfie_and_diag1

and

   >high-order function oper(fct, s) where
        fct is the function of one variable f to apply to the string s (fct will be one of diag_1_sym, rot_90_clock, selfie_and_diag1)

#Examples:

s = "abcd\nefgh\nijkl\nmnop"  
oper(diag_1_sym, s) => "aeim\nbfjn\ncgko\ndhlp"  
oper(rot_90_clock, s) => "miea\nnjfb\nokgc\nplhd"  
oper(selfie_and_diag1, s) => "abcd|aeim\nefgh|bfjn\nijkl|cgko\nmnop|dhlp"

```cpp
#include <iostream>
#include <string>
#include <sstream>
#include <vector>

class Opstrings3
{
public:
    static std::string diag1Sym(const std::string &strng);
    static std::string rot90Clock(const std::string &strng);
    static std::string selfieAndDiag1(const std::string &strng);
    // ... complete oper
    template<typename Func>
    static std::string oper(Func func, const std::string &s);
};

std::string Opstrings3::diag1Sym(const std::string &strng){
    std::stringstream ss(strng);
    std::string temp;
    std::string restr;

    ss >> temp;
    int n = temp.size();
    std::vector<std::vector<std::string>> res(n);
    for (int i = 0; i < res.size();i++){
        res[i].resize(n);
    }
        for (int i = 0; i < n; ++i)
        {
            res[i][0] = temp[i];
        }
    for (int i = 1; i < n; ++i)
    {
        ss >> temp;
        for (int j = 0; j < n;j++){
            res[j][i] = temp[j];
        }
    }
    for (int i = 0; i < n;i++){
        for (int j = 0; j < n;j++){
            restr+=res[i][j];
        }
        restr += '\n';
    }

    return restr.substr(0,restr.size()-1);
}

std::string Opstrings3::rot90Clock(const std::string &strng){
    std::string diagstr = Opstrings3::diag1Sym(strng);
    std::stringstream ss(diagstr);
    std::string temp;
    std::string res;
    while (ss >> temp)
    {
        for (int i = temp.size() - 1; i >= 0;i--){
            res += temp[i];
        }
        res += '\n';
    }
    return res.substr(0, res.size() - 1);

}

std::string Opstrings3::selfieAndDiag1(const std::string &strng){
    std::string diagstr = Opstrings3::diag1Sym(strng);

    std::stringstream ss1(strng);
    std::stringstream ss2(diagstr);
    std::string temp1;
    std::string temp2;
    std::string res;

    while((ss1>>temp1)&&(ss2>>temp2)){
        res =res + temp1 + '|' + temp2 + '\n';
    }
    return res.substr(0, res.size() - 1);
}

template<typename Func>
std::string Opstrings3::oper(Func func, const std::string &s){
    return func(s);
}
```

方法二：

```cpp
namespace Opstrings3
{
  std::string diag1Sym(const std::string &strng) {
    int n = strng.find('\n');
    std::string s = strng;
    for (int i = 0; i < n; ++i)
      for (int j = 0; j < n; ++j)
        s[j * (n + 1) + i] = strng[i * (n + 1) + j];
    return s;
  }
  
  std::string rot90Clock(const std::string &strng) {
    int n = strng.find('\n');
    std::string s = strng;
    for (int i = 0; i < n; ++i)
      for (int j = 0; j < n; ++j)
        s[j * (n + 1) + n - i - 1] = strng[i * (n + 1) + j];
    return s;
  }
  
  std::string selfieAndDiag1(const std::string &strng) {
    int n = strng.find('\n'), w = 2 * (n + 1);
    std::string s(w * n - 1, '\n');
    for (int i = 0; i < n; ++i) {
      s[i * w + n] = '|';
      for (int j = 0; j < n; ++j)
        s[j * w + i + n + 1] = s[i * w + j] = strng[i * n + i + j];
    }
    return s;
  }
  
  template <typename F>
  std::string oper(F f, const std::string &s) { return f(s); }
}
```