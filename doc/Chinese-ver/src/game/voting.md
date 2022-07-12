voting文件：
{

    enum
    {
	    VOTE_DESC_LENGTH=64, { 投票信息最大长度 }
	    VOTE_CMD_LENGTH=512, { 指令最大长度 }
	    VOTE_REASON_LENGTH=16, { 投票理由最大长度 }

	    MAX_VOTE_OPTIONS=128, { 投票最大项数 }
    };

    struct CVoteOptionClient // 用于控制启动器的投票内容显示
    {
    	CVoteOptionClient *m_pNext; // 向服务器发送要投票的内容
	    CVoteOptionClient *m_pPrev; // 保存上一个投票内容
    	char m_aDescription[VOTE_DESC_LENGTH]; // 投票信息
    };

    struct CVoteOptionServer // 用于处理服务端的投票
    {
    	CVoteOptionServer *m_pNext; // 检测投票是否存在，以及处理投票成功后的效果
    	CVoteOptionServer *m_pPrev; // 辅助检测投票是否存在，以及处理投票成功后的效果
    	char m_aDescription[VOTE_DESC_LENGTH]; // 投票信息
    	char m_aCommand[1]; // 投票的项目
    };
}