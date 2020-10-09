# Dynamic programming

- Binomial Coefficient
    - one-dimensional array: two-dimensional array wastes half of the space, and each 'row' is only used to store values once
    - Since the array type is int[], overflow may occur
```java
class Playground {
    public static int bin(int n, int k){
        if(k>n/2) k=n-k; // if k is more than half of n, some calculation are redundant. Recall (n k) = (n n-k).
        
        int B[] = new int[k+1];
        for(int i=1; i<=n; i++){
            for(int j=k; j>=0;j--){
                if(j==0 || j==i){
                    B[j]=1;
                    continue;
                }
                else{
                    B[j]=B[j]+B[j-1];
                }
            }
            
            System.out.println("row:"+i);
            for(int j=0; j<=k; j++){
                System.out.print(B[j]+" ");
                System.out.println();
            }
        }
        return B[k];
    }
    
    public static void main(String[ ] args) {
        System.out.println("Ans:"+bin(4,2)); // 4!/(2!(4-2)!) = 6
    }
}
```
