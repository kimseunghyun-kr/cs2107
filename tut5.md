1000C2 = 499500
1.17 * 100 * 1000 ^0.5
M = 1000
1000 > 369

with probability more than 0.5, there is a pair of messages tagged with 
the same value

M = 2^33
1.17*(2^64)^0.5
1.17*2^32
M > 1.17*2^32
with probability more than 0.5, there is a pair of messages tagged with 
the same value

set S : k = 2^7
set T : m = 2^5
n = 16

p = 0.04726687186

0.5 = 1-2.17^-(x * 128 * 2^-16)
log(0.5) = -(x*0.001953125)log(2.17)
x = 458.0855962

4(a)
it is to prevent further access should a malicious actor gets access of the authentication token, reduce the possibility of the mallory from acessing the account through limiting the time in which the authentication token is valid



4(b)(i)
m = d || r || u
y = H(m)

d : date and time (precision upto seconds) of the token creation
represented

r : a randomly selected 128-bit string, which is to be served as
salt

u : 10-character user id

mallory can create m thru exhaustive search d, r
and H(m) respectively

security determined by length of d, r , as hash H is deterministic, no secret present,

4(b)(ii)

mac is defined to be an encryption standard where even if the mallory has access to numerous pairs of (mac, ptext), mallory is unable to forge new mac.

through mac assumption, mallory becomes unable to forge y(mac) even if he knows m.

k should be kept by server to generate Mac, and store it in token. If attacker able to generate valid token, then attacker must know the secret key (contradiction to Mac being unforgeable).

-> also as mallory cannot sniff the comms so cannot just take the alice token

4(c)(i)
it is costly to constantly generate a 128 bit token every time a user logs in, and compare the 128 bit token. 


4(c)(ii)
the mac based variant fails when 
- the secret key is leaked
- the MAC has vulnerability,
- the MAC is not implemented correctly.

5
such tempering will be detected as the c' decrypted will be gibberish after block 1, due to the usage of CBC mode
as c2 xor t3 -> c3 originally 
and not c3 xor t2 -> c2 {changed case}
unless the attacker knows the plaintext and re-encrypted the c' by AES CBC mode with the plaintext block 2 and block 3 swapped

(b)
Let’s assume that the attacker
know a message b and the corresponding <n, v, c, t1, t2, . . . , tn, tn+1>.

should V2 not be checked, the total length of the blocks is not checked and the V3 just uses the unchecked length. then, the attacker can just append message on b to make {btilda}, while sending a message up to length n, which will be verified true, as the message up to n is valid for {btilda} which is until where V3 checks

(c)correction:

HMAC does not guarantee confidentiality as it is deterministic. If 2 blocks can be swapped and give a valid result, it means the data in those 2 blocks are the same { HMAC is still a collision resistant HASH }

(d)
Correction
Use authenticated encryption modes like CGM or GCM (designed for AES)
->{encrypt then mac(?)}

{from textbook : 
The encryption can be efficiently carried out in this
way: choose a random AES 128-bit key k, encrypt k using PKC, and encrypt F using
AES (with suitable mode, say GCM, CBC or CTR) with k as the key}

auth using pkc, confidentiality with aes gcm mode encrypt(?)

<!-- Encryption is designed to provide confidentiality. It does not 
necessary guarantee integrity and authenticity.  -->


