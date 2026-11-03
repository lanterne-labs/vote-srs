# vote-srs

**The public parameters the tartuffe.me vote app proves ballots with**, for every poll. This is Barretenberg's structured reference string (SRS), as Aztec publishes it. Voters' browsers fetch it through jsDelivr, at a pinned commit.

| File | Bytes | SHA-256 | What |
|---|---|---|---|
| `g1_compressed.dat` | 4,194,304 | `fad8203ae1fd103658d4bb33b2b4cf126a28352b5de4684737cff23cc15fb94b` | the first 2^17 G1 points (32 B each) of `https://crs.aztec-cdn.foundation/g1_compressed.dat` |
| `g2.dat` | 128 | `01797bfc4de5a96f0e516a9ea4537d18786dc30cb991aca4274c95822b69c32f` | `https://crs.aztec-cdn.foundation/g2.dat`, whole |

Every ballot circuit fits in 2^17 points. A larger circuit in a later poll would need a new file here, under a new commit.

The browser checks each file's SHA-256 before it uses the file, and refuses it on a mismatch. A host that serves other bytes therefore cannot change a proof. To check the files yourself:

```sh
curl -s -r 0-4194303 https://crs.aztec-cdn.foundation/g1_compressed.dat | shasum -a 256
curl -s https://crs.aztec-cdn.foundation/g2.dat | shasum -a 256
```

The protocol and the prover are in [lanterne-labs/isoloir](https://github.com/lanterne-labs/isoloir). The app is in [lanterne-labs.github.io](https://github.com/lanterne-labs/lanterne-labs.github.io). Contact: lanternelabs@proton.me
