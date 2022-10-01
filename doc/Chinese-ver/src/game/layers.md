# CLayers介绍: { 负责控制地图贴图 }

## layers.h函数讲解:

```C++
{
    class CLayers
    {
    	int m_GroupsNum; { 记录地图内图层(Group)的数量 }
    	int m_GroupsStart; { 图层最下层的图层ID }
    	int m_LayersNum; { 记录地图内的贴图数量 }
    	int m_LayersStart; { 最下层的贴图ID }
    	CMapItemGroup *m_pGameGroup; { 地图中的区块(mapitem) }
	    CMapItemLayerTilemap *m_pGameLayer; { 地图中的贴图区块 }
	    class IMap *m_pMap; { 对应的地图 }

    public:
    	int NumGroups() const { return m_GroupsNum; }; { 获取m_GroupsNum }
    	class IMap *Map() const { return m_pMap; }; { 获取对应的地图(m_pMap) }
    	CMapItemGroup *GameGroup() const { return m_pGameGroup; }; { 获取游戏区块(mapitem, m_pGameGroup) }
    	CMapItemLayerTilemap *GameLayer() const { return m_pGameLayer; }; { 获取贴图区块(m_pGameLayer) }
    };
}
```

## layers.cpp函数讲解:

```C++
{
    CLayers::CLayers()
    {
        初始化变量和类
    }

    void CLayers::Init(class IKernel *pKernel)
    {
        初始化地图中的区块与贴图Tile和Quad，
        并强制设置Game层（mapitem）紧紧贴在地图上，
        不会随着玩家移动。
    }

    CMapItemGroup *CLayers::GetGroup(int Index) const
    {
	    获取地图内的有着对应编号(Index)的Group组
    }

    CMapItemLayer *CLayers::GetLayer(int Index) const
    {
    	获取对应编号的贴图层(通常与GetGroup搭配使用)
    }

}
```