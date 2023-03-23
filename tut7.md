(a)

eve has Bob's private key
from Bob private key, Eve can decrypt encrpyted k by Alice which was encrypted through Bob public
decrypted k = session key , all messages are known

(b)
x, y can be obtained via decrypting with BOB, ALICE private key
but because p, a, b is unknown, unable to calculate k = y^amodp = x^bmodp

• Still does not know a and b since it was not sent directly over the network 
• Cannot compute g^(ab) modp easily without knowing a and b 
• Forward secrecy is preserved!

3.
<!-- use AES CBC mode of chaining --> ->incorrect

{ 
    ans key

• Store metadata ℎ𝑖 = H(hi-1 || H(fi))
• Let ℎ0= H(0)
• When first file comes, 
• Meta data ℎ1 = H(ℎ0 || 𝐻(𝑓1))
• When second file comes, 
• Meta data ℎ2 = 𝐻(ℎ1||𝐻(𝑓2))
• And so on
• When query i,
• Return meta data ℎi


ii) use a tree data structure with leftmost leaf -> H(f1)
    rightmost leaf -> H(fk) 

    time taken to update = -> depends on the tree
    R2 -> query result can be computed in (i-jlogn) -> tree -> only need tree traversal to extract data from tree

}



4
(a) D not correct
collision resistant is defined as difficult to find 2 inputs that hash to the same output. the mere existence of m and m' such that H(m) = H(m') does not fit the definition

(b)
    the xor of the 2 collision functions is still collision resistant, and thus H() is a collision resistant hash

    sha3(m) XOR sha3(m) is  == 0

(c)
    not collision resistant,
    H1(0001) = sha3(0001) xor sha3(1000)
    H1(1000) = sha3(1000) xor sha3(0001) 
    reverses of string x all collides, not collision resistant

(d) 
    H1(1100) = sha3(1100) xor sha3(1100) = 0
    H1(0011) = sha3(0011) xor sha3(0011) = 0

    many that collide to 0, not collsion resistant

    for others

    if string is a palindrome
    H1(0110) = sha3(0110) xor sha3(1001)
    H1(1001) = sha3(1001) xor sha3(0110)

    if string is palindrome, 1s complement always collide
    or
    the r(x) xor 1 for any x that is a palindrome always collide, for