## Rust Spotify API

## What does the app do?
The program lets the user to pass (as program arguments) a query and his Spotify token, and if those are valid, it will print the response from the official Spotify API.

## Programming Languages:
- Rust

## Frameworks & Libraries:
- futures - https://crates.io/crates/futures | https://docs.rs/futures/latest/futures/
- reqwest - https://crates.io/crates/reqwest | https://docs.rs/reqwest/latest/reqwest/
- tokio - https://tokio.rs | https://docs.rs/tokio/latest/tokio/
- serde - https://serde.rs | https://docs.rs/serde/latest/serde/
- serde-json - https://github.com/serde-rs/json

## Implementation:
Within the *data.rs* module there are defined the entity classes (structs):
```rust
#[derive(Serialize, Deserialize, Debug)]
pub struct Artist {
    name: String
}

#[derive(Serialize, Deserialize, Debug)]
pub struct Album {
    name: String,
    artists: Vec<Artist>,
}

#[derive(Serialize, Deserialize, Debug)]
pub struct Track {
    name: String,
    href: String,
    popularity: u32,
    album: Album,
}
```
And the DTOs:
```rust
pub mod dto {
    pub mod responses {
        use serde::{Deserialize, Serialize};

        #[derive(Serialize, Deserialize, Debug)]
        pub struct ListResponse<T> {
            pub items: Vec<T>
        }
    }
}
```
The *main.rs* file contains the logic: formatting the url, making the *GET* request and handling the response.