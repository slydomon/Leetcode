# Dynamic Programming

## Pacman Type
Top-down: Fixed number of choices and therefore won't have for loop within recursive function.
  ex. Longest common subsequence: move i, move j, or if(s1[i] == s2[j]) move both.
Buttom-up: Only need contant number of previous states to form the next answer
  ex. Longest common subsequence: lookup[i, j] = max(lookup[i-1, j], lookup[i, j-1]).
  
## Allegator Pacman Type
Top-down: Need to go through all the current choices to find the solution and therefore will have for loop within recursive function.
Buttom-up: The next state relys on all the previous states.
***only have one sub problems

## Divide and Conquer
Separate into several sub problems and combines the results from all of them `
