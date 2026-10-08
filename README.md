# 称骨先生 · Chenggu Culture Sage

> 传统称骨民俗文化解读专家（WorkBuddy Agent 专家包）

「称骨先生」是一个**传统文化与民俗知识**讲解型 AI 专家，用「收集生辰 → 脚本固定查表计算 → 歌诀文化解读」的工程化流程，把传统称骨歌的数值算法与民俗文化讲清楚。

它**不是**算命先生，不做宿命论判断、不预测命运、不渲染吉凶。所有计算均由脚本确定性查表完成，杜绝 AI 心算幻觉。

---

## 特点

- **确定性计算**：年柱按六十甲子、月柱按农历月、日柱按农历日、时柱按时辰，四项权重相加得出骨重（几两几钱），全程走脚本查表，不靠模型心算
- **文化解读**：把对应骨重的传统歌诀用「文化内涵 + 劝勉」的口吻讲清，附劝勉建议与免责声明
- **干支历法讲解**：讲清六十甲子、干支换算、农历月日时的含义，以及称骨歌的历史文化背景

## 目录结构

```
chenggu-culture-expert/
├── .codebuddy-plugin/
│   └── plugin.json                 # 专家包注册信息
├── agents/
│   └── chenggu-culture-expert.md   # 专家行为设定
├── avatars/
│   └── expert.png                  # 头像
├── skills/
│   └── chenggu-calc/               # 称骨计算技能
│       ├── SKILL.md                # 技能流程说明
│       ├── scripts/chenggu_cli.py  # 固定查表计算脚本
│       └── references/data.md      # 完整数据表（六十甲子、权重、51 条歌诀、6 档等级）
├── LICENSE
└── README.md
```

## 使用方式

### 直接运行计算脚本

无需任何依赖，Python 3 即可：

```bash
# 参数：--year 公历年 --month 农历月 --day 农历日 --hour 时辰
python skills/chenggu-calc/scripts/chenggu_cli.py --year 1990 --month 3 --day 5 --hour 辰时
```

或传入 JSON：

```bash
python skills/chenggu-calc/scripts/chenggu_cli.py --json '{"year":1990,"month":3,"day":5,"hour":"辰时"}'
```

输出包含：年干支、四柱权重、总骨重（几两几钱）、对应歌诀文化解读、等级。

### 安装为 WorkBuddy 专家

将整个专家包目录放入 WorkBuddy 的「我的专家」目录：

```
C:\Users\<用户名>\.workbuddy\plugins\marketplaces\my-experts\plugins\chenggu-culture-expert\
```

然后在 WorkBuddy 中完成注册，即可在专家列表里使用「称骨先生」。

### 使用示例

- 帮我算一下称骨：1990年农历三月初五辰时
- 给我讲讲称骨歌的由来和干支历法
- 称骨里的年柱、月柱、日柱、时柱分别是什么意思？

## 计算说明

| 柱 | 取权重依据 | 说明 |
|----|-----------|------|
| 年柱 | 六十甲子（60 个） | 由公历年份换算干支 `((年-4)%60+60)%60` 取下标 |
| 月柱 | 农历月（1-12） | 正月到腊月各有一个权重 |
| 日柱 | 农历日（1-30） | 初一到三十各有一个权重 |
| 时柱 | 出生时辰（12 个） | 子时到亥时各有一个权重 |

四项权重相加即为「总骨重」，范围 2.1～7.1 两。

## 免责声明

称骨歌属传统民俗文化内容，计算结果仅供娱乐与文化参考，请理性看待，不代替现实中的判断与决策。

## License

[MIT](./LICENSE)
