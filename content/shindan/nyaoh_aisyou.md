+++
date = '2025-11-26T23:39:54+09:00'
draft = false
title = 'nyaohとの相性診断'
+++

{{< rawhtml >}}
<div id="quiz-container">
  <div id="quiz-intro" class="quiz-section active">
    <h2>nyaohとの相性診断</h2>
    <p>いくつかの質問に答えて、あなたとnyaohの相性をチェックしましょう</p>
    <button onclick="startQuiz()" class="btn-primary">診断を開始</button>
  </div>

  <div id="quiz-questions" class="quiz-section">
    <div class="progress-bar">
      <div id="progress" class="progress-fill"></div>
    </div>
    <p class="question-counter">質問 <span id="current-q">1</span> / <span id="total-q">5</span></p>
    
    <div id="question-content">
      <h3 id="question-text"></h3>
      <div id="answer-options" class="answer-grid"></div>
    </div>
  </div>

  <div id="quiz-result" class="quiz-section">
    <h2>診断結果</h2>
    <div class="result-display">
      <div class="result-item">
        <h3>友達相性</h3>
        <div class="result-percentage" id="final-friend">50%</div>
        <p id="friend-message"></p>
      </div>
      <div class="result-item">
        <h3>恋愛相性</h3>
        <div class="result-percentage" id="final-love">50%</div>
        <p id="love-message"></p>
      </div>
    </div>
    <div style="text-align: center; margin-top: 2rem;">
      <button onclick="resetQuiz()" class="btn-primary">もう一度診断する</button>
    </div>
  </div>
</div>

<style>
* {
  box-sizing: border-box;
}

#quiz-container {
  max-width: 720px;
  margin: 3rem auto;
  padding: 0;
  background: #ffffff;
  border-radius: 16px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.07), 0 10px 20px rgba(0, 0, 0, 0.1);
  overflow: hidden;
  border: 1px solid rgba(0, 0, 0, 0.08);
}

.quiz-section {
  display: none;
  padding: 3rem 2.5rem;
}

.quiz-section.active {
  display: block;
  animation: fadeIn 0.3s ease-out;
}

@keyframes fadeIn {
  from { 
    opacity: 0; 
    transform: translateY(8px); 
  }
  to { 
    opacity: 1; 
    transform: translateY(0); 
  }
}

/* イントロ画面 */
#quiz-intro {
  text-align: center;
}

#quiz-intro h2 {
  font-size: 2rem;
  margin: 0 0 1rem 0;
  color: #1a1a1a;
  font-weight: 700;
  letter-spacing: -0.02em;
}

#quiz-intro p {
  font-size: 1.05rem;
  color: #6b7280;
  margin: 0 0 2.5rem 0;
  line-height: 1.6;
}

.btn-primary {
  display: inline-block;
  background: #2563eb;
  color: #ffffff;
  border: none;
  padding: 1rem 2.5rem;
  font-size: 1rem;
  font-weight: 600;
  border-radius: 10px;
  cursor: pointer;
  transition: all 0.2s cubic-bezier(0.4, 0, 0.2, 1);
  box-shadow: 0 2px 4px rgba(37, 99, 235, 0.2);
  font-family: inherit;
}

.btn-primary:hover {
  background: #1d4ed8;
  transform: translateY(-1px);
  box-shadow: 0 4px 8px rgba(37, 99, 235, 0.3);
}

.btn-primary:active {
  transform: translateY(0);
}

/* プログレスバー */
.progress-bar {
  width: 100%;
  height: 4px;
  background: #e5e7eb;
  margin-bottom: 2rem;
  position: relative;
  overflow: hidden;
}

.progress-fill {
  height: 100%;
  background: linear-gradient(90deg, #2563eb 0%, #3b82f6 100%);
  transition: width 0.4s cubic-bezier(0.4, 0, 0.2, 1);
  width: 0%;
}

.question-counter {
  text-align: center;
  color: #6b7280;
  margin: 0 0 2.5rem 0;
  font-size: 0.875rem;
  font-weight: 500;
  letter-spacing: 0.025em;
}

#question-text {
  font-size: 1.5rem;
  margin-bottom: 2.5rem;
  text-align: center;
  color: #1f2937;
  font-weight: 600;
  line-height: 1.5;
}

