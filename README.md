## Name: AGILAN J
## Reg no: 212224100002


# EX-NO-13-MESSAGE-AUTHENTICATION-CODE-MAC

## AIM:
To implement MESSAGE AUTHENTICATION CODE(MAC)

## ALGORITHM:

1. Message Authentication Code (MAC) is a cryptographic technique used to verify the integrity and authenticity of a message by using a secret key.

2. Initialization:
   - Choose a cryptographic hash function \( H \) (e.g., SHA-256) and a secret key \( K \).
   - The message \( M \) to be authenticated is input along with the secret key \( K \).

3. MAC Generation:
   - Compute the MAC by applying the hash function to the combination of the message \( M \) and the secret key \( K \): 
     \[
     \text{MAC}(M, K) = H(K || M)
     \]
     where \( || \) denotes concatenation of \( K \) and \( M \).

4. Verification:
   - The recipient, who knows the secret key \( K \), computes the MAC using the received message \( M \) and the same hash function.
   - The recipient compares the computed MAC with the received MAC. If they match, the message is authentic and unchanged.

5. Security: The security of the MAC relies on the secret key \( K \) and the strength of the hash function \( H \), ensuring that an attacker cannot forge a valid MAC without knowledge of the key.

## Program:

```c
#include <stdio.h>
#include <string.h>

#define KEY "secretkey"

unsigned int mac(char *msg, char *key)
{
    unsigned int m = 0;
    int i;

    for (i = 0; msg[i] != '\0'; i++)
        m ^= msg[i];

    for (i = 0; key[i] != '\0'; i++)
        m ^= key[i];

    return m;
}

int main()
{
    char msg[100];
    unsigned int sent, received;

    printf("Enter message: ");
    fgets(msg, sizeof(msg), stdin);
    msg[strcspn(msg, "\n")] = '\0';

    sent = mac(msg, KEY);
    received = mac(msg, KEY);

    printf("Sent MAC: %u\n", sent);
    printf("Received MAC: %u\n", received);

    if (sent == received)
        printf("Message is authentic.\n");
    else
        printf("Integrity check failed.\n");

    return 0;
}
```


## Output:

<img width="740" height="397" alt="2026-09-01 at 2 11 17 PM" src="https://github.com/user-attachments/assets/8bbf47cd-28bc-4593-b41f-a08e6e97ca7c" />


## Result:
The program is executed successfully.
