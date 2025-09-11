# Release Notes

## v0.10.5

### cashc compiler

- 🐛 Fix bug in new TypeScript typings for artifact.

## v0.10.4

### cashc compiler

- 🐛 Fix bug in new --format ts option.

## v0.10.3

### cashc compiler

- ✨ Add --format ts option to cashc CLI to generate TypeScript typings for the artifact.
CashScript SDK
- ✨ Add automatic TypeScript typings for Contract class when artifact is generated using the cashc CLI with the --format ts option.

## v0.10.2

### cashc compiler

- ✨ Add support for using underscores in numeric literals to improve readability, e.g. 1_000_000.
- ✨ Add support for using scientific notation in numeric literals, e.g. 1e6 or 1E6.

### CashScript SDK

- 🐛 Fix fee calculation when using SignatureAlgorithm.ECDSA.
- 🛠️ Clean up dependencies.

## v0.10.1

### CashScript SDK

- 🐛 Fix bug with MockNetworkProvider returning the wrong Network type (now returns Network.MOCKNET / "mocknet").
- 🐛 Fix bug in debug tooling where incorrect placeholder keys were used when evaluating transactions with P2PKH inputs.

## v0.10.0

In this version we added proper debugging support for transactions and integration with the BitAuth IDE.

Thanks mainnet_pat for the initiative and significant contributions!

### cashc compiler

- ✨ Add console.log() statements for debugging.
- ✨ Extend require() statements to allow custom error messages for debugging.
- 🛠️ Update artifact format to allow for new debugging features.
- 🛠️ Update dependencies to new major versions.
CashScript SDK
- ✨ Add support for transaction evaluation and debugging using libauth templates.
transaction.debug() & transaction.bitauthUri()
Output BitAuth IDE URI for debugging when transaction is rejected.
- ✨ Add MockNetworkProvider to simulate network interaction for debugging and testing.
Add randomUtxo(), randomToken() and randomNft() functions to generate dummy UTXOs for testing.
- ✨ Add CashScript Jest utilities for automated testing.
expect(transaction).toLog(message)
expect(transaction).toFailRequire()
expect(transaction).toFailRequireWith(message)
- 🐛 Fix bug with type exports.
- 🛠️ Update visibility of several classes.
Make artifact, networkProvider, addressType and encodedConstructorArgs public on Contract class.
Make contract, abiFunction, encodedFunctionArgs, inputs and outputs public on Transaction class.
Make networkProvider, inputs and outputs public on TransactionBuilder class.
Make privateKey public on SignatureTemplate class and add getSignatureAlgorithm() method.
- 🛠️ Improve some error messages.
- 🛠️ Add new FailedRequireError, FailedTransactionEvaluationError and FailedTransactionError classes.
- 💥 BREAKING: Remove exported transaction error Reason enum + FailedTimeCheckError and FailedSigCheckError classes in favour of the new error classes.
- 💥 BREAKING: Remove all deprecated references to meep including meep strings from errors and transaction.meep().
- 💥 BREAKING: Separate the Argument type into FunctionArgument and ConstructorArgument and rename encodeArgument to encodeFunctionArgument.

## v0.9.3

### cashc compiler

- 🛠️ Migrate from antlr4ts to ANTLR's official TypeScript target to remove circular dependency issues.

## v0.9.2

### CashScript SDK

- 🐛 Fix bug where UTXOs would be needlessly retrieved from the network during build() calls.
- 🐛 Fix off-by-one fee calculation error with transactions that have many outputs.
- 🐛 Fix bug where no error was thrown when invalid NFT commitment or token category were provided.
- 🛠️ Export all interfaces from CashScript's interfaces.ts.
- 🛠️ Merge duplicate code between Transaction.ts and TransactionBuilder.ts.

## v0.9.1

### CashScript SDK

- 🐛 Fix TransactionBuilder export bug.

## v0.9.0

### CashScript SDK

