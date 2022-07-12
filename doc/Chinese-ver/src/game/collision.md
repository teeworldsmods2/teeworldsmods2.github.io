CCollision介绍：
{
    主要负责控制游戏地图，碰撞箱等
}

collision.h文件讲解:
{

    class CCollision
    {
        class CTile *m_pTiles; { 地图内的对应区块 }
        int m_Width; { 地图宽度 }
        int m_Height; { 地图高度 }
        class CLayers *m_pLayers; { 地图中的贴图 }

    public:
        enum
        {
            COLFLAG_SOLID=1, { 碰得到的区块 }
            COLFLAG_DEATH=2, { 碰到会死但能穿过的区块 }
            COLFLAG_SOLID=4, { 能抵挡钩子，当单独存在于index中时，没有碰撞箱 }
        };

        bool CheckPoint(float x, float y) { 检测此坐标下的区块有没有碰撞体积 }
        bool CheckPoint(vec2 Pos) { 同上 }
        int GetCollisionAt(float x, float y) { 获取当前坐标下的区块是啥(但是返回值不是mapitem里面的数字，而是pow(2, 与mapitems对应); ) }
        int GetWidth() { 获取宽度 }
        int GetHeight() { 获取长度 }
    }
}

collision.cpp函数讲解:
{

    CCollision::CCollision()
    {
        初始化变量
    }

    void CCollision::Init(class CLayers *pLayers)
    {
        用于初始化地图.
        初始化内容包含：
            贴图
            地图大小
            地图区块
    }

    int CCollision::GetTile(int x, int y)
    {
        获取对应x和y上面的地图区块（不获取实体层，实体层只在游戏开始时读取一次），
        但是返回值不是mapitem里面的数字，而是pow(2, 与mapitems对应);
    }

    bool CCollision::IsTileSolid(int x, int y)
    {
        如果对应的x和y坐标上的区块是COLFLAG_SOLID（无法被穿过）类型，
        那么返回true，否则返回false
    }

    int CCollision::IntersectLine(vec2 Pos0, vec2 Pos1, vec2 *pOutCollision, vec2 *pOutBeforeCollision)
    {
        检测Pos0和Pos1中有没有包含COLFALG_SOLID类型的区块，
        如果有，且有第三个参数，那么设置第三个参数pOutCollision的值为区块所在的位置（靠近Pos0的区块），
        如果第四个参数的值不为NULL，那么设置第四个参数pOutBeforeCollision的值为在检测到区块前的地方的坐标。

        如果pOutCollision为vec2(12, 12), 且Pos1对Pos0来说是在朝右下角移动，
        那么pOutBeforeCollision的值为vec2(11, 13)
    }

    void CCollision::MovePoint(vec2 *pInputPos, vec2 *InoutVel, float Elasticity, int *pBounces)
    {
        简单地移动位置，同时保证不会穿墙。
    }

    void CCollision::TextBox(vec2, vec2 Size)
    {
        检测在此处移动会不会穿墙
    }

    void CCollision::MoveBox(vec2 *pInoutPos, vec2 *pInoutVel, vec2 Size, float Elasticity)
    {
        移动碰撞箱，同“void CCollision::MovePoint(vec2 *pInputPos, vec2 *InoutVel, float Elasticity, int *pBounces)”
    }
}
