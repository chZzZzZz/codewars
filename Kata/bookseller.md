#8Help the bookseller
A bookseller has lots of books classified in 26 categories labeled A, B, ... Z. Each book has a code c of 3, 4, 5 or more capitals letters. The 1st letter of a code is the capital letter of the book category. In the bookseller's stocklist each code c is followed by a space and by a positive integer n (int n >= 0) which indicates the quantity of books of this code in stock.

For example an extract of one of the stocklists could be:
L = {"ABART 20", "CDXEF 50", "BKWRK 25", "BTSQZ 89", "DRTYM 60"}.
You will be given a stocklist (e.g. : L) and a list of categories in capital letters e.g : M = {"A", "B", "C", "W"}

 and your task is to find all the books of L with codes belonging to each category of M and to sum their quantity according to each category.

For the lists L and M of example you have to return the string (in Haskell/Clojure a list of pairs):  (A : 20) - (B : 114) - (C : 50) - (W : 0)
 where A, B, C, W are the categories, 20 is the sum of the unique book of category A, 114 the sum corresponding to "BKWRK" and "BTSQZ", 50 corresponding to "CDXEF" and 0 to category 'W' since there are no code beginning with W.

If L or M are empty return string is "" (Clojure should return an empty array instead).

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
#include <sstream>

int get_num(std::string &str){
    std::string num = str.substr(str.find(' '), str.size());
    std::stringstream ss(num);
    int n;
    ss >> n;
    return n;
}
class StockList
{
public:
  static std::string stockSummary(std::vector<std::string> &lstOfArt, std::vector<std::string> &categories);
};
std::string StockList::stockSummary(std::vector<std::string> &lstOfArt, std::vector<std::string> &categories)
{
    if(lstOfArt.empty()||categories.empty())
        return "";
    
    std::string result = "";
   
    
    for(auto cate : categories){
        int sum=0;
        std::string aa;
        std::stringstream ss;
        for(auto book:lstOfArt){
            if(book[0]==cate[0]){
                int booknum = get_num(book);
                sum += booknum;
            }
        }
        ss << sum;
        ss >> aa;
        result += "(" + cate + " : " + aa + ")"+" - ";
    }
    result = result.substr(0,result.size()-3);
    return result;

}
```

方法二  

```cpp
class StockList {
public:
  static std::string stockSummary(std::vector<std::string> &books, std::vector<std::string> &categories) {
    if (books.empty() || categories.empty())
      return "";

    int stocks['Z' + 1] = {0};
    for (const std::string &book : books) {
        std::size_t position = book.find_first_of(" ", 2, 1);
        stocks[book[0]] += std::atoi(book.data() + position);
    }

    std::string result = "";
    for (const std::string &category : categories) {
      result = result
        + (result.empty() ? "" : " - ")
        + "(" + category[0] + " : " + std::to_string(stocks[category[0]]) + ")";
    }

    return result;
  }
};
```