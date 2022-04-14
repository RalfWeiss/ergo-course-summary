# Pin Lock Contract

## depositTransaction

- input boxes 

inputs = selectUnspentBoxes(toSpend = userFunds)

- output box : pinLockBox 

| meaning      | Register | content                               |
| ------------ | -------- | ------------------------------------- |
| value        | R1       | userFunds/2                           |
| guard script | R2       | INPUTS(0).R4 == hashed(OUTPUTS(0).R4) |
|              | R4       | hashedPin                             |

- depositTransaction

```
val depositTransaction = Transaction(
      inputs       = userParty.selectUnspentBoxes(toSpend = userFunds),
      outputs      = List(pinLockBox),
      fee          = MinTxFee,
      sendChangeTo = userParty.wallet.getAddress
    )
```



```mermaid
flowchart TD

  %% adjust margin-top: lines = 5; margin-top -12ex --> (lines-1) * 3 ex
  walletBox1("<table style='text-align:left; margin-top: -9ex; margin-bottom: 0;' > 
    <tr><th><b>box in wallet: buyer #1</b></th></tr> 
    <tr><td>R0 <b>value</b>: 100.000.000 nanoERGs</td></tr>     
    <tr><td>R1 <b>guard</b>: pk(buyer)</td></tr> 
    <tr><td>R2 <b>tokens</b>: none</td></tr> 
    </table>")

  %% adjust margin-top: lines = 5; margin-top -12ex --> (lines-1) * 3 ex
  pinLockBox("<table style='text-align:left; margin-top: -10ex; margin-bottom: 0;' > 
    <tr><th><b>pinLockBox #2</b></th></tr> 
    <tr><td >R0 <b>value</b>: 50.000.000 nanoERGs</td></tr> 
    <tr><td >R1 <b>guard</b>: <br/><pre>INPUTS(0).R4 == <br/>hashed(OUTPUTS(0).R4)</pre></td></tr> 
    <tr><td>R2 <b>tokens</b>: none</td></tr> 
    <tr><td >R4 <b>pin</b>: hashed(1293)</td></tr>     
    </table>  ")

  walletBox2("<table style='text-align:left; margin-top: -9ex; margin-bottom: 0;' > 
    <tr><th><b>box in wallet: buyer #3</b></th></tr> 
    <tr><td>R0 <b>value</b>: 49.000.000 nanoERGs</td></tr>     
    <tr><td>R1 <b>guard</b>: pk(buyer)</td></tr> 
    <tr><td>R2 <b>tokens</b>: none</td></tr> 
    </table>")

  %% adjust margin-top: lines = 5; margin-top -12ex --> (lines-1) * 3 ex
  withdrawBox("<table style='text-align:left; margin-top: -9ex; margin-bottom: 0;' > 
    <tr><th><b>withdrawBox #4</b></th></tr> 
    <tr><td>R0 <b>value</b>: 49.000.000 nanoERGs</td></tr> 
    <tr><td>R1 <b>guard</b>: pk(buyer)</td></tr> 
    <tr><td>R2 <b>tokens</b>: none</td></tr>     
    <tr><td>R4 <b>pin</b>: 1293</td></tr>
    </table>  ")


  Tx1[["deposit"]]
  Tx2[["withdraw"]]


  walletBox1 --> Tx1
  Tx1 --> pinLockBox
  Tx1 --> walletBox2 
  pinLockBox --> Tx2 --> withdrawBox

```