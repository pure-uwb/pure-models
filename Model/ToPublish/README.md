# Tamarin models for PURE
This is the README for the Tamarin models associated with the paper "PURE: Payments with UWB RElay-protection".

The Tamarin models are based on the [EMV models](https://github.com/EMVrace/EMVerify) by David Basin, Ralf Sasse, and Jorge Toro-Pozo for their IEEE S&P 2021 paper "The EMV Standard: Break, Fix, Verify", see their [project page](https://emvrace.github.io/).

## Files
- EMV_Mastercard_SecureRanging_Ext.spthy: The Tamarin model of the Mastercard kernel with the PURE extension
- EMV_Mastercard_SecureRanging_Ext.proof: The proof of the above model
- Mastercard.oracle: Proof-support oracle

## Modifications
The model is based on the EMV contactless model by Basin et al. 
Their model contains the Visa and Mastercard kernel and allows for different Offline Data Authentication, Transaction Authorization, and Cardholder Verification methods.
This allows for different configurations that can be verified individually in the presence of other configurations.

We base our model on one configuration, namely the Mastercard kernel with CDA and a high transaction value.
We limit the model to the Mastercard kernel by removing the Visa model. Thus, we analyze the Mastercard in isolation without the presence of the Visa kernel.
Compared to the original models, we do not restrict the model to one Cardholder Verification Method. In addition we allow a card to perform Consumer Device Cardholder Verification (in our model ODCVM) which is usually performed by mobile phones by for example checking a finger print.

The model is extended with the Diffie-Hellman key exchange of PURE. 
We proof non-injective agreement on the half keys by including them in the transaction data.
In addition to the authentication properties, we prove the original secrecy properties on the shared and private key of the card and the PIN as well as our new secrecy lemma on the derived secret of PURE.


## Proof
The model was automatically proven with the Tamarin prover release version 1.8.0 with the help of the provided oracle. The derivation check timeout was set to two minutes.

The proof took 60 minutes on a computing server running Ubuntu 20.04.3 with two Intel(R) Xenon(R) E5-2650 v4@2.20GHz CPUs (with 12 cores each) and 256GB of RAM. We limited the used threads to at most 14 and the RAM to at most 32GB.