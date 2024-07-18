## Clone A Linked List With Next And Random Pointer
## Brute
We create a map with a original node and copy node. Then we link the pointers.
![[Screenshot (476).png]]

```cpp
clonell(head)

{

    temp=head

    map<node*,node*>mp

    while(temp!=null)

    {

        newnode=temp-data

        mp[temp]=newnode

        temp=temp-next

    }

    temp=head

    while(temp!=null)

    {
        copynode=mp[temp]

        copynode-next=mp[temp-next]

        copynode-random=mp[temp-random]

        temp=temp-next

    }

    return mp[head]

}
```
O(2N)
O(2N)
## Optimal
We mutate the original list and insert our new nodes in between the two nodes of the original list and make the same connections. After that we remove the original list's connections.
![[Screenshot (477).png]]

![[Screenshot (479).png]]
O(3N)
O(N)
```cpp
insertnode(head)
{
    temp=head
    while(temp!=null)
    {

        nextele=temp-next

        copy=temp-data

        copy-next=nextele

        temp-next=copy

        temp=nextele
     }
}

connectrandom(head)
{
    temp=head
    while(temp!=null)
    {
        copynode=temp-next

        if(temp-random)
	        copynode-random=temp-random-next
        else 
	        copynode-random=NULL
        
        temp=temp-next-next
}

getdeepcopy(head)
{
    temp=head
    dummynode=new node(-1)
    res=dummynode
    while(temp!=null)
    {
        res-next=temp-next

        res=res-next

    temp-next=temp-next-next

    temp=temp-next

   }

    return dummynode-next

}

clonell(head)
{
    if(!head)
	    return nullptr

    insertnode(head)

    connectrandom(head) 

    return getdeepcopy(head)
}
```

## Trees
Binary Tree
Complete Binary Tree
Pre, In, Post (order traversals)