- ✨ Add new advanced TransactionBuilder class that allows combining UTXOs from multiple different smart contracts and P2PKH UTXOs in a single transaction.
- 🛠️ Deprecate all meep functionality. Meep has been unmaintained for years and does not support many new CashScript features. Meep functionality will be removed in a future release.
https://x.com/CashScriptBCH/status/1713928572677583023

## v0.8.2

### CashScript SDK

- 🐛 Fix bug with Vite build.
- ✨ Expose ElectrumNetworkProvider#performRequest to allow raw Electrum requests if needed.

## v0.8.1

### CashScript SDK

- 🐛 Fix bug where a different property order of NFT inputs/outputs would cause errors.

## v0.8.0

⚠️ From v0.8.0 onwards, CashScript is a Pure ESM package. This means that you can no longer use require() to import cashscript or cashc.

This release also contains several breaking changes, please refer to the migration notes for more information.

### cashc compiler

- ✨ Add support for the new CashTokens introspection functionality (tokenCategory,nftCommitmentand tokenAmountfor both in- and outputs).
- ✨ Add LockingBytecodeP2SH32 to generate the new P2SH32 standard locking script.
- 🐛 Fix optimisation bug that caused OP_0NOTEQUAL to be applied to non-integer values.
- 💥 BREAKING: Move to Pure ESM.
- 💥 BREAKING: Rename LockingBytecodeP2SH to LockingBytecodeP2SH20 - but it is recommended to change over to the new P2SH32 for security reasons.

### CashScript SDK

- ✨ Add support for CashTokens.
.to() now takes a token parameter that can be used to send CashTokens.
UTXOs that are retrieved with contract.getUtxos() include a token field if they are token UTXOs.
UTXOs that are passed into .from() can also include this token field to send tokens.
Add .withoutTokenChange() to disable automatic token change outputs.
Note that only the ElectrumNetworkProvider supports CashTokens at this time.
Note that NFTs do not support automatic UTXO selection
- ✨ Add contract.tokenAddress to get the token-enabled address of a contract.
- ✨ Add fromP2PKH() to add P2PKH inputs to a smart contract transaction.
Note: this was in the SDK before as experimentalFromP2PKH(). It has now been released as an official feature.
- 💥 BREAKING: Move to Pure ESM.
- 💥 BREAKING: Remove "testnet" & "staging" network options.
- 💥 BREAKING: contract.address returns p2sh32 address by default, this can be configured to be p2sh20 on contract initialization.
- 💥 BREAKING: Move the configuration of the network provider to an options object on contract initialization.
- 💥 BREAKING: Use bigint rather than number for all instances of "script numbers" (e.g. function arguments) and satoshi amounts.
- 💥 BREAKING: Replace contract.getRedeemScriptHex() with contract.bytecode.
- 💥 BREAKING: Remove BitboxNetworkProvider.
- 💥 BREAKING: All signature templates use SIGHASH_ALL | SIGHASH_UTXOS now, this new default can be overwritten in the constructor of the SignatureTemplate.
https://x.com/CashScriptBCH/status/1662092546372255744

## v0.7.5

### CashScript SDK

- 🐛 Fix a bug with chipnet connection

## v0.7.4

### cashc compiler

- 🛠️ Internal refactoring
CashScript SDK
- 🐛 Fix a bug with ESM exports

## v0.7.3

### CashScript SDK

- ✨ Add "chipnet" network option to ElectrumNetworkProvider, used to connect to the May 2023 testnet.
- 🛠️ Renamed network options "testnet" & "staging" to "testnet3" and "testnet4" respectively. Old options will be removed in a future release.

## v0.7.2

### cashc compiler

- 🐛 Fix bug where contracts using checkMultiSig() were unspendable.
CashScript SDK
- ✨ Add signatureAlgorithm parameter to SignatureTemplate to allow ECDSA signatures.

## v0.7.1

