# 测试场景 for scene & interaction / character testing

## description

一只主角的史莱姆，拿起地上的水瓜种子种到菜盆里。拿着魔法棒在植物一定范围内施法一次，植物就会长大一个阶段。收集四个果实放到篮子里。

## Class Attributes

```json
Character : Object

- super (extended from h2d.Object) // as reminding, object has: transform, parent, child lists;
- sprite (as child)
- controller : Either PlayerController | AutoController (for NPC) // removed, controller now is isolated class for multiplayer
- triggers / events

Player : Character

- super (attributes extended from super class)
- state : State
- interactions (ref: https://heaps.io/documentation/h2d-events-and-interactivity.html)
- toolInventory : List[Tool] // Tool: Enum{TestGrowthMagic, Axe, Pickaxe, etc.}
- currentTool : Empty | Tool // The active tool, only one tool can be active at once, cannot hold tool when carrying other stuffs
- carry : Item
- isCarry : Boolean // Player can take limited interaction when carrying something

TestGrowthMagic : Tool // 史莱姆会把常用的工具藏在肚子里，需要用的时候变出来用。每种工具对应不同的互动效果

Abstract Item : Object

- super
- ID
- sprite
- attributes
- triggers

Seed : Fruit

// 种子可以是一种特殊的水果，拥有发芽的能力

Machine : Object

- ID
- sprite
- description
- etc.

PlantSoil : Machine // 类似花盆的东西，一个盆种一个植物

- super
- state
- plant
- interaction

Plant : Object

- super
- sprite
- state
- child

Plant_Waterfruit : Plant

- super
- stage // 植物的阶段，参考水瓜的文档
- water // 浇水参数，测试场景用1
- env_factor // 环境参数，表示环境对植株的影响，1
- growth // 生长槽，填满了进下一阶段 // 几种实现：累计槽满了清空进下一阶段；累计槽到一定值，改阶段改图片；累计槽满了，鲨了这个instance造个新的不同阶段instance
- time_birth
- genetic_info // 遗传数据
- - water_rate
- - env_rate
- - growth_rate
- - fruit_genetic_info // 用于创建水瓜果实的数据
- fruits : List[Fruit] 在生出果子的阶段创建四个果子对象，每次更新果子对象的数据 | fruit_data : 对应水瓜的数据，摘下来时复制一份创建新实体，二选一

Fruit : Object

- super
- sprite
- flavor
- tastes:
- - 这部分请快速找数值策划来搞
- genetic_info

Fruit_Waterfruit : Fruit

- super

Container : Object

- super
- content : List[]

Basket : Container

- super
- capacity | meshing // meshing指类似大菠萝物品栏一样的爬格子堆东西
```
