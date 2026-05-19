# 📊 Estado del Ecosistema ELPESOQUEVALE / RORROCOIN
**Última actualización:** 2026-05-19  
**Mantenido por:** RORROCOIN ([@Rorrote](https://github.com/Rorrote))

---

## 🪙 Tokens

| Token | Símbolo | Red | Tipo | Contrato | Estado |
|-------|---------|-----|------|----------|--------|
| RORROCOIN | RORROCOIN | Base | Reward | [`0x41ec37f323dd43ec33d612a2750d1874fb652b07`](https://basescan.org/token/0x41ec37f323dd43ec33d612a2750d1874fb652b07) | ✅ Activo |
| ELPESOQUEVALE | EPV | Base | Utility | [`0x3cc38833fc7ad6e374285c144792700c9e4ecfca`](https://basescan.org/token/0x3cc38833fc7ad6e374285c144792700c9e4ecfca) | ✅ Activo |
| PEXOCOIN | PEXO | Base | Utility | `pexocoin.cb.id` | ✅ Activo |
| PESOMEXICO | PESO | Base | Utility | `pesomexico.cb.id` | ✅ Activo |

### Zora
- RORROCOIN: https://zora.co/RORROCOIN
- ELPESOQUEVALE: https://zora.co/elpesoquevale

---

## 📄 Smart Contracts Desplegados

| Contrato | Tipo | Red | Dirección | Estado |
|----------|------|-----|-----------|--------|
| `Rebase.sol` | Staking | Base | [`0x89fA20b30a88811FBB044821FEC130793185c60B`](https://basescan.org/address/0x89fA20b30a88811FBB044821FEC130793185c60B) | ✅ Desplegado |
| `Splitter.sol` | Distribution | Base | [`0x6bc86cb06db133e939cc9d3cd27b6b34772dd0cb`](https://basescan.org/address/0x6bc86cb06db133e939cc9d3cd27b6b34772dd0cb) | ✅ Desplegado |
| `Ownable.sol` | Helper | Base | — | ✅ Desplegado |
| `mini-app` | Frontend | World App / Base | — | ⏳ Pendiente |

---

## 🔐 Ajustes de Seguridad — Acciones Realizadas

### ⚠️ Incidente: Wallets Comprometidas
Se detectó que las siguientes wallets tuvieron exposición de llave privada y fueron marcadas como **NO USAR**:

| Wallet | Estado |
|--------|--------|
| `0x985fa00D8eA4a43a029649e6167373Df10E30BB8` | ⛔ COMPROMETIDA |
| `0x1edf70cd95c78069c96465febf08231240c78058` | ⛔ COMPROMETIDA |

### ✅ Nueva Wallet Segura
Todos los activos, ownership de contratos y operaciones futuras deben usar:

```
0xc19949ac844495cD60887Cbd276D292a59e5379C
```

### 📋 Checklist de Migración de Seguridad

- [ ] Transferir ownership de `Rebase.sol` a nueva wallet → [Write Contract en BaseScan](https://basescan.org/address/0x89fA20b30a88811FBB044821FEC130793185c60B#writeContract)
- [ ] Transferir ownership de `Splitter.sol` a nueva wallet → [Write Contract en BaseScan](https://basescan.org/address/0x6bc86cb06db133e939cc9d3cd27b6b34772dd0cb#writeContract)
- [ ] Agregar nueva wallet como distribuidor autorizado en `Splitter.sol`
- [ ] Vaciar tokens RORROCOIN y ELPESOQUEVALE de wallets comprometidas
- [ ] Vaciar ETH/BASE de wallets comprometidas

### Pasos para transferir ownership (Rebase y Splitter)
1. Abrir el contrato en BaseScan → Write Contract
2. Conectar la wallet actual owner (comprometida) en MetaMask
3. Ejecutar `transferOwnership` con la nueva dirección: `0xc19949ac844495cD60887Cbd276D292a59e5379C`
4. Confirmar la transacción
5. Verificar el nuevo owner con `owner()` en Read Contract

---

## 🌐 Identidades y Canales

| Plataforma | Handle / URL |
|------------|-------------|
| Farcaster | [rrorrocoin.base.eth](https://farcaster.xyz/rrorrocoin.base.eth) |
| Dune Analytics | [dune.com/rorrocoin](https://dune.com/rorrocoin) |
| Base App | [base.app/profile/rorrocoin](https://base.app/profile/rorrocoin) |
| Twitter/X | [@RORROCOIN](https://x.com/RORROCOIN) / [@ELPESOQUEVALE](https://x.com/ELPESOQUEVALE) |
| TikTok | [@rorrocoin](https://www.tiktok.com/@rorrocoin) |
| Instagram | @RORROCOIN / @ELPESOQUEVALE / @ELRORROTE1 |
| Discord | ELPESOQUEVALE |
| LinkedIn | RORROCOIN19 |

---

## 🔗 ENS & Coinbase IDs

| ID | Red |
|----|-----|
| `rrorrocoin.base.eth` | Base / Farcaster |
| `rorrocoin.farcaster.eth` | Farcaster |
| `aid2house.cb.id` | Coinbase |
| `elpesoquevale.cb.id` | Coinbase |
| `pexocoin.cb.id` | Coinbase |
| `pesomexico.cb.id` | Coinbase |

---

> Panel de control visual: [agente-publicidad-app-131ce858.base44.app](https://agente-publicidad-app-131ce858.base44.app)
