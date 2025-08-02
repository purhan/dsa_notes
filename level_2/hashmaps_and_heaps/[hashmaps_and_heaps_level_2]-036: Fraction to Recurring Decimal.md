# Problem Statement
1. You are given two numbers which represent the numerator and denominator of a fraction.
2. You have to convert this fraction into a decimal.
3. If the decimals are repeating recursively, then you have to put the recurring sequence inside a bracket.

[Tutorial](https://www.youtube.com/watch?v=2cRS9dNa780&list=PL-Jc9J83PIiEp9DKNiaQyjuDeg3XSoVMR&index=39)

# Thought Process
- Really just look at the code, implementation sucks and there is too much going on
- Basic idea is:
- Till decimal place, we will calculate normally
- After decimal, we will store remainder in a map. If a remainder repeats, we insert bracket before it and return the answer


# Code
```cpp
#define lli long long

class Solution {
public:
    string fractionToDecimal(lli num, lli den) {
        if(num == 0) return "0";
        string res;

        if((num < 0) ^ (den < 0)) res += '-';
        num = abs(num), den = abs(den);

        res += to_string(num / den);    // add part before decimal

        if(num % den == 0) return res;  // in case no decimal further

        res += '.';

        unordered_map<lli, int> mp;

        lli r = num % den;
        while(r > 0) {
            if(mp.count(r) > 0) {
               res.insert(mp[r], 1, '(');   // insert `(`, `once`, at position `mp[r]`
               res += ')';
               return res;
            }

            mp[r] = res.size();

            r *= 10;

            res += to_string(r / den);
            r %= den;
        }

        return res;
    }
};
```

# Problem Links
- https://leetcode.com/problems/fraction-to-recurring-decimal/
