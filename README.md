# calc_power

Implement pow(x, n), which calculates x raised to the power n (i.e., $x^n$). Here x is sizeof(double), n is sizeof(int).

1. Naive way:
```
    double myPow(double x, int n) {
        if(n==0)
            return 1.;
        
        return n>0?myPow(x, n-1)*x:myPow(x, n+1)/x;
        
    }

  # time complexity: O(N)
  # space complexity: O(N)

```

2. Better way (Binary exponentiation):

The basic idea here is to use the fact that $x^n$ can be derived from:

a. $(x^2)^{n/2}$ if n is even.
b. $x*(x^2)^{(n-1)/2}$ if n is odd.

```
    double myPow(double x, int n) {
        if(n==0)
            return 1.;
        if (n<0)
            return 1./myPow(x, -n);
        if(n%2)
            return x*myPow(x*x, n/2);
        else
            return myPow(x*x,n/2);    
    }

  # time complexity: O(logN)
  # space complexity: O(logN)
```


3. Corner case:
   If n=INT_MIN or n=-2147483648, -n will overflow.
<!-- language: lang-php -->
<pre><code>
    double myPow(double x, int n) {
        if(n==0)
            return 1.;
        if (n<0&& <b>n!=INT_MIN</b>)
            return 1./myPow(x, -n);
        if(n%2)
            return x*myPow(x*x, n/2);
        else
            return myPow(x*x,n/2);    
    }

  # time complexity:O(logN)
  # space complexity:O(logN)
</pre></code>

   
