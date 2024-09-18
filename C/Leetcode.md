## 数组

### 704.二分查找

```
二分搜索法
在一个数组里找target,在则返回target的下标,不在则返回-1
```
- while循环 left < right 还是 left <= right ?
- nums[mid]>target,更新右区间,left = mid 还是 mid - 1 ?
---
首先明确 <u>区间是开还是闭</u> 是否包含 left 和 right  影响到while条件

#### 左闭右闭

**left = 0, right = nums.size()-1** 注意是减1,nums.size()-1!

区间[1,1] 1=1 有没有意义？有 所以 left<=right

**while( left <= right )**

**mid=(left+right)/2**

**if( nums[mid] > target )** 更新左区间的右边界

> **right=mid?**还是**mid-1?** 我们已经确定**mid != target** 那么接下来的区间**不要包含 mid** 如果 right=mid,那么接下来的区间是接下来的区间是[ left, mid ) 边界处理有问题,可能死循环看 while  条件 right=left 就不合法了 ,所以 right 只能是 mid-1

**else if ( nums[mid] < target ) left=mid+1**
**else return mid;**以上两者都不是的话,就只剩下 nums[mid] == target 那么 mid 就是 下标
}return -1; 不存在的话,返回-1

#### 左闭右开

区间[1,1) 能等于吗? left 和 right 相等的情况有意义吗? 没有意义,没有意义我还进行循环干什么

while( left < right ) 

nums[mid] < target  我是左闭右开的搜素区间,本来就不包含mid了所以right=mid没问题

right = mid 如果 right = mid - 1 ,那么就少搜索了一个元素

nums[mid] > target 

left=mid+1 因为左闭 新的搜索区间要改变 且不多不少元素

> tips: 左闭右开时,right=nums.size() 不用减1

#### 代码

```c++
int search(vector<int>& nums, int target) {
        int low = 0;
        int high = nums.size()-1;
        int mid = (low + high) / 2;
        while(low <= high){
            if(nums[mid] > target){
                high = mid - 1;
                mid = (low + high) / 2;
            }
            else if(nums[mid] < target){
                low = mid + 1;
                mid = (low + high) / 2;
            }
            else if(nums[mid] == target)
                return mid;
        }
        return -1;
    }
  19ms
```

前提是数组有序且无重复元素

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

