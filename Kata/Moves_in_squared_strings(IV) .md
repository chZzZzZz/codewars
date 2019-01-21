#18.Moves in squared strings (IV)

You are given a string of n lines, each substring being n characters long: For example:

>s = "abcd\nefgh\nijkl\nmnop"  
We will study some transformations of this square of strings.

   Symmetry with respect to the main cross diagonal: diag_2_sym (or diag2Sym or diag-2-sym)

  >diag_2_sym(s) => "plhd\nokgc\nnjfb\nmiea"

   Counterclockwise rotation 90 degrees: rot_90_counter (or rot90Counter or rot-90-counter)

   >rot_90_counter(s)=> "dhlp\ncgko\nbfjn\naeim"

   selfie_diag2_counterclock (or selfieDiag2Counterclock or selfie-diag2-counterclock) It is initial string + string obtained by symmetry with respect to the main cross diagonal + counterclockwise rotation 90 degrees .

   >s = "abcd\nefgh\nijkl\nmnop" --> 
    "abcd|plhd|dhlp\nefgh|okgc|cgko\nijkl|njfb|bfjn\nmnop|miea|aeim"

   or printed for the last:

>selfie_diag2_counterclock  
abcd|plhd|dhlp  
efgh|okgc|cgko  
ijkl|njfb|bfjn  
mnop|miea|aeim  

#Examples:

s = "abcd\nefgh\nijkl\nmnop"  
oper(diag_2_sym, s) => "plhd\nokgc\nnjfb\nmiea"  
oper(rot_90_counter, s) => "dhlp\ncgko\nbfjn\naeim"  
oper(selfie_diag2_counterclock, s) => "abcd|plhd|dhlp\nefgh|okgc|cgko\nijkl|njfb|bfjn\nmnop|miea|aeim"

```cpp
#include <iostream>
#include <string>
#include <sstream>
#include <vector>

class Opstrings4
{
public:
    static std::string diag2Sym(const std::string &strng);
    static std::string rot90Counter(const std::string &strng);
    static std::string selfieDiag2Counterclock(const std::string &strng);
    // your function oper...
    template <typename Func>
    static std::string oper(Func func, const std::string &s);
};

std::string Opstrings4::diag2Sym(const std::string &strng){
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

    std::string diag1str = restr.substr(0,restr.size()-1);
    std::string diag2str;
    for (int i = diag1str.size() - 1; i >= 0;i--){
        diag2str += diag1str[i];
    }
    return diag2str;
}

std::string Opstrings4::rot90Counter(const std::string &strng){
    std::string diag2str = Opstrings4::diag2Sym(strng);
    std::stringstream ss(diag2str);
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

std::string Opstrings4::selfieDiag2Counterclock(const std::string &strng){
    std::string diagstr = Opstrings4::diag2Sym(strng);
    std::string rotstr = Opstrings4::rot90Counter(strng);
    std::stringstream s(strng);
    std::string temp1;
    std::stringstream ss(diagstr);
    std::string temp2;
    std::stringstream sss(rotstr);
    std::string temp3;
    std::string result;

    while((s>>temp1)&&(ss>>temp2)&&(sss>>temp3)){
        result = result + temp1 + '|' + temp2 + '|' + temp3 + '\n';
    }
    return result.substr(0, result.size() - 1);
}
template <typename Func>
std::string Opstrings4::oper(Func func,const std::string &s){
    return func(s);
}
```