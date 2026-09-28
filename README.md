# Build fingerprints

Every deploy of the private line (currently at https://comm.drye.dev) writes one file here: the SHA-256 of every
file of code the app runs, as served, with the commit it was built from and the time it went live.

- `latest.json` is what is live now.
- `builds/<commit>.json` is every deploy, kept forever.

The live server publishes the same information at `https://comm.drye.dev/api/build`. The status section of
https://comm.drye.dev/about/ downloads every file, hashes it on your device, and compares it with both. This
repository is the half that does not come from the server: its history is public, and anyone can keep a copy.

It is written by the same people who run the server, so it is a public record, not an independent witness. What it
gives you is a permanent, timestamped statement of what each build was supposed to be, made before you asked.
