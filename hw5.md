## UML類別圖
```mermaid
classDiagram
    direction LR

    class Player {
        - id: int
        - name: string
        - maxHP: int
        - currentHP: int
        - attackPower: int
        - gold: int
        - currentFloor: int
        + move(direction: string): void
        + attack(target: MonsterInstance): void
        + takeDamage(amount: int): void
        + isDead(): boolean
    }

    class Floor {
        - floorNumber: int
        + generateRoomInstance(RoomType): RoomInstance
        + getMonsterTypesForFloor(): List~MonsterType~
    }

    class MonsterType {
        - id: int
        - name: string
        - baseHP: int
        - attackPower: int
    }

    class MonsterInstance {
        - id: int
        - currentHP: int
        - monsterType: MonsterType
        + takeDamage(amount: int): void
        + performAttack(target: Player): void
    }

    class UpgradeOption {
        - id: int
        - name: string
        - basePrice: int
        + getEffectivePrice(playerFloor: int): int
    }
    
    %% M:N Associative Classes (聯結類別)
    class FloorRoomConfig {
        + weight: int
    }
    class PlayerUpgradeLog {
        + purchaseTime: DateTime
        + purchasePrice: int
    }


    %% Relationships (關聯)
    Player "1" -- "1" Floor : locatedIn
    
    %% Floor 與 RoomType (透過 FloorRoomConfig 聯結)
    Floor "1" -- "*" FloorRoomConfig : definesConfig
    RoomType "1" -- "*" FloorRoomConfig : configuredBy
    
    %% Player 與 UpgradeOption (透過 PlayerUpgradeLog 聯結)
    Player "1" -- "*" PlayerUpgradeLog : logsPurchase
    UpgradeOption "1" -- "*" PlayerUpgradeLog : loggedFor

    %% MonsterType 與 MonsterInstance (實例化)
    MonsterType "1" -- "*" MonsterInstance : instantiates
    
    %% Floor 包含 MonsterInstance
    Floor "1" -- "*" MonsterInstance : contains
