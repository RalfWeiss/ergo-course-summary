# adacapo21/plutusPioneerProgram/PLUTUS PIONEER PROGRAM COHORT 2

Based on: [Oracle Core](https://github.com/adacapo21/plutusPioneerProgram/blob/main/week6Documentation.md)

Attempt to reproduce the diagram using `mermaid` syntax.

## Oracle

```mermaid
flowchart LR  
  %% Definition of Input UTxO`s
  U1( <b>Oracle</b><hr />NFT<br/>1.75 )
  U2( <b>Swap</b><hr />100 ada)
  U3( <b>Buyer</b><hr />175 usd + 1 ada)

  %% Input connections to Tx1
  U1 -- <p align='left'><b>use<br/></b></p> --> T1
  U2 -- <p align='left'><b>swap&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<br/><br/></b></p> --> T1
  U3 --> T1

  %% Definition of Tx1
  T1[[Tx 1]]

  %%  Definition of Tx1`s Output UTxO`s
  U4( <b>Oracle</b><hr />NFT + 1 ada<br/>1.75 )
  U5( <b>Seller</b><hr />175 usd)
  U6( <b>Buyer</b><hr />100 ada)

  %% Output connections of Tx1
  T1 --> U4 & U5 & U6

```

## Swap

```mermaid
flowchart LR  
  %% Definition of Input UTxO`s
  U1( <b>Oracle</b><hr />NFT<br/>1.75 )
  U2( <b>Swap</b><hr />100 ada)
  U3( <b>Buyer</b><hr />175 usd + 1 ada)

  %% Input connections to Tx1
  U1 -- <p align='left'><b>use<br/></b></p> --> T1
  U2 -- <p align='left'><b>swap&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<br/><br/></b></p> --> T1
  U3 --> T1

  %% Definition of Tx1
  T1[[Tx 1]]

  %%  Definition of Tx1`s Output UTxO`s
  U4( <b>Oracle</b><hr />NFT + 1 ada<br/>1.75 )
  U5( <b>Seller</b><hr />175 usd)
  U6( <b>Buyer</b><hr />100 ada)

  %% Output connections of Tx1
  T1 --> U4 & U5 & U6

  %% Input connections to Tx2
  U4 -- <p align='left'><b>update<br/><br/></b> ---> T2

  %% Definition of Tx2
  T2[[Tx 2]]

  %%  Definition of Tx2`s Output UTxO`s
  U7( <b>Oracle</b><hr />NFT<br/>1.77 )
  U8( <b>Owner</b><hr />1 ada)

  %% Output connections of Tx2
  T2 --> U7 & U8
```

Another attempt:

```mermaid
flowchart LR  
  
  C0(( )) 
  C1(( )) 
  C2(( ))
  U1( <p>Script</p><hr />100 ada<br/>Datum )

  C0 --> U1
  U1 -- <p align='left'><b>Redeemer<br/><br/></b></p> --- C1
  C1 ---> C2

  C4(( )):::invisible

  C4 --> C2

  style C1 fill:none,stroke:none;
  
  classDef comment fill:#f333,stroke-dasharray: 5 5;
  classDef dottedLink stroke:#333,stroke-width:4px,color:red,stroke-dasharray: 8 12;
  classDef invisible fill:none,stroke:none;

  %% Attempt to split a connector line; the splitted lines should share the same link styling
  linkStyle 1,2 stroke:#333,stroke-width:4px,color:red,stroke-dasharray: 8 12;
  %% seems not to work !!  
  %% linkStyle 2 dottedLink;

  %% not possible with classDefs
  %% style C4 fill:none,stroke:none;
``` 