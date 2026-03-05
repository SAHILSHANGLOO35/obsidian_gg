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

When the user wants to interact with some contract - basically telling that contract to do something, `User` will give us `an array of accounts` and they will also `give some bunch of bytes` - which we call the `Instruction Data`.

## Anchor

![[Pasted image 20260221194955.png]]

## Macros in Anchor

##### The `#[program]` Module:

```rust
pub mod calculator {
	use super::*;
}
```

The `#[program]` macro marks this module as the **entry point container**. Anchor scans every `pub fn` inside this module and treats them as instruction handlers. `use super::*` brings in everything from the outer scope (like our account structs) so we can reference them inside the functions.

#### The Data Account

```rust
#[account]
struct DataShape {
	pub num: u32,
}
```

The `#[account]` macro does several critical things:
- First, it implements **serialization/deserialization** using Borsh (Binary Object Representation Serializer for Hashing) so our struct can be written to and read from Solana's raw byte storage.
- Second, it attaches an 8-byte **discriminator** (a hash of the struct name) to the front of the stored data — this lets Anchor verify at runtime that an account actually contains a `DataShape` and not some other account type, preventing type confusion attacks.
- Third, it implements the `AccountSerialize` and `AccountDeserialize` traits Anchor needs internally.

##### The `Initialize` Context

```rust
#[derive(Accounts)]
pub struct Initialize<'info> {}
```

