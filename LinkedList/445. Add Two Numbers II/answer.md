
You are given two non-empty linked lists representing two non-negative integers. The most significant digit comes first and each of their nodes contains a single digit. Add the two numbers and return the sum as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

 ```
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def addTwoNumbers(self, l1: Optional[ListNode], l2: Optional[ListNode]) -> Optional[ListNode]:
        num1 = 0
        num2 = 0
        
        # Traverse the first list and construct the number
        temp = l1
        while temp:
            num1 = num1 * 10 + temp.val
            temp = temp.next

        # Traverse the second list and construct the number
        temp = l2
        while temp:
            num2 = num2 * 10 + temp.val
            temp = temp.next

        # Calculate the sum of both numbers
        total_sum = num1 + num2

        # If the sum is 0, return a ListNode with value 0
        if total_sum == 0:
            return ListNode(0)

        # Create a stack to hold digits of the sum
        stack = []

        # Push the digits of the sum onto the stack
        while total_sum:
            stack.append(total_sum % 10)
            total_sum //= 10

        # Create the result linked list
        result = ListNode(0)
        temp = result

        # Pop the digits from the stack and create the linked list
        while stack:
            digit = stack.pop()
            temp.next = ListNode(digit)
            temp = temp.next

        return result.next
```
