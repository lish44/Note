# 公司
--------

### 热更新包裹
1. 修改GameInfoConfig.txt里面的版本号 对应svn最新版本号
2. 在打包里面点对应资源
    + 有图选完整打包
    + 一来就点生成link
    + 有xlua点packXLuaScript
3. 点一键生成热更包
4. 有战斗相关的要先去看config文件夹下的battleconfig，然后和web里面的battleconfig对比（web只能多不能少）
5. 

### tag管理器
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using UnityEngine;
using UnityEngine.UI;
using YoukiaUnity.App;
using YoukiaCore;
using YoukiaUnity.GUI.AorUI.Core;
using System.Collections;
class TestWindow : MonoSwitch
{
    private AorButton m_btnClose;
    private PageTagManager m_PageTagManager;
    private List<TagIconType> m_tagIconTypes;
    public override void OnAwake()
    {
        base.OnAwake();
        m_btnClose = GameUtils.GetChild<AorButton>(transform, "closeBtn");
        m_PageTagManager = GameUtils.GetChild<PageTagManager>(transform, "RightPageTagPref");
        m_tagIconTypes = new List<TagIconType>() { TagIconType.T1, TagIconType.T2, TagIconType.T3 };
    }

    protected override void Initialization()
    {
        base.Initialization();
        GameUtils.JustAddOneButtonEvent(m_btnClose, Close);

        List<string> strTabs = new List<string>() { "1", "2", "3" };
        List<string> norIconPath = new List<string>() {
            GameUtils.GetTagIconName(TagIconType.T1, TagState.UnSelect),
            GameUtils.GetTagIconName(TagIconType.T2, TagState.UnSelect),
            GameUtils.GetTagIconName(TagIconType.T3, TagState.UnSelect)
        };
        List<string> SelectIconPath = new List<string>() {
            GameUtils.GetTagIconName(TagIconType.T1, TagState.Select),
            GameUtils.GetTagIconName(TagIconType.T2, TagState.Select),
            GameUtils.GetTagIconName(TagIconType.T3, TagState.Select)
        };
        m_PageTagManager.IconAtlasMatPath = Def.AtlasMat_Path_TagIcon_xNew;
        m_PageTagManager.InitData(strTabs, norIconPath, SelectIconPath, OnTagChange, null, new Vector2(0, -85));
    }
    private void OnTagChange(int index, GameObject arg2, GameObject arg3)
    {
        var t = m_tagIconTypes[index];
        switch (t)
        {
            case TagIconType.T1:
                Log.Debug("1");
                break;
            case TagIconType.T2:
                Log.Debug("2");
                break;
            case TagIconType.T3:
                Log.Debug("3");
                break;
        }
    }
    private void Close()
    {
        ShowWindowManager.Instance.CloseWindow<TestWindow>();
    }
}
```
+ norIconPath 就是图集的名字
+ m_PageTagManager.IconAtlasMatPath 及时图集的材质球路径

### image图集用法
```csharp    
var path = "Ui/BattleSoloView_New/BattleSoloView_New_RGB";
var matPath = "Ui/BattleSoloView_New/BattleSoloView_New_Mat";
m_img.LoadImage(path, "0", null, matPath);
```
+ 第二个参数是图片名字
+ 第三个参数是回调

### Top栏通用材料显示

资源
+ 添加ResTitle节点，然后只需要添加CommonLoadParent脚本 然后选择ResTitle的type就对了

元宝
+ 添加MoneyTitle节点，然后同样添加CommonLoadParent脚本 然后选择MoneyTiele2的type


### 行军皮肤图集
1. 找到图集对应路径 `C:\Workspace\Kr_Patch\Unity\Assets\Resources\Role\Panoramic_npc\assets` 
2. 图集打到对应文件夹里面，没有新建
    + 文件文字必须以 __world__ 开头
    + 进去只保留 .tps 文件其他删了
    + 把图片拷贝进 ..Sprites
    + 开始打
	
	![图集](https://raw.githubusercontent.com/lish44/pic/main/res/202205162325946.png)
4. 再unity中右键创建图集
    + ![截图](https://gitee.com/rehma/pic/raw/master/res/20210803115138.png)
5. 创建prefab设置 预制体一般以army 开头
    + root 换路径
    + root 换mat材质球
    + root 换第一张图
6. 去配置表修改测试
    > 主要修改perfab
    + ResSkinConfig.txt
    + MapArmyConfig.txt

### 红点
+ RedPointModel.cs 里面加红点枚举 RedPointType
+ 然后在RedPointPref.cs 里面写逻辑
    - 在UpdateData方法里面写枚举写 红点的枚举判断
    - 然后写对应的方法，这方法里面的逻辑就是最终显示红点的逻辑
+ 用的时候先要Init一哈，init的第二个参数就是脚本里面的m_Data，可以用来刷新逻辑的判断
+ 然后就是抛对应红点的刷新事件: `Main.Inst.GlobalEvent.DispatchEvent(eNameUI.RedPoint_Update, RedPointType.SecretTreasure_Main);`

#### 红点找
1. 找组件看组件身上的红点类型，然后去redpointpref.cs里面查找相关的显示逻辑
1. 找按钮 看view有没有获取按钮的红点
2. 没有找到的话看Net层有没

#### 活动的红点主页签
1.活动的data继承ActivityDataBase后里面有个ShowRedPoint方法，这个就是监测页签红点的


### 聊天皮肤修改
1. 先打图集
2. 然后edit
3. 然后去ResSkinConfig.txt 用原来的数据测试 如22207 修改名字如 ChatView1改成10，然后发包裹去测试

### 活动相关
+ 活动data继承后有2个解析 需要重写
+ 一般从活动大厅打开界面会自动保存打开的时间，没有的话需要用自己的data调用SaveOpenTime方法
    - 在CommonActivityItemBase.cs里面的`_detailData.SaveOpenTime();`
+  
