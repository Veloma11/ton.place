# ton.place
to find the lowest price on  ton.place
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract PriceFinder {
    uint256[] public prices;

    // Функция для добавления цены
    function addPrice(uint256 price) public {
        prices.push(price);
    }

    // Функция для нахождения минимальной цены
    function findLowestPrice() public view returns (uint256) {
        require(prices.length > 0, "No prices available");

        uint256 lowestPrice = prices[0];
        for (uint256 i = 1; i < prices.length; i++) {
            if (prices[i] < lowestPrice) {
                lowestPrice = prices[i];
            }
        }
        return lowestPrice;
    }
}
mkdir price-finder-project
cd price-finder-project
npx hardhat
// scripts/deploy.js
async function main() {
  const [deployer] = await ethers.getSigners();

  console.log("Deploying contracts with the account:", deployer.address);

  const PriceFinder = await ethers.getContractFactory("PriceFinder");
  const priceFinder = await PriceFinder.deploy();

  console.log("PriceFinder deployed to:", priceFinder.address);
}

main()
  .then(() => process.exit(0))
  .catch(error => {
    console.error(error);
    process.exit(1);
  });
npx hardhat run scripts/deploy.js --network ropsten
