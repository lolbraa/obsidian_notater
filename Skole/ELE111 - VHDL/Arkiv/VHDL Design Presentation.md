All interactive flip-flops are state machines, but perhaps implisite.

Divide and conquer: Ikke ha en FSM (finite state machine), men del opp i ulike prosesser
- En FSM for tx-protokollen (4-5 states)
- Loop select (fra CPU interface eller RXD)
- Insert Xon/Xoff
- Evt. Post processing 
- CTS: Stopp til Tx protocol

Code conventions: [VHDL Conventions - EmLogic AS](https://emlogic.no/vhdl-conventions/)