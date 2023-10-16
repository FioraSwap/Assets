# FioraSwap Supported Assets
These are the guidelines to get a custom asset listed on [FioraSwap](https://www.fioraswap.com).

## Governance
Regardless of adherence to this guidelines, new asset listings will be ultimately determined by FioraSwap DAO governance.

## ERC20 Tokens
- Please follow & extend the official [ERC20](https://eips.ethereum.org/EIPS/eip-20) token standard.
- Ideally, use the well audited [OpenZeppelin](https://github.com/OpenZeppelin/openzeppelin-contracts/tree/master/contracts/token/ERC20) implementation as this will facilitate compatibility with FioraSwap, and security for your contract.

### Compatibility
- Functions:
  - Following the standard, your contract should already include the following functions:
      ```solidity
      function name() public view returns (string memory);
      
      function symbol() public view returns (string memory);
      
      function decimals() public view returns (uint8);
      ```
      
- Events:
  - Following the standard, your contract should already include the following events:
      ```solidity
      event Transfer(address indexed from, address indexed to, uint256 value);
      ```

## ERC721 Tokens
- Please follow & extend the official [ERC721](https://eips.ethereum.org/EIPS/eip-721) token standard.
- Ideally, use the well audited [OpenZeppelin](https://github.com/OpenZeppelin/openzeppelin-contracts/tree/master/contracts/token/ERC721) implementation as this will facilitate compatibility with FioraSwap, and security for your contract.
- For a better understanding of contract/collection level metadata, please refer to the [OpenSea Specification](https://docs.opensea.io/docs/contract-level-metadata).
- We recommend using [IPFS](https://docs.ipfs.tech) for storing metadata, and for URIs.

### Compatibility
- Functions:
  - Following the standard, your contract should already include the following functions:
      ```solidity
      function name() public view returns (string memory);
      
      function symbol() public view returns (string memory);
      
      function tokenURI(uint256 tokenId) public view returns (string memory);
      ```
  - Additionally, your contract must include custom functions:
      ```solidity
      /**********************************************************
        This function returns a link to the contract/collection
        metadata. This is needed for providing an image to the
        entire contract/collection, and optionally changing the
        contract/collection name.
      **********************************************************/
      function contractURI() public view returns (string memory);
      ```
      
- Events:
  - Following the standard, your contract should already include the following events:
      ```solidity
      event Transfer(address indexed from, address indexed to, uint256 indexed tokenId);
      ```
  - Additionally, your contract must include custom events:
      ```solidity
      /**********************************************************
        This event should be emitted when a function is called
        to update the link for the contract/collection level
        metadata. (i.e. For a rebrand)
      **********************************************************/
      event ContractURI();

      /**********************************************************
        This event should be emitted when a function is called
        to update the links for the metadata of every token in
        the contract/collection. (i.e. For a reveal)
      **********************************************************/
      event URIAll();

      /**********************************************************
        This event should be emitted when a function is called
        to update the link for the metadata of a single token
        in the contract/collection. (i.e. For a fix)
      **********************************************************/
      event URI(uint256 tokenId);
      ```
      
### Metadata
- Contract/Collection:
  - Make sure the `JSON` object containing the metadata for the contract/collection has the following properties:
    ```json
    {
      "name": "String. Optional. This will replace the contract/collection name retreived from the blockchain.",
      "image": "String. Required. This will be used to represent the entire contract/collection."
    }
    ``` 

- Token:
  - Make sure the `JSON` objects containing the metadata for the tokens has the following properties:
    ```json
    {
      "name": "String. Optional. This is for providing a unique name to each token. If none is given the token name will be 'CollectionName #TokenId'.",
      "image": "String. Required. This will be used to represent the token.",
      "imageV2 or image_v2": "String. Optional. This can be used for collections with multiple visual representations(2D/3D). If provided it will display this image in the app."
    }
    ``` 

## ERC1155 Tokens
- Please follow & extend the official [ERC1155](https://eips.ethereum.org/EIPS/eip-1155) token standard.
- Ideally, use the well audited [OpenZeppelin](https://github.com/OpenZeppelin/openzeppelin-contracts/tree/master/contracts/token/ERC1155) implementation as this will facilitate compatibility with FioraSwap, and security for your contract.
- For a better understanding of contract/collection level metadata, please refer to the [OpenSea Specification](https://docs.opensea.io/docs/contract-level-metadata).
- We recommend using [IPFS](https://docs.ipfs.tech) for storing metadata, and for URIs.

### Compatibility
- Functions:
  - Following the standard, your contract should already include the following functions:
      ```solidity
      function uri(uint256 tokenId) public view returns (string memory);
      ```
  - Additionally, your contract must include custom functions:
      ```solidity
      /**********************************************************
        This function is not part of the ERC1155 standard, but
        we suggest adding it to provide you contract/collection
        with a name at the blockchain level. This is OPTIONAL
        and can be ignored in favor of fetching it via metadata.
      **********************************************************/
      function name() public view returns (string memory);

      /**********************************************************
        This function is not part of the ERC1155 standard, but
        we suggest adding it to provide you contract/collection
        with a symbol at the blockchain level. This is OPTIONAL
        and can be ignored in favor of fetching it via metadata.
      **********************************************************/
      function symbol() public view returns (string memory);

      /**********************************************************
        This function returns a link to the contract/collection
        metadata. This is needed for providing an image to the
        entire contract/collection, and optionally changing the
        contract/collection name and symbol.
      **********************************************************/
      function contractURI() public view returns (string memory);
      ```
      
- Events:
  - Following the standard, your contract should already include the following events:
      ```solidity
      event TransferSingle(address indexed operator, address indexed from, address indexed to, uint256 id, uint256 value);

      event TransferBatch(address indexed operator, address indexed from, address indexed to, uint256[] ids, uint256[] values);
      
      event URI(string value, uint256 indexed id);
      ```
  - Additionally, your contract must include custom events:
      ```solidity
      /**********************************************************
        This event should be emitted when a function is called
        to update the link for the contract/collection level
        metadata. (i.e. For a rebrand)
      **********************************************************/
      event ContractURI();

      /**********************************************************
        This event should be emitted when a function is called
        to update the links for the metadata of every token in
        the contract/collection. (i.e. For a reveal)
      **********************************************************/
      event URIAll();
      ```
      
### Metadata
- Contract/Collection:
  - Make sure the `JSON` object containing the metadata for the contract/collection has the following properties:
    ```json
    {
      "name": "String. Optional if provided by contract. This will replace the contract/collection name retreived from the blockchain.",
      "symbol": "String. Optional if provided by contract. This will replace the contract/collection symbol retreived from the blockchain.",
      "image": "String. Required. This will be used to represent the entire contract/collection."
    }
    ``` 

- Token:
  - Make sure the `JSON` objects containing the metadata for the tokens has the following properties:
    ```json
    {
      "name": "String. Optional. This is for providing a unique name to each token. If none is given the token name will be 'CollectionName #TokenId'.",
      "image": "String. Required. This will be used to represent the token.",
    }
    ``` 