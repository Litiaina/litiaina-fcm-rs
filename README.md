
# Firebase Cloud Messaging API v1 Rust Crate

This Rust crate provides a convenient way to send notifications using Firebase Cloud Messaging (FCM) API v1. It leverages async/await for asynchronous operations and supports loading service account credentials from a JSON file.

## Installation

Add this crate to your `Cargo.toml`:

```toml
[dependencies]
fcm-rs = { git = "https://github.com/Litiaina/fcm-rs", branch = "main" }
```

## Usage

Below is an example of how to use this crate to send a notification:

```rust
use fcm_rs::{ client::FcmClient, models::{ Message, Notification } };

#[tokio::main]
async fn main() -> Result<(), Box<dyn std::error::Error>> {
    let service_account_path = "path/to/service_account";

    // Create a new FCM client
    let client = FcmClient::new(service_account_path).await?;

    // Define the message with the target device token and notification details
    let message = Message {
        token: Some(token),
        notification: Some(Notification {
            title: Some(title.clone()),
            body: Some(body.clone()),
        }),
        data: None,
        android: Some(AndroidConfig {
            priority: Some("high".into()),
        }),
        apns: Some(ApnsConfig {
            headers: Some(ApnsHeaders {
                apns_priority: Some("10".into()),
            }),
        }),
    };

    // Send the message and handle the response
    let response = client.send(message).await?;
    println!("FCM response: {:?}", response);

    Ok(())
}
```

## Contribution

Contributions are welcome! Feel free to submit issues or pull requests.

## Contact

For any queries or suggestions, please open an issue on the GitHub repository.
