# Talkza security and privacy

## Design
- **End-to-end encryption.** Each message gets its own random key and is sealed with an authenticated cipher (XSalsa20-Poly1305). That message key is then locked separately for each member of the chat with X25519 public-key encryption. The server stores only the scrambled message and the locked keys.
- **Keys stay on the device.** The private key is created on the device and kept in secure storage (hardware-backed on phones). The server never receives it.
- **Recovery phrase.** The user can lock a backup of their key with a recovery phrase they control. Without the phrase, nobody, including the Talkza team, can restore it.
- **No phone number.** Accounts use a username and password only.
- **Device list.** Users see every signed-in device, can remove one, and are warned when a new device signs in.
- **Safety defaults.** Strangers land in a requests inbox. New contacts get a scam check. Users can lock the app and single chats with a PIN or biometrics.
- **Database protection.** Row-level security limits each user to their own chats and data.
- **Business deals.** A restaurant's deals are encrypted on the owner's device like any other message. The Talkza server cannot send them for the owner.

## Evidence
See [test-results](test-results/README.md), test T6, for a check that stored messages are scrambled.

## Known limits and open items
- The encryption design has **not had an independent security audit**. Screenshots cannot prove end-to-end encryption; an audit can.
- If a device's key differs from the account's key, messages sent from it could not be opened. A fix that keeps every device's key on record was deployed on 2026-10-30. A retest is pending (T8).
- Database permissions are reviewed before each release.
- Messages already sent from a device with a different key stay unreadable until that device opens the latest version.
