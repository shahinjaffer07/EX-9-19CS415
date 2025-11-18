## EX-NO-9-RSA-Algorithm

## AIM:
To Implement RSA Encryption Algorithm in Cryptography

## Algorithm:

Step 1: Design of RSA Algorithm  
The RSA algorithm is based on the mathematical difficulty of factoring the product of two large prime numbers. It involves generating a public and private key pair, where the public key is used for encryption, and the private key is used for decryption.

Step 2: Implementation in Python or C 
This algorithm can be implemented in languages like Python or C by performing large integer calculations for key generation, encryption, and decryption, utilizing libraries for modular arithmetic if necessary.

Step 3: Algorithm Description  
1. Key Generation:
   - Select two large prime numbers \( p \) and \( q \).
   - Calculate \( n = p \times q \), which will be used as the modulus.
   - Compute the totient \( \phi(n) = (p - 1)(q - 1) \).
   - Choose a public exponent \( e \) such that \( e \) is coprime with \( \phi(n) \).
   - Compute the private key \( d \), which is the modular inverse of \( e \) mod \( \phi(n) \).

2. Encryption:
   - Convert the plaintext message \( M \) into a numerical form \( m \) (such that \( 0 \le m < n \)).
   - Compute the ciphertext \( c \) using the formula: \( c = m^e \mod n \).

3. Decryption:
   - Use the private key \( d \) to recover \( m \) from \( c \) using: \( m = c^d \mod n \).
   - Convert \( m \) back into the original message \( M \).

Step 4: Mathematical Representation  
- Encryption: \( E(m) = m^e \mod n \)
- Decryption: \( D(c) = c^d \mod n \)

Step 5: **Security Foundation  
The security of RSA relies on the difficulty of factoring large numbers; thus, choosing sufficiently large prime numbers for \( p \) and \( q \) is crucial for security.

## Program:

```
#include <stdio.h>
#include <stdlib.h>

long long gcd(long long a,long long b){ while(b){ long long t=b; b=a%b; a=t;} return a; }

long long modexp(long long a,long long e,long long m){
    long long r=1; a%=m;
    while(e){ if(e&1) r=(r*a)%m; a=(a*a)%m; e>>=1; }
    return r;
}

long long modinv(long long a,long long m){
    long long t=0, nt=1, r=m, nr=a;
    while(nr){
        long long q = r / nr;
        long long tmp = nt; nt = t - q*nt; t = tmp;
        tmp = nr; nr = r - q*nr; r = tmp;
    }
    if(r>1) return -1;
    if(t<0) t += m;
    return t;
}

int main(void){
    long long p,q,n,phi,e,d,m,enc,dec;
    printf("p: "); if(scanf("%lld",&p)!=1) return 0;
    printf("q: "); if(scanf("%lld",&q)!=1) return 0;
    n = p*q; phi = (p-1)*(q-1);
    do{ printf("e (coprime with %lld): ", phi); if(scanf("%lld",&e)!=1) return 0; } while(gcd(e,phi)!=1);
    d = modinv(e,phi);
    if(d<0){ puts("No modular inverse for e."); return 1; }
    printf("Public: (n=%lld,e=%lld)\nPrivate:(n=%lld,d=%lld)\n", n,e,n,d);
    printf("message (int < n): "); if(scanf("%lld",&m)!=1) return 0;
    enc = modexp(m,e,n);
    dec = modexp(enc,d,n);
    printf("encrypted: %lld\ndecrypted: %lld\n", enc, dec);
    return 0;
}

```

## Output:

<img width="725" height="353" alt="Screenshot 2025-11-18 201633" src="https://github.com/user-attachments/assets/37f19500-5b07-4a9b-860b-3ac3cbf08b64" />

## Result:
 The program is executed successfully.
