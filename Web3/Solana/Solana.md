## Data Model on Solana

![[Pasted image 20260209004900.png]]

## Solana Contract

``` rust-lib.rs
pub fn solana_counter (
	program_id: PublicKey,
	accounst: [AccountInfo],
	instruction_data: [u8]
) {}
```

Every Smart Contract developer let the users interact with the program using 3 arguments as shown in the code snippet above.

## Flow of Solana Contract Program

Initially, We know that there are `Data Models on Solana`.
`Data Model` says-
- there are `User Accounts - wallets` - where `people's Solana` is present,
- there will be `Smart Contracts` that the user will deploy, and
- there are `Data Accounts` where the final data is stored.

When the user wants to interact with some contract - basically telling that contract to do something, `User` will give us `an array of accounts` and they will also `give some bunch of bytes` - which we call the `Instruction Data` 