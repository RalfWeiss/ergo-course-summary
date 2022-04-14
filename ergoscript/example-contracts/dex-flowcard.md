# DEX dApp FlowCard

https://stackoverflow.com/questions/66631182/can-i-control-the-direction-of-flowcharts-in-mermaid

![DEX FlowCard](/images/ergo-dex-flowcard.png)

The following diagram fully (and formally) specifies all of the five transactions that must be created **off-chain** by the DEX dApp. It also specifies all of the spending conditions that should be verified **on-chain**.


```mermaid
flowchart LR

  %% Guard pkBuyer
  subgraph pkBuyer["<b>pk(buyer)</b>"]
    direction TB

    %% the margin-top reduction is only necessary for VSCode not for Github
    balance("<table style='text-align:left; margin-top: -2ex; margin-bottom: 0;' > 
    %% balance("<table style='text-align:left; margin-bottom: 0;' > 
      <tr><th '><b>balance</b></th></tr> 
      <tr><td style='color:red'>E: ERG</td></tr> 
      </table>  ")

    %% adjust margin-top: lines = 4; margin-top -9ex --> (lines-1) * 3 ex
    %% refund("<table style='text-align:left; margin-top: -9ex; margin-bottom: 0;' > 
    refund("<table style='text-align:left; margin-bottom: 0;' > 
      <tr><th '><b>refund</b></th></tr> 
      <tr><td style='color:red'>ergAmt: ERG</td></tr> 
      </table>  ")

  end

  TBo[["Buy Order"]]

  %% Guard buyOrder
  subgraph buyOrder["<b>buyOrder</b>"]
    direction TB

    %% adjust margin-top: lines = 4; margin-top -9ex --> (lines-1) * 3 ex
    bid("<table style='text-align:left; margin-top: -9ex; margin-bottom: 0;' > 
      <tr><th '><b>bid</b></th></tr> 
      <tr><td style='color:red'>E: ERG</td></tr> 
      </table>  ")

  end


  balance ---> TBo
  TBo --> bid
  TBo --> refund

```


## Buy Order Transaction

A buyer creates a `Buy Order` transaction. The transaction spends `E` amount of ERGs (which we will write `E: ERG`) from one or more boxes in the `pk(buyer)` wallet. The transaction creates a `bid` box with `ergAmt: ERG` protected by the `buyOrder` script. 

The `change` box is created to make the input and output sums of the transaction balanced.

```mermaid
flowchart LR

  %% adjust margin-top: lines = 5; margin-top -12ex --> (lines-1) * 3 ex
  %% balance("<table style='text-align:left; margin-top: -12ex; margin-bottom: 0;' > 
  balance("<table style='text-align:left; margin-top: -6ex; margin-bottom: 0;' > 
    <tr><th '><b>balance</b></th></tr> 
    <tr><td >Guard: pk(buyer)</td></tr> 
    <tr><td style='color:red'>E: ERG</td></tr> 
    </table>  ")

  %% adjust margin-top: lines = 5; margin-top -12ex --> (lines-1) * 3 ex
  change("<table style='text-align:left; margin-top: -12ex; margin-bottom: 0;' > 
    <tr><th '><b>change</b></th></tr> 
    <tr><td >Guard: pk(buyer)</td></tr> 
    <tr><td style='color:red'>E - ergAmt: ERG</td></tr> 
    </table>  ")


  TBo[["Buy Order"]]


  %% adjust margin-top: lines = 5; margin-top -12ex --> (lines-1) * 3 ex
  bid("<table style='text-align:left; margin-top: -12ex; margin-bottom: 0;' > 
    <tr><th '><b>bid</b></th></tr> 
    <tr><td >Guard: buyOrder</td></tr> 
    <tr><td style='color:red'>ergAmt: ERG</td></tr> 
    </table>  ")

  balance ---> TBo
  TBo ---> bid
  TBo ---> change

```

## Cancel Buy, Cancel Sell Transactions

At any time, the `buyer` can cancel the order by sending `CancelBuy` transaction. The transaction should satisfy the guarding `buyOrder` contract which protects the `bid` box. 

As you can see on the diagram, both the `Cancel` and the `Swap` transactions can spend the `bid` box. 

When a box has spending alternatives (or spending paths) then each alternative is identified by a unique name prefixed with `!` (`!cancel` and `!swap` for the `bid` box). Each alternative path has specific spending conditions. 

In our example, when the `Cancel Buy` transaction spends the `bid` box the `?buyer` condition should be satisfied, which we read as “**the signature for the buyer address should be presented in the transaction**”. Therefore, only buyer can cancel the buy order. This “signature” condition is only required for the `!cancel` alternative spending path and not required for `!swap`.

```mermaid
flowchart LR

  %% adjust margin-top: lines = 5; margin-top -12ex --> (lines-1) * 3 ex
  bid("<table style='text-align:left; margin-top: -12ex; margin-bottom: 0;' > 
    <tr><th '><b>bid</b></th></tr> 
    <tr><td >Guard: buyOrder</td></tr> 
    <tr><td style='color:red'>ergAmt: ERG</td></tr> 
    </table>  ")

  %% adjust margin-top: lines = 5; margin-top -12ex --> (lines-1) * 3 ex
  refund("<table style='text-align:left; margin-top: -12ex; margin-bottom: 0;' > 
    <tr><th '><b>refund</b></th></tr> 
    <tr><td >Guard: pk(buyer)</td></tr> 
    <tr><td style='color:red'>ergAmt: ERG</td></tr> 
    </table>  ")


  T[["Cancel Buy"]]

  bid -- "!cancel<br/>?buyer<br/><br/><br/>" ---> T
  T ---> refund

```

