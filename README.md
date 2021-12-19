# interview-bit--array--partitions

**----> Question:**

You are given a 1D integer array B containing A integers.

Count the number of ways to split all the elements of the array into 3 contiguous parts so that the sum of elements in each part is the same.

Such that : sum(B[1],..B[i]) = sum(B[i+1],...B[j]) = sum(B[j+1],...B[n]) 



Problem Constraints
1 <= A <= 105

-109 <= B[i] <= 109



Input Format
First argument is an integer A.

Second argument is an 1D integer array B of size A.



Output Format
Return a single integer denoting the number of ways to split the array B into three parts with the same sum.



Example Input
Input 1:

 A = 5
 B = [1, 2, 3, 0, 3]
Input 2:

 A = 4
 B = [0, 1, -1, 0]


Example Output
Output 1:

 2
Output 2:

 1


Example Explanation
Explanation 1:

 There are no 2 ways to make partitions -
 1. (1,2)+(3)+(0,3).
 2. (1,2)+(3,0)+(3).
Explanation 2:

 There is only 1 way to make partition -
 1. (0)+(-1,1)+(0).


**-----> Code:**

**1st method(cumulative sum):**

int Solution::solve(int A, vector<int> &B) {
    
    long long int sum=0;
    for(int i=0;i<A;i++){
        sum+=B[i];
    }

    if(sum%3!=0){
        return 0;
    }

    long long int sum1=0,count=0,ans=0,one=sum/3;

    for(int i=0;i<A-1;i++){
        sum1+=B[i];

        if(sum1==2*one){
            ans+=count;
        }
        if(sum1==one){
            count++;
        }
    }

    return ans;
}
  
  
**2nd method:**
  
 int Solution::solve(int A, vector<int> &B) {

    int sum=0;
    for(int i=0;i<A;i++){
        sum+=B[i];
    }

    if(sum%3!=0){
        return 0;
    }

    int sum1=sum/3,x=0;
    vector<int> p,s;
    
    for(int i=0;i<A;i++){
        x+=B[i];
        if(x==sum1){
            p.push_back(i);
        }
    }

    x=0;

    for(int i=A-1;i>=0;i--){
        x+=B[i];
        if(x==sum1){
            s.push_back(i);
        }
    }

    int total=0,n=0,count=0;

    for(int i=0;i<p.size();i++){
        for(int j=0;j<s.size();j++){
            total=0;
            n=0;
            for(int k=p[i]+1;k<s[j];k++){
                total+=B[k];
                n=1;
            }

            if(total==sum1 && n==1){
                count++;
            }
        }
    }

    return count;

}

