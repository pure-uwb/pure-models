# Notes on Changes

## Comparing Simplified with non-simplyfied

- There are additional rules for DH exchange:
    - compromising Ephemeral keys
    - DH exchange rules between GPO and ?

- The DDA and SDA rules are commented out. It is just CDA without the presence of DDA or SDA

- However, the different CVMs and Transaction authorization methods remain.

- The Visa part is removed. Just lookes ar Mastercard in the absence of Visa.

 
## Comparing extended and siplified

- add kdf

- comment out the ephemeral key compromise
additional changes in DH rules.

- Addapt the old rules to include the DH exchange.
    - Adapt Terminal and Card state facts.
    - Move the card receiving AIP and AFL to beginning of DH exchange
    - add DH to actionstate facts.
    - include DH in AC
    - Add action facts for new lemmas

- Add lemmas on DH:
    - Auth
    - secrecy


## Discussion 30.8.
- Current models: cards and no phones
    - would need to adapt model.
    - later
    - How to sell?
- Patrick: anpassungen in non PAN models
    - Bereinigen, was da ist.
- Optional: verhandlung von UWB
    - Downgrades ausschliessen
    - AIP

## some notes
- optional TODO:
    - Add compromised key
        - vermutlich unnütz
        - interleving ist drin.
    - Add public key to mac, Verfy with SDAD
        - nicht dringend
        - 

- To Discuss: 
    - Do we need an agreement property on the Secret?


- We send the DH material as part of the transaction to the bank. As the terminal and card agree on it and the terminal and bank communicate over a secure channel, the card and terminal also agree on the DH material.