/* 質問と選択肢 */
.answer-grid {
  display: flex;
  flex-direction: column;
  gap: 0.75rem;
  margin-bottom: 0;
}

.answer-btn {
  padding: 1.25rem 1.5rem;
  background: #f9fafb;
  border: 2px solid #e5e7eb;
  border-radius: 10px;
  cursor: pointer;
  transition: all 0.15s ease;
  text-align: left;
  font-size: 1rem;
  color: #1f2937;
  font-weight: 500;
  line-height: 1.5;
  font-family: inherit;
}

.answer-btn:hover {
  border-color: #2563eb;
  background: #ffffff;
  transform: translateX(4px);
  box-shadow: 0 2px 8px rgba(37, 99, 235, 0.12);
}

.answer-btn:active {
  transform: translateX(2px);
}

/* 結果画面 */
#quiz-result h2 {
  text-align: center;
  color: #1a1a1a;
  margin: 0 0 2.5rem 0;
  font-size: 1.875rem;
  font-weight: 700;
  letter-spacing: -0.02em;
}

.result-display {
  display: grid;
  grid-template-columns: 1fr;
  gap: 1.25rem;
  margin: 0 0 2.5rem 0;
}

.result-item {
  padding: 2rem;
  background: linear-gradient(135deg, #f9fafb 0%, #f3f4f6 100%);
  border-radius: 12px;
  text-align: center;
  border: 1px solid #e5e7eb;
}

.result-item h3 {
  margin: 0 0 1.25rem 0;
  font-size: 1.125rem;
  color: #1f2937;
  font-weight: 600;
}

.result-percentage {
  font-size: 3.5rem;
  font-weight: 800;
  color: #2563eb;
  margin: 0 0 1.25rem 0;
  letter-spacing: -0.03em;
  line-height: 1;
}

.result-item p {
  color: #4b5563;
  line-height: 1.7;
  font-size: 0.95rem;
  margin: 0;
}

#quiz-result > div:last-child {
  text-align: center;
  margin: 0;
}

/* レスポンシブ */
@media (max-width: 768px) {
  #quiz-container {
    margin: 1.5rem;
    border-radius: 12px;
  }

  .quiz-section {
    padding: 2rem 1.5rem;
  }

  #quiz-intro h2 {
    font-size: 1.625rem;
  }

  #quiz-intro p {
    font-size: 1rem;
  }

  .btn-primary {
    padding: 0.875rem 2rem;
    font-size: 0.95rem;
  }

  .result-percentage {
    font-size: 2.75rem;
  }

  .answer-btn {
    padding: 1.125rem 1.25rem;
    font-size: 0.95rem;
  }
}

@media (max-width: 480px) {
  #quiz-container {
    margin: 1rem;
  }

  .quiz-section {
    padding: 1.75rem 1.25rem;
  }

  #quiz-intro h2 {
    font-size: 1.5rem;
  }

  .result-percentage {
    font-size: 2.5rem;
  }
}
</style>

