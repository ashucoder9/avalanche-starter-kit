
Deploy erc20: forge create --rpc-url local-c --private-key $PK src/native-token-bridge/mocks/ExampleWASH.sol:ExampleWASH

Deploy bridge on source: forge create --rpc-url local-c --private-key $PK src/native-token-bridge/ERC20Source.sol:ERC20Source --constructor-args "0x17aB05351fC94a1a67Bf3f56DdbB941aE6c63E25" "0x8db97C7cEcE249c2b98bDC0226Cc4C2A57BF52FC" "0x5DB9A7629912EBF95876228C24A848de0bfB43A9"

deploy bridge on subnet: forge create --rpc-url mysubnet --private-key $PK src/native-token-bridge/ERC20Destination.sol:ERC20Destination --constructor-args "0x0C8a4406e5CC48B1dDfd702018E9999E01978F2f" "0x8db97C7cEcE249c2b98bDC0226Cc4C2A57BF52FC" "0x55e1fcfdde01f9f6d4c16fa2ed89ce65a8669120a86f321eef121891cab61241" "0x4Ac1d98D9cEF99EC6546dEd4Bd550b0b287aaD6D" "Wrapped ASH" "WASH" "18"

mint some erc20 on source: cast send --rpc-url local-c --private-key $PK 0x5DB9A7629912EBF95876228C24A848de0bfB43A9 "deposit()" --value 5000000000000000000000

check balance: cast call --rpc-url local-c --private-key $PK 0x5DB9A7629912EBF95876228C24A848de0bfB43A9 "balanceOf(address)" 0x8db97C7cEcE249c2b98bDC0226Cc4C2A57BF52FC

approve some tokens: cast send --rpc-url local-c --private-key $PK 0x5DB9A7629912EBF95876228C24A848de0bfB43A9 "approve(address, uint256)" 0x4Ac1d98D9cEF99EC6546dEd4Bd550b0b287aaD6D 2000000000000000000000

send some tokens: cast send --rpc-url local-c --private-key $PK 0x4Ac1d98D9cEF99EC6546dEd4Bd550b0b287aaD6D "send((bytes32, address, address, uint256, uint256, uint256), uint256)" "(0x989aa64d32a316c2ebd45812995753ffcaebd0b5e1f34a9a7c21a5238f4f24e2, 0x52C84043CD9c865236f11d9Fc9F56aa003c1f922, 0x8db97C7cEcE249c2b98bDC0226Cc4C2A57BF52FC, 0, 0, 69420)" 1000000000000000000000

check balance on mysubnet: cast call --rpc-url mysubnet --private-key $PK 0x52C84043CD9c865236f11d9Fc9F56aa003c1f922 "balanceOf(address)" 0x8db97C7cEcE249c2b98bDC0226Cc4C2A57BF52FC
