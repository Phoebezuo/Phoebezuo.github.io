---
layout:     post
title:      Magma Summary
date:       2020-10-18
summary:    Magma Summary Notes for MATH2088
categories: Magma cryptosystem
---

- [Magma Basic Usage](#magma-basic-usage)
  - [Arithmetic](#arithmetic)
  - [Index](#index)
  - [Boolean Operation](#boolean-operation)
  - [Control Structure](#control-structure)
  - [Type Conversion](#type-conversion)
- [Mathematics Theorem](#mathematics-theorem)
  - [Euclidean Algorithm](#euclidean-algorithm)
  - [Lucas-Lehmer Test](#lucas-lehmer-test)
  - [Coincidence Index ($CI$)](#coincidence-index-ci)
    - [Common Statistic of $CI$](#common-statistic-of-ci)
    - [Cipher vs $CI$](#cipher-vs-ci)
    - [Digraph Coincidence Index](#digraph-coincidence-index)
  - [Coincidence Discriminant ($CD$)](#coincidence-discriminant-cd)
    - [Common Statistic of $CD$](#common-statistic-of-cd)
- [Substitution Cipher](#substitution-cipher)
  - [Setup](#setup)
  - [Encoding](#encoding)
  - [Decoding](#decoding)
  - [Decoding Techniques](#decoding-techniques)
    - [Method 1](#method-1)
    - [Method 2](#method-2)
    - [Method 3](#method-3)
  - [Check Validity](#check-validity)
- [Vigenere Cipher](#vigenere-cipher)
  - [Setup](#setup-1)
  - [Encoding](#encoding-1)
  - [Decoding](#decoding-1)
  - [Decoding Techniques](#decoding-techniques-1)
- [Transposition Cipher](#transposition-cipher)
  - [Setup](#setup-2)
  - [Encoding](#encoding-2)
  - [Decoding](#decoding-2)
  - [Decoding Techniques](#decoding-techniques-2)
    - [Method 1](#method-1-1)
    - [Method 2](#method-2-1)

# Magma Basic Usage

```
SetLogFile("filename");
load "MagmaProcedures.txt";
```

## Arithmetic

- Assignment: `:=`
- Division: `23 div 3;`
- Residue: `23 mod 4;`
- Logarithm: $log_{10}100 =$ `Log(10,100);`
- Random select a 50 digit number: `Random(10^49, 10^50);`
- Factorial: $18! =$ `Factorial(18);`
- Greatest Common Divisior: `GCD(1333,234);`
- Check a number if prime or not: `IsPrime(7);`

## Index

*Note:* Magma sequences are indexed from 1, not 0.

```
loyal:="God save the Queen";
loyal[3],loyal[5..6],loyal[14..18];
// d sa Quene
```

- `alphabet[15];` means the 15th element in alphabet array 
- `Index(alphabet, "Q");` means the index of "Q" in alphabet array

## Boolean Operation

- $x = y$ means `x eq y`
- $x \neq y$ means `x ne y`
- $x < y$ means `x lt y`
- $x \leq y$ means `x le y`
- $x > y$ means `x gt y`
- $x \geq y$ means `x ge y`
- $x \in A$ means `x in y`

## Control Structure

- while

    ```
    while boolean do
        statements;
    end while;
    ```

- repeat-until

    ```
    repeat
        statements;
    until boolean;
    ```

- for

    ```
    for i:= a to b by c do
        statements;
    end for;
    ```
    Also,
    ```
    for i in domain do
        statements;
    end for;
    ```

- if-then-else
   
    ```
    if boolean then 
        statements;
    elif boolean then 
        statements;
    else
        statements;
    end if;
    ```

## Type Conversion

- Convert `MonStgElt` to `CryptTxt`

    ```
    C:=SubstitutionCryptosystem();
    CryptTxt:=Encoding(C,MonstgElt);
    ```

- Convert `CryptTxt` to `MonStgElt`

    ```
    MonStgElt:=String(CryptTxt);
    ```

- Convert `MonStgElt` to `CryptKey`

    ```
    system:=VigenereCryptosystem(N);
    CryptKey:=system!"abc..";
    ```

# Mathematics Theorem

## Euclidean Algorithm

```
MATH2088GCD:=function(a,b)
    while b ne 0 do
        r:= a mod b;
        a:=b;
        b:=r;
    end while;
    return a;
end function;
```

## Lucas-Lehmer Test

```
CheckMersenne:=procedure(p)
    m:=2^p-1;
    r:=4;
    for i:=1 to p-2 do
        r:= (r^2-2) mod m;
    end for;
    
    if r eq 0 then 
        print "M(",p,")=",m,"is prime";
    else 
        print "M(",p,")=",m,"is not prime";
    end if; 
end procedure;
```

## Coincidence Index ($CI$)

Suppose there are N letters in the text, $CI = \frac{\sum k_i(k_1 - 1)}{N(N-1)}$, where $k_i$ is the number of times the ith symbol appears. 

### Common Statistic of $CI$

- Random string of text: $CI = \frac{1}{26} \approx 0.0385$
- English text: $CI \approx 0.066$

### Cipher vs $CI$

- $CI(Substitution) = CI(English)$
- $CI(Random) < CI(Vig_80) < CI(Vig_20) < CI(English)$
    - Vig_80 means vigenere cipher with ken length 80.
    - Vig_20 means vigenere cipher with ken length 20.
- $CI(Transposition) = CI(English)$

### Digraph Coincidence Index 

- Letters for random text are adjacent: $CI \approx 0.001$.
- Letters for English text are NOT adjacent: $CI \approx 0.004$.
- Letters for English text are adjacent: $CI \approx 0.007$.

## Coincidence Discriminant ($CD$)

$CD = \sum_{x,y}(p(x,y) - p(x,-)p(-,y))^2 = \sum_{x,y}(p(x,y) - s(x,y))^2$, where

- $p(x,y)$ is the probability that a randomly chosen digraph is xy.
- $p(x,-)$ is the probability that a randomly chosen digraph begin with x.
- $p(x,-)$ is the probability that a randomly chosen digraph begin with x.
- $s(x,y)$ is the relative frequency in a piece of normal text.

### Common Statistic of $CD$

- Letters for English text are NOT adjacent: $CD \approx 0.001$.
- Letters for English text are adjacent: $CD \approx 0.005$.

# Substitution Cipher

A substitution cipher is a method of enciphering a message by replacing all occurrences of the various letters by other letters, according to some key. The ith letter of the alphabet is replaced everywhere by the jth letter, where $j \equiv i + k \mod 26$.

## Setup

```
system:=SubstitutionCryptosystem();
```

- Random generate a key 

    ```
    key:=RandomKey(system);
    ```
- Specify the key

    ```
    key:=system!"BCDEFGHIJKLMNOPQRSTUVWXYZA";
    ```
    key should be a genuine permutation of the letters A to Z, otherwise, magma cannot calculate the inverse key. 

## Encoding

```
PT:=Encoding(system, message);
CT:=Enciphering(key, PT);
```

## Decoding

```
yek:=InverseKey(key);
Enciphering(yek, CT);
```

## Decoding Techniques

### Method 1

1. Find the most frequently letters using `SortedFreqDist(CryptTxt);`. For example, the most frequent occurrence is letter Z, followed by letter F.
   
    <img src='https://i.loli.net/2020/10/18/3nV2yTOokUiIGmB.png' alt='3nV2yTOokUiIGmB'/>

2. According to approximate percentage of occurrences of the various letters in English text, it shows that E > T > A > O > I > N. 
   
   <img src='https://i.loli.net/2020/10/18/kgXNrTmcBFzo3EV.png' alt='kgXNrTmcBFzo3EV'/>

3. Find all places in CryptTxt that is start with F, end with Z. The occurrence of `F*Z` in CT corresponds to `T*E` in PT. Suppose, the output is `FEZ`.
   
    ```
    MonStgElt:=String(CryptTxt);
    for i:=1 to #MonStgElt-2 do
        if MonStgElt[i] eq "F" and MonStgElt[i+2] eq "Z" then 
            print MonStgElt[i..i+2]; 
        end if; 
    end for;
    ```

    <img src='https://i.loli.net/2020/10/18/Ggx6IfLTh4u3bpR.png' alt='Ggx6IfLTh4u3bpR'/>

4. Use `freqkey` to guess at decoding key based on letter frequencies. Note that `guess_key` is already inverse key. 
   
   ```
   guess_key:=system!freqkey(CryptTxt);
   ```

   <img src='https://i.loli.net/2020/10/18/m1JpvrcjwugEdtY.png' alt='m1JpvrcjwugEdtY'/>
   
   It shows:
   - `T` in PT = `F` in CT
   - `H` in PT = `I` in CT, `H` in PT $\neq$ `E` in CT
   - `E` in PT = `Z` in CT

5. So swap `I` and `H` in guessing key using `swap`. Let `H` in PT = `E` in CT. 
    ```
    swap("I","H",~guess_key);
    ```

### Method 2

1. `MostCommonPolygraphs` is to find the most frequent ploygraphs (short sequence of letters) in a string. The following code is to find all the trigraph occurrences in guessing plaintext with a relative frequency greater than 0.01. 
   
    ```
    MostCommonPolygraphs(guess_PT, 3, 0.01);
    ```

    <img src='https://i.loli.net/2020/10/18/g1EnJq6ZLyTkNBW.png' alt='g1EnJq6ZLyTkNBW'/>

2. Output is `THE, HES, ARD`, but it should be `THE, HER, AND`. So swap `S` to `R` and `R` to `N`. 
   
   ```
   swap("S","R",~guess_key);
   swap("R","N",~guess_key);
   ```
   
### Method 3

Using `BestSubstitutionKey(CryptTxt)` will automates the procedure to guess a deciphering key from letter frequencies and then progressively alerting it to increase the common-word score.

<img src='https://i.loli.net/2020/10/18/PR6vFuAh1GqMmTf.png' alt='PR6vFuAh1GqMmTf'/>

## Check Validity

Using `Score` to check its correctness, the higher the better. 

```
guess_PT:=Enciphering(guess_key, CryptTxt);
Score(guess_PT, Common);
```

# Vigenere Cipher

The ith letter of the message is enciphered with the jth translation cipher and n-letter word as key, where $j \equiv i \mod n$. 

## Setup

N is the length of the key. 

```
system:=VigenereCryptosystem(N);
key:=system!"ABC..";
``` 

## Encoding

```
PT:=Encoding(system, message);
CT:=Enciphering(key, PT);
```

According to this chart

<img src='https://i.loli.net/2020/10/18/foqY3bNOITyHQj9.png' alt='foqY3bNOITyHQj9'/>

- If PT is "HOTEL", it encodes to be [7,14,19,4,11]
- If key is "BAT", it encodes to be [1,0,24]

```
7  14  19  4  11
1   0  24  1   0
-----------------
8  14  17  5  11
```

[8,14,17,5,11] translate to alphabet is "IORFL", thus the cipher text is "IORFL". (Note that 17 at 3rd index is calculate from 19 + 24 - 26 = 17)

## Decoding

```
yek:=InverseKey(key);
Enciphering(yek, CT);
```

If key is "CARSLAW", the inverse key is "YAJIPAE"

```
key: C  A  R  S  L  A  W
yek: Y  A  J  I  P  A  E 
```
- idx(C) - 1 + idx(Y) - 1 = 26
- idx(A) - 1 + idx(A) - 1 = 0
- idx(R) - 1 + idx(J) - 1 = 26
- idx(S) - 1 + idx(I) - 1 = 26
- idx(L) - 1 + idx(P) - 1 = 26
- idx(A) - 1 + idx(A) - 1 = 0
- idx(W) - 1 + idx(E) - 1 = 26
  
## Decoding Techniques

1. Find the key length using `Decimation(string, start, period)`. For example, `Decimation(alpha, 2, 3)` means starting with 1st letter, print every 3rd letter of alpha, which outputs `BEHKNQTW`. 

    ```
    for i:=2 to 20 do
        print "Period:",i,"CI:",CoincidenceIndex(Decimation(MonStgElt,1,i));
    end for;
    ```

    N will be the key length that is smaller number that gives a CI near 0.06. 

2. Use `SortedFreqDist` to find which letter occurs most frequently in this decimation. The most frequently letter in normal English text is E. 

    ```
    for i:=1 to N do
        SortedFreqDist(Decimation(MonStgElt, i, N))[1];
    end for;
    ```

3. For each decimation, use `alphabet[Index(alphabet, "ß") - Index(alphabet, "E") + 1)]` to get the letter in current index of key, where `ß` is the most frequent letter in `MonSstgElt` cipher text. 

# Transposition Cipher

Transposition cipher do not change the frequencies of the various letters at all. 

<img src='https://i.loli.net/2020/10/18/HN3vlU9hGjdVWTP.png' alt='HN3vlU9hGjdVWTP'/>

## Setup

N is the length of the key. 

```
system:=TranspositionCryptosystem(N);
key:=system![1,2,..];
``` 

## Encoding

```
PT:=Encoding(system, message);
CT:=Enciphering(key, PT);
```

## Decoding

Sometimes, it will need to reverse the key using `yek:=system!Reverse(key);`

```
PT:=Enciphering(key, CT);
```

## Decoding Techniques

### Method 1

1. The length of key can be found by using `CoincidenceIndex(Decimation(MonStgElt, start, period))`.

    ```
    for N:=2 to 20 do
        for i:=2 to m do
            "N=",N,"i=",i,CoincidenceIndex(Decimation(MonStgElt,[1,i],N));
        end for;
    end for;
    ```

    N will be the key length that is smaller number that gives a CI near 0.07. 

    <img src='https://i.loli.net/2020/10/18/KNYOeBQTxRznCyA.png' alt='KNYOeBQTxRznCyA'/>

    This implies the key length m should be 7.

2. Also using `CoincidenceIndex(Decimation(MonStgElt, start, period))` to find which two columns are adjacent. 

    ```
    for j:=1 to N-1 do
        for i:=j+1 to N do
            j,i,": CI=",CoincidenceIndex(Decimation(MonStgElt,[j,i],N));
        end for;
    end for;
    ```

    <img src='https://i.loli.net/2020/10/18/spyRg8G1zm5x7PQ.png' alt='spyRg8G1zm5x7PQ'/>
    
    This implies the key is [6,7,3,1,2,4,5] or its inverse.

### Method 2

1. The length of key can be found by using `CheckPeriod(MonStgElt, [2..50], 0.007, 0.005)`. The parameters are
   
   - `[2..50]` means ask this function to check all the numbers m from 2 to 50 as possible key length. 
   - `0.007` means test `CoincidenceIndex(Decimation(MonStgElt,[i,j],m))` > 0.007.
   - `0.005` means test `CoincidenceDiscriminant(Decimation(MonStgElt,[i,j],m)` > 0.005.

    The output N will be the length of key. 

2. Find the adjacent columns using `FindAdjacencies(MonStgElt, N, 0.006, 0.005)`. The parameters are
   
   - `N` the key length. 
   - `0.006` means test `CoincidenceIndex(Decimation(MonStgElt,[i,j],N))` > 0.006. 
   - `0.005` means test `CoincidenceDiscriminant(Decimation(MonStgElt,[i,j],N))` > 0.005.

3. Use `CompareDigraphs(Decimation(MonStgElt,[i,j],N),sample)` to check the sequence of key, where sample is also type `MonStgElt`.
   
```
for i:=1 to N do
    for k:=0 to N-2 do
        j:=(i+k) mod 23+1;
        if CompareDigraphs(Decimation(MonStgElt,[i,j],N),sample) lt 0.0045 then
            i,j;
        end if;
    end for;
end for;
```

   - If the result has low value, means it does follow the sequence of key.
   - If the result has high value, means it does NOT follow the sequence of key.