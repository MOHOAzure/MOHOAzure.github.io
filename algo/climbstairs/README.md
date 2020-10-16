# Climb a staircase

## Question:
You are climbing a staircase. It takes n steps to reach to the top.
Each time you can either climb 1 or 2 steps. In how many distinct ways can you climb to the top?
Note: Given n will be a positive integer.

## Answer:

```java
class Playground {
    public static int stepCountDivideA(int n){
        int step;
        if(n<=2) step=n;
        else{
            step=stepCount(n-1)+stepCount(n-2);
        }
        
        return step;
    }
    
    public static int stepCountDP(int n){
        int[] step = new int[n];
        step[0]=1;
        step[1]=2;
        
        for(int i=2; i<n;i++){
            step[i]=step[i-1]+step[i-2];
        }
        
        return step[n-1];
    }
    
    public static void main(String[ ] args) {
        System.out.println(stepCountDP(4));
    }
}
```
