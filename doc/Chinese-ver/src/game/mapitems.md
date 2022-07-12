mapitems文件介绍：
{
    控制地图中的区块
}

mapitems.h：

{
    enum
    {
    	LAYERTYPE_INVALID=0,    // 地图编辑器使用，服务器不使用 |、
    	LAYERTYPE_GAME,         // 地图编辑器使用，服务器不使用 |、
    	LAYERTYPE_TILES,        // 地图编辑器使用，服务器不使用 |、
    	LAYERTYPE_QUADS,        // 地图编辑器使用，服务器不使用 |、

    	MAPITEMTYPE_VERSION=0,  // 地图编辑器使用，服务器不使用 |、
    	MAPITEMTYPE_INFO,       // 地图编辑器使用，服务器不使用 |、
    	MAPITEMTYPE_IMAGE,      // 地图编辑器使用，服务器不使用 |、
    	MAPITEMTYPE_ENVELOPE,   // 地图编辑器使用，服务器不使用 |、
	    MAPITEMTYPE_GROUP,      // 地图编辑器使用，服务器不使用 |、
    	MAPITEMTYPE_LAYER,      // 地图编辑器使用，服务器不使用 |、
    	MAPITEMTYPE_ENVPOINTS,  // 地图编辑器使用，服务器不使用 |、


        // 地图信封(Envelope)动画，不做介绍 |
	    CURVETYPE_STEP=0,
    	CURVETYPE_LINEAR,
    	CURVETYPE_SLOW,
    	CURVETYPE_FAST,
    	CURVETYPE_SMOOTH,
    	NUM_CURVETYPES,
        // 地图信封(Envelope)动画，不做介绍 |

    	// 游戏(Game)实体
	    ENTITY_NULL=0, //实体占位
	    ENTITY_SPAWN, //玩家出生点
	    ENTITY_SPAWN_RED, //红队玩家出生点
	    ENTITY_SPAWN_BLUE, //蓝队玩家出生点
    	ENTITY_FLAGSTAND_RED, //红队旗帜出生点
	    ENTITY_FLAGSTAND_BLUE, //蓝队旗帜出生点
    	ENTITY_ARMOR_1, //甲生成点
    	ENTITY_HEALTH_1, //血生成点
    	ENTITY_WEAPON_SHOTGUN, //散弹枪生成点
    	ENTITY_WEAPON_GRENADE, //榴弹枪生成点
    	ENTITY_POWERUP_NINJA, //忍者生成点
    	ENTITY_WEAPON_RIFLE, //激光器生成点
    	NUM_ENTITIES, //记录实体数量

        // 游戏(Game)区块
    	TILE_AIR=0, //区块占位
    	TILE_SOLID, //可以钩 && 有实体的区块的区块
    	TILE_DEATH, //杀死玩家 && 没有实体的区块
    	TILE_NOHOOK, //可以反弹玩家钩子 && 有实体的区块

    	TILEFLAG_VFLIP=1,     // 不重要，实际编程中用不到 |、
    	TILEFLAG_HFLIP=2,     // 不重要，实际编程中用不到 |、
    	TILEFLAG_OPAQUE=4,    // 不重要，实际编程中用不到 |、
	    TILEFLAG_ROTATE=8,    // 不重要，实际编程中用不到 |、

    	LAYERFLAG_DETAIL=1,   // 不重要，实际编程中用不到 |、
    	TILESLAYERFLAG_GAME=1 // 不重要，实际编程中用不到 |、

	    ENTITY_OFFSET=255-16*4, 计算实体和区块的分界点
    };

    // 不重要，实际编程中用不到 |
    struct CPoint
    {
	    int x, y; // 22.10 fixed point
    };

    // 不重要，实际编程中用不到 |
    struct CColor
    {
    	int r, g, b, a;
    };

    // 不重要，实际编程中用不到 |
    struct CQuad
    {
    	CPoint m_aPoints[5];
    	CColor m_aColors[4];
	    CPoint m_aTexcoords[4];

    	int m_PosEnv;
	    int m_PosEnvOffset;

    	int m_ColorEnv;
	    int m_ColorEnvOffset;
    };

    class CTile
    {
    public:
	    unsigned char m_Index; // 详情看collision.md
    	unsigned char m_Flags;
    	unsigned char m_Skip;
	    unsigned char m_Reserved;
    };

    // 不重要，实际编程中用不到 |
    struct CMapItemInfo
    {
	    int m_Version;
    	int m_Author;
    	int m_MapVersion;
    	int m_Credits;
    	int m_License;
    };

    // 不重要，实际编程中用不到 |
    struct CMapItemImage_v1
    {
    	int m_Version;
    	int m_Width;
    	int m_Height;
    	int m_External;
    	int m_ImageName;
	    int m_ImageData;
    };

    // 不重要，实际编程中用不到 |
    struct CMapItemImage : public CMapItemImage_v1
    {
    	enum { CURRENT_VERSION=2 };
    	int m_Format;
    };

    // 不重要，实际编程中用不到 |
    struct CMapItemGroup_v1
    {
    	int m_Version;
    	int m_OffsetX;
    	int m_OffsetY;
    	int m_ParallaxX;
    	int m_ParallaxY;

    	int m_StartLayer;
    	int m_NumLayers;
    };


    // 不重要，实际编程中用不到 |
    struct CMapItemGroup : public CMapItemGroup_v1
    {
	    enum { CURRENT_VERSION=3 };

    	int m_UseClipping;
    	int m_ClipX;
    	int m_ClipY;
    	int m_ClipW;
    	int m_ClipH;

    	int m_aName[3];
    };

    // 不重要，实际编程中用不到 |
    struct CMapItemLayer
    {
    	int m_Version;
    	int m_Type;
	    int m_Flags;
    };

    // 不重要，实际编程中用不到 |
    struct CMapItemLayerTilemap
    {
    	CMapItemLayer m_Layer;
	    int m_Version;

    	int m_Width;
    	int m_Height;
    	int m_Flags;

    	CColor m_Color;
	    int m_ColorEnv;
	    int m_ColorEnvOffset;

    	int m_Image;
    	int m_Data;

	    int m_aName[3];
    };

    // 不重要，实际编程中用不到 |
    struct CMapItemLayerQuads
    {
    	CMapItemLayer m_Layer;
    	int m_Version;

    	int m_NumQuads;
    	int m_Data;
    	int m_Image;

    	int m_aName[3];
    };

    // 不重要，实际编程中用不到 |
    struct CMapItemVersion
    {
	    int m_Version;
    };

    // 不重要，实际编程中用不到 |
    struct CEnvPoint
    {
    	int m_Time; // in ms
    	int m_Curvetype;
	    int m_aValues[4]; // 1-4 depending on envelope (22.10 fixed point)

	    bool operator<(const CEnvPoint &Other) { return m_Time < Other.m_Time; }
    };

    // 不重要，实际编程中用不到 |
    struct CMapItemEnvelope_v1
    {
    	int m_Version;
    	int m_Channels;
    	int m_StartPoint;
    	int m_NumPoints;
    	    int m_aName[8];
    };
    
    // 不重要，实际编程中用不到 |
    struct CMapItemEnvelope : public CMapItemEnvelope_v1
    {
    	enum { CURRENT_VERSION=2 };
    	    int m_Synchronized;
    };
}