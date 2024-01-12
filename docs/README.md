# Stein's algorithm using Dlang

Binary GCD Algorithm

## Source code

```d
import std.stdio;
import std.traits;

// Template function to find the GCD using Stein's algorithm for non negative integral types
T steinGCD(T)(T a, T b) if (isIntegral!T && isUnsigned!T)
{
    // Base cases
    if (a == b)
        return a;

    if (a == T(0))
        return b;

    if (b == T(0))
        return a;

    // If both a and b are even, divide them by 2
    if ((a & T(1)) == T(0) && (b & T(1)) == T(0))
        return steinGCD(a >> T(1), b >> T(1)) << T(1);

    // If a is even and b is odd, divide a by 2
    if ((a & T(1)) == T(0))
        return steinGCD(a >> T(1), b);

    // If a is odd and b is even, divide b by 2
    if ((b & T(1)) == T(0))
        return steinGCD(a, b >> T(1));

    // If both a and b are odd, subtract smaller from larger
    if (a > b)
        return steinGCD((a - b) >> T(1), b);

    return steinGCD((b - a) >> T(1), a);
}

void main()
{
    // Example #1 usage with integers
    uint num1 = 48u;
    uint num2 = 18u;

    uint gcdUInt = steinGCD(num1, num2);
    writeln("\nGCD of ", num1, " and ", num2, " is ", gcdUInt);

    // Example #2 usage with longs
    ulong num3 = 105L;
    ulong num4 = 45L;

    ulong gcdULong = steinGCD(num3, num4);
    writeln("GCD of ", num3, " and ", num4, " is ", gcdULong);
}
```
## Output

Enter into the Dub Package folder, type `dub run` and type `Return` to run it...

```
GCD of 48 and 18 is 6
GCD of 105 and 45 is 15
```

## Wikipedia

  - [Entry](https://en.wikipedia.org/wiki/Binary_GCD_algorithm)
