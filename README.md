# G3-TunR

Browser tool for the Segway/Ninebot MAX G3 over Web Bluetooth. One file, no build, no deps, no backend.

## What is solid vs. not
Solid: AES-128-CBC framing with CRC16-CCITT, plaintext serial read → key derivation → encrypted session, chunked writes, notify parsing, backup/restore, config persistence.
Not solid: the G3 register IDs. Defaults are lineage guesses (`0x60/0x61/0x62` speed, `0x7C` cruise, `0x7B` KERS, `0x7D` tail light, `0x7E` zero start). Fix them in Config — the map is JSON, no code edit needed.

## Finding real registers
1. Console → Read range `0x00`–`0xFF` → copy the output.
2. Change exactly one setting in the official app.
3. Sweep again and diff. The changed byte is the register.
4. Add it to the map.

## Limits
- No firmware flashing (ST-Link territory).
- Serial write = region change; works on stock 1.6.3, patched on 1.6.4+.
- Not yet validated on live hardware.

MIT
