# 技术方案 - 背单词网站

## 架构概览
单文件 Web 应用：HTML + CSS + JavaScript，无后端依赖。

## 技术选型

| 层级 | 技术 | 说明 |
|------|------|------|
| 结构 | HTML5 | 语义化标签 |
| 样式 | CSS3 | Flexbox + Grid，CSS 变量 |
| 逻辑 | Vanilla JavaScript (ES6+) | 无框架依赖 |
| 发音 | Web Speech API | 浏览器内置 TTS |
| 存储 | localStorage | 浏览器本地持久化 |
| 字体 | 系统默认字体 | 中文苹方/微软雅黑，英文 Segoe UI |

## 数据流

```
词库数据 (JS数组) → 随机抽取 → 生成选项 → 用户选择
                                    ↓
                              判断对错 → 更新统计
                                    ↓
                              答错 → 写入 localStorage
                                    ↓
                              错题本 ← 读取 localStorage
```

## 数据结构

### 单词条目
```javascript
{
  id: number,        // 唯一标识
  word: string,      // 英文单词
  phonetic: string,  // 音标
  meaning: string,   // 中文释义
  pos: string        // 词性 (n./v./adj./adv./...)
}
```

### 错题本 (localStorage)
```javascript
// Key: "wrong_words"
// Value: JSON array of word objects
[
  { id: 1, word: "peril", meaning: "危险", wrongCount: 3, lastWrong: "2026-06-20" },
  ...
]
```

### 统计 (localStorage)
```javascript
// Key: "stats"
// Value: JSON object
{
  totalAttempted: 150,    // 总答题数
  totalCorrect: 120,      // 正确数
  wrongWordIds: [1,5,23], // 错题词ID列表
}
```

## 核心算法

### 随机抽词
```javascript
// Fisher-Yates 洗牌后的循环队列，保证每个单词都会被抽到
function getNextWord() {
  if (queue.length === 0) {
    queue = shuffle([...wordBank]);
  }
  return queue.pop();
}
```

### 干扰项生成
```javascript
// 从词库中随机选3个不同于正确答案的单词的释义
function generateOptions(correctWord) {
  const others = wordBank.filter(w => w.id !== correctWord.id);
  const distractors = shuffle(others).slice(0, 3).map(w => w.meaning);
  return shuffle([correctWord.meaning, ...distractors]);
}
```

### Web Speech API 发音
```javascript
function speakWord(word) {
  const utterance = new SpeechSynthesisUtterance(word);
  utterance.lang = 'en-US';
  utterance.rate = 0.8; // 稍慢速
  speechSynthesis.speak(utterance);
}
```

## 浏览器兼容性
- Chrome 90+
- Edge 90+
- Firefox 88+
- Web Speech API 兼容性：以上浏览器均支持

## 文件大小预估
- HTML 结构：~5KB
- CSS 样式：~5KB
- JavaScript 逻辑：~15KB
- 词库数据：~80KB (1500词 × ~50字节/词)
- **总计：~105KB**，加载极快
