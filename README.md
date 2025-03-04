# nobing_hans
OpenCC configuration for traditional Chinese to simplified Chinese, with ambiguities preserved in traditional forms

This repository used material from [BYVoid/OpenCC](https://github.com/BYVoid/OpenCC) and [簡繁轉換一對多列表](https://zh.wikipedia.org/wiki/%E7%B0%A1%E7%B9%81%E8%BD%89%E6%8F%9B%E4%B8%80%E5%B0%8D%E5%A4%9A%E5%88%97%E8%A1%A8).

# 无併简体
保留合併简化字繁体形式的简体中文的OpenCC配置方案

此仓库使用了来自[BYVoid/OpenCC](https://github.com/BYVoid/OpenCC)和[簡繁轉換一對多列表](https://zh.wikipedia.org/wiki/%E7%B0%A1%E7%B9%81%E8%BD%89%E6%8F%9B%E4%B8%80%E5%B0%8D%E5%A4%9A%E5%88%97%E8%A1%A8)的材料。

你在打字的时候是否希望分开被合併的简化字，比如髮和發，乾和幹？这個配置方案保留了OpenCC简体方案中大部分简化对应关係，但去除了造成合併简化字的对应关係。同时，微调了部分多对多的繁简关係。

## RIME使用方法

參见[RIME的说明文档](https://github.com/rime/home/wiki/RimeWithSchemata#%E5%AE%9A%E8%A3%BD%E6%8C%87%E5%8D%97)。

将`nobinghans.txt`和`t2nobinghans.json`下载到用户文件夹（默认为`C:\Users\您的用户名\AppData\Roaming\Rime`）下的`opencc`文件夹内。

给一個**以繁体字库为基础**的RIME输入方案（如朙月拼音）打补丁，替换原先的繁简转换开关（switch），參见下方示例。

```
patch:
  switches/@2:
    options: [ noop, simplification, nobing_hans ]
    states:
      - 字型：繁體
      - 字型：简体
      - 字型：无併简体
    reset: 2
  nobing_hans:
    opencc_config: t2nobinghans.json
    option_name: nobing_hans
```

其中`reset: 2`表示每次切换到该输入法时強制切换到第三（2+1）種用字模式。您也可以改为`0`、`1`，或直接删除。

打完补丁後重新部署即可。

## 实现说明

本项目使用OpenCC默认繁转简转换表，並找出中文维基百科条目《簡繁轉換一對多列表》（除了「一对一（全同异体字）」章节）涉及的所有合併简化字，並去除对应转换条件。对默认转换表中一繁对多简的字手动校对。

《簡繁轉換一對多列表》收例过鬆，如「体」「體」这樣既是繁简体亦是正异体关係的一对字也列入其中，这些转换关係需要手动补回。若您發现有些应简化的字保留了繁体形式，或者有什麼校对错误和收字建议，歡迎提issue或 pull request。

## 其他说明
- 感谢[自由雨日](https://zh.wikipedia.org/wiki/User:%E8%87%AA%E7%94%B1%E9%9B%A8%E6%97%A5)、[杰里毛斯](https://zh.wikipedia.org/wiki/User:%E6%9D%B0%E9%87%8C%E6%AF%9B%E6%96%AF)协助审校複杂转换表。
