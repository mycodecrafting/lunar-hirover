# Lunar Rover Entropy and Address Generator

The purpose of this tool is to:
 1. Generate a single random value that can be [affixed to a lunar rover](https://www.hiro.so/blog/launching-a-bitcoin-treasure-hunt-on-the-moon) and used to generate addresses on a set of [supported chains](#supported-chains).
 2. Display the associated public addresses for the [supported chains](#supported-chains) so that funds can be sent to those addresses.

This tool generates a random entropy value using the [ChaCha20Rng](https://rust-random.github.io/rand/rand_chacha/struct.ChaCha20Rng) Cryptographically Secure Random Number Generator. This is the value that will be affixed to the lunar rover.

This entropy value can be used to generate a 24-word mnemonic phrase, which can be imported into various wallets to generate addresses on that chain. 

## Installation
To install, go to the Actions tab of this repository, and click the "Upload Build" action in the left Actions panel. Click on the latest workflow run in the list, and download the appropriate binary for your operating system.

Extract the downloaded zip file, and navigate to the extracted folder. Once again, extract the zip file inside that folder. This will create a file called `lunar-hirover`. Congrats, you’ve installed the tool!

## Usage

The following instructions are for macOS usage; instructions may vary slightly depending on the OS.

### Basic Usage
 
In the terminal, navigate to the tool’s installed location. Run:
```sh
./lunar-hirover
```
in the terminal. Something like the following will be displayed:
```sh
Using random entropy.
00a92…8328
# STX Address: SP2Y...8Y07
# BTC Address: 1JJV…WN1A
# ETH Address: 0x9fe7…f1f32
# NOTE: The ETH address can be used to receive funds on the Polygon, Fantom, BNB, Optimism, and Arbitrum chains.
# DOGE Address: DJpj…JGWeH
# LTC Address: LLXk…ZNc8
```
The first value represents the entropy value that is used to generate the mnemonic. The rest of the values are the public addresses generated from that mnemonic on each chain.

### Piping Entropy to the Clipboard

To run the program without viewing the mnemonic, run:
```sh
./lunar-hirover | pbcopy
```
***Note: `pbcopy` will not be available on all operating systems. For windows, use `clip`.***

This will send the entropy value directly to your clipboard while still displaying the public addresses that were generated.

### Environment Variables
The tool can also be run in a few other modes using environment variables. Environment variables can be used with the following format in the terminal:
```sh
ENV_VAR_NAME=ENV_VAR_VALUE ./lunar-hirover
```
#### ENTROPY=00a92…9534
This runs the tool with the entered entropy value rather than generating a random value. This can be used to see the public addresses associated with a mnemonic generated by the entered entropy value.

#### PRINT_PRIVATE_DATA=TRUE
This logs additional information to the console, including the mnemonic and private keys.

#### USE_DEFAULT_ENTROPY=TRUE
This uses a default entropy value. This is for debugging purposes. *DO NOT FUND THE ACCOUNTS GENERATED BY THIS ENTROPY VALUE*.

## Converting Entropy to Mnemonic
Here are two options for converting the entropy value to a 24-word mnemonic phrase:

### Using Ian Coleman's Mnemonic Code Generator
 - Go to https://iancoleman.io/bip39/
 - Check the box that says "Show Entropy Details"
 - Paste the entropy value generated by this tool (or that you've found affixed to the lunar rover) into the Entropy field
 - Scroll down to see the mnemonic phrase in the "BIP39 Mnemonic" field

### Using This Tool
Run this tool using the following [environment variables](#environment-variables):
```sh
PRINT_PRIVATE_DATA=TRUE ENTROPY=[entropy_value] ./lunar-hirover
```
This will log an output that includes the mnemonic.

### Supported Chains
The tool will calculate and display public addresses for the following chains:
 - BTC
 - DOGE
 - ETH (and EVM compatible chains)
    - Arbitrum
    - BNB
    - Fantom
    - Optimism
    - Polygon
 - LTC
 - STX
