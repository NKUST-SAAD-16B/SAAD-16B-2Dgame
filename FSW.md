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

## 有限狀態機-骷髏
```mermaid
stateDiagram-v2
    [*] --> idle
    idle --> walk
    walk --> idle
    chase -->idle
    chase --> attack
    attack --> walk
    hurt --> idle
    anystate --> hurt
    anystate --> dead
    anystate --> chase
```
