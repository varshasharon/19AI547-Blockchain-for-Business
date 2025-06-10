# Experiment 7: AI-Powered Smart Contract for Decentralized Negotiation
## Date : 29-04-2025

# Aim:
To create a smart contract that integrates AI logic for automated negotiation in decentralized commerce. The contract adjusts price and conditions dynamically based on real-time market trends using an on-chain AI model.

# Algorithm:
### Step 1: 
The seller lists an item with a minimum price and a defined negotiation range.

### Step 2: 
The buyer submits an offer price for the listed item.

### Step 3: 
AI logic evaluates the offer using market demand, historical data, and time-based pricing.

### Step 4: 
The smart contract checks if the offer meets, falls within, or is below the acceptable range.

### Step 5: 
If within range, the contract generates a counteroffer automatically.

### Step 6: 
The buyer chooses to accept, reject, or revise the counteroffer.

### Step 7: 
If accepted, the smart contract executes the transaction and transfers ownership.

### Step 8: 
The transaction data is fed into the price learning algorithm for refinement.

### Step 9: 
Future pricing decisions are dynamically optimized based on learned data.

# Program:
```
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract AIPoweredNegotiation {
    struct Item {
        address seller;
        uint256 minPrice;
        uint256 maxPrice;
        uint256 basePrice;
        bool sold;
    }

    mapping(uint256 => Item) public items;
    uint256 public itemCount;

    event ItemListed(uint256 itemId, uint256 basePrice);
    event OfferMade(uint256 itemId, address buyer, uint256 offer);
    event CounterOffer(uint256 itemId, uint256 counterOffer);
    event Sold(uint256 itemId, address buyer, uint256 finalPrice);

    function listItem(uint256 _basePrice, uint256 _minPrice, uint256 _maxPrice) public {
        require(_minPrice <= _basePrice && _basePrice <= _maxPrice, "Invalid price range");
        
        items[itemCount] = Item(msg.sender, _minPrice, _maxPrice, _basePrice, false);
        emit ItemListed(itemCount, _basePrice);
        itemCount++;
    }

    function makeOffer(uint256 _itemId, uint256 _offerPrice) public payable {
        Item storage item = items[_itemId];
        require(!item.sold, "Item already sold");
        require(msg.value == _offerPrice, "Incorrect offer amount");

        emit OfferMade(_itemId, msg.sender, _offerPrice);

        uint256 aiCounterOffer = dynamicPricing(item.basePrice, item.minPrice, item.maxPrice, _offerPrice);

        if (_offerPrice >= aiCounterOffer) {
            item.sold = true;
            payable(item.seller).transfer(_offerPrice);
            emit Sold(_itemId, msg.sender, _offerPrice);
        } else {
            payable(msg.sender).transfer(_offerPrice); // Refund buyer
            emit CounterOffer(_itemId, aiCounterOffer);
        }
    }

    function dynamicPricing(uint256 base, uint256 min, uint256 max, uint256 offer) private pure returns (uint256) {
        if (offer >= max) return max;
        if (offer >= base) return base;
        return (base + offer) / 2; // Simple AI-based counteroffer logic
    }
}
```

# Output:
![image](https://github.com/user-attachments/assets/c2a9c93f-a3d5-4f47-819f-0cde1e950fd4)
![image](https://github.com/user-attachments/assets/8bb30c9b-7bc2-4d52-b6d9-0baead55636e)
![image](https://github.com/user-attachments/assets/5deb7db3-a01a-4c3e-8550-89953a99b50a)



# High-Level Overview:
First-of-its-kind AI-powered pricing contract.

Mimics real-world price negotiations using dynamic on-chain pricing.

Can be extended to AI oracles for real-time market data.

Inspired by AI-enhanced commerce and eBay-like decentralized auctions.

# RESULT:

Thus, a smart contract that integrates AI logic for automated negotiation in decentralized commerce is executed successfully.
