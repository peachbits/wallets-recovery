# CasaHODL recovery

How to recover funds from a 3-of-5 Casa Bitcoin Wallet without using Casa software or servers.\
Install Electrum 3.2.3 or later: https://electrum.org/#download.

NOTE: Electrum can be finicky with hardware signing device support, especially on Linux. In order to prevent errors, ensure that you only have ONE Electrum instance running and make sure ALL your hardware devices are plugged in rather than plugging and unplugging the devices as you sign.

## Linux Only

Install the appropriate libraries for your hardware wallets:\
`sudo apt-get install libusb-1.0-0-dev libudev-dev`\
`sudo pip3 install btchip-python`\
`sudo pip3 install trezor`\
`sudo pip3 install keepkey`

## Linux Only

Run electrum. For testnet, run `electrum --testnet`.\
Create a new wallet and give it a name.\
Choose “multi-signature wallet”.\
Select “From 5 cosigners”.\
Select “Require 3 signatures”.\
Click next.

For cosigner 1 of 5:\
Choose “hardware wallet”.\
Plug in the hardware device 1 if it isn’t already plugged in.\
Click next.\
Select your hardware device and click next.\
Select p2sh-segwit multisig.\
The derivation path should change to something like: `m/48'/0'/0'/1'`. Replace it with the derivation path from your recovery data, which will look something like: `m/49/0/0`.\
Click next, then next again on the master public key screen.

For cosigner 2 of 5:\
Choose “cosign with hardware device”.\
Plug in the hardware device 2 if it isn’t already plugged in.\
Click next.\
Select your hardware device and click next.\
Select p2sh-segwit multisig.\
The derivation path should change to something like: `m/48'/1'/0'/1'`. Replace it with the derivation path from your recovery data.\
Click next.

For cosigner 3 of 5:\
Choose “cosign with hardware device”.\
Plug in the hardware device 3 if it isn’t already plugged in.\
Click next.\
Select your hardware device and click next.\
Select p2sh-segwit multisig.\
The derivation path should change to something like `m/48'/1'/0'/1'`. Replace it with the derivation path from your recovery data.\
Click next.

For cosigner 4 of 5:\
Choose “Enter cosigner key” and click next.\
Paste the “Mobile Device Key” for the appropriate account from your recovery data.\
Click next.

For cosigner 5 of 5:\
Choose “Enter cosigner key” and click next.\
Paste the “Recovery Device Key” for the appropriate account from your recovery data.\
Click next.

On the password screen, leave both fields blank and click next.

Electrum will now initialize your wallet and display all of the transactions that have been received and sent by it. If you don’t see your transactions show up after a minute or so, something went wrong during the process and Electrum derived the wrong set of addresses.

To send your assets to a new wallet, click on the “send” tab and fill in the “pay to” field with and address owned by your new wallet. Click the “max” button to sweep all of the value out of the wallet, and slide the “fee” bar to an appropriate fee depending upon your urgency.

Once you click “send” you will be prompted to confirm the amount and destination address on each hardware device.

Upon completing the third signature, the “broadcast” button will no longer be greyed out. Click “broadcast” and then copy the transaction id into a block explorer to check that the transaction has propagated across the network.