<script>
document.addEventListener('DOMContentLoaded', function() {
  // 質問データ
  const questions = [
    {
        question: "朝型？夜型？",
        answers: [
        { text: "A. 朝型", friend: 5, love: 10 },
        { text: "B. 夜型", friend: 2, love: 5 },
        { text: "C. どちらでもない", friend: 0, love: 0 }
        ]
    },
    {
        question: "休日の過ごし方は？",
        answers: [
        { text: "A. 外に出かける", friend: 5, love: 0 },
        { text: "B. 家でゆっくり", friend: 10, love: 10 },
        { text: "C. だらだら寝て過ごす", friend: -10, love: -10 }
        ]
    },
    {
        question: "連絡頻度の好みは？",
        answers: [
        { text: "A. 毎日たくさん欲しい", friend: 5, love: 10 },
        { text: "B. 程よく欲しい", friend: 5, love: 0 },
        { text: "C. あまり連絡しない", friend: 0, love: -10 }
        ]
    },
    {
        question: "返信の速さは？",
        answers: [
        { text: "A. すぐ返す", friend: 5, love: -10 },
        { text: "B. 気づいたら返す", friend: 10, love: 5 },
        { text: "C. けっこう遅い", friend: -5, love: -10 }
        ]
    },
    {
        question: "初対面で人見知りする？",
        answers: [
        { text: "A. する", friend: 5, love: 0 },
        { text: "B. しない", friend: 10, love: 10 },
        { text: "C. 相手による", friend: -6, love: 0 }
        ]
    },
    {
        question: "決断スピードは？",
        answers: [
        { text: "A. 即決タイプ", friend: 10, love: 6 },
        { text: "B. 考えて決める", friend: 0, love: 5 },
        { text: "C. 優柔不断", friend: -5, love: -15 }
        ]
    },
    {
        question: "インドア？アウトドア？",
        answers: [
        { text: "A. インドア派", friend: 10, love: 10 },
        { text: "B. アウトドア派", friend: -5, love: -10 },
        { text: "C. 半々くらい", friend: 5, love: 0 }
        ]
    },
    {
        question: "サプライズされるのは好き？",
        answers: [
        { text: "A. 大好き", friend: 5, love: 10 },
        { text: "B. まあ好き", friend: 5, love: 0 },
        { text: "C. 苦手", friend: -5, love: -5 }
        ]
    },
    {
        question: "感情は顔に出る？",
        answers: [
        { text: "A. 出まくる", friend: 10, love: 15 },
        { text: "B. 普通", friend: 5, love: 5 },
        { text: "C. 出ない", friend: -5, love: 0 }
        ]
    },
    {
        question: "落ち込んだ時どうしてほしい？",
        answers: [
        { text: "A. 話を聞いてほしい", friend: 10, love: -6 },
        { text: "B. 放っといてほしい", friend: 5, love: 5 },
        { text: "C. 状況次第", friend: 0, love: 0 }
        ]
    },

    {
        question: "好きになったら？",
        answers: [
        { text: "A. 一途", friend: 10, love: 13 },
        { text: "B. わりと柔軟", friend: 6, love: 0 },
        { text: "C. 気持ちが変わりやすい", friend: 6, love: -10 }
        ]
    },
    {
        question: "物事は計画して動く？",
        answers: [
        { text: "A. 計画派", friend: -5, love: 0 },
        { text: "B. その時次第", friend: 0, love: 0 },
        { text: "C. 勢いで行く", friend: 15, love: 10 }
        ]
    },
    {
        question: "金銭感覚は？",
        answers: [
        { text: "A. 超堅実", friend: 0, love: 10 },
        { text: "B. 普通", friend: 5, love: 5 },
        { text: "C. 使いがち", friend: 5, love: 5 }
        ]
    },
    {
        question: "スキンシップの好み",
        answers: [
        { text: "A. かなり好き", friend: 5, love: 16 },
        { text: "B. ほどほど", friend: 5, love: 5 },
        { text: "C. あまり得意じゃない", friend: 5, love: -9 }
        ]
    },
    {
        question: "異性の友達はアリ？",
        answers: [
        { text: "A. 全然OK", friend: 0, love: -6 },
        { text: "B. ちょっと不安", friend: 0, love: 10 },
        { text: "C. だいぶ不安", friend: -5, love: 5 }
        ]
    },
    {
        question: "嘘を見抜ける？",
        answers: [
        { text: "A. 結構わかる", friend: 5, love: 10 },
        { text: "B. 普通", friend: 0, love: 0 },
        { text: "C. ぜんぜん気づかない", friend: -5, love: -10 }
        ]
    },
    {
        question: "食の好みは？",
        answers: [
        { text: "A. 冒険する", friend: 5, love: 2 },
        { text: "B. 好きなもの固定", friend: 10, love: 10 },
        { text: "C. 気分による", friend: 0, love: 0 }
        ]
    },
    {
        question: "旅行は？",
        answers: [
        { text: "A. 行き当たりばったりOK", friend: 5, love: 10 },
        { text: "B. 計画必須", friend: -10, love: -10 },
        { text: "C. どっちも好き", friend: 0, love: 0 }
        ]
    },
    {
        question: "天気が悪くなってる気がする！",
        answers: [
        { text: "A. 外出する", friend: -5, love: -5 },
        { text: "B. 家にいる", friend: 5, love: 10 },
        { text: "C. どっちでもいい", friend: 0, love: 0 }
        ]
    },
    {
        question: "ケンカしたら？",
        answers: [
        { text: "A. すぐ仲直りしたい", friend: 10, love: 10 },
        { text: "B. 時間ほしい", friend: 5, love: 5 },
        { text: "C. 相手次第", friend: -10, love: -10 }
        ]
    },

    {
        question: "甘えるタイプ？",
        answers: [
        { text: "A. 甘える", friend: 5, love: 10 },
        { text: "B. 甘えられる方", friend: 10, love: 15 },
        { text: "C. どっちも苦手", friend: -5, love: -5 },
        { text: "D. どっちも好き", friend: 15, love: 15 }
        ]
    },
    {
        question: "プレゼントは？",
        answers: [
        { text: "A. 実用性！", friend: 5, love: 5 },
        { text: "B. ロマン重視", friend: 0, love: 10 },
        { text: "C. 何でも嬉しい", friend: 10, love: 10 }
        ]
    },
    {
        question: "部屋は？",
        answers: [
        { text: "A. きれいめ", friend: 10, love: 0 },
        { text: "B. ちょい散らかる", friend: 0, love: 5 },
        { text: "C. カオス", friend: -10, love: -15 }
        ]
    },
    {
        question: "好きな性格は？",
        answers: [
        { text: "A. 明るい人", friend: 10, love: 10 },
        { text: "B. 落ち着いた人", friend: 5, love: 10 },
        { text: "C. どっちも好き", friend: 5, love: 5 }
        ]
    },
    {
        question: "SNSの使用頻度は？",
        answers: [
        { text: "A. よく使う", friend: -6, love: -15 },
        { text: "B. ほどほど", friend: 0, love: 0 },
        { text: "C. あまり見ない", friend: 15, love: 5 }
        ]
    },
    {
        question: "笑いのツボは？",
        answers: [
        { text: "A. 浅い", friend: 10, love: 5 },
        { text: "B. 普通", friend: 0, love: 0 },
        { text: "C. 深い", friend: -5, love: -10 }
        ]
    },
    {
        question: "約束は？",
        answers: [
        { text: "A. 絶対守る", friend: 10, love: 10 },
        { text: "B. だいたい守る", friend: 0, love: 0 },
        { text: "C. 忘れがち", friend: -10, love: -10 }
        ]
    },
    {
        question: "食べるスピードは？",
        answers: [
        { text: "A. 速い", friend: 5, love: 0 },
        { text: "B. 普通", friend: 0, love: 0 },
        { text: "C. 遅い", friend: 5, love: 5 }
        ]
    },
    {
        question: "ペットは？",
        answers: [
        { text: "A. 大好き", friend: 10, love: 5 },
        { text: "B. どちらでも", friend: 0, love: 0 },
        { text: "C. 苦手", friend: -5, love: -5 }
        ]
    },
    {
        question: "ハグは好き？",
        answers: [
        { text: "A. 好き", friend: 5, love: 10 },
        { text: "B. 恥ずかしいけど好き", friend: 0, love: 5 },
        { text: "C. 苦手", friend: -5, love: -5 }
        ]
    },
    {
        question: "乗り物酔いする？",
        answers: [
        { text: "A. する", friend: -5, love: 5 },
        { text: "B. しない", friend: 10, love: 0 },
        { text: "C. たまにする", friend: 10, love: 10 }
        ]
    },
    {
        question: "ロマンチック好き？",
        answers: [
        { text: "A. 大好き", friend: 0, love: -10 },
        { text: "B. ほどほど", friend: 0, love: 5 },
        { text: "C. 苦手", friend: -5, love: -10 }
        ]
    },
    {
        question: "大勢と過ごすのは？",
        answers: [
        { text: "A. 好き", friend: 10, love: 0 },
        { text: "B. 少人数が好き", friend: 5, love: 15 },
        { text: "C. 一人が好き", friend: -5, love: -5 }
        ]
    },
    {
        question: "引きずるタイプ？",
        answers: [
        { text: "A. 引きずる", friend: -5, love: -10 },
        { text: "B. 切り替え早い", friend: 10, love: 10 },
        { text: "C. 時と場合による", friend: 0, love: 0 }
        ]
    },
    {
        question: "海と山どっち好き？",
        answers: [
        { text: "A. 海", friend: 5, love: 10 },
        { text: "B. 山", friend: 10, love: 5 },
        { text: "C. どちらでも", friend: 10, love: 10 }
        ]
    },
    {
        question: "照明は？",
        answers: [
        { text: "A. 明るい方が好き", friend: 10, love: 10 },
        { text: "B. 暗めが好き", friend: 5, love: 10 },
        { text: "C. どっちでも", friend: 0, love: 0 }
        ]
    },
    {
        question: "寒がり？暑がり？",
        answers: [
        { text: "A. 寒がり", friend: 5, love: 5 },
        { text: "B. 暑がり", friend: 0, love: 0 },
        { text: "C. 普通", friend: 0, love: 0 }
        ]
    },
    {
        question: "寝る時間は？",
        answers: [
        { text: "A. 早い", friend: 10, love: 10 },
        { text: "B. 遅い", friend: -5, love: -5 },
        { text: "C. 日による", friend: -20, love: -15 }
        ]
    },
    {
        question: "ファッションは？",
        answers: [
        { text: "A. シンプル", friend: 10, love: 10 },
        { text: "B. 派手め", friend: 0, love: 0 },
        { text: "C. 気分で変える", friend: 5, love: 5 }
        ]
    },
    {
        question: "好きになるスピードは？",
        answers: [
        { text: "A. 早い", friend: 5, love: 0 },
        { text: "B. ゆっくり", friend: 10, love: 15 },
        { text: "C. 場合による", friend: 0, love: 10 }
        ]
    },
    {
        question: "記念日は？",
        answers: [
        { text: "A. 大事にする", friend: 0, love: -5 },
        { text: "B. 普通", friend: 0, love: 0 },
        { text: "C. あまり気にしない", friend: 5, love: 10 }
        ]
    },
    {
        question: "嫉妬は？",
        answers: [
        { text: "A. しやすい", friend: -5, love: 15 },
        { text: "B. 普通", friend: 0, love: 0 },
        { text: "C. しにくい", friend: 10, love: -10 }
        ]
    },
    {
        question: "相手の趣味に合わせる？",
        answers: [
        { text: "A. 合わせる", friend: 15, love: 10 },
        { text: "B. 少しだけ", friend: 0, love: 0 },
        { text: "C. あまり合わせない", friend: -5, love: -15 }
        ]
    },
    {
        question: "料理する？",
        answers: [
        { text: "A. よくする", friend: 10, love: 10 },
        { text: "B. たまにする", friend: 5, love: 5 },
        { text: "C. ほぼしない", friend: -5, love: -5 }
        ]
    },
    {
        question: "ゲームは？",
        answers: [
        { text: "A. 大好き", friend: 10, love: 5 },
        { text: "B. ちょっとする", friend: 5, love: 5 },
        { text: "C. あまりしない", friend: -15, love: -5 }
        ]
    },
    {
        question: "怖い話好き？",
        answers: [
        { text: "A. 平気", friend: 10, love: -5 },
        { text: "B. ちょっと苦手", friend: 5, love: 15 },
        { text: "C. 無理", friend: 10, love: 10 }
        ]
    },
    {
        question: "デート場所は？",
        answers: [
        { text: "A. 静かなお店", friend: -10, love: -10 },
        { text: "B. にぎやかな場所", friend: 5, love: 5 },
        { text: "C. その時次第", friend: 0, love: 0 }
        ]
    },
    {
        question: "思考タイプは？",
        answers: [
        { text: "A. ロジカル", friend: 10, love: 0 },
        { text: "B. 直感派", friend: 0, love: 10 },
        { text: "C. 半々", friend: 5, love: 5 }
        ]
    },
    {
        question: "ポジティブ？",
        answers: [
        { text: "A. ポジティブ", friend: 15, love: 15 },
        { text: "B. 普通", friend: 0, love: 0 },
        { text: "C. ネガティブ寄り", friend: -30, love: -35 }
        ]
    },
    {
        question: "物言いは？",
        answers: [
        { text: "A. 率直", friend: 5, love: 15 },
        { text: "B. オブラート", friend: 5, love: -5 },
        { text: "C. どっちも使う", friend: 0, love: 0 }
        ]
    },
    {
        question: "長電話は？",
        answers: [
        { text: "A. 好き", friend: -10, love: -10 },
        { text: "B. たまになら", friend: 0, love: 10 },
        { text: "C. 苦手", friend: 5, love: 5 }
        ]
    },
    {
        question: "人に頼るのは？",
        answers: [
        { text: "A. 得意", friend: 10, love: 5 },
        { text: "B. 普通", friend: 0, love: 0 },
        { text: "C. 苦手", friend: -5, love: -5 }
        ]
    },
    {
        question: "予定が崩れたら？",
        answers: [
        { text: "A. ストレス", friend: -15, love: -15 },
        { text: "B. 柔軟に対応", friend: 15, love: 10 },
        { text: "C. まあまあ気になる", friend: 0, love: -5 }
        ]
    },
    {
        question: "グループLINEでは？",
        answers: [
        { text: "A. よく話す", friend: 10, love: -5 },
        { text: "B. ときどき話す", friend: 10, love: 0 },
        { text: "C. 見る専", friend: 5, love: 5 }
        ]
    },
    {
        question: "プレッシャーに強い？",
        answers: [
        { text: "A. 強い", friend: 10, love: -5 },
        { text: "B. 普通", friend: 0, love: 0 },
        { text: "C. 弱い", friend: 5, love: 10 }
        ]
    },
    {
        question: "掃除の頻度は？",
        answers: [
        { text: "A. よくする", friend: 10, love: 8 },
        { text: "B. たまにする", friend: 0, love: 0 },
        { text: "C. ほぼしない", friend: -10, love: -5 }
        ]
    },
    {
        question: "優先するのは？",
        answers: [
        { text: "A. 自分の気持ち", friend: 5, love: 10 },
        { text: "B. 相手の気持ち", friend: 10, love: 5 },
        { text: "C. バランス", friend: 5, love: 5 }
        ]
    },
    {
        question: "カラオケ好き？",
        answers: [
        { text: "A. 大好き", friend: -10, love: -5 },
        { text: "B. たまに行く", friend: 0, love: 0 },
        { text: "C. あまり行かない", friend: 5, love: 5 }
        ]
    },
    {
        question: "運動は？",
        answers: [
        { text: "A. よくする", friend: 10, love: 10 },
        { text: "B. たまにする", friend: 10, love: 10 },
        { text: "C. 全然しない", friend: 15, love: 5 }
        ]
    },
    {
        question: "買い物の仕方は？",
        answers: [
        { text: "A. 即決", friend: 10, love: 5 },
        { text: "B. 迷う", friend: 5, love: 5 },
        { text: "C. 比較して決める", friend: 15, love: 5 }
        ]
    },
    {
        question: "人間関係で大事なのは？",
        answers: [
        { text: "A. 信頼", friend: 10, love: 10 },
        { text: "B. ノリの良さ", friend: 5, love: 5 },
        { text: "C. 気楽さ", friend: 15, love: 15 }
        ]
    },
    {
        question: "仕事や勉強のスタイルは？",
        answers: [
        { text: "A. コツコツ派", friend: 10, love: 0 },
        { text: "B. 追い込み派", friend: 5, love: 5 },
        { text: "C. 気分でやる", friend: -5, love: 15 }
        ]
    }
  ];

  let currentQuestion = 0;
  let friendScore = 0;
  let loveScore = 0;
  
  // 各質問の平均値からの最大偏差・最小偏差を計算
  let friendMaxDeviation = 0, friendMinDeviation = 0;
  let loveMaxDeviation = 0, loveMinDeviation = 0;
  
  questions.forEach(q => {
    const friendValues = q.answers.map(a => a.friend);
    const loveValues = q.answers.map(a => a.love);
    
    // 各質問の平均値を計算
    const friendAvg = friendValues.reduce((sum, val) => sum + val, 0) / friendValues.length;
    const loveAvg = loveValues.reduce((sum, val) => sum + val, 0) / loveValues.length;
    
    // 平均からの最大偏差・最小偏差を累積
    friendMaxDeviation += Math.max(...friendValues.map(v => v - friendAvg));
    friendMinDeviation += Math.min(...friendValues.map(v => v - friendAvg));
    loveMaxDeviation += Math.max(...loveValues.map(v => v - loveAvg));
    loveMinDeviation += Math.min(...loveValues.map(v => v - loveAvg));
  });

  window.startQuiz = function() {
    const intro = document.getElementById('quiz-intro');
    const questionsSection = document.getElementById('quiz-questions');
    
    if (intro && questionsSection) {
      intro.classList.remove('active');
      questionsSection.classList.add('active');
      showQuestion();
    }
  };

  function showQuestion() {
    const q = questions[currentQuestion];
    
    const questionText = document.getElementById('question-text');
    const answerOptions = document.getElementById('answer-options');
    const currentQ = document.getElementById('current-q');
    const totalQ = document.getElementById('total-q');
    const progress = document.getElementById('progress');
    
    if (questionText) questionText.textContent = q.question;
    if (currentQ) currentQ.textContent = currentQuestion + 1;
    if (totalQ) totalQ.textContent = questions.length;
    
    const progressPercent = ((currentQuestion) / questions.length) * 100;
    if (progress) {
      progress.style.width = progressPercent + '%';
    }
    
    if (answerOptions) {
      answerOptions.innerHTML = '';
      
      q.answers.forEach((answer, index) => {
        const btn = document.createElement('button');
        btn.className = 'answer-btn';
        btn.textContent = answer.text;
        btn.onclick = () => selectAnswer(index);
        answerOptions.appendChild(btn);
      });
    }
  }

  function selectAnswer(index) {
    const answer = questions[currentQuestion].answers[index];
    
    friendScore = Math.max(0, Math.min(100, friendScore + answer.friend));
    loveScore = Math.max(0, Math.min(100, loveScore + answer.love));
    
    setTimeout(() => {
      currentQuestion++;
      if (currentQuestion < questions.length) {
        showQuestion();
      } else {
        showResult();
      }
    }, 300);
  }

  function showResult() {
    document.getElementById('quiz-questions').classList.remove('active');
    document.getElementById('quiz-result').classList.add('active');
    
    // 平均からの偏差を0-100%に正規化
    const friendPercentage = Math.round(((friendScore - friendMinDeviation) / (friendMaxDeviation - friendMinDeviation)) * 100);
    const lovePercentage = Math.round(((loveScore - loveMinDeviation) / (loveMaxDeviation - loveMinDeviation)) * 100);
    
    document.getElementById('final-friend').textContent = friendPercentage + '%';
    document.getElementById('final-love').textContent = lovePercentage + '%';
    
    document.getElementById('progress').style.width = '100%';
    
    // メッセージを生成
    let friendMsg = '';
    if (friendPercentage >= 80) friendMsg = '最高の友達になれそうです。価値観がとても合っています。';
    else if (friendPercentage >= 60) friendMsg = '良い友達関係が築けるでしょう。一緒にいて楽しい時間を過ごせるはずです。';
    else if (friendPercentage >= 40) friendMsg = '普通の友達関係です。お互いを理解し合えば仲良くなれるでしょう。';
    else friendMsg = '少し価値観が違うかもしれません。でも違いを楽しめる関係になれる可能性があります。';
    
    let loveMsg = '';
    if (lovePercentage >= 80) loveMsg = '運命の相手かもしれません。恋愛相性は抜群です。';
    else if (lovePercentage >= 60) loveMsg = '素敵な恋愛関係が築けそうです。お互いを尊重できる関係になれるでしょう。';
    else if (lovePercentage >= 40) loveMsg = '恋愛相性は普通です。努力次第で良い関係になれるかもしれません。';
    else loveMsg = '恋愛は難しいかもしれません。しかし友達としては良い関係が築けるはずです。';
    
    document.getElementById('friend-message').textContent = friendMsg;
    document.getElementById('love-message').textContent = loveMsg;
  }

  window.resetQuiz = function() {
    currentQuestion = 0;
    friendScore = 0;
    loveScore = 0;
    
    document.getElementById('quiz-result').classList.remove('active');
    document.getElementById('quiz-intro').classList.add('active');
    
    document.getElementById('progress').style.width = '0%';
  };
});
</script>
{{< /rawhtml >}}