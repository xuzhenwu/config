# Zotero 

开源，灵活的文献管理软件

## 基本步骤

**步骤** - 请严格按照这个步骤进行

* 安装程序
* 登录账户
* 设置链接
  * mklink /j C:/zotero/storage D:/ONEDRIVE/LOCAL_STORAGE
* 关闭文件首选项中的文件同步选项
* 选择同步
* 等待连接文件
* 添加插件
  * 如果过早添加插件，sci-hub插件会自动添加文献
  * 或者就不添加sci-hub文献，手动添加
* 关闭


## Zotero 7

Zotero 7是最新的版本，自动更新，仅需添加较少插件

* 安装
  * https://www.zotero.org/support/beta_builds
* 插件
  * Linter
    * https://github.com/northword/zotero-format-metadata
  * 其他插件暂不需要使用
* 样式
  * 中文样式（配合Linter进行中英文混排）
    * https://github.com/redleafnew/Chinese-STD-GB-T-7714-related-csl
* 使用
  * 同步设置（配合onedrive, 核心是文献分类经zotero线上同步，pdf文件库经onedrive同步，避免两台电脑同时修改导致崩溃)
    - https://www.zhihu.com/search?type=content&q=zotero%20onedrive%E5%90%8C%E6%AD%A5
  * Word快捷键设置
    - https://www.zotero.org/support/word_processor_plugin_shortcuts
  * 引用颜色
    - https://forums.zotero.org/discussion/65642
  * 设置文件夹自动继承
    - https://forums.zotero.org/discussion/68833/sources-in-sub-folders-not-showing-up-in-higher-level-folders
  * ctrl会高亮显示文献所在的组
    - https://forums.zotero.org/discussion/22870/display-collections-to-which-an-item-belongs


## EndNote to Zotero

Endnote在选取文献后，导出xml文件，然后在zotero中导入（引用和pdf都会同时导入）

https://www.zotero.org/support/kb/endnote_import


## Zotero 6（不再建议使用）

* 插件列表及添加方式
  * https://www.zotero.org/support/plugins


* 比较有用的是preview插件（pdf和citation)
  * https://github.com/windingwind/zotero-pdf-preview
    * known issues: 部分第三方pdf软件编辑后，下划线和高亮无法预览，但添加的文字可以正常显示
  * https://github.com/dcartertod/zotero-plugins


