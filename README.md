# micro-diff-up
A differential based updater for microprocessors and microcontrollers.
## Working Theory
The premise of this updater is to create a differential Intel HEX format image maintaining addressing offsets, then applying the changes at corresponding memory locations.
1. Retrive the current microcontroller software version from the microcontroller with its checksum
2. Validate the checksum and the current microcontroller software version using a lookup table.
3. Determine what the new microcontroller software version should be.
4. Compare the current microcontroller software version with the new microcontroller software version to be installed.
5. Generate a new Intel HEX file, retaining address offsets and programming content that differs.
6. Generate a checksum for the Intel HEX file.
7. Optionally, cryptographically sign the Intel HEX file checksum for microcontroller verification.
6. Optionally, compress the generated Intel HEX file.
7. Transfer the new microcontroller software version checksum in addition to the generated Intel HEX file with checksum to the microcontroller.
8. The microcontroller then optionally decompresses the generated Intel HEX file.
9. The microcontroller then optionally verifies the generated Intel HEX file checksum.
10. The microcontroller allocates a buffer of microcontroller erase size.
11. The microcontroller reads data from memory locations specified by the Intel Hex memory locations of microcontroller erase size to the allocated buffer.
12. The microcontroller applies changes as indicated in the generated Intel HEX file at the offset in the allocated buffer.
13. The allocated buffer is then written back to the microcontroller at the original address.
14. The process is continued until the generated HEX file is completely processed.
15. After the entire generated HEX file is processed, the start address to final address is checksummed.
16. The checksum is then compared to the new microcontroller software version checksum.
17. The update process is then complete.
