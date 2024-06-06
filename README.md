# Tamarin Models for PURE

This README accompanies the Tamarin models associated with the paper "PURE: Payments with UWB RElay-protection".

Our Tamarin models are based on the [EMV models](https://github.com/EMVrace/EMVerify) by David Basin, Ralf Sasse, and Jorge Toro-Pozo. These models have been used to prove results published in the IEEE S&P 2021 paper "The EMV Standard: Break, Fix, Verify", see also the [project page](https://emvrace.github.io/).

## How to install Tamarin

Follow the instruction on the [tamarin-prover](https://tamarin-prover.com/#installation) website. For ubuntu users, we suggest downloading the [v1.8](https://github.com/tamarin-prover/tamarin-prover/releases/tag/1.8.0) from Github.

## Files

The formal proofs described in our paper can be reproduced using the following files:

- `EMV_Mastercard_SecureRanging_Ext.spthy`: The Tamarin model of the Mastercard kernel modelling the PURE extension
- `EMV_Mastercard_Secure_Ranging_Ext_proof.spthy`: The proofs for the model
- `Mastercard.oracle`: Proof-support oracle

## Modifications of the Original Sources

The original model by Basin et al. is more general and contains besides the Mastercard also the Visa kernel. Furthermore, it allows for different Offline Data Authentication methods, Transaction Authorization, and Cardholder Verification methods. This allows for the verification of different configurations in the presence of other configurations.

For our purposes, we need only one configuration, namely the Mastercard kernel with Combined Data Authentication (CDA) and high transaction values. We thus remove the Visa kernel completely and analyze the Mastercard kernel in isolation.
Compared to the original models, we do not restrict our model to a single Cardholder Verification Method (CVM), but allow cards to perform On-Device Cardholder Verification (ODCVM) which is performed on the cardholder's device, such as a mobile phone, and includes checks such as face or finger print recognition.

To model the extension of the EMV standard proposed in PURE, we have extended the model with a Diffie-Hellman key exchange. 
We abstract the UWB ranging by modeling the timing data as a nonce created by the card that it sends in clear to the terminal.
We proof non-injective agreement on the Diffie-Hellman shares and the timing data by including them in the integrity protected transaction data.
In addition to the integrity properties, we prove the original secrecy properties of the shared and private keys of the card and of the PIN. Furthermore, we prove a new secrecy lemma on the derived secret established by the Diffie-Hellman extension of the original protocol.


## Proofs

The claims (lemmas) in the model have been automatically proven using the Tamarin prover release version 1.8.0 using the provided oracle. The derivation check timeout was set to two minutes.

The proofs took 65 minutes on a computing server running Ubuntu 20.04.3 with two Intel(R) Xenon(R) E5-2650 v4@2.20GHz CPUs (with 12 cores each) and 256GB of RAM. We have limited the number of threads to 14 and the memory consumption (RAM) to 32GB.

The proofs were executed with the following command `tamarin-prover-release-1.8.0 --prove EMV_Mastercard_Secure_Ranging_Ext.spthy --heuristic=O --oraclename=Mastercard.oracle +RTS -N14 -M32G -RTS --output=EMV_Mastercard_Secure_Ranging_Ext.proof  --derivcheck-timeout=120`

## How to load the proofs

To load the proof run `tamarin-prover  --prove EMV_Mastercard_Secure_Ranging_Ext_proof.spthy --derivcheck-timeout=0`

Following is the expected results

```
==============================================================================
summary of summaries:

analyzed: EMV_Mastercard_Secure_Ranging_Ext_proof.spthy

  processing time: 4695.21s

  executable (exists-trace): verified (392 steps)
  executable_ODCVM (exists-trace): verified (274 steps)
  bank_accepts (all-traces): verified (636 steps)
  auth_to_terminal_minimal (all-traces): verified (243 steps)
  auth_to_terminal (all-traces): verified (941 steps)
  auth_to_terminal_minimal_dh (all-traces): verified (163 steps)
  auth_to_terminal_dh (all-traces): verified (2367 steps)
  auth_to_bank_minimal (all-traces): verified (241 steps)
  auth_to_bank (all-traces): verified (849 steps)
  secrecy_MK (all-traces): verified (6 steps)
  secrecy_privkCard (all-traces): verified (7 steps)
  secrecy_PIN (all-traces): verified (3 steps)
  secrecy_PAN (all-traces): falsified - found trace (40 steps)
  secrecy_SIGMA (all-traces): verified (10211 steps)

==============================================================================
```


