# Problem Statement
1. You are given a string str.
2. Complete the body of printSS function - without changing signature - to calculate and print all subsequences of str.
Use sample input and output to take idea about subsequences.

Note -> The online judge can't force you to write the function recursively but that is what the spirit of question is. Write recursive and not iterative logic. The purpose of the question is to aid learning recursion and not test you.

[Tutorial](https://www.youtube.com/watch?v=Ke8TPhHdHMw&list=PL-Jc9J83PIiFxaBahjslhBD1LiJAV7nKs&index=34)

# Thought Process

# Code
```cpp
void printSubsequence(string s, string ans){

	if(s.length()==0){
		cout<<ans<<endl;
		return;
	}

	char ch=s[0];
	string ros=s.substr(1);
	printSubsequence(ros,ans+"");
	printSubsequence(ros,ans+ch);
}

```

# Problem Links
- https://www.pepcoding.com/resources/online-java-foundation/recursion-on-the-way-up/print-subsequence-official/ojquestion