# Operators

## Topics
1. Operators definition
1. Types of Operators
  - Arithmetic Operators
  - Assignment Operators
  - Relational Operators
  - Logical Operators
  - Bitwise Operators
  - Ternary Operators
1. Operator Precedence


## Code example

```java

package org.lousing.andrii.primitives;

public class Operators {

  public static void showDemo() {
    System.out.println("---Arithmetic Unary Operators---");
    int i = +10;
    int i2 = -10;
    int i3 = ++i;
    int i4 = i++;
    System.out.println("i = " + i);
    int i5 = --i;
    int i6 = i--;

    System.out.println("i2 = " + i2);
    System.out.println("i3 = " + i3);
    System.out.println("i4 = " + i4);
    System.out.println("i5 = " + i5);
    System.out.println("i6 = " + i6);

    System.out.println("---Binary Arithmetic Operators---");
    // + - / % *
    int i7 = 10 + 1;
    int i8 = i7 - 1;
    int i9 = i8 / 2;
    int i10 = i9 % 2;
    int i11 = 5 % 10;
    int i12 = i10 * 3;

    System.out.println("i7 = " + i7);
    System.out.println("i8 = " + i8);
    System.out.println("i9 = " + i9);
    System.out.println("i10 = " + i10);
    System.out.println("i11 = " + i11);
    System.out.println("i12 = " + i12);

    System.out.println("---Assignment Operators---");
    // = += -= *= /= %=
    int i13 = 10;
    i13 += 2;
    i13 -= 4;

    System.out.println("i13 = " + i13);

    System.out.println("---Relational Operators---");
    // == != > < >= <=
    int i14 = 10;
    int i15 = 20;

    System.out.println("i14 == i15 is " + (i14 == i15));
    System.out.println("i14 != i15 is " + (i14 != i15));
    System.out.println("i14 < i15 is " + (i14 < i15));
    System.out.println("i14 > i15 is " + (i14 > i15));
    System.out.println("i14 <= i15 is " + (i14 <= i15));
    System.out.println("i14 >= i15 is " + (i14 >= i15));

    System.out.println("---Logical Operators---");
    // & : Logical AND returns true when both the operands are true.
    // && : Shortcircuit AND
    // | : Logical OR
    // || : Shortcircuit OR
    // ! : Logical NOT
    // ^ : Exclusive OR

    // System.out.println(false & (5 / 0 == 0)); // Runtime Exception
    System.out.println(false && (5 / 0 == 0)); // false
    // System.out.println(true | (5 / 0 == 0)); // Runtime Exception
    System.out.println(true || (5 / 0 == 0)); // true
    System.out.println("!true is " + !true);
    System.out.println("true ^ true is " + (true ^ true));
    System.out.println("true ^ false is " + (true ^ false));
    System.out.println("false ^ false is " + (false ^ false));
    System.out.println("false ^ true is " + (false ^ true));

    System.out.println("---Bitwise Operators---");
    // & copies a bit if present in both operands
    // ! copies a bit if present in either operands
    // ^ copies a bit if set in one operand but not both
    // ~ flips the bits
    // >> move a number of bits to the right specified by the right operand
    // >>> move a number of bits to the right specified by the right operand and
    // fill with zeros
    // << move the left operand bits by the number of bits specified by the right
    // operand
    System.out.println("4 & 5 = " + (4 & 5)); // 4
    /*
     * 1 0 0
     * & & &
     * 1 0 1
     * -----
     * 1 0 0
     *
     *
     */

    System.out.println("4 | 5 = " + (4 | 5)); // 5
    /*
     * 1 0 0
     * | | |
     * 1 0 1
     * -----
     * 1 0 1
     */

    System.out.println("4 ^ 5 = " + (4 ^ 5)); // 1
    /*
     * 1 0 0
     * ^ ^ ^
     * 1 0 1
     * -----
     * 0 0 1
     */

    System.out.println("~1 is " + ~1);
    System.out.println(Integer.toBinaryString(1)); // 00000001 if the first bit is 0 it meaans positive int
    System.out.println(Integer.toBinaryString(-2)); // 11111110 if the first bit is 1 it means negative int
    System.out.println((byte) 0b11111110); // -2
    System.out.println((byte) 0b10000000); // -128 = -(2^7)
    System.out.println((byte) 0b11000000); // -64 = -(2^7) + (2^6)
    System.out.println("5 = " + 0b101); // 00000101
    System.out.println("5 >> 1 is " + (0b101 >> 1)); // 00000010
    System.out.println("5 in binary format is " + Integer.toBinaryString(5));
    System.out.println("2 in binary format is " + Integer.toBinaryString(2));
    int negativeByteValue = 0b11111111111111111111111110000000;
    System.out.println("-128 is " + negativeByteValue);
    System.out.println("-128 >>> 1 is " + (negativeByteValue >>> 1)); // 01111111111111111111111111000000
    System.out.println("-128 >> 1 is " + (negativeByteValue >> 1)); // 11111111111111111111111110000000

    System.out.println("5 = " + 0b101);
    System.out.println("5 << 1 is " + (0b101 << 1));
    System.out.println("5 in binary format  is " + Integer.toBinaryString(5));
    System.out.println("10 in binary format  is " + Integer.toBinaryString(10));
    System.out.println("10 * 2 = 10 << 1 = " + (10 << 1)); // x << y = x * (2 ^ y)
    System.out.println("10 / 2 = 10 >> 1 = " + (10 >> 1)); // x >> y = x / (2 ^ y)

    System.out.println();

  }
}
```
