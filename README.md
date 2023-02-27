# Kele Pool Ethereum Staking 

The contract adopts the upgradeable solution of the open source project [Openzeppelin](https://github.com/OpenZeppelin/openzeppelin-contracts), so that when Ethereum 2.0 is officially launched, the contract can be upgraded to support contract withdrawal, and also to support the project’s future expansion of NFT, games and other new functions.


[Kele Pool Staking Platform](https://www.kelepool.com/)

## Contracts

Proxy Contract: [0xACBA4cFE7F30E64dA787c6Dc7Dc34f623570e758](https://etherscan.io/address/0xACBA4cFE7F30E64dA787c6Dc7Dc34f623570e758#code)

Logic contracts: [0x2ba03c98fee1f538ff158766c2870196198e8e1d](https://etherscan.io/address/0x2ba03c98fee1f538ff158766c2870196198e8e1d#code)

## Audit

[SlowMist Audit Report](./SlowMist%20Audit%20Report%20-%20KelePoolStaking.pdf)

## Introduction

```
Notice:

1. In order to improve the statistical accuracy of the channel staked amount, the V2 version of the staking contract supports the transmission of source channel parameters.

2. This version adds a contract calling method (depoositV2/createValidatorV2)

3. It will not affect the third-party channels that have been connected to the earlier V1 version before, and the third-party channels can be upgraded on demand.

4. When the V1 version is still used or the source is not passed when using the V2 contract, the system defaults to counting income and dividends according to the registered address.

5. If you use the V2 version, you need to update the ABI and calling method at the same time, and the contract address remains unchanged. For details, please refer to the code for calling the contract below.
```

#### Stake ≥ 32 ETH

If the amount staked by the user is more than 32ETH, the token will be staked to the [ETH2.0 official deposit contract address](https://etherscan.io/address/0x00000000219ab540356cBB839Cbe05303d7705Fa) immediately, and a validator will be created for the user at the same time. We will not manage the user’s funds. After ETH2.0 is officially launched in the future, users can withdraw funds directly from the official Ethereum channel through withdrawal credentials.

Stake ≥ 32 ETH require an additional 0.05ETH for each verification node as a node operating fee. If you plan to create 1 node, you need to transfer 32.05ETH, and if you plan to create 3 nodes, you need to transfer 96.15ETH.

If you want to access our staking platform by calling the contract, these parameters required for this form of staking can be obtained after being generated by the ETH2.0 official CLI tool:
https://github.com/ethereum/staking-deposit-cli

```
    function createValidatorV2(
        uint8 role, // Constant values: 1
        bytes32 source, // partner source
        bytes calldata pubkeys,// validator's public key
        bytes calldata withdrawal_credentials, // withdrawal credentials
        bytes calldata signatures,// signatures
        bytes32[] calldata deposit_data_roots// Merkle roots
    ) external payable
```

#### Stake ＜ 32 ETH

If the staked amount is less than 32 ETH, you can stake a minimum amount of 0.01 ETH, and wait for it in the contract to exceed 32 ETH in total, and the total stake will be created. We will manage the user’s funds and protect the safety of the funds. In the future, after ETH2.0 is officially launched, we will open the withdrawal interface for users.

```
	function depositV2(bytes32 source) external payable
```


# 可乐矿池ETH质押合约

合约采用了开源项目[Openzeppelin](https://github.com/OpenZeppelin/openzeppelin-contracts)的可升级方案，以便于以太坊2.0正式上线时可通过升级合约来支持合约提现，同时也为了支持项目未来可扩展NFT、游戏等新功能。


[可乐矿池质押平台](https://www.kelepool.com/)

## 合约地址

代理合约：[0xACBA4cFE7F30E64dA787c6Dc7Dc34f623570e758](https://etherscan.io/address/0xACBA4cFE7F30E64dA787c6Dc7Dc34f623570e758#code)

逻辑合约：[0x2ba03c98fee1f538ff158766c2870196198e8e1d](https://etherscan.io/address/0x2ba03c98fee1f538ff158766c2870196198e8e1d#code)

## 主要功能

```
注意：

1.为了提高渠道质押金额的统计准确率，质押合约V2版本支持传递source渠道参数。

2.此版本新增合约调用方法（depoositV2/createValidatorV2）

3.不会影响之前已经对接了早期V1版本的第三方渠道，第三方渠道可按需升级。

4.仍使用V1版本或使用V2合约时未传递source，系统默认按注册地址方式统计收益及分红。

5.若使用V2版本需同时更新ABI及调用方法，合约地址不变，具体请参考下边调用合约的代码。

```



#### 大额质押

用户质押的数量大于32ETH，代币会立即质押到[ETH2.0官方存款合约地址](https://etherscan.io/address/0x00000000219ab540356cBB839Cbe05303d7705Fa)，同时为用户创建验证者。我们不会管理用户的资金，未来ETH2.0正式上线后，用户可通过存款凭证直接从以太坊官方渠道提现。

大额质押每个验证节点需要额外0.05ETH的手续费作为节点运营费用，如果你准备创建1个节点，需要转入32.05ETH，如果你准备创建3个节点，需要转入96.15ETH。

如果你希望通过调用合约来接入我们的质押平台，大额质押需要的这些参数，可通过ETH2.0官方CLI工具生成后获得：
https://github.com/ethereum/staking-deposit-cli


```
    function createValidatorV2(
        uint8 role, // 常量：1
        bytes32 source, // 渠道商标识
        bytes calldata pubkeys,// 验证者公钥
        bytes calldata withdrawal_credentials, // 存款凭证
        bytes calldata signatures,// 签名
        bytes32[] calldata deposit_data_roots//莫克尔树根
    ) external payable
```

#### 小额质押

用户质押的数量小于32ETH，你可以最低质押0.01ETH，等待合约中小额总质押数量累计超过32才会自动创建验证节点，我们会管理用户的资金及保护资金安全。未来ETH2.0正式上线后，我们会为用户开放提现接口。

```
	function depositV2(bytes32 source) external payable
```