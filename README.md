# clone-lin-maker-pot-drip

Experimental uint64-scale LIN clone of Maker/Sky `Pot.drip` (Dai Savings Rate
chi accumulator). **Proofs live in** [kbelludoo/lin-open](https://github.com/kbelludoo/lin-open).

- Class: EXPERIMENTAL (RAY' = 1e9; mainnet RAY = 1e27 does not fit i64)
- Upstream: [makerdao/dss](https://github.com/makerdao/dss) `src/pot.sol` at
  `fa4f6630afb0624d04a003e920b0d71a00331d98` (AGPL-3.0-or-later). Hash-pinned,
  **not vendored**.
- LIN: `src/lin_maker_pot_drip.lin` — explicit `(dsr, chi, now, rho)`, 128-bit
  rpow (half-up) and floor rmul, fail-closed on `now < rho` and overflow.
- C11 oracle: `test/oracles/maker_pot_drip_c11.c` (`__int128` XOR portable limbs)

Named goldens (`dsr = RAY' + 1e6`): dt=2 drip **1002001000** vs linear
**1002000000**; dt=10 **1010045120** vs **1010000000**.

Not claimed: uint256 / sDAI / sUSDS / vat.ilks parity, TVL, replacing Maker/Sky/EVM.
Reproduce proofs in lin-open: `make maker-pot-drip-proof`
