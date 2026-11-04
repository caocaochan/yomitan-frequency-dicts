# Yomitan frequency dictionaries

Chinese word frequency dictionaries for [Yomitan](https://github.com/yomidevs/yomitan),
built from real-world text and segmented into words with [HanLP](https://github.com/hankcs/HanLP).
Each one shows a word's rank in Yomitan (1 = most common).

| Dictionary | Shows in Yomitan as | Source | Words | Download |
| --- | --- | --- | --- | --- |
| Bilibili | **Bilibili** | 2.29B Bilibili comments (25% sample) | 1,958,154 | [Bilibili.zip](https://github.com/caocaochan/yomitan-frequency-dicts/releases/latest/download/Bilibili.zip) |
| Danmei | **Danmei** | 2,047 danmei novels | 264,348 | [Danmei.zip](https://github.com/caocaochan/yomitan-frequency-dicts/releases/latest/download/Danmei.zip) |

## Install

1. Download a zip from the table above, or from the [latest release](https://github.com/caocaochan/yomitan-frequency-dicts/releases/latest).
2. In Yomitan, open Settings → Dictionaries → Import and pick the zip.
3. Make sure Yomitan's language is set to Chinese.

Both dictionaries are simplified Chinese, rank-based, and have no readings, so they work alongside any
Chinese dictionary (CC-CEDICT and others).

## Bilibili

Casual, spoken-style internet Chinese: slang such as 好家伙, 破防, 离谱 and 三连 ranks high.

- **Source:** 2,289,260,938 comments from Bilibili videos (duplicate comment IDs removed).
- **Cleaning:** removed reply prefixes (`回复 @name :`), @mentions, emote codes such as `[doge]`,
  links and video IDs. Comments were split into sentences, and identical sentences were segmented once
  and counted by how often they appear.
- **Sample:** this is a partial build from a random 25% of the sentences (256 of 1024 hash shards).
  A full build will replace it.
- **Segmentation:** HanLP `COARSE_ELECTRA_SMALL_ZH` and `FINE_ELECTRA_SMALL_ZH` together. A coarse word
  is kept whole if it is a headword in one of 9 Chinese dictionaries (CC-CEDICT, 汉语大词典, Moegirlpedia
  and others); otherwise it is counted as the fine words inside it. This gives 7.38B Chinese word tokens.
- **Kept:** words made only of Chinese characters and seen at least 5 times. Runs of one repeated
  character four or more long (啊啊啊啊) are dropped; 哈哈哈 is kept.

Compounds that no dictionary lists are split into fine-grained parts (都是 → 都 + 是, 十周年 → 十 + 周年),
so they don't get a rank of their own.

## Danmei

Written narrative Chinese from danmei (BL) web novels.

- **Source:** every novel on zhenhunxiaoshuo.com, 2,047 novels and 640.9M tokens.
- **Segmentation:** HanLP coarse-grained tokenizer, which keeps compounds and idioms together.
- **Kept:** words seen at least 5 times in at least 3 different novels. The 3-novel rule removes most
  character names.

The dictionaries contain only words and their ranks, no source text.
