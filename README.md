# Multithreaded TCP Client–Server

A Python client–server application over TCP sockets. The server handles **several clients at the same time**, one thread per client. Each client sends a power expression such as `3^5`; the server computes the result and sends it back, and the client measures the **round-trip time (RTT)** of every request.

Built for a Computer Networks course at Imam Mohammad Ibn Saud Islamic University.

## Features

- **Concurrent server:** a new thread for each connected client
- **Thread-safe shared state:** the count of active clients is updated under a `threading.Lock`
- **Input validation:** malformed requests get a clear error message instead of crashing the server
- **Graceful disconnect:** the client sends `Finish` to close the connection, and the server cleans up
- **RTT measurement:** the client prints the response time of each request in milliseconds

## Example

```
Enter expression (format: base^exponent), or type 'Finish' to exit: 3^5
Result from server: 3^5 = 243  |  RTT: 1.204 ms

Enter expression (format: base^exponent), or type 'Finish' to exit: hello
Result from server: x ERROR: send as: base^exponent (e.g., 3^5)  |  RTT: 0.981 ms
```

## How to run

Requires Python 3, no extra packages.

1. Start the server:
   ```bash
   python Server.py
   ```
2. In `Client.py`, set `HOST` to the server's IP address (use `127.0.0.1` when both run on the same computer).
3. Start one or more clients, each in its own terminal:
   ```bash
   python Client.py
   ```

The server listens on port `5000`.

## Files

| File | Role |
|---|---|
| `Server.py` | accepts connections and serves each client in its own thread |
| `Client.py` | sends expressions, prints results and RTT |

## Team

Built with a classmate. **My contribution:** co-developed the server's multithreading and the request handling and validation.
