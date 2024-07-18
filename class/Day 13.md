## Palindrome List
## Brute
convert it to string or array.
OR
use stack to push the elements then again traverse on the LL and check with the stack.

## Optimal
We can use slow and fast pointer to find mid. We have to reverse the end half of the LL. then we put two pointers, one at the start and one at the mid. The we just iterate on both and compare.
![[Screenshot (475).png]]

T.C:- O(N/2) + O(N/2) + O(N) => O(2N)
S.C:- O(1)

## Reverse LL In Groups Of K
## Optimal
Have a reverse function. then iterate on LL and for every window k, reverse it.

T.C:- O(2N) (according to mam)
pseudo code
```cpp
reversell(head)
{
    temp=head
    prev=null
    
    while(temp!=null)
    {
        front=temp->next
        temp->next=prev
        prev=temp
        temp=front
        }
        return prev
}

getkthnode(temp,k)
{
    k-=1//because we start from 1st node so k-1+1=k
    while(temp!=null && k>0)
    {
        k--
        temp=temp-next
        }
        
        return temp
}

kreverse(head,k)
{
    temp=head
    prevlast=null
    
    while(temp!=null)
    {
        kthnode=getkthnode(temp,k)
        if(kthnode==NULL)
        {
            if(prevlast) {}
	            prevlast-next=temp
            }

            break
    }
    nextnode=kthnode-next
    reversell(temp)

    if(temp==head)
    {
        head=kthnode
    }
    else
    {
        prevlast-next=kthnode
 
        prevlast=temp
        temp=nextnode
    }

    return head;
```

## LRU Cache (imp)
Implemented using doubly linked list and map. (map stores the key and address of the node where the value exists)
==Functions:-==
`LRUCache(capacity)`: intialises the caches capactiy
`get(key)`: return value of the key if key exists, else -1. (key = process (analogy to understand))
`put(key, value)`: If key already in LRU cache then value gets updated. otherwise add the key, value pair.

If the number of keys exceed the capacity of the cache, we will remove the least recently used one.

```js
input: LRUcache,put,put,get,put,get,put,get,get,get
2, [1,1],[2,2],[1],[3,3],[2],[4,4],[1],[3],[4]
```

Pseudo code:
```cpp
head=new node(-1,-1)

tail=new node(-1,-1)

int cap

map<int,node*>mp

LRUCache(int capacity)

{

    cap=capacity

    head-next=tail

    tail-prev=head

}

void addnode(newnode)

{

    temp=head-next

    newnode-next=temp

    newnode-prev=head

    head-next=newnode

    temp-prev=newnode

    }

    void deletenode(delnode)

    {

        delprev=delnode-prev

        delnext=delnode-next

        delprev-next=delnext

        delnext-prev=delnext

        }

    int get(key)

    {

        if(mp.find(key)!=mp.end())

       { resnode=mp[key]

        int ans=resnode-val

        mp.erase(key)

        delnode(resnode)

        addnode(resnode)

        mp[key]=head->next

        return ans

        }

        else

        return -1

        }

    void put(key,val)

    {

        if(mp.find(key)!=mp.end())

        {

            existingnode=mp[key]

            mp.erase(key)

            delnode(existingnode)

        }

        if(mp.size()==cap)

        {

            mp.erase(tail-prev-key)

            delnode(tail-prev)

            }

            addnode(newnode(key,val))

            mp[key]=head-next
```

```cpp
/**

 * Definition for a binary tree node.

 * struct TreeNode {

 *     int val;

 *     TreeNode *left;

 *     TreeNode *right;

 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}

 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}

 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}

 * };

 */

// class Solution {

// public:

//     int solve(TreeNode* root, int sum = 0, int sum2 = 0) {

//         if(root == NULL)

//             return 0;

  

//         sum += solve(root->right, sum, sum2);

//         sum += root->val;

//         root->val = sum;

//         solve(root->left, sum, sum2);

//         sum2 += (root->left != NULL) ? root->left->val : 0;

  

//         return sum + sum2;

//     }

  

//     TreeNode* bstToGst(TreeNode* root) {

//         solve(root);

  

//         return root;

//     }

// };

class Solution {

public:

    void reverseInOrder(TreeNode* node, int& sum) {

        if (!node) return;

        reverseInOrder(node->right, sum);

        sum += node->val;

        node->val = sum;

        reverseInOrder(node->left, sum);

    }

  

    TreeNode* bstToGst(TreeNode* root) {

        int sum = 0;

        reverseInOrder(root, sum);

        return root;

    }

};
```

