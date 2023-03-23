public key

7B F0 DA 9B 4B 0F 1B 21 CF 4A 90 67 EA 49 87 67
04 EA 0E 5D 0E 72 C5 20 A0 4D 2C D7 F6 7F 26 0E
B3 F5 D2 D0 1A 04 B1 68 4F 22 D5 D1 34 5A 42 49
19 D6 BF 0D 34 95 8B CD 07 33 17 48 B1 46 5F 44
43 5B 67 79 2B F2 94 45 60 5C 14 AE FB A2 5C 69
03 C1 D3 18 61 62 8C 8A B9 88 17 A5 00 C1 10 18
94 0B FE AF 33 11 AD 54 CE 16 2F 50 35 32 AF 59
17 35 08 A5 AF B5 A0 FB 0A C1 DE 58 D9 37 95 32
5F 6F B8 C1 EF E1 3B 7D EF 47 B9 6F BD DF 1C BD
87 AB CA 96 0C 67 11 CD 07 6A F7 80 C3 D4 A0 83
24 9F 14 36 AD E1 99 E8 03 FA 72 A3 0E 83 DF D5
BB 91 6D 6F 44 4D 95 28 93 FB D5 40 A9 F8 4C D3
43 68 7B 4F AF 9C 15 38 B5 69 44 D3 0D CA 15 46
2A B3 A5 CF 6A 57 55 57 D6 71 78 3F 89 C1 A8 8B
F6 6D 84 84 F7 5F 60 AB 7B 79 9A 50 DC 25 88 8B
5A EF DB 5B 01 A5 23 7E 4E 2A 83 3E 04 8B 12 34

public key : key available to public used for initial encrypt

n is the public key

exponent is 65537 usually

advantage of having small exponent reduces overhead of computing the sign

google is DSA base

2.

v = H(S)[:128] == IV
K = H(H(S))[:128] == key


attacker knows 
 - protocol


aes cbc mode = ci = Ek(xi-1 xor pi)

as attacker can obtain multiple ciphertexts sent by bob, he can obtain information that IV is the same for all ciphertext

{corr: hash function used is deterministic. without random seed, IV will be consistent, and so k too. eavesdropper can thus use ciphertext which includes IV to find k, should the Hash func be known to the eavesdropper(eve)}

3.
java.util.Random is not cryptographically secure and deterministic. assuming that the adversary is aware of the algorithm and the hash used, through the IV, which is H(s), he can just H^-1(IV) and find out that the seed is just used from the time. With that knowledge, he can generate the secret key for every possible timeframe. 
{
    corr: If attacker does not know the time, the attacker can stil try all possible seeds since the seed is only 32 bits.
}


4.
Java.security.SecureRandom relies on almost truly random inputs such as the difference in time of individual keyboard inputs, and thus is usually not deterministic.

Bob does use a correct mechanism to get S.

However, Bob still made the mistake of making IV public, and just doing H(S). From the ciphertext, the adversary may still figure out that k = H(IV) as the hash is deterministic. (q2)

5(a)

10 is not sufficient as alphanumeric = {0-9 = 10 + a-z = 26 + A-Z = 26 = 62}

assume 64 = 2^6
for 10 inputs == 2^60, assumed to be reasonably computable time in the tutorial paper

(but if there is a 1sec wait then things go different assuming only 1 device used cuz its gonna take vv long)

{

correction :  password to have at least 29 bits of entropy to 
be secure against online attacks.
• If cryptographic keys are to be generated from the password, and offline attacks 
are possible, then the password should have at least 128 bits of entropy, based 
on NITS recommendation of 128 bits for crypto keys.

as online 10 * 5.954 = 59.54 > 29 for online. sufficient

}


5(b)
client = P 
Server = V


- Derive an “offline attack” and discuss whether 10-character p is
sufficient.

--> assume no oracle

attacker has c u h, objective is to get p

c = ENC(k, r)
h = mac(k, r)
k = SHA3(p).

p = 2^60 {assuming alphanumeric}
attacker can try to exhaustively search through the passwords
by SHA3(p) = k
and using the info of c and h to see if the password p, by decrypting c and h with the respective algorithms and seeing if the random string r obtained is the same for both

by entropy, insufficient as 59.54 < 128 bits of entropy for offline attack
and also insufficient as entirety requires 2^60 operations of finding p, which is assumed to be feasible in this tut

- Suppose there is an implementation flaw and r is also fixed with
value 0....0. What is the implication?

if r fixed with 0 ...0
if r is fixed with 0 .. 0 , entire algo becomes deterministic and not random as the inputs of the k , r values used in ENC and mac are fixed.
system becomes more vulnerable

- for typical home wifi access point, how many characters (assuming they are randomly chosen) are required?

For home wifi access point, need 22 characters to be safe from offline attack. (RFC4086)


6.
attacker knows
plaintext m
ciphertext
IV

objective: authenticate without key k to generate a mac for a different message

from m and ciphertext, m xor c to get long pseudorandom sequence q1...qn

as ctr is used, r1 = enc(IV+j)
j increased by 1 every byte of plaintext m string.
as encryption is deterministic, able to find how for every IV,pseudorandom number sequence is obtained, which can be used to make new mac thru xor with new plaintext m

{


    corr :

    Key idea: make use of xor property and aes ctr mode's cycle of the IV to use xor and get the new mac.


}

7.
Can Mallory generate a c' that would be decrypted to

“Ux gives Uy $9999 dollars”?

from

Ux gives Uy $1000 dollars”,



yes. possible stream cipher IV + 1 every byte of string,

as ciphertext known, mallory can find sequence r {originally obtained from enck(IV+j) for some j } from plaintext xor ciphertext, with DNC condition for the x and y unknown values

he can then try modifying the portion of the of the sequence that corresponds to 1000 to 9999, would only require mallory to try (2^4 * 4) times -- 2^6 times.


