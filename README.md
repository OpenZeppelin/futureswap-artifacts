### Compiled bytecode of audited contracts

Following a special request from the FutureSwap team, we have compiled the audited Solidity files and reference in this report the resulting bytecode. The compilation settings were:

- Compiler version `0.5.17+commit.d19bba13.Linux.g++` with SHA256 checksum `c35ce7a4d3ffa5747c178b1e24c8541b2e5d8a82c1db3719eb4433a1f19e16f3`
- Optimizer: enabled
- Number of runs: 100
- EVM Version: Istanbul

We have not verified that the audited version of the code matches the deployed system on mainnet. To reduce the need to trust third parties, we encourage users to conduct such verification by themselves when the system is open-sourced, using their most trusted set of tools and infrastructure of choice to read information from the Ethereum blockchain. Users and developers willing to conduct such process must be aware of the following caveats.

Verifying deployed bytecode is not sufficient to ensure the correct behavior of a smart contract system - creation code and initialization parameters should be understood and verified as well.

When compiling contracts without linking libraries, the Solidity compiler inserts placeholders for the addresses of libraries in the bytecode. Therefore, to obtain the executable bytecode, one needs to link contracts to the addresses of deployed libraries in mainnet (read more about it in [the Solidity documentation](https://docs.soliditylang.org/en/v0.5.17/using-the-compiler.html)). We are including the compiled bytecode with both unlinked and linked libraries. The addresses used for linking were provided privately by the FutureSwap team.

Even in the case where the FutureSwap team has deployed the exact latest audited version of the in-scope contracts (corresponding to commit `be8d371a40f21b863ec7a99445bad92e6c8d17f1` of the [`fs-core` repository](https://github.com/futureswap/fs-core/) and commmit `6c0dd5e65bef41f13043a380f6a875315b25bcd7` of the [`fs_token` repository](https://github.com/futureswap/fs_token/)), there might be expected differences between the actual deployed code in mainnet and the compiled bytecode referenced in this report. In particular, one should be aware that:

- Due to [Solidity's call protection for libraries](https://docs.soliditylang.org/en/v0.5.17/contracts.html#call-protection-for-libraries), bytecode of libraries is changed at deploy time. In other words, the compiled bytecode for a library can be different to what is actually deployed on chain. In practice, this translates to the fact that the bytecode of libraries we reference will have 20-bytes-long sequences of zeros instead of the actual address of the library.
- From the [Solidity documentation](https://docs.soliditylang.org/en/v0.5.17/metadata.html), since the resulting bytecode of the compiled contracts contains the metadata hash, any change to the metadata results in a change of the bytecode. This includes changes to a filename or path, and since the metadata includes a hash of all the sources used, a single whitespace change results in different metadata, and different bytecode. In practice, this translates to the fact that the bytecode of libraries and contracts we reference may have a different metadata hash attached at the end of the executable bytecode, as the absolute paths of the compiled files inevitably differs.

The audited contracts' creation and runtime bytecode can be found in this repository.
