# TradeArcana Smart Contract

**TradeArcana** is a decentralized card trading platform built on the Stacks blockchain, allowing players to mint, buy, sell, and trade non-fungible cards in a transparent, secure, and fun environment. Whether you're a collector, trader, or strategist, TradeArcana provides the tools to create, list, and exchange unique cards that hold both value and rarity in the game world.

---

## Features

- **Card Creation**: Admins can mint new cards with customizable attributes, including name, attack, defense, rarity, and element.
- **Card Listing**: Players can list their cards for sale at a specified price.
- **Card Purchase**: Users can purchase cards from the marketplace, transferring the appropriate STX to the seller.
- **Direct Card Trading**: Players can directly trade cards with each other, exchanging cards one-to-one.
- **Card Details**: Get detailed information about any card, including its attributes, market status, and ownership.

---

## Contract Components

### Constants

- `contract-owner`: The address of the contract owner (admin).
- `err-owner-only`: Error for non-admin users attempting admin functions.
- `err-not-token-owner`: Error for users attempting to perform actions without owning the token.
- `err-invalid-card`: Error for an invalid card ID.
- `err-card-exists`: Error for trying to mint a card that already exists.
- `err-insufficient-payment`: Error for insufficient STX balance when buying a card.

### NFT Definition

- **card**: The main NFT representing each card in the game. Each card has an associated unique ID.

### Data Maps

- **card-attributes**: Stores the attributes of each card, such as name, attack, defense, rarity, and element.
- **card-market**: Stores market listings for cards, including the price and seller's address.

### Variables

- **next-card-id**: A counter to keep track of the next available card ID.

---

## Functions

### Admin Functions

- **create-card**: Allows the admin to mint a new card with specific attributes.
  - Inputs: `name`, `attack`, `defense`, `rarity`, `element`
  - Returns: Card ID of the newly created card.

### Trading Functions

- **list-card**: Allows a user to list a card for sale on the marketplace.
  - Inputs: `card-id`, `price`
  - Returns: `true` if the card is successfully listed.

- **unlist-card**: Allows a user to remove a card from the marketplace.
  - Inputs: `card-id`
  - Returns: `true` if the card is successfully unlisted.

- **buy-card**: Allows a user to buy a card listed on the marketplace.
  - Inputs: `card-id`
  - Returns: `true` if the card is successfully bought and transferred.

- **trade-cards**: Allows two users to trade cards directly with each other.
  - Inputs: `send-card-id`, `receive-card-id`, `counterparty`
  - Returns: `true` if the trade is successful.

### Read-Only Functions

- **get-card-details**: Fetches the details (attributes) of a specific card.
  - Inputs: `card-id`
  - Returns: A map containing the card's attributes.

- **get-market-listing**: Retrieves the market listing of a specific card, including the price and seller.
  - Inputs: `card-id`
  - Returns: A map containing the listing details.

- **get-card-owner**: Retrieves the current owner of a specific card.
  - Inputs: `card-id`
  - Returns: The principal (address) of the current owner.

---

## Usage

### 1. Creating a Card
Only the contract owner can create cards by specifying the card's name, attack, defense, rarity, and element. This will mint the card and add it to the `card-attributes` map with a unique ID.

### 2. Listing and Selling Cards
Players can list their owned cards for sale by setting a price. After listing, the card is transferred to the contract and made available for others to purchase.

### 3. Buying Cards
Anyone can buy a card from the marketplace by transferring the specified amount of STX to the seller. Upon successful payment, the card is transferred to the buyer.

### 4. Trading Cards
Users can trade cards directly with each other by transferring cards between themselves.

---

## Example Transactions

### 1. Creating a Card
```clarity
(create-card "Fire Dragon" 10 8 5 "Fire")
```

### 2. Listing a Card
```clarity
(list-card 1 50)
```

### 3. Buying a Card
```clarity
(buy-card 1)
```

### 4. Trading Cards
```clarity
(trade-cards 1 2 "STX12345...") 
```

---

## Security Considerations

- **Ownership Verification**: All transactions that require ownership verification, such as listing or trading cards, ensure the caller is the rightful owner of the card by checking the NFT owner.
- **Error Handling**: The contract includes error handling for invalid actions, such as attempting to transfer or buy a non-existent card or trying to perform actions without ownership.

---

## Future Enhancements

- **Card Upgrades**: Introduce the ability to upgrade cards' attributes, making them more powerful for battle.
- **Card Rarity**: Enhance the rarity system with different levels, adding more depth to card collection and trading.
- **Leaderboard**: Create a ranking system based on players' card collections or battle victories.

---

## License

TradeArcana is open-source and licensed under the [MIT License](LICENSE).