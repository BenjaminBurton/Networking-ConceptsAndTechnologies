# enterprise network architectural design


### An Architectural Design starting from scratch

1. Having a Load Balancer before the firewall

```js
          PC -> Load Balancer -> Firewall -> Internal Network
                                       |
                                       +--> Switch -> Servers
                                       |
                                       +--> Router -> Cloud (Internet)

```

2. Having a Load Balancer after the firewall

```js
          PC -> Firewall -> Load Balancer -> Internal Network
                                       |
                                       +--> Switch -> Servers
                                       |
                                       +--> Router -> Cloud (Internet)
```

## 3 Cloud Providers

### CompuCloud

![Screenshot](CompuCloud.png)


### AWS Cloud

![Screenshot](AWS.png)
### Azure Cloud

![Screenshot](Azure.png)

editing in progress
