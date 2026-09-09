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

#include <stdio.h>
#include <string.h>

unsigned long generateMAC(char message[], char key[])
{
    unsigned long mac = 0;
    int i;

    for (i = 0; message[i] != '\0'; i++)
        mac = (mac * 31) + message[i];

    for (i = 0; key[i] != '\0'; i++)
        mac = (mac * 31) + key[i];

    return mac;
}

int main()
{
    char message[100], key[100], verify[100];
    unsigned long mac, verifyMac;

    ;

    printf("Enter the message: ");
    fgets(message, sizeof(message), stdin);
    message[strcspn(message, "\n")] = '\0';

    printf("Enter the secret key: ");
    fgets(key, sizeof(key), stdin);
    key[strcspn(key, "\n")] = '\0';

    mac = generateMAC(message, key);

    printf("\nGenerated MAC: %lu\n", mac);

    printf("\nEnter the message for verification: ");
    fgets(verify, sizeof(verify), stdin);
    verify[strcspn(verify, "\n")] = '\0';

    verifyMac = generateMAC(verify, key);

    printf("Computed MAC: %lu\n", verifyMac);

    if (mac == verifyMac)
        printf("Message is authentic and unchanged.\n");
    else
        printf("Message is NOT authentic or has been modified.\n");

    return 0;
}


## Output:
<img width="722" height="382" alt="image" src="https://github.com/user-attachments/assets/20e18c6f-0027-4415-91c2-66b7d724156b" />


## Result:
The program is executed successfully.
