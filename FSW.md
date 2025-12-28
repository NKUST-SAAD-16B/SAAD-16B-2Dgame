## 有限狀態機-玩家

```mermaid
stateDiagram-v2
    [*] --> idle
    idle --> walk
    idle --> jump
    idle -->attack
    walk --> jump
    walk --> run
    walk --> idle
    jump --> idle
    run --> jump
    run --> idle
    attack --> idle
    hurt --> idle
    anystate --> hurt
    anystate --> dead
```