@cashscript/utils
🐛 Fix bug where 64bit integers could not be decoded.

## v0.7.0

### cashc compiler

- ✨ Add destructuring assignments, e.g. bytes2 left, bytes1 right = 0x123456.split(2)
- ✨ Add constant keyword, e.g. int constant x = 10;
- ✨ Add multiplication, e.g. int x = 5 * 5
- ✨ Add native introspection/covenants
- 💥 BREAKING: Remove all old introspection/covenant functionality (tx.version, tx.hashPrevouts, tx.hashSequence, tx.outpoint, tx.bytecode, tx.value, tx.sequence, tx.hashOutputs, tx.locktime, tx.hashtype, OutputP2PKH, OutputP2SH, OutputNullData)
See the migration notes for details on migrating from the old introspection to the new native introspection methods.
- 💥 BREAKING: Remove sig to datasig casting since this was only useful for old covenants
- 🐛 Fix ESM build

### CashScript SDK

- ✨ Add "staging" network option to ElectrumNetworkProvider, used to connect to the May 2022 testnet
- 🛠️ Deprecate old introspection/covenant functionality. You can still use pre-0.7 contracts with the new SDK, but this support will be removed in a future release.
- 💥 BREAKING: arguments of type datasig must be 64 bytes in length, effectively enforcing Schnorr
- 🐛 Fix ESM build
- 🐛 Small fixes
https://x.com/RoscoKalis/status/1529072055756414976

## v0.6.5

### cashc compiler

🐛 Fix cashc version

## v0.6.4

### cashc compiler

✨ Add byte type alias for bytes1

## v0.6.3

- 🛠️ Use ES2015 for the "module" output for better compatibility

## v0.6.2

### CashScript SDK

- 🐛 Fix typing issue with BitcoinRpcNetworkProvider

## v0.6.1

### CashScript SDK

- 🐛 Fix bug with incorrect fee calculation when providing custom fee per byte

## v0.6.0

### cashc compiler

- ✨ Add date literal (gets converted to int timestamp)
- 🛠️ Update ParseError messages
- 🐛 The final statement in a contract now MUST be a require statement (in all branches)
- 🐛 Empty contracts and functions are now considered invalid
- 🐛 Fix bug where certain covenants could become unspendable due to incorrect bytesize calculation
- 💥 BREAKING: Covenants using tx.bytecode now include a placeholder OP_NOP that gets replaced when constructor arguments are provided in the CashScript SDK. If you're not using the CashScript SDK, refer to the replaceBytecodeNop() function to see the steps required to do so manually.
- 💥 BREAKING: Remove --args parameter from the CLI, since this is too error prone with the recent changes in mind
- 💥 BREAKING: Restructure exports

### CashScript SDK

- ✨ Add BitcoinRpcNetworkProvider that connects to a BCH node RPC
- 💥 BREAKING: Remove dependency on cashc and remove CashCompiler export
https://x.com/RoscoKalis/status/1371896417443282956

## v0.5.7

### cashc compiler

- 🐛 Better error reporting for parsing/lexing errors

## v0.5.6

### cashc compiler

- 🐛 Make compiler fail early when encountering lexing/parsing errors, rather than performing error recovery
- 🐛 Allow empty hex literals (i.e. 0x)

## v0.5.5

### CashScript SDK

- ✨ Add 'regtest' as a possible network for NetworkProviders.

### v0.5.4

- 📦 Add dual build system (CommonJS and ES Modules) to accommodate tree-shaking.

## v0.5.3

### CashScript SDK

- ✨ Add getRedeemScriptHex() function to the Contract class.
- 🐛 Fix a bug where transaction locktime could not specifically be set to 0.
- 🐛 Fix a bug where signature buffers were not checked for size.

## v0.5.2

### cashc compiler

- 🐛 Fix a bug where an incorrect error message was displayed in Firefox when an incompatible pragma version was used.

