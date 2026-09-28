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

## The witness

Each `builds/<commit>.json` is signed with a key that exists only on the machine that deploys, and the signature is
entered in [Sigstore's Rekor](https://docs.sigstore.dev/logging/overview/), a public append-only transparency log
run by the OpenSSF. `builds/<commit>.bundle.json` holds the signature and the Rekor entry; `latest.json` names the
log index. Rekor is the part that is not us: its entry proves this exact record existed at that time and has not
changed since. To verify:

```
cosign verify-blob --key cosign.pub --bundle builds/<commit>.bundle.json builds/<commit>.json
```

`cosign.pub` in this repository is the public half of that key.
