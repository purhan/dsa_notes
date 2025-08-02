# Problem Statement
In a deck of cards, each card has an integer written on it.

Return true if and only if you can choose X >= 2 such that it is possible to split the entire deck into 1 or more groups of cards, where:

    Each group has exactly X cards.
    All the cards in each group have the same integer.

[Tutorial](https://www.youtube.com/watch?v=UvpXInRkZ3Q&list=PL-Jc9J83PIiEp9DKNiaQyjuDeg3XSoVMR&index=50)

# Thought Process
- Sounds easy but isnt _that_ easy, just a lil tricky
- We can only create such groups if:
  - No item has frequency 1, since X>=2
  - All items can be divided into groups (of size say K, and K can't be 1), this part is a little tricky...
  - If an item has frequency F, then it F must be divisible by K
  - If all items have `F % K == 0`, answer is true, else its false
  - K is what we have to find, so we simply take GCD of all frequencies and call it K. If K == 1, its not valid so we return false

# Code
```cpp
class Solution {
public:
    bool hasGroupsSizeX(vector<int>& deck) {
        unordered_map<int, int> freq;
        for(auto i: deck) freq[i]++;

        int freqGCD = freq[deck[0]];        // freqGCD is what we are calling `K` in the notes above

        for(int i = 0; i < deck.size(); ++i) {
            if(freq[deck[i]] == 1) return false;
            freqGCD = gcd(freqGCD, freq[deck[i]]);
        }

        if(freqGCD <= 1) return false;

        return true;
    }
};
```

# Problem Links
- https://leetcode.com/problems/x-of-a-kind-in-a-deck-of-cards/
