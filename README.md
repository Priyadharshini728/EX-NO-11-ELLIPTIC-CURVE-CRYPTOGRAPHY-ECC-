# EX-NO-11-ELLIPTIC-CURVE-CRYPTOGRAPHY-ECC
## NAME:PRIYADHARSHINI P
## REGISTER NUMBER: 212224040252
## DATE:27-02-2026
## Aim:
To Implement ELLIPTIC CURVE CRYPTOGRAPHY(ECC)


## ALGORITHM:

1. Elliptic Curve Cryptography (ECC) is a public-key cryptography technique based on the algebraic structure of elliptic curves over finite fields.

2. Initialization:
   - Select an elliptic curve equation \( y^2 = x^3 + ax + b \) with parameters \( a \) and \( b \), along with a large prime \( p \) (defining the finite field).
   - Choose a base point \( G \) on the curve, which will be used for generating public keys.

3. Key Generation:
   - Each party selects a private key \( d \) (a random integer).
   - Calculate the public key as \( Q = d \times G \) (using elliptic curve point multiplication).

4. Encryption and Decryption:
   - Encryption: The sender uses the recipient’s public key and the base point \( G \) to encode the message.
   - Decryption: The recipient uses their private key to decode the message and retrieve the original plaintext.

5. Security: ECC’s security relies on the Elliptic Curve Discrete Logarithm Problem (ECDLP), making it highly secure with shorter key lengths compared to traditional methods like RSA.

## Program:
```
#include <stdio.h>

typedef struct{ long long x,y; }P;

long long inv(long long a,long long m){
    long long m0=m,t,q,x0=0,x1=1;
    while(a>1){ q=a/m; t=m; m=a%m; a=t;
        t=x0; x0=x1-q*x0; x1=t; }
    return x1<0?x1+m0:x1;
}

P add(P A,P B,long long a,long long p){
    P R; long long l;
    if(A.x==B.x && A.y==B.y)
        l=(3*A.x*A.x+a)*inv(2*A.y,p)%p;
    else
        l=(B.y-A.y)*inv(B.x-A.x,p)%p;

    R.x=(l*l-A.x-B.x)%p;
    R.y=(l*(A.x-R.x)-A.y)%p;

    R.x=(R.x+p)%p; R.y=(R.y+p)%p;
    return R;
}

P mul(P P1,long long k,long long a,long long p){
    P R=P1; k--;
    while(k--) R=add(R,P1,a,p);
    return R;
}

int main(){
    long long p,a,pa,pb;
    P G,A,B,SA,SB;

    scanf("%lld%lld",&p,&a);
    scanf("%lld%lld",&G.x,&G.y);
    scanf("%lld%lld",&pa,&pb);

    A=mul(G,pa,a,p);
    B=mul(G,pb,a,p);

    SA=mul(B,pa,a,p);
    SB=mul(A,pb,a,p);

    printf("A:(%lld,%lld)\nB:(%lld,%lld)\n",A.x,A.y,B.x,B.y);
    printf("Secret:(%lld,%lld)",SA.x,SA.y);
}

```

## Output:
<img width="1250" height="897" alt="image" src="https://github.com/user-attachments/assets/84621007-6923-46c2-a53a-0f4aaec01676" />



## Result:
The program is executed successfully

