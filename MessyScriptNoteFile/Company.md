# 公司
--------

### 热更新包裹
1. 修改GameInfoConfig.txt里面的版本号 对应svn最新版本号
2. 在打包里面点对应资源
    + 有图选完整打包
    + 有新增图点生成link
    + 有xlua点packXLuaScript
3. 点一键生成热更包

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

