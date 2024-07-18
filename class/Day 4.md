## Topics
Bit manipulation
Bit masking
## Missing Number

## Bit masking
`1 ko jitna left shift kroge vo hamara mask hoga`

Application: 
- It checks whether the bit is set or not
- Turning a bit

Example:
(5) 1 0 1

## ## Check whether K-th bit is set or not
```cpp
bool checkKthBit(int n, int k)
    {
            if((1 << k) & n)
                return true;
                
            return false;
    }
```

## Count set bits

