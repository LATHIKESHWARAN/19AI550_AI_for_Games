# Ex.No: 6  Implementation of Zombie survival game using A* search 
### DATE: 13/09/24                                                                          
### REGISTER NUMBER : 212222230072
### AIM: 
To write a python program to simulate the Zomibie Survival game using A* Search 
### Algorithm:
1. Start the program
2. Import the necessary modules
3. Initiate the pygame engine and window
4. Collect the Zombie image and resize it within a display window 
5. Create a Euclidean distance heuristic function to find the distance from current location to Target position
6.  Move the Zombie towards the target by A* search 
7.  In main, create the obstacles and move the player by Key movements up, down,left and right 
10.  Update the display every time 
11.  Stop the program
### Program:

```python
# Define a large negative and positive value to represent infinity
INF = float('inf')

# Alpha-Beta Pruning function
def alpha_beta_pruning(depth, node_index, maximizing_player, values, alpha, beta):
    # Base case: leaf node is reached
    if depth == 3:
        return values[node_index]
    
    if maximizing_player:
        max_eval = -INF
        # Recur for the two children of the current node
        for i in range(2):
            eval = alpha_beta_pruning(depth + 1, node_index * 2 + i, False, values, alpha, beta)
            max_eval = max(max_eval, eval)
            alpha = max(alpha, eval)
            
            # Prune the branch
            if beta <= alpha:
                break
        return max_eval
    else:
        min_eval = INF
        # Recur for the two children of the current node
        for i in range(2):
            eval = alpha_beta_pruning(depth + 1, node_index * 2 + i, True, values, alpha, beta)
            min_eval = min(min_eval, eval)
            beta = min(beta, eval)
            
            # Prune the branch
            if beta <= alpha:
                break
        return min_eval

# Driver code : 
if __name__ == "__main__":
    # This is the terminal/leaf node values of the game tree
    values = [3, 5, 6, 9, 1, 2, 0, -1]

    print("Optimal value:", alpha_beta_pruning(0, 0, True, values, -INF, INF))
```
### Output:
<img width="1128" alt="377505777-24ec26e2-cbce-4aeb-b866-0918b98e1d39" src="https://github.com/user-attachments/assets/0a7976c5-c8c1-47e2-be9a-f53331355daa">


### Result:
Thus the simple Zombie survival game was implemented using python.
