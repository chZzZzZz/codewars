#7 Speed Control
example：x = [0.0, 0.19, 0.5, 0.75, 1.0, 1.25, 1.5, 1.75, 2.0, 2.25]  record the car's position every s second ,s = 15s,return the max speed

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

class GpsSpeed
{
public:
    static int gps(int s, std::vector<double> &x)
    {
        if(x.size()<=1) return 0;
        
        std::vector<int> delta;
        
        for(int i=1;i<x1.size();i++)
        {
            delta.push_back((x[i]-x[i-1])*3600/s);
            
        }
        sort(delta.begin(),delta.end());
        return delta.back();
    }
};

int main()
{
	GpsSpeed mygps;
	std::vector<double> ss={0.0, 0.23, 0.46, 0.69, 0.92, 1.15, 1.38, 1.61};
	int result = mygps.gps(20,ss);
	std::cout<<result<<std::endl;
	return 0;
}
```

方法二：

```cpp
class GpsSpeed
{
public:
    static int gps(int s, std::vector<double> &x);
};

int GpsSpeed::gps(int s, std::vector<double> &x)
{
    double maxDis, subDis;
    int res = 0;
    if(x.size() > 1)
    {
        for(int i = 1; i < x.size(); ++i)
        {
            subDis = x[i] - x[i - 1];
            maxDis = (maxDis > subDis) ? maxDis : subDis;
        }
        
        res = maxDis * 3600 / s;
    }
    
    return res;
}
```