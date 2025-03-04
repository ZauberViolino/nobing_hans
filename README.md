# nobing_hans
OpenCC configuration for traditional Chinese to simplified Chinese, with ambiguities preserved in traditional forms

This repository used material from [BYVoid/OpenCC](https://github.com/BYVoid/OpenCC) and [簡繁轉換一對多列表](https://zh.wikipedia.org/wiki/%E7%B0%A1%E7%B9%81%E8%BD%89%E6%8F%9B%E4%B8%80%E5%B0%8D%E5%A4%9A%E5%88%97%E8%A1%A8).

# 无併简体
保留合併简化字繁体形式的简体中文的OpenCC配置方案

此仓库使用了来自[BYVoid/OpenCC](https://github.com/BYVoid/OpenCC)和[簡繁轉換一對多列表](https://zh.wikipedia.org/wiki/%E7%B0%A1%E7%B9%81%E8%BD%89%E6%8F%9B%E4%B8%80%E5%B0%8D%E5%A4%9A%E5%88%97%E8%A1%A8)的材料。

你在打字的时候是否希望分开被合併的简化字，比如髮和發，乾和幹？这個配置方案保留了OpenCC简体方案中大部分简化对应关係，但去除了造成合併简化字的对应关係，並微调了部分多对多的繁简关係。

## RIME使用方法
给一個**以繁体字库为基础**的RIME输入方案（如朙月拼音）打补丁，參见[RIME的说明文档](https://github.com/rime/home/wiki/RimeWithSchemata#%E5%AE%9A%E8%A3%BD%E6%8C%87%E5%8D%97)和下方示例。

```
patch:
  switches/@2:
    options: [ noop, simplification, nobing_hans]
    states:
      - 字型：繁體
      - 字型：简体
      - 字型：无併简体
    reset: 2
  nobing_hans:
    opencc_config: t2nobinghans.json
    option_name: nobing_hans
```
