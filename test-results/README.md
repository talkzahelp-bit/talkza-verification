# Test results

App version: web builds deployed on 2026-10-30 (package version 1.0.0). Tested on a local copy of the app and on the live site. Test accounts held made-up data and were deleted afterwards.

| ID | Feature | What was tested | Expected | Actual | Result | Date |
|---|---|---|---|---|---|---|
| T1 | Username sign-up | Create an account with a username, password and display name; sign in | Account created, signed in, chat list shown | As expected | Pass | 2026-10-30 |
| T2 | One-to-one chat | Open a chat from the chat list on a new account | Chat opens with the contact's name and an empty message list | As expected | Pass | 2026-10-30 |
| T3 | Chat opening on the owner's phone | Owner opened a chat that earlier showed a blank screen | Name and messages show | Worked on retry; the original blank screen was not reproduced | Pass, cause unconfirmed | 2026-10-30 |
| T4 | Hungry Hours connection | Endpoint called with no token, a fake token and a GET request | 401, 401 and 405 | 401 "missing or invalid token", 401 "unknown or revoked token", 405 | Pass | 2026-10 (earlier session) |
| T5 | Deal card | A deal from Hungry Hours sent to a chat | Card with logo, offer, "% OFF" and "View deal" button | Owner screenshot showed two cards with logo, 20% OFF and View deal | Pass | 2026-10-30 |
| T6 | Stored messages are scrambled | Read recent message records in the database | Only scrambled text and locked keys; no readable text | Records held only a nonce, ciphertext and per-member locked keys | Pass | 2026-10-30 |
| T7 | Type check and deploy | Run the type check; deploy to production after each change | No errors; site ready | No errors; site ready each time | Pass | 2026-10-30 |
| T8 | Messages from a device with a different key | After the key-history fix, reopen the chat that showed "Can't be opened" | Messages open | Not yet retested | Pending | |
| T9 | Deal posted to Status | Deal sent with "Also post deals to my Status" on | A Status update appears | Not yet confirmed | Pending | |
| T10 | Message yourself, private contact names | Open "Message yourself"; set a private name | Own chat opens; name shows only for the user | Not yet tested end to end | Pending | |

## Known failures
- Before 2026-10-30, some deal messages showed "Can't be opened on this device" because the sending device had a different key. A fix was deployed; see T8.
- On 2026-10-30, deals did not send automatically after three had gone out, because of a daily limit. The limit was removed and deployed on 2026-10-30.