## v0.5.1

### CashScript SDK

- ✨ The .send() function now returns a TransactionDetails object. This extends the libauth Transaction with added txid and hex fields.
Because it extends the previous return type, this is backwards compatible.
Since this now returns the transaction hex as a field, using .send(true) to return the transaction hex is deprecated and will be removed in a future release.
- 🐛 Improve reliability of the ElectrumNetworkProvider when sending multiple concurrent requests.
https://x.com/RoscoKalis/status/1301521593399685121

## v0.5.0

### CashScript SDK

CashScript used to be very tightly coupled with BITBOX. This proved to be problematic after maintenance for BITBOX was stopped. The main objective of this update is to allow CashScript to be used with many different BCH libraries.

- ✨ Add withoutChange() function to disable change outputs for a transaction.
- ✨ SignatureTemplate can now be used with BITBOX keypairs, bitcore-lib-cash private keys, WIF strings, and raw private key buffers, rather than only BITBOX.
- 💥 Remove Sig alias for SignatureTemplate that was deprecated in v0.4.1.
- 💥 BREAKING: Refactor contract instantiation flow
A contract is now instantiated by providing a compiled artifact, constructor arguments and an optional network provider.
Anyone can implement the NetworkProvider interface to create a custom provider. The CashScript SDK offers three providers out of the box: one based on electrum-cash (default), one based on FullStack.cash' infrastructure, and one based on BITBOX. See the NetworkProvider docs for details.
See the migration notes for details on migrating from the old contract instantiation flow.
- 💥 BREAKING: Remove the artifacts 'networks' field and .deployed() functionality, This proved to be confusing and is better suited to be handled outside of the CashScript SDK.
- 💥 BREAKING: .send() now returns a libauth Transaction instead of a BITBOX Transaction object. Alternatively a raw flag can be passed into the function to return a raw hex string.
- 🛠️ Removed BITBOX as a dependency in favour of libauth for utility functions.
https://x.com/RoscoKalis/status/1298645699559596033

## v0.4.4

### cashc compiler

- 🐛 Fix a bug where covenants would not always get verified correctly when the first require(checkSig(...)) statement was inside a branch.

## v0.4.3

### cashc compiler

- 🐎 Add compiler optimisations.

## v0.4.2

Re-add README files to NPM that were accidentally removed in the v0.4.0 release.

## v0.4.1

### cashc compiler

- 🐎 Add optimisations to bitwise operators.
- 🐚 New CLI arguments.
Add --opcount|-c flag that displays the number of opcodes in the compiled bytecode.
Add --size|-s flag that displays the size in bytes of the compiled bytecode.
- 🔣 Add trailing comma support.

### CashScript SDK

- 📛 Rename Sig to SignatureTemplate to better convey its meaning.
Sig still exists for backward compatibility, but is deprecated and will be removed in a later release.
https://x.com/RoscoKalis/status/1267440143624884227

## v0.4.0

### cashc compiler

- ✨ Add .reverse() member function to bytes and string types.
- ✨ Add bitwise operators &, ^, |.
- ✨ Allow casting int to variable size bytes based on size parameter.
- 💥 BREAKING: Casting from int to unbounded bytes type now does not perform OP_NUM2BIN. Instead it is a purely semantic cast to signal that an integer value should be treated as a bytes value.
- 🏇 Compiler optimisations.
Use NUMEQUALVERIFY for the final function in a contract.
Only drop the final VERIFY if the remaining stack size is less than 5.
Pre-calculate OutputNullData argument size.
- 🐛 Fix a bug where return type of sha1 was incorrectly marked as bytes32.
- 🐛 Data.decodeBool only treated numerical zero as false, now any zero-representation is considered false (e.g. 0x0000, -0, ...).

### CashScript SDK

