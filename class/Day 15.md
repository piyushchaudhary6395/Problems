Level Order Traversal
In order using stack
```cpp
stack st
head=root
vector<int> in
while(true)
{
    if(node!=null)
    {
        st.push(node)
        node=node-left
    }
    else
    {
        if(st.empty())
	        break
	        
        node=st.top()
        st.pop()
        node=node-right
    }
}
```
pre order using stack
```cpp

preorder(root)
{
    if(root==null)
	    return
    stack<node*>st
    curr=root
    while(!st.empty()|| curr!=null)
    {
        while(curr!=null)
        print(curr-data)
        if(curr-right)
	        st.push(curr-right)
        curr=curr-left
        }
    if(!st.empty())
    {
	      curr=st.top()
	      st.pop()  
    }
}
```
post order using stack
```cpp
vector<int>post
stack<node*>st
while(!st.empty())
{
    curr=st.top()
    post.pb(curr-val)
    st.pop()

    if(curr-left!=null)
	    st.push(curr-left)
    if(curr-right!=null)
	    st.push(curr-right)

}
	reverse(post.begin(),post.end())

	return post;
```

## Do In, Pre, Post all In A Single Function Or Traversal
```cpp
vi pre,po,in  
if(root==null)  
	return {}  
stack<pair<node*,int>>st  
st.push({root,1})  
while(!st.empty())  
{  
	auto it=st.top()  
	st.pop()  
	if(it.second==1)  
	{  
	pre.pb(it.first-data)  
	it.second=2  
	st.push(it)  
	if(it.first-left!=null)  
	st.push({it.first-left,1})  
	}  
	else if(it.second==2)  
	{  
	in.pb(it.first-data)  
	it.second=3  
	st.push(it)  
	if(it.first-right!=null)  
		st.push({it.first-right,1})  
	}  
	else  
		post.pb(it.first-data)  
	vv res  
	res.pb(pre)  
	res.pb(in)  
	res.pb(post)  
	return res  
}
```

## Print The Nodes in Zig Zag Pattern
![[Screenshot (480).png]]
```cpp
vector<int> res

if(root==null)
	return res

queue<node*>q

q.push(root)

bool LTR=1

while(!q.emty())
{
    int sz=q.size();
    vector<int>rows(sz)

    for(int i=0;i<sz;i++)
    {
        node=q.front()
        q.pop()
        int idx=LTR?i:sz-i-1
        row[idx]=node-val

        if(node-left)
	        q.push(node-left)

        if(node-right)
	        q.push(node-right)
    }

    LTR=!LTR
    res.pb(row)
}

return res
```

## Height
### Recursion
If tree is skewed then this is not good.
```cpp

```
### Level Order
If last level is fully filled then this is not good.

## Diameter Of Tree
```cpp
diameter(node,diam)
if(!node)
	return 0

lh=diameter(node-left,diam)
rh=diameter(node-right,diam)
diam=max(diam,lh+rh)
```

