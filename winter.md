Basic aim is we have to provide a message to the server which generates a signature for this and once we do this, we have to generate another message having the same signature


` def keygen(cls):
        sk = [os.urandom(32) for _ in range(32)]
        vk = [cls.hash(x, 256) for x in sk]
        return cls(sk, vk)`


Here, we have two variables, an sk corresponding to a secret key and a vk corresponding to verification key.
The sk is a private key, while vk is the public key which is availbale to everyone. sk is used for generating signatures while vk is used to verify these signatures
The secret key is a list of 32 random numbers. The verification key is the secret key which is hashed 256 times.
vk is used for verifying the signatures. sk is gonna be hashed some amount of times at the beginning, then while verifying, its gonna be hashed another some amount of times to get a total of 256 hashes.

`
def hash(cls, x, n):
        for _ in range(n):
            x = sha256(x).digest()
        return x
`
This function is basically used to hash(SHA 256) any given input 'n' number of times.

`def sign(self, msg):
        m = self.hash(msg, 1)
        sig = b''.join([self.hash(x, 256 - n) for x, n in zip(self.sk, m)])
        return sig`
This defines a function to sign a given message. This then hashes the message to a length of 32 bytes, which gives the number of times we need to hash sk values. We get 32 values, and we hash the sk values  that many number of times. The value of each byte is used to hash the first random chunk that many number of times.

For verification, we continue hashing by feeding back the message and signature. Thus if we have hashed the original message n times, we hash it 256 - n times. We compare the hashed message with the orginal message at the end, if that works, we get the flag.


