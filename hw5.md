## UML類別圖
```mermaid
classDiagram
    direction LR

    %% Core Classes (核心類別)
    class Player {
        - health: int
        - floorLevel: int
        - attackPower: int
        - gold: int
        + takeDamage(amount: int): void
        + gainGold(amount: int): void
        + move(newRoom: Room): void
    }

    class Room {
        - roomID: int
        - roomType: string
        + enter(player: Player): void
        + exit(player: Player): void
    }

    class UpgradeOption {
        - name: string
        - attributeCategory: string
        - basePrice: int
        + applyEffect(player: Player): void
        + getPrice(player: Player): int
    }

    class Event {
        - name: string
        - category: string
        - description: string
        - effect: string
        + trigger(player: Player): void
    }

    class Monster {
        - name: string
        - attackPower: int
        - goldDrop: int
        - health: int
        + attack(target: Player): void
        + dropLoot(): void
    }

    %% Associative Classes (聯結類別) - for M:N relationships
    class PlayerUpgradeLog {
        + purchaseTime: DateTime
        + finalPrice: int
    }

    class PlayerEventLog {
        + encounterTime: DateTime
        + playerChoice: string
    }

    class RoomMonsterConfig {
        + quantity: int
        + spawnChance: float
    }

    %% Relationships (關係)
    Player "1" -- "1" Room : isLocatedIn
    
    Player "1" -- "*" PlayerUpgradeLog : logsPurchase
    UpgradeOption "1" -- "*" PlayerUpgradeLog : loggedFor

    Player "1" -- "*" PlayerEventLog : logsEncounter
    Event "1" -- "*" PlayerEventLog : loggedFor

    Room "1" -- "*" RoomMonsterConfig : definesConfig
    Monster "1" -- "*" RoomMonsterConfig : configuredBy
