# Sei Assetlist
This repository provides a publicly maintained registry of assets on Sei.

## Contributing
We encourage all creators on Sei to contribute any tokens or assets to this repository. To propose changes directly, you can open a Pull Request against this repository.

1. [Fork the repository](https://guides.github.com/activities/forking/), then [clone](https://docs.github.com/en/get-started/exploring-projects-on-github/contributing-to-a-project#cloning-a-fork) the forked repository locally.
2. Make changes to the repository. Ensure that your changes confirm to the contribution guides below.
3. Commit and push your changes to your forked repository.
4. Once your changes have been pushed to your forked repository, [make a Pull Request](https://git-scm.com/downloads) against this repository.

## Schema
Each `json` in this repository should follow a specific schema. Refer to the schemas for each file in the `./schema/` directory for details about how each field should be formatted.

### assetlist.json
This file maintains a list of assets that have been deployed to Sei. Both native and EVM based tokens are stored here. To differentiate between EVM based tokens and Native tokens, you can infer it from the `base` or `type_asset` property.
- For `base`, EVM compatible tokens typically have `0x` contract addresses, while native coins have `sei` addresses (for `cw20` tokens), `factory/*` tokens for Tokenfactory native tokens, and `ibc/*` for `ics20` tokens.

As a general guideline, please ensure that:
- The token you are contributing does not already exist in the assetlist for the chain.
- The token you are contributing has a unique `name` for the chain.
- The fields adhere to the schema defined in `./schema`. Please read the `description` of each field in the schema to understand what the contents of each field should be.

#### base
For each token, `base` should be the contract address (for `erc20` and `cw20` tokens) or start with (ibc/*) or (factory/*) for `ics20` and tokenfactory tokens.

#### denom_units
Each token should have 2 denom_units.
- The first denom unit represents the base denom. This is the minimum unit of the token, hence `denom` should match `base` exactly, and `exponent` should be 0.
- The second denom unit represents the denom that is intended for use. For this `denom_unit`, `denom` should be the `display` denom for the token, and `exponent` should be the number of decimal places this unit is allowed to have. For example, since 1 sei = 1000000 usei, and usei is the base denom, a sei value cannot have more than 6 decimal places, hence the exponent for the sei `denom` should be 6.

## Images
Each token in the assetlist should have an associated image. This is encapsulated in the assetlist in the images field, which should contain a link to a `.png`, `.svg`, or both. 
To ensure that your token images can be accessed from this assetlist, you should commit those image files to this repo.
1. Check the `./images` directory to see if any files can be used. (Especially for bridged stablecoins).
2. If the `.png` and `.svg` files of your token does not already exist, upload your files to the `./images` directory of this repo.
3. Ensure that your token assetlist points to `https://raw.githubusercontent.com/Seitrace/sei-assetlist/main/images/<YOUR_FILE_NAME>`

## Querying
To query the files in the assetlist directly, you can make call github directly (eg. https://raw.githubusercontent.com/Seitrace/sei-assetlist/main/assetlist.json).

Alternatively, you can query the sei-app-api (GET app-api.seinetwork.io/assetList). Note that this API only returns some curated properties and may not always return the most up-to-date assetlist.

## Disclaimer
The contents of this repository do not imply any endorsement of the information provided. No due diligence, technical or otherwise, has been conducted on the information contained herein. The maintainers of this repository and the individuals associated with it accept no responsibility for any consequences arising from the use of this information.

Additionally, no verification of claims made in any associated metadata has been performed. The maintainers have absolute discretion and the final say in any additions to or modifications of the list. Use of this repository and its contents is entirely at your own risk.
