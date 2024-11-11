# Exp-10-IMPLEMENT-DIFFIE-HELLMAN-KEY-EXCHANGE
## AIM:
To implement the Diffie-Hellman Key Exchange algorithm using C language.
## ALGORITHM:
### Step 1: 
Both Alice and Bob shares the same public keys g and p. 
### Step 2: 
Alice selects a random public key a. 
### Step 3:
Alice computes his secret key A as g a mod p.
### Step 4:
Then Alice sends A to Bob.
### Step 5:
Similarly Bob also selects a public key b and computes his secret key as B and sends the same back to Alice.
### Step 6:
Now both of them compute their common secret key as the other one’s secret key power of a mod p.

## PROGRAM:
```c

//DEVELOPED BY : Vignesh R
// REGISTER NO. : 212223240177
#include <stdio.h>


long long int mod_exp(long long int base, long long int exp, long long int mod) {
    long long int result = 1;
    while (exp > 0) {
        // If exp is odd, multiply base with result
        if (exp % 2 == 1)
            result = (result * base) % mod;

        // Now exp must be even, so divide by 2 and square the base
        exp = exp >> 1; // equivalent to exp = exp / 2
        base = (base * base) % mod;
    }
    return result;
}

int main() {
    long long int P, G, a, b, x, y, ka, kb;

    printf("\n********* Diffie-Hellman Key Exchange Algorithm **********\n\n");

    // Step 1: Agree on public values P (prime number) and G (primitive root)
    printf("Enter a prime number P: ");
    scanf("%lld", &P); // A prime number P is taken
    printf("The value of P: %lld\n", P);

    printf("Enter a primitive root G for P: ");
    scanf("%lld", &G); // A primitive root G is taken
    printf("The value of G: %lld\n\n", G);

    // Step 2: Alice selects a private key a
    printf("Enter the private key for Alice (a): ");
    scanf("%lld", &a);
    x = mod_exp(G, a, P); // Alice's public key x = G^a % P
    printf("The public key for Alice (x = G^a mod P): %lld\n", x);

    // Step 3: Bob selects a private key b
    printf("Enter the private key for Bob (b): ");
    scanf("%lld", &b);
    y = mod_exp(G, b, P); // Bob's public key y = G^b % P
    printf("The public key for Bob (y = G^b mod P): %lld\n\n", y);

    // Step 4: Exchange public keys and generate the shared secret key
    ka = mod_exp(y, a, P); // Alice computes the shared key ka = y^a % P
    kb = mod_exp(x, b, P); // Bob computes the shared key kb = x^b % P

    // Step 5: Display the shared secret keys (ka and kb should be equal)
    printf("Shared secret key for Alice (ka = y^a mod P): %lld\n", ka);
    printf("Shared secret key for Bob (kb = x^b mod P): %lld\n", kb);

    if (ka == kb) {
        printf("\nDiffie-Hellman Key Exchange successful. Both parties share the same key.\n");
    } else {
        printf("\nError: The keys for Alice and Bob do not match.\n");
    }

    return 0;
}
```
## Output:
![image](https://github.com/user-attachments/assets/fb89153a-33e0-4595-97c1-803d759a253e)



## Result:
Thus the Diffie-Hellman key exchange algorithm had been successfully implemented using C.
