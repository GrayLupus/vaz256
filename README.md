# VAZ256™

Verified Abbreviated Zeta 256 bits (VAZ256) - is a post-quantum cryptographic digital signature scheme that combines Dilithium5 and SHAKE256 for secure digital signatures and efficient compressed 32-byte public keys.


## API Overview

```rust
use vaz256::{keygen, sign, verify, SecretKey, PublicKey, Signature};

// Generate a random keypair
let (sk, pk) = keygen().unwrap();

// Or create a SecretKey from known bytes/hex
let sk = SecretKey::from_hex("0000000000000000000000000000000000000000000000000000000000000000").unwrap();
let sk = SecretKey::from_bytes(&[0u8; 32]).unwrap();

// Derive the PublicKey from a SecretKey (new in v2.0)
let pk = PublicKey::from_secret_key(&sk).unwrap();

// Convert keys to/from raw bytes (new in v2.0)
let sk_bytes = sk.to_bytes();
let pk_bytes = pk.to_bytes();
let sk2 = SecretKey::from_bytes(&sk_bytes).unwrap();
let pk2 = PublicKey::from_bytes(&pk_bytes).unwrap();

// Hex serialization (existing API)
let sk_hex = sk.to_hex();
let pk_hex = pk.to_hex();
let sk3 = SecretKey::from_hex(&sk_hex).unwrap();
let pk3 = PublicKey::from_hex(&pk_hex).unwrap();

// Sign and verify
let msg = b"hello world";
let sig = sign(msg, &sk).unwrap();
assert!(verify(msg, &sig, &pk).is_ok());

// Signature serialization
let sig_bytes = sig.to_bytes();
let sig_hex = sig.to_hex();
let sig2 = Signature::from_bytes(&sig_bytes).unwrap();
let sig3 = Signature::from_hex(&sig_hex).unwrap();
```

## Acknowledgments and Third-Party Code

This project includes modified code from the following open-source projects:

- Parts of CRYSTALS-Dilithium Rust implementation by Quantum Blockchains
  - Original Repository: https://github.com/Quantum-Blockchains/dilithium
  - Original License: GPL-3.0
  - Which itself was ported from the reference implementation at: https://github.com/pq-crystals/dilithium

VAZ256™ is built upon these foundations but includes significant modifications and original work. The name "VAZ256" is a trademark of Fran Luis Vazquez Alonso.

## Features
- Hybrid post-quantum security based on Dilithium5
- Compact 32-byte public keys using SHAKE256
- Pure Rust implementation
- Zero-dependency core functionality
- Comprehensive test suite and benchmarks

## Security Considerations - **Use at Your Own Risk**
- This implementation is currently in development and has not been audited
- Use in production systems is not recommended until formal security analysis is complete

## Performance
Benchmark results and performance characteristics using RockChip RK3562 2.0 GHz.
- Key generation time ~ 1.33 ms
- Signing time ~ 5.00 ms
- Signature verification time ~ 1.01 ms

## Documentation
Full documentation is available at [docs.rs/vaz256](https://docs.rs/vaz256)

## Contributing
Contributions are welcome! Please feel free to submit a Pull Request.

## Copyright and License

Copyright (C) 2025 Fran Luis Vazquez Alonso

VAZ256™ is a trademark of Fran Luis Vazquez Alonso. The name "VAZ256" and "Verified Abbreviated Zeta" may not be used for derivative works without express permission.

This program is free software: you can redistribute it and/or modify
it under the terms of the GNU General Public License as published by
the Free Software Foundation, either version 3 of the License, or
(at your option) any later version.

### Contact Information
- Email: cybervazquez@protonmail.com

The complete text of the GNU General Public License can be found in the LICENSE file
in this repository or at <https://www.gnu.org/licenses/>.