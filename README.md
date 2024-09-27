Median in a row wise sorted matrix in Java
Here, in this page we will discuss the program to find median in a row wise sorted matrix in Java Programming Language. We are given a row-wise sorted matrix of size r*c, we need to find the median of the matrix given. It is assumed that r*c is always odd.

Median in a row wise sorted matrix in Java
Method Discussed :
Method 1 : Naive Method
Method 2 : Efficient Method.
Method 1 :
Declare an array of r*c size and iterate over the entire matrix to store all the elements of the matrix in the array.
Now sort the array.
Then we can print the middle element from the array.
Time and Space Complexity :
Time-Complexity : O(r*c*log(r*c))
Space-Complexity : O(r*c)
Method 1 : Code in Java
Run
import java.util.Arrays;
 
public class Main
{
    
    public static void main(String[] args)
    {
        int r = 3, c = 3;
        int mat[][]= { {1,3,5}, {2,6,9}, {3,6,9} };
        
        int[] arr;
         
     
        arr = new int[9];
        int x=0;
        
        for(int i=0; i<3; i++){
            for(int j=0; j<3; j++){
                arr[x++] = mat[i][j];
            }
        }
    
        for(int i=0; i<9; i++){
            for(int j=i+1; j<9; j++){ 
                if(arr[i]>arr[j]){
                    int temp = arr[i];
                    arr[i] = arr[j];
                    arr[j] = temp;
                }
            }
        }
    
        System.out.println("Median of the given matrix is : "+ arr[4]);
      
    }
}
Output :
Median of the given matrix is 5
Method 2 :
Find every subset of the array.
For each subset
Now, apply binary search on the range of numbers from minimum to maximum, find the mid from the minimum and maximum and get a count of numbers less than or equal to our mid. And accordingly change the minimum or maximum.
For a number to be median, there should be (r*c)/2 numbers smaller than that number.
For every number, we get the count of numbers less than that by using upper_bound() in each row of the matrix, if it is less than the required count, the median must be greater than the selected number, else the median must be less than or equal to the selected number.
Time and Space Complexity :
Time-Complexity : O(r*log(c))
Space-Complexity : O(1)
Method 2 : Code in Java
Run
import java.util.Arrays;
 
public class Main
{
    
    static int binaryMedian(int m[][],int r, int c)
    {
        int max = Integer.MIN_VALUE;
        int min = Integer.MAX_VALUE;
         
        for(int i=0; i<r ; i++)
        {
           
            if(m[i][0] < min)
                min = m[i][0];
             
            if(m[i][c-1] > max)
                max = m[i][c-1];
        }
         
        int desired = (r * c + 1) / 2;
        while(min < max)
        {
            int mid = min + (max - min) / 2;
            int place = 0;
            int get = 0;
             
            for(int i = 0; i < r; ++i)
            {
                 
                get = Arrays.binarySearch(m[i],mid);
                 
                if(get < 0)
                    get = Math.abs(get) - 1;
                 
                else
                {
                    while(get < m[i].length && m[i][get] == mid)
                        get += 1;
                }
                 
                place = place + get;
            }
             
            if (place < desired)
                min = mid + 1;
            else
                max = mid;
        }
        return min;
    }
     
    public static void main(String[] args)
    {
        int r = 3, c = 3;
        int m[][]= { {1,3,5}, {2,6,9}, {3,6,9} };
         
        System.out.println("Median is " + binaryMedian(m, r, c));
    }
}
Output :
Median is 5
