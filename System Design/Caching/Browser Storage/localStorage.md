# localStorage

- `localStorage` is a web API that allows websites to store key-value pairs in browser's local storage.
- The data persists even after browser window is closed.
- The data is stored on the client-side, and it is accessible only within the same origin(i.e., domain, protocol and port)
- Typically `localStorage` allows up to 5-10 MB of data per domain.
- Data is stored as strings. Non-string data must be serialized (e.g., using `JSON.stringify()`) and deserialized (e.g., using `JSON.parse()`)

## API Methods

| Method / Property     | Description                                                  |
| --------------------- | ------------------------------------------------------------ |
| `setItem(key, value)` | Store a key-value pair in `localStorage`                     |
| `getItem(key)`        | Retrieve the value for a given key                           |
| `removeItem(key)`     | Remove a key-value pair from `localStorage`                  |
| `clear()`             | Clear all the items in `localStorage` for the current origin |
| `length`              | Get the number of items in `localStorage`                    |

## Use Cases

1. **Session Data**: Storing user preferences, authentication tokens, or UI state across page reloads or sessions
2. **User Preferences**: For example, theme settings, language preferences and other non-sensitive settings
3. **Caching**: Storing data like JSON responses, other assets for offline usage or faster load times.

## Limitations and Challenges

1. **Storage Size**: Since `localStorage` has size limit of 5-10 MB, it may not be suitable for larger datasets.
2. **No Expiration**: Data stored in `localStorage` doesn't have and expiration mechanism. You have to manually manage and clear old data.
3. **Vulnerable to Browser Clearing**: Users can clear `localStorage` manually or via browser settings, which can lead to data loss.
4. **Not Secure**: Data stored is accessible by any script on the same domain, which could be security risk, especially with sensitive data (e.g., authentication tokens or user data). You should not store sensitive information in `localStorage`
5. **No Cross-Browser/Device Sync**: `localStorage` data is specific to the browser on a specific device. It doesn't sync across devices or browsers.

## Security Concerns

1.

## Best Practices
