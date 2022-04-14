
Based on [Data Model/Box](https://docs.ergoplatform.com/dev/data-model/box/)
a box is made up of registers (and nothing but registers!), we allow every box in the system to have up to 10 registers. We denote the registers as R_0,R_1,...,R_9. 

From these registers, four are filled with mandatory values: 

| Register | Meaning |
| -- | -- |
| **R_0** | monetary value |
| **R_1** | serialized guard script / protecting script |
| **R_2** | tokens |
| **R_3** | 
- declared **creation height**, 
- **unique identifier of transaction** which created the coin and 
- also an **index of the box in the transaction**. <br />
___Or___
- identifier of a transaction which created the box and 
- output index in the transaction and 
- also creation height.
|


❩

Medium Left Parenthesis Ornament
&#10088;   &#x2768;

Medium Right Parenthesis Ornament
&#10089; &#x2769;


```mermaid
flowchart LR
  %% Defining the UTxO's
  U1("<table style='text-align:left; text-transform: uppercase; background-color: red; margin-top: -6.5rem; margin-botom: 120px' > 
    <tr style='background-color: blue'><th  style='color: yellow; text-transform: lowercase; background-color: green;'>Bob #3</th></tr> 
    <tr><td style='color:red'>100 ada</td></tr> 
    <tr><td>0</td></tr> 
    <tr><td>usw.</td></tr> </table> 
  ")
  %% lines = 6; margin-top -10em --> lines + 3 em
  U2("<table style='text-align:left; margin-top: -18ex; margin-bottom: 0;' > 
    <tr><th '>Bob #3</th></tr> 
    <tr><td style='color:red'>100 ada</td></tr> 
    <tr><td>0</td></tr>     

    <tr style='color: blue; ' ><td>usw.</td></tr> 
    </table>  ")
  %% lines = 8; margin-top -10em --> lines + 3 em
  U21("<table style='text-align:left;margin-top: -21ex;' > 
    <tr '  ><th >Bob #3</th></tr> 
    <tr><td style='color:red'>100 ada</td></tr> 
    
    <tr><td>0</td></tr>     
    <tr style='color: blue; ' ><td>usw.</td></tr> 

    </table>  ")
  U1 --> U2  --> U21
  Alice("<p style='text-align:left'><b><u>Alice #1</u></b><br/>50 ada"<br/>1</p>)

  Charlie("<pre>Charlie,100: &nbsp; &ast; &period; /\<>   </pre>")
  C["<p align='left'> <b>Charlie #3</b><hr /><span  align='left'>Line 2</span><br />Lasat Line </p>"]
  U3("<table> <tr><th>Bob #2</th></tr> <tr><td align='left'>100 ada<br /></td></tr></table> ")
  U4("<table> <tr><th>Bob #3</th></tr> <tr align='left'> <td>100</td> </tr> <tr><td>(100 ada)</td> </tr> <tr align='left'> <td>null</td> </tr></table>")
```

