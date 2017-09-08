Reverse digits of an integer.

Example1: x = 123, return 321
Example2: x = -123, return -321

click to show spoilers.

Note:
The input is assumed to be a 32-bit signed integer. Your function should return 0 when the reversed integer overflows.

```
class Solution {
public:
    int reverse(int x) {
        long long reverseX = 0;
        while(x != 0){
        	int remainder = x % 10;
        	reverseX = reverseX * 10 + remainder;
        	x /= 10;
        }

        if(reverseX > INT_MAX || reverseX < INT_MIN){
        	return 0;
        }
        return reverseX;
    }
};
```
