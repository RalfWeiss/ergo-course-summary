# Class 1

[Video](https://youtu.be/pMVfTEgqyTc)

- ErgoScript Class 1
  - Txs
  - Examples
  - GuardScript / ErgoScript
  - Technical Knowledge

## Transaction

```mermaid
flowchart LR
  %% Comment
    U1(Input-Box 1)
    U2(Input-Box 2)
    U3(Input-Box 3)

    U4(Output-Box 1)
    U5(Output-Box 2)
    U6(Output-Box 3)    

    T1[[Transaction]]:::transaction

    U1 & U2 & U3 --> T1
    T1 ---> U4 & U5 & U6
    U6 -.- I(Mining Fee):::comment
  %% Styling
    classDef transaction fill:#f9f,stroke:#333,stroke-width:4px;
    classDef comment fill:#f333,stroke-dasharray: 5 5;
```

- models the outputs
- if all input boxes can be spent then the `Tx` goes through
- all Inputs must been spent



```mermaid
flowchart LR  
  T1[[Set Pin]]
  T2[[Unlock Pin]]
  T3[[Change Pin]]

  U1[Box 1] --> T1 --> U2
  U2[<b>Box 2</b><p align='left'>R.4 = 1234</p>]

  U2 --> T2 --> B3[Box 3]
  X[<p align='left'><b>Guard:</b><br/> Self.R4 == Output.R4</p>] 
  X -.- U2

  U2 --> T3 --> U3
  U3[<b>Box 2</b><p align='left'>R.4 = 5678</p>]

```