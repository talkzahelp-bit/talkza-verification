# Talkza architecture (high level)

| Layer | Technology |
|---|---|
| App | One codebase in Expo / React Native, running as a web app and an Android app |
| Backend | Supabase: Postgres database, sign-in, realtime updates, file storage and edge functions |
| Hosting | Web app on Vercel at https://talkza-beta.vercel.app |
| Encryption | TweetNaCl (X25519 and XSalsa20-Poly1305), done on the user's device |
| Calls | Peer-to-peer WebRTC audio and video |
| Push | Firebase Cloud Messaging for Android (not verified) |

## How a message travels
1. The sender's device encrypts the message and locks its key for each member.
2. The scrambled message is saved in the database and delivered in realtime.
3. Each member's device unlocks the key with its own private key and reads the message.

## Business connection
A restaurant on Hungry Hours connects once with a one-time token. Hungry Hours then sends its menu and deals to a Talkza endpoint. The owner's own app turns each deal into an encrypted message card and sends it.

No source code is published in this repository.
