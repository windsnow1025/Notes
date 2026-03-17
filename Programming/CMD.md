# CMD

| Instructions                   | Code                                                                                                     |
|--------------------------------|----------------------------------------------------------------------------------------------------------|
| List Subfiles                  | dir                                                                                                      |
| IP configuration               | ipconfig (/all)                                                                                          |
| Refresh Local DNS              | ipconfig /flushdns                                                                                       |
| Disable Temporary IPv6 Address | netsh interface ipv6 set privacy state=disable                                                           |
| DNS Lookup                     | nslookup [dns_server]                                                                                    |
| Network Reset                  | netsh winsock reset                                                                                      |
| View Excluded Port             | netsh interface ipv4 show excludedportrange protocol=tcp                                                 |
| Add Excluded Port              | netsh int ipv4 add excludedportrange protocol=tcp startport=<start_port> numberofports=<number_of_ports> |
| View Port Usage                | netstat -ano\|findstr :[port]                                                                            |
| Print Routing Table            | route print                                                                                              |
| Delete Service                 | sc delete                                                                                                |
| System Scan                    | sfc /scannow                                                                                             |
