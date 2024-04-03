# Create a Windows network trace

I usually use tcpdump on *nix machines and used to use wireshark on Windows but this would mean that Wireshark would need to get installed.

You can use `netsh` to capture the network traffic.

```
netsh trace start capture=yes maxSize=4096 tracefile=c:\temp\trace.etl level=verbose
netsh trace stop
```

Once you have your trace file you can convert it to something wireshark understands by downloading the Microsoft provided `etl2pcapng.exe` from [GitHub](https://github.com/microsoft/etl2pcapng)

Then convert the `trace.etl` file.

```
etl2pcapng trace.etl
```

This will product a `trace.pcapng` file that you can open up with Wireshark
