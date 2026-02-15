# Bitwise operators.
- & : 0&1 --> 0 ,1&1 --> 1
- | : 0&1 --> 1 ,1&1 --> 0
- ^ : 0&1 --> 1 ,1&1 --> 0
- ~ : ~1 --> 0 ,~0 --> 1

# Shift operators.
- There are two operators for shifting bits.
- Left Shift (<<) : Shifts a number to left by appending zero digits.
- ```js
    //example
    5<<2 --> 00101 --> 10100 == 20  which is the same as  5 * 2^2 =20;
- right Shift (>>) : Shifts a number to the right by removing the last few binary digits of the number.
- ```js
    //example
    5>>2 --> 00101 --> 00001 == 1 which is the same as  5 / (2^2) =1;

# Useful tricks.
- n | (1 << x) : sets the x-th bit in the number n.
- (n >> x) & 1 : Check if a bit is set or Not.
- n & ~(1 << x) : clears the x-th bit in the number n.
- To check if the number is divisible by a power of 2:
- ```js
    bool isDivisibleByPowerOf2(int n, int k) {
        int powerOf2 = 1 << k;//generate 2 power k;
        return (n & (powerOf2 - 1)) == 0;//it checks if n is divisble by 2 power k.
    }
    // Time complexcity : O(1);
- To check if an integer is a power of 2:
- ```js
    bool isPowerOfTwo(unsigned int n) {
        if(n & (n-1)==0){
            return true;
        }
        return false;
    }
    // any 2 power number as only one set bit and remaining all bits are zeros.
    // if n is a power of 2 then n-1 as all lower bit are 1`s.
    // n=8 --> 1000 --> n-1 --> 0111 --> n & n-1 ==0;