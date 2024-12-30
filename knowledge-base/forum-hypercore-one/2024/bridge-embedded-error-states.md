Thread: bridge-embedded-error-states
0x3639 | 2023-06-13 11:08:50 UTC | #1

Document Orchestrator Errors and What they mean

ErrUnknownNetwork= errors.New("unknown network")
ErrInvalidToAddress                     = errors.New("invalid destination address")
ErrBridgeNotInitialized                 = errors.New("bridge info is not initialized")
ErrOrchestratorNotInitialized           = errors.New("orchestrator info is not initialized")
ErrTokenNotBridgeable                   = errors.New("token not bridgeable")
ErrNotGuardian                          = errors.New("sender is not a guardian")
ErrTokenNotRedeemable                   = errors.New("token not redeemable")
ErrBridgeHalted                         = errors.New("bridge is halted")
ErrInvalidRedeemPeriod                  = errors.New("invalid redeem period")
ErrInvalidRedeemRequest                 = errors.New("invalid request")
ErrInvalidTransactionHash               = errors.New("invalid transaction hash")
ErrInvalidNetworkName                   = errors.New("invalid network name")
ErrInvalidContractAddress               = errors.New("invalid contract address")
ErrInvalidToken                         = errors.New("invalid token standard or token address")
ErrTokenNotFound                        = errors.New("token not found")
ErrInvalidEDDSASignature                = errors.New("invalid ed25519 signature")
ErrInvalidEDDSAPubKey                   = errors.New("invalid eddsa public key")
ErrInvalidECDSASignature                = errors.New("invalid secp256k1 signature")
ErrInvalidDecompressedECDSAPubKeyLength = errors.New("invalid decompressed secp256k1 public key length")
ErrInvalidCompressedECDSAPubKeyLength   = errors.New("invalid compressed secp256k1 public key length")
ErrNotAllowedToChangeTss                = errors.New("changing the tss public key is not allowed")
ErrInvalidJsonContent                   = errors.New("metadata does not respect the JSON format")
ErrInvalidMinAmount                     = errors.New("invalid min amount")
ErrTimeChallengeNotDue                  = errors.New("time challenge not due")
ErrNotEmergency                         = errors.New("bridge not in emergency")
ErrInvalidGuardians                     = errors.New("invalid guardians")
ErrSecurityNotInitialized               = errors.New("security not initialized")
ErrBridgeNotHalted                      = errors.New("bridge not halted")

-------------------------

sol | 2023-06-13 14:23:38 UTC | #2

It will take time to provide information about each of these cases.
Are there any that you want to prioritize?

-------------------------

0x3639 | 2023-06-13 14:43:49 UTC | #3

Yes, I was going to prioritize them by looking at log files. I wanted to prioritize the ones that impact uptime or halt / start the bridge.  Also, was going to look at DM with @sumamu to try and piece together what I know.  

Once I get through that I might try to look at the code to see if I can figure out what they mean (the ones that are not so clear).

I’ll work on this a little and then let’s discuss how I can piece this all together

-------------------------

sol | 2023-06-13 15:18:22 UTC | #4

Please post the ones you want to know about.
There are many situations that can cause the bridge to halt.

Sumamu, please share any technical documentation you have for the bridge. We'd appreciate your insight.

-------------------------

