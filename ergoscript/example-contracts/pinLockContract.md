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
flowchart LR

  %% adjust margin-top: lines = 5; margin-top -12ex --> (lines-1) * 3 ex
  wallet("<table style='text-align:left; margin-top: -9; margin-bottom: 0;' > 
    <tr><th '><b>box in wallet</b></th></tr> 
    <tr><td >R0 <b>value</b>: 100.000.000</td></tr>     
    <tr><td >R1 <b>guard</b>: pk(user)</td></tr> 
    </table>  ")

  %% adjust margin-top: lines = 5; margin-top -12ex --> (lines-1) * 3 ex
  pinLockBox("<table style='text-align:left; margin-top: -9ex; margin-bottom: 0;' > 
    <tr><th '><b>pinLockBox</b></th></tr> 
    <tr><td >R0 <b>value</b>: 50.000.000</td></tr> 
    <tr><td >R1 <b>guard</b>: <br/>INPUTS(0).R4 == <br/>hashed(OUTPUTS(0).R4)</td></tr> 
    <tr><td >R4 <b>pin</b>: hashed(1293)</td></tr>     
    </table>  ")

  %% adjust margin-top: lines = 5; margin-top -12ex --> (lines-1) * 3 ex
  withdrawBox("<table style='text-align:left; margin-top: -9ex; margin-bottom: 0;' > 
    <tr><th '><b>withdrawBox</b></th></tr> 
    <tr><td >Guard: pk(user)</td></tr> 
    <tr><td >R4 <b>pin</b>: hashed(1293)</td></tr>
    </table>  ")


  TDeposit[["deposit"]]
  TWithdraw[["withdraw"]]


  wallet --> TDeposit --> pinLockBox --> TWithdraw --> withdrawBox

```