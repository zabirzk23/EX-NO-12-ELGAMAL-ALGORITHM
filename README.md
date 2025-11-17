# EX-NO-12-ELGAMAL-ALGORITHM

## AIM:
To Implement ELGAMAL ALGORITHM

## ALGORITHM:

1. ElGamal Algorithm is a public-key cryptosystem based on the Diffie-Hellman key exchange and relies on the difficulty of solving the discrete logarithm problem.

2. Initialization:
   - Select a large prime \( p \) and a primitive root \( g \) modulo \( p \) (these are public values).
   - The receiver chooses a private key \( x \) (a random integer), and computes the corresponding public key \( y = g^x \mod p \).

3. Key Generation:
   - The public key is \( (p, g, y) \), and the private key is \( x \).

4. Encryption:
   - The sender picks a random integer \( k \), computes \( c_1 = g^k \mod p \), and \( c_2 = m \times y^k \mod p \), where \( m \) is the message.
   - The ciphertext is the pair \( (c_1, c_2) \).

5. Decryption:
   - The receiver computes \( s = c_1^x \mod p \), and then calculates the plaintext message \( m = c_2 \times s^{-1} \mod p \), where \( s^{-1} \) is the modular inverse of \( s \).

6. Security: The security of the ElGamal algorithm relies on the difficulty of solving the discrete logarithm problem in a large prime field, making it secure for encryption.

## Program:

```
#include <stdio.h>
long long modExp(long long base, long long exp, long long mod) {
 long long res = 1;
 while (exp > 0) {
 if (exp % 2) res = (res * base) % mod;
 base = (base * base) % mod;
 exp /= 2;
 }
 return res;
}
int main() {
 long long p, g, privA, pubA, k, msg, c1, c2, dec;
 printf("Enter prime p, generator g, private key: ");
 scanf("%lld %lld %lld", &p, &g, &privA);
 pubA = modExp(g, privA, p);
 printf("Public key: %lld\n", pubA);
 printf("Enter message and random k: ");
 scanf("%lld %lld", &msg, &k);
 c1 = modExp(g, k, p);
 c2 = (msg * modExp(pubA, k, p)) % p;
 printf("Encrypted (c1, c2): (%lld, %lld)\n", c1, c2);
 dec = (c2 * modExp(c1, p - 1 - privA, p)) % p;
 printf("Decrypted message: %lld\n", dec);
 return 0;
}
```

## Output:

<img width="737" height="291" alt="image" src="https://github.com/user-attachments/assets/1e17adee-76b7-42d4-8661-ef15e6aec9ef" />

## Result:
The program is executed successfully.
