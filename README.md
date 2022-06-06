# Comp305_TheMostValuableTreeProblem
Optional project for the Spring 2022 Comp305 - Data Structures and Algorithms course of Koç University 


Problem: Given an edge representation of a tree structure with weighted nodes, return the value of the structure which has the largest sum possible by making at most k cuts to the tree (In O(nk) time). A cut deletes the node and its children from the structure.

Input: A file containing lines of integers seperated by a single space is given. First line contains the number of nodes and number of allowed cuts. Second line is the costs for corresponding nodes. Rest of the lines are pairs representing an edge between the numbered nodes. Number 1 is the root. 

Solution Idea: 
1) Construct the tree with the given information, it should take O(n) time. 

2) Calculate the T value for each node starting from the bottom. A T value is the value that corresponds to the sum of the children's value and the nodes value. This can be done in O(n) time iteratively by starting from the leaf nodes since the T value of a node is the sum of its children's T values and its value. 

3) Regardless of how many cuts are allowed, the cut that gives the best result is always the node with the lowest negative T value. Proof is done below. Finding the minimum T value and cutting the node takes O(n) time. 

4) Recalculate the T values (O(n) time) and repeat steps 3-4 until either no more negative cuts can be made or k cuts have been made. 


First Approach (Includes false assumtion, skip to second approach for the correct solution): 

  1)Constructing the tree: The most difficult part for me was constructing the tree in O(n) time. First I assumed that the parents would be numbered before the children, so in any given pair the smaller value would be the parent and the larger one would be the child. This allowed quick construction of a list representation of the tree by iterating through the edge information only once (list-of-edges L s.t. L[i-1] contains a list with the numbers of its children). 
  2)Calculating T values: This false assumption also made it easier to calculate the T values because starting from the end of the list, children are guaranteed to appear before their parents. Keeping a list T of T values s.t. T[i-1] = Ti and using it as a look-up table its possible to calculate all the T values in one reverse iteration. 
  
  Learning that node numbers didn't necessarily have this assumed property, I took a different approach. 
  
 Second Approach: 
  1) I created a list of lists such that L[i-1] contained all the node numbers to which node i had a connecting edge. This list contained each node twice. My first goal was to go from this to a list where L[i-1] would only contain the children's numbers and not its parent's. I wrote a function called purge which takes a root number and starts visiting its children in L to remove itself from the children's indexes. This works because the root number is guaranteed not to have a parent in its list, and once it's been cleaned from its children's lists, those lists are also guarantee not to have a parent in them, so the function moves onto their children's lists and removes the parent values from the lists. This takes O(n) time because in the worst case, every element is visited once and V-1 items are removed. 

















  
