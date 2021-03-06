---
id: manage-cent-os
title: Interacting with the Centrifuge Node
---

The following section lists the API calls to perform functions like sending documents, validating proofs and so on. For more information, see [Centrifuge Node API documentation](https://app.swaggerhub.com/apis-docs/centrifuge.io/cent-node/0.0.3).

## Invoice Document service

* To create a list of precise proofs for the specified fields of the document given by ID:

  ```bash
  $ curl -X POST "https://localhost/document/IDENTIFIER/proof" -H "authorization:\${hex(CentrifugeID)}" \ 
  -H   "accept: application/json" -H "Content-Type: application/json" \
  -d "{ \"identifier\": \"string\", \"type\": \"string\", \"fields\": [ \"string\" ]}"
  ```

  Replace the _IDENTIFIER_ parameter with the ID of your document.

* To create a list of precise proof for the specified fields of the given version of the document given by ID:

  ```bash
  $ curl -X POST "https://localhost/document/IDENTIFIER/VERSION/proof" -H "authorization:\${hex(CentrifugeID)}" \ 
  -H "accept: application/json" -H "Content-Type: application/json" \
  -d "{ \"identifier\": \"string\", \"type\": \"string\", \"version\": \"string\", \
  \"fields\": [ \"string\" ]}"
  ```
  Replace the _IDENTIFIER_ and _VERSION_ parameters with the ID and version of your document.
* To get an invoice:

  ```bash
  $ curl -X POST "https://localhost/invoice/get" -H "authorization:\${hex(CentrifugeID)}" \ 
  -H "accept: application/json" -H "Content-Type: application/json" \
  -d "{ \"document_identifier\": \"string\"}"
  ```

* To create an invoice:

  ```bash
  curl -X POST "https://localhost/invoice" -H "accept: application/json" -H "authorization:\${hex(CentrifugeID)}" \
  -H "Content-Type: application/json" -d "{ \"collaborators\": [ \"string\" ], \
  \"data\": { \"invoice_status\": \"string\", \"invoice_number\": \"string\", \
  \"sender_name\": \"string\", \"sender_street\": \"string\", \"sender_city\": \
  \"string\", \"sender_zipcode\": \"string\", \"sender_country\": \"string\", \
  \"recipient_name\": \"string\", \"recipient_street\": \"string\", \
  \"recipient_city\": \"string\", \"recipient_zipcode\": \"string\", \
  \"recipient_country\": \"string\", \"currency\": \"string\", \
  \"gross_amount\": \"string\", \"net_amount\": \"string\", \
  \"tax_amount\": \"string\", \"tax_rate\": \"string\", \
  \"recipient\": \"string\", \"sender\": \"string\", \"payee\": \"string\", \
  \"comment\": \"string\", \"due_date\": \"2018-10-22T01:36:35.832Z\", \
  \"date_created\": \"2018-10-22T01:36:35.832Z\", \"extra_data\": \"string\" }}"
  ```

## Minting an NFT

To mint an NFT from the Centrifuge invoice document:

  ```bash
  $ curl -X POST "https://localhost/token/mint" -H "accept: application/json" -H "authorization:\${hex(CentrifugeID)}" \
  -H "Content-Type: application/json" -d "{ \"identifier\": \"string\", \"registry_address\": \"string\", \"deposit_address\": \"string\", \
  \"proof_fields\": [ \"string\" ]}"
  ```
 
On Rinkeby testnet a payment obligation  [NFT registry](https://rinkeby.etherscan.io/address/0xdb0581a9328664855328addb0e251184640f9e5d) is deployed.

The payment obligation can be minted with an invoice document. 

The address [`0xdb0581A9328664855328AdDb0E251184640f9e5D`](https://rinkeby.etherscan.io/address/0xdb0581a9328664855328addb0e251184640f9e5d) can be used as `registry_address`

The following `proof_fields` are required `["invoice.gross_amount", "invoice.currency", "invoice.due_date", "collaborators[0]"]`
to mint a payment obligation NFT.

The `deposit_address` can be any arbitrary address which should own the NFT. 
  


