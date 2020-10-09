# Dynamic programming

- Binomial Coefficient
```java
class Playground {
    public static int bin(int n, int k){
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