- ✨ Add ability to provide hardcoded inputs to the transaction rather than use CashScript's coin selection.
- 💥 BREAKING: Refactor the transaction flow to a fluent API
Remove the TxOptions argument and other arguments to the Transaction send() function.
Instead these parameters are passed in through fluent functions from(), to(), withOpReturn(), withAge(), withTime(), withHardcodedFee(), withFeePerByte() and withMinChange().
After specifying at least one output with either to() or withOpReturn()the transaction is ready. From here the transaction can be sent to the network with the send() function, the transaction hex can be returned with the build() function, or the meep debugging command can be returned with the meep() function.
- 💥 Remove Contract.fromCashFile() and Contract.fromArtifact() which were deprecated in favour or Contract.compile() and Contract.import() in v0.2.2.
Migration
This update contains several breaking changes. See the migration notes for a full migration guide.

https://x.com/RoscoKalis/status/1264921879346917376

## v0.3.3

### cashc compiler

- 🐛 Fix bug where variables could not reliably be used inside OutputNullData instantiation.
https://x.com/RoscoKalis/status/1224389493769342979

## v0.3.2

### cashc compiler

- ✨ Add OutputNullData(bytes[] chunks), an output type to enforce OP_RETURN outputs.
- 🐚 CLI improvements
The --output|-o flag is now optional, if it is omitted or manually set to -, the artifact will be written to stdout rather than a file.
Add --asm|-A flag that outputs only Script in ASM format instead of a full JSON artifact.
Add --hex|-h flag that outputs only Script in hex format instead of a full JSON artifact.
Add --args|-a flag that allows you to specify constructor arguments that are added to the generated bytecode.
- ⚠️ The CLI does not perform type checking on these arguments, so it is recommended to use the CashScript SDK for type safety.
- 🐛 Fix a compilation bug that allowed compilation of "unverified covenants" (#56).
- 🐛 Fix a compilation bug that allowed compilation of OutputP2PKH(...) without new keyword (#57).

### CashScript SDK

- 🌐 Browser support! You can now use CashScript inside web projects. Filesystem-based functionality such as compilation from file are not supported due to the nature of web, so CashScript files have to be read in a different way (e.g. Fetch API) and then passed into the CashScript SDK.
- 👛 Add minChange to transaction options. If this minChange is not reached, the change will be added to the transaction fee instead.
https://x.com/RoscoKalis/status/1223280232343515136

## v0.3.1

### cashc compiler

- ⚠️ Add warnings when a contract exceeds 201 opcodes or 520 bytes.
- 🐛 Fix a bug where an incorrect number of items were dropped from the stack after execution of a branch.
CashScript SDK
- ✨ Improve error handling.
Further specified FailedTransactionError into FailedRequireError, FailedSigCheckError, FailedTimeCheckError and a general fallback FailedTransactionError.
Add Reason enum with all possible reasons for a Script failure - can be used to catch specific errors.
- 🔍 Add instance.opcount and instance.bytesize fields to all contract instances.
- 🐛 Fix a bug where the size of a preimage was not accounted for in fee calculation for covenants.
https://x.com/RoscoKalis/status/1217101473743544320

## v0.3.0

### cashc compiler

- ✨ Covenants abstraction! All individual preimage fields can be accessed without manual decoding, passing, and verification.
Available fields: tx.version, tx.hashPrevouts, tx.hashSequence, tx.outpoint, tx.bytecode, tx.value, tx.sequence, tx.hashOutputs, tx.locktime, tx.hashtype.
When any of these fields is used inside a function, this function is marked covenant: true, and requires a preimage as parameter (automatically passed by CashScript SDK).
The correct fields are efficiently cut out of the preimage and made available.
The first occurrence of require(checkSig(sig, pubkey)); is identified, and preimage verification is inserted using the same sig/pubkey. Important: if you have multiple checkSig statements, keep in mind that the first will be used for verification.
Automatically cuts off VarInt from scriptCode, so tx.bytecode contains the actual contract bytecode.
- ✨ Output instantiation! Automatically construct output formats for covenant transactions.
new OutputP2PKH(bytes8 amount, bytes20 pkh)
new OutputP2SH(bytes8 amount, bytes20 scriptHash)
- 🐛 Fix bug with invalid output when the final statement in a contract is an if-statement.
CashScript SDK
- ✨ Add fee option to TransactionOptions. This allows you to specify a hardcoded fee for your transaction.
- ✨ Automatically pass in sighash preimage into covenant functions. Important: uses the hashtype of the first signature in the parameters for generation of this preimage.
- 💫 Better fee estimation for transactions with many inputs.
https://x.com/RoscoKalis/status/1204765863062188033

## v0.2.3

### cashc compiler

- 🐛 Fix a bug where unequal bytes types (e.g. bytes3 & bytes8) could not be concatenated together, as they were considered different types.
https://x.com/RoscoKalis/status/1202220857566908416

## v0.2.2

### CashScript SDK

- 🐛 Remove minimaldata encoding in OP_RETURN outputs that caused incompatibility with SLP.
- 📛 Renamed Contract.fromCashFile to Contract.compile.
The new function allows to pass in a path to a .cash file, or a string of the contract source code.
Contract.fromCashFile still exists for backward compatibility, but is deprecated and will be removed in a later release.
- 📛 Renamed Contract.fromArtifact to Contract.import.
The new function allows to pass in a path to a .json artifact file, or a JSON object of the artifact.
Contract.fromArtifact still exists for backward compatibility, but is deprecated and will be removed in a later release.
- 🛠️ instance.export's file argument is now optional.
If it is provided, the artifact is written to the file, if not, it is returned as an object.
https://x.com/RoscoKalis/status/1192900277105389568

## v0.2.1

### cashc compiler

- ✨ Support bytes types with bounded size, e.g. bytes1, bytes13, bytes32.
- 🐛 Fix bug in bytecode optimisation
CashScript SDK
- ✨ Support bytes types with bounded size, e.g. bytes1, bytes13, bytes32.
- 🐦 Automatically output meep command on failed transaction error.
- 🔨 Make the hashtype parameter in signature placeholders optional.
https://x.com/RoscoKalis/status/1186554051720167424

## v0.2.0

### cashc compiler

- 🐎 Implement compiler optimisations
For the final use of a variable, it is retrieved with OP_ROLL rather than OP_PICK. This removes the need to clean the stack at the end of a contract.
Final OP_VERIFY OP_TRUE is removed as there is an implicit OP_VERIFY at the end of a Script.
OP_VERIFY is merged with preceding opcode where applicable.
Shallow OP_PICK and OP_ROLL are replaced by hardcoded opcodes (e.g. OP_SWAP, OP_DUP).
Several other bytecode optimisations.
- ✨ Add pragma keyword to specify intended compiler version.
Example: pragma cashscript ^0.2.0;
Contract fails to compile when compiler version does not satisfy constraints.
- 🚨 Add CashProof for all individual bytecode optimisations and for example contracts from 0.1.2 to 0.2.0.
- 🐛 Add "default case" for function selection that fixes a vulnerability where people could spend funds by not calling any function.
- ⬆️ Update dependencies.

### CashScript SDK

- ⬆️ Update cashc and other dependencies.
https://x.com/RoscoKalis/status/1178843657069154305

## v0.1.2

### CashScript SDK

- ✨ Add support for OP_RETURN outputs.
- 🐛 Improved error handling.
- 🐛 Poll for transaction details to make sure it's available.
- 🔥 Enable optional mainnet - NOT RECOMMENDED
- 🔨 UTXO selection refactor
- 🚨 Improve Transaction testing
https://x.com/RoscoKalis/status/1174910060691984385

## v0.1.1

### CashScript SDK

- 🐛 Bug fixes with incorrect parameter encoding for string/bool/int types.

## v0.1.0

- 🎉 Initial release.
