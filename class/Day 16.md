## Topics
construct tree from inorder and preorder traversal
construct a tree from inorder and postorder traversal

input:
    inorder:[40,20,50,10,60,30]
    preorder:[10,20,40,50,30,60]

## construct tree from inorder and preorder traversal

Step1: createa map to store indices of elements in the inorder traversal. interate through inorder and store its index in the map using the element as key and index as value

step2 : create a recursive function say buildtree
preorder array
preorder-prestart (0)
preorder-preend(n-1)
inorder array
inorder-instart(0)
inorder-inend(m-1)
map for look up

step3: prestart<preend, 
     instart< inend
     
step4: root node for current subtree is the first element in the preorder (preorder[prestart]). Find the index of root node in the inorder traversal using map inmap[rootvalue]. this is rootIndex

step5: left subtree range will be from instart to rootIndex

we can get number of nodes in left subtree

 step6: recursive calls for left and right and adjust indices.

```cpp
build tree(vi &pre,int prestart,int preend,vi &in,int instart,int inend,map<int,int>&inmap)
{
    if(prestart>preend || instart>inend)
	    return NULL;

    Node* root=new Node(preorder[prestart])

int inroot=inmap[root->val]

int numleft=inroot-instart

root->left=buildtree(preorder,prestart+1,prestart+numleft,inorder,instart,inroot-1,inmap)

root->right=buildtree(preorder,prestart+1+numsleft,preend,inorder,inroot+1,inend,inmap);

return root

}

buildtree(vi preorder, vi inorder)
{
    map<int,int>inmap;

    for(int i=0;i<inorder.size();i++)

    {

        inmap[inorder[i]]=i;

    }

    Node* root=builtree(preorder,0,preorder.size()-1,inorder,0,inorder.size()-1,inmamp)

    return root;

}
```


Longest path is the diameter in tree.
## Diameter Of Tree

![[Screenshot (481).png]]

## Find The Lowest Common Ancestor In A BT
![[Screenshot (482).png]]

## Find Left View Of Binary Tree
```cpp
vector<int> leftView(Node *root)  
{  

if(root==NULL) 
	return {};  
	
queue<Node*>q;  
vector<int>ans;  
q.push(root);  
while(q.size()>0){  
	int sz = q.size();  
	for(int i = 0; i<sz; i++){  
	Node* N = q.front();  
	q.pop();  
	if(i==0){  
		ans.push_back(N->data);  
	}  
	if(N->left) q.push(N->left);  
	if(N->right) q.push(N->right);  
	}  
}  
	return ans;  
}
```

## Find Right View Of Binary Tree
```cpp

```
