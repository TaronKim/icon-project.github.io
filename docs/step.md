# Transaction Fee

Transaction fee is calculated as `usedStep * stepPrice`.

- Where `stepPrice` is the ICX exchange rate, and `usedStep` is the sum of `stepCost` for each action processed in the transaction.

- If `usedStep` reaches the `stepLimit` before finishing the execution, the transaction will fail with `out of step` error, but the amount of `stepLimit` is deducted from your balance.  

- Before executing your transaction, your account must hold at least `stepLimit * stepPrice` amount of ICX. If you do not have sufficient ICX, your transaction will fail immediately.

You can query the `stepCost` of each action, the maximum possible `stepLimit` value you can set, and the `stepPrice`. 

- SCORE Address - cx0000000000000000000000000000000000000001
- [getStepCost](https://github.com/icon-project/governance/blob/master/README.md#getstepcosts)
- [getMaxStepLimit](https://github.com/icon-project/governance/blob/master/README.md#getmaxsteplimit)
- [getStepPrice](https://github.com/icon-project/governance/blob/master/README.md#getstepprice)

```bash
root@b65c6a4cccf8:/tbears# cat stepcost.json 
{
    "jsonrpc": "2.0",
    "id": 1,
    "method": "icx_call",
    "params": {
        "to": "cx0000000000000000000000000000000000000001",
        "dataType": "call",
        "data": {
            "method": "getStepCosts"
        }
    }
}
root@b65c6a4cccf8:/tbears# tbears call -u https://bicon.net.solidwallet.io/api/v3 stepcost.json
response : {
    "jsonrpc": "2.0",
    "result": {
        "default": "0x186a0",
        "contractCall": "0x61a8",
        "contractCreate": "0x3b9aca00",
        "contractUpdate": "0x5f5e1000",
        "contractDestruct": "-0x11170",
        "contractSet": "0x7530",
        "get": "0x0",
        "set": "0x140",
        "replace": "0x50",
        "delete": "-0xf0",
        "input": "0xc8",
        "eventLog": "0x64",
        "apiCall": "0x0"
    },
    "id": 1
}
```

```bash
root@b65c6a4cccf8:/tbears# cat maxsteplimit.json 
{
    "jsonrpc": "2.0",
    "id": 2,
    "method": "icx_call",
    "params": {
        "to": "cx0000000000000000000000000000000000000001",
        "dataType": "call",
        "data": {
            "method": "getMaxStepLimit",
            "params": {
                "contextType": "invoke"
            }
        }
    }
}
root@b65c6a4cccf8:/tbears# tbears call -u https://bicon.net.solidwallet.io/api/v3 maxsteplimit.json 
response : {
    "jsonrpc": "2.0",
    "result": "0x9502f900",
    "id": 2
}
```

```bash
root@07dfee84208e:/tbears# cat stepprice.json 
{
    "jsonrpc": "2.0",
    "id": 3,
    "method": "icx_call",
    "params": {
        "to": "cx0000000000000000000000000000000000000001",
        "dataType": "call",
        "data": {
            "method": "getStepPrice"
            }
        }
    }
}
root@07dfee84208e:/tbears# tbears call -u https://bicon.net.solidwallet.io/api/v3 stepprice.json 
response : {
    "jsonrpc": "2.0",
    "result": "0x2540be400",
    "id": 3
}
```
