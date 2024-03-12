## 栈

### 20.有效的括号

```
给定一个只包括 `'('`，`')'`，`'{'`，`'}'`，`'['`，`']'` 的字符串 `s` ，判断字符串是否有效。
有效字符串需满足：
1.左括号必须用相同类型的右括号闭合.
2.左括号必须以正确的顺序闭合.
3.每个右括号都有一个对应的相同类型的左括号。
```

字符串不一定都是(){}[] 左括号后面不一定接着右括号 如 {[]} 
后进的括号先出,栈

**判断字符串的有效性**:
遍历字符串,如果是左括号,入栈.
如果是右括号,看栈顶元素,如果匹配,则消掉括号,出栈.

```c++
bool isValid(string s) {
        stack<char> cs;
        for(int i=0; i<s.size();i++){
            if(s[i] == '{' || s[i] == '[' || s[i] == '(')cs.push(s[i]);
            //左括号入栈
            else if ( s[i] == ')'){
                 if ( cs.empty() || cs.top() != '(') return false;
                 else cs.pop();
            }
             else if ( s[i] == ']'){
                 if ( cs.empty() || cs.top() != '[') return false;
                 else cs.pop();
            }
             else if ( s[i] == '}'){
                 if ( cs.empty() || cs.top() != '{') return false;
                 else cs.pop();
            }
        }
        return cs.empty();
    }
3ms 不知道为什么是3ms
```

```c++
class Solution {
public:
    bool isValid(string s) {
        stack<char> A;
        for(int i = 0; i < s.size(); i++)
        {
            if(s[i] == '(' || s[i] == '{'  || s[i] == '[') A.push(s[i]);
            if(s[i] == ')')
            {
                if(A.empty() || A.top() != '(') return false;
                A.pop();
            }
            if(s[i] == '}')
            {
                if(A.empty() || A.top() != '{' ) return false;A.pop();
            }
            if(s[i] == ']')
            {
                if(A.empty() || A.top() != '[') return false;A.pop();
            }
        }
        return A.empty();
    }
};
0ms
```

