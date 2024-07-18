## Intersection of Two Linked Lists
## Brute
We count the length's of both linked lists. Whichever one is bigger we traverse on it till their absolute difference. If their addresses are equal we return.
```cpp
class Solution {
public:
    ListNode *getIntersectionNode(ListNode *headA, ListNode *headB) {
        int s1 = 0;
        int s2 = 0;

        ListNode* temp = headA;
        while(temp != NULL) {
            s1++;
            temp = temp->next;
        }

        temp = headB;
        while(temp != NULL) {
            s2++;
            temp = temp->next;
        }

        int diff = abs(s1 - s2);
        if(s1 > s2) {
            while(diff) {
                headA = headA->next;
                diff--;
            }

            while(headB != NULL) {
                if(headA == headB)
                    return headA;
                    
                headB = headB->next;
                headA = headA->next;
            }
        }
        else {
            while(diff) {
                headB = headB->next;
                diff--;
            }

            while(headB != NULL) {
                if(headA == headB)
                    return headA;

                headB = headB->next;
                headA = headA->next;
            }
        }

        return NULL;
    }
};
```

## Better
Note: We can also use map or set.

## Optimal (Two Pointer)
Traverse on both linked lists simultaneously when one reaches its end node initialise it to the head of the other linked list, when the other linked list reaches it's end initialize it to the head of the first linked list. Now their distances are equal. Simply traverse and return.
```cpp
```

## Add two numbers represented as LL
```cpp
```
## Delete Nth node from end of LL
One way is to count the size of the LL then do another iteration.

Good way is to maintain two pointers at the start of LL, then move the forward one till `N` then move both of them simultaneously. When the forward pointer reaches the last node, the backward pointer will be pointing just before the node to delete.

Note: Don't know why this code is not working without the if condition.
```cpp
ListNode* removeNthFromEnd(ListNode* head, int n) {
        ListNode* p1 = head;
        ListNode* p2 = head;

        while(n--)
            p2 = p2->next;

        if(p2==NULL) return p1->next;

        while(p2->next != NULL) {
            p2 = p2->next;
            p1 = p1->next;
        }

        ListNode* to_delete = p1->next;
        p1->next = p1->next->next;
        delete to_delete;

        return head;
    }
```

## Rotate List (Homework)
## Reorder List (Homework)
## Merge Sort a linked list (Homework)
