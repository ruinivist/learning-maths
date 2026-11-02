# Message Delivery

Anything you don't encrypt is lost. You want to share a message with someone, but neither of you knows the other's key. What can you do?

## Solution

The problem in the book is framed differently, but this version is more apt.

The key idea is Shamir's three-pass protocol, which lets two people transfer a message without sharing their secret keys.

### How it works mathematically

Let:

- $M$: Original message
- $E_A$: Your encryption
- $E_B$: Your colleague's encryption
- $D_A,D_B$: Corresponding decryption operations

| Step               | Operation           | Message           |
| ------------------ | ------------------- | ----------------- |
| 1. You → Colleague | Encrypt with A      | $E_A(M)$       |
| 2. Colleague → You | Add encryption B    | $E_B(E_A(M))$  |
| 3. You → Colleague | Remove encryption A | $E_B(M)$       |
| 4. Colleague       | Remove encryption B | $M$            |

For the protocol to work, the encryption operations must commute, so you can remove A while B remains.
