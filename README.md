### 1.P1087 FBI树
用tree[i]表示节点的类型，调用递归在s的下标1到2^n,如果当前为叶子节点则直接判断输出否则每次继续调用左子树和右子树最后由左孩子和右孩子整合出该节点类型 ,最后调用输出函数后序遍历输出。
```
#include<iostream>
#include<algorithm> 
using namespace std;
int n;
string s;
char tree[5009];
void build(int p, int pl, int pr) {
    //当前节点为p,包括的范围为pl到pr
    if (pl == pr) {//如果当前为叶子节点直接判断当前节点类型并返回
        if (s[pl] == '0') {
            tree[p] = 'B';
        }
        else {
            tree[p] = 'I';
        }
        return;
    }
    int mid = (pl + pr) / 2;
    //分别调用左孩子和右孩子
    //左孩子为2*p,右孩子为2*p+1
    build(2 * p, pl, mid);
    build(2 * p + 1, mid + 1, pr);
    //由左孩子和右孩子信息判断出当前节点类型
    if (tree[2 * p] == 'B' && tree[2 * p + 1] == 'B') {
        tree[p] = 'B';
    }
    else if (tree[2 * p] == 'I' && tree[2 * p + 1] == 'I') {
        tree[p] = 'I';
    }
    else {
        tree[p] = 'F';
    }
}
void print(int p,int pl,int pr) {
    
    int mid = (pl + pr) / 2;
    if (pl == pr) {//如果当前为叶子节点直接输出并返回
        cout << tree[p];
        return;
    }
    //后续遍历输出
    print(2 * p, pl, mid);
    print(2 * p + 1, mid + 1, pr);
    cout << tree[p];
}
int main()
{

    cin >> n;
    cin >> s;
    s = " " + s;
    build(1, 1, 1 << n);
    print(1, 1, 1 << n);
    return 0;
}

```
### 2.P1030 求先序排列

