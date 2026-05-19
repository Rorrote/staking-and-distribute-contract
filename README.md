# Staking and Distribution Contracts — ELPESOQUEVALE Ecosystem

> Parte del ecosistema [ELPESOQUEVALE](https://zora.co/elpesoquevale) | Token: [RORROCOIN](https://zora.co/RORROCOIN) | Red: Base  
> Mantenido por [@Rorrote](https://github.com/Rorrote) — Conductor del podcast ELPESOQUEVALE

---

## ⚠️ Aviso de Seguridad

Las siguientes wallets están **comprometidas** y **NO deben usarse**:
- ~~`0x985fa00D8eA4a43a029649e6167373Df10E30BB8`~~ — ⛔ COMPROMETIDA
- ~~`0x1edf70cd95c78069c96465febf08231240c78058`~~ — ⛔ COMPROMETIDA

**✅ Wallet segura activa (usar siempre esta):**
```
0xc19949ac844495cD60887Cbd276D292a59e5379C
```

**Acción pendiente:** Transferir ownership de `Rebase.sol` y `Splitter.sol` a la wallet segura via [BaseScan Write Contract](https://basescan.org/address/0x6bc86cb06db133e939cc9d3cd27b6b34772dd0cb#writeContract).

---

## 📄 Contratos Desplegados en Base

| Contrato | Dirección | BaseScan |
|----------|-----------|----------|
| `Rebase.sol` (Staking) | `0x89fA20b30a88811FBB044821FEC130793185c60B` | [Ver](https://basescan.org/address/0x89fa20b30a88811fbb044821fec130793185c60b) |
| `Splitter.sol` (Distribution) | `0x6bc86cb06db133e939cc9d3cd27b6b34772dd0cb` | [Ver](https://basescan.org/address/0x6bc86cb06db133e939cc9d3cd27b6b34772dd0cb) |

---

## 🪙 Tokens del Ecosistema

| Token | Símbolo | Contrato | Zora |
|-------|---------|----------|------|
| RORROCOIN | RORROCOIN | [`0x41ec37...`](https://basescan.org/token/0x41ec37f323dd43ec33d612a2750d1874fb652b07) | [zora.co/RORROCOIN](https://zora.co/RORROCOIN) |
| ELPESOQUEVALE | EPV | [`0x3cc388...`](https://basescan.org/token/0x3cc38833fc7ad6e374285c144792700c9e4ecfca) | [zora.co/elpesoquevale](https://zora.co/elpesoquevale) |
| PEXOCOIN | PEXO | `pexocoin.cb.id` | — |
| PESOMEXICO | PESO | `pesomexico.cb.id` | — |

---

## Mechanism Explanation

### 1. Rebase Contract (`Rebase.sol`)

The `Rebase` contract serves as the primary staking hub. It allows users to stake ERC20 tokens or ETH, and in return, they receive a corresponding amount of "reTokens" (rebasing tokens).

*   **Staking Tokens:** Users can stake any ERC20 token or native ETH (which is converted to WETH internally). When tokens are staked, the `Rebase` contract interacts with a dynamically created `ReToken` contract specific to the staked token. This `ReToken` contract then mints new `reTokens` to the user, representing their staked position.
*   **Dynamic `ReToken` Creation:** For each unique token staked, the `Rebase` contract deploys a minimal proxy (`cloneDeterministic`) of the `ReToken` contract. This ensures that each staked token has its own dedicated `reToken` that tracks its rebasing logic.
*   **Application Integration:** The `Rebase` contract allows for integration with various "applications" (represented by smart contract addresses). When a user stakes, they specify an `app` address. The `Rebase` contract then calls the `onStake` function on the specified `app` contract, notifying it of the new stake.
*   **Unstaking Tokens:** Users can unstake their tokens, which involves burning the `reTokens` and transferring the original staked tokens back to the user. Similarly, the `onUnstake` function on the `app` contract is called.
*   **Restaking Tokens:** Users can transfer their staked position from one application to another without fully unstaking and restaking.

### 2. Splitter Contract (`Splitter.sol`)

The `Splitter` contract is responsible for receiving reward tokens and distributing them proportionally to users who have staked through the `Rebase` contract.

*   **Reward Token:** Initialized with a specific `rewardToken` (an ERC20 token) that it will distribute.
*   **Distributors:** Only authorized `distributors` (addresses added by the contract owner) can send `rewardToken` to the `Splitter` contract for distribution.
*   **`StakeTracker` Integration:** Uses a `StakeTracker` contract to keep track of user stakes and reward distributions over time via snapshots.
*   **Claiming Rewards:** Users can `claim` their accumulated rewards proportionally to their stake at each snapshot.

### 3. StakeTracker Contract (`StakeTracker.sol`)

A specialized ERC20Snapshot token that acts as a ledger for tracking user stakes and reward allocations.

---

## Usage Instructions

### Deployment

1.  **Deploy `Rebase.sol`:** Deploy the `Rebase` contract. Note the address of the deployed `Rebase` contract.
    *   Deployed on Base: [`0x89fA20b30a88811FBB044821FEC130793185c60B`](https://basescan.org/address/0x89fa20b30a88811fbb044821fec130793185c60b)
2.  **Deploy `Splitter.sol`:** Deploy the `Splitter` contract, providing the `stakeToken` and `rewardToken` addresses as constructor arguments.
    *   Deployed on Base: [`0x6bc86cb06db133e939cc9d3cd27b6b34772dd0cb`](https://basescan.org/address/0x6bc86cb06db133e939cc9d3cd27b6b34772dd0cb)

### Staking Tokens (via `Rebase` contract)

To stake ERC20 tokens:

1.  Approve the `Rebase` contract to spend your ERC20 tokens:
    ```solidity
    IERC20(YOUR_TOKEN_ADDRESS).approve(REBASE_CONTRACT_ADDRESS, AMOUNT_TO_STAKE);
    ```
2.  Call the `stake` function on the `Rebase` contract:
    ```solidity
    Rebase.stake(YOUR_TOKEN_ADDRESS, AMOUNT_TO_STAKE, SPLITTER_CONTRACT_ADDRESS);
    ```

To stake ETH:
```solidity
Rebase.stakeETH(SPLITTER_CONTRACT_ADDRESS) payable;
```

### Unstaking Tokens

```solidity
Rebase.unstake(YOUR_TOKEN_ADDRESS, AMOUNT_TO_UNSTAKE, SPLITTER_CONTRACT_ADDRESS);
Rebase.unstakeETH(AMOUNT_TO_UNSTAKE, SPLITTER_CONTRACT_ADDRESS);
```

### Distributing Rewards (via `Splitter` contract)

1.  Owner adds distributor (use wallet segura: `0xc19949ac844495cD60887Cbd276D292a59e5379C`):
    ```solidity
    Splitter.addDistributor(0xc19949ac844495cD60887Cbd276D292a59e5379C);
    ```
2.  Approve and split:
    ```solidity
    IERC20(REWARD_TOKEN_ADDRESS).approve(SPLITTER_CONTRACT_ADDRESS, AMOUNT_OF_REWARD);
    Splitter.split(AMOUNT_OF_REWARD);
    ```

### Claiming Rewards

```solidity
Splitter.claim(YOUR_RECEIVING_ADDRESS, MAX_SNAPSHOTS_TO_PROCESS);
Splitter.getUnclaimedEarnings(YOUR_ADDRESS, MAX_SNAPSHOTS_TO_PROCESS);
```

---

## 🌐 Ecosystem Links

| Plataforma | URL |
|------------|-----|
| Farcaster | [farcaster.xyz/rrorrocoin.base.eth](https://farcaster.xyz/rrorrocoin.base.eth) |
| Base App | [base.app/profile/rorrocoin](https://base.app/profile/rorrocoin) |
| Dune Analytics | [dune.com/rorrocoin](https://dune.com/rorrocoin) |
| Twitter/X | [@RORROCOIN](https://x.com/RORROCOIN) / [@ELPESOQUEVALE](https://x.com/ELPESOQUEVALE) |
| TikTok | [@rorrocoin](https://www.tiktok.com/@rorrocoin) |
| Discord | ELPESOQUEVALE |
| Panel de Control | [agente-publicidad-app-131ce858.base44.app](https://agente-publicidad-app-131ce858.base44.app) |
| Status | [STATUS.md](./STATUS.md) |

---

> **ELPESOQUEVALE** — Contra la desigualdad social. Únete y apoya.
