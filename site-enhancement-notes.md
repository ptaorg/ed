# PTA運営適正化指針サイト 強化指示メモ

## 反映方針

1. リンク切れ対策
   - 現行URLを優先する。
   - リンク切れが確認された場合のみ、実在確認済みのアーカイブURLを併記する。
   - 推測でアーカイブURLを作らない。
   - 表示名は「現行リンク」「アーカイブ」に分ける。

2. 用語統一
   - 「入会届」「入会申込書」「加入申込書」「加入届」「入会書類」などは、本文上は原則として「入会申込記録」に統一する。
   - ただし、既存資料名・引用中の様式名は原資料の名称を残す。
   - 説明文では「紙の申込書に限定せず、電子回答、署名済み文書、会則確認記録等を含む」と明記する。

3. 黄色マーカー
   - 重要な制度上の結論には mark クラスを使う。
   - 例：<span class="mark">入会申込記録のない会費請求は、後から検証できない。</span>
   - 例：<span class="mark">PTAの活動規模は、適法に集められる会員、会費、人員に応じて設計する。</span>

4. 追加すべき図解
   - 問題構造フロー：入会申込記録なし → 会費徴収 → 名簿提供 → 教職員関与 → 任意性喪失
   - 適正運用フロー：PTA説明 → 入会申込記録 → PTA会員名簿 → PTA会費請求 → 活動規模の再設計
   - マインドマップ：入会申込記録、個人情報、会計分離、職務専念義務、公的媒体、公平性

## CSS追記案

```css
.mark {
  background: linear-gradient(transparent 46%, #fff176 46%);
  font-weight: 900;
  color: #101828;
}
.flow {
  display: flex;
  gap: .65rem;
  align-items: stretch;
  margin: 1.4rem 0;
  overflow-x: auto;
}
.flow .step {
  min-width: 168px;
  flex: 1;
  background: #fff;
  border: 1px solid var(--border-color);
  border-radius: 13px;
  padding: .95rem;
  position: relative;
}
.flow .step:not(:last-child)::after {
  content: "→";
  position: absolute;
  right: -.62rem;
  top: 50%;
  transform: translateY(-50%);
  background: var(--main-color);
  color: #fff;
  width: 1.35rem;
  height: 1.35rem;
  border-radius: 50%;
  display: grid;
  place-items: center;
  font-weight: 900;
  z-index: 2;
}
.step-label {
  font-size: .76rem;
  font-weight: 900;
  color: #fff;
  background: var(--main-color);
  display: inline-block;
  border-radius: 999px;
  padding: .1rem .55rem;
  margin-bottom: .45rem;
}
.step-title {
  font-weight: 900;
  color: var(--main-color);
  margin-bottom: .25rem;
}
.mindmap {
  display: grid;
  grid-template-columns: repeat(3, minmax(0, 1fr));
  gap: .9rem;
  margin: 1.5rem 0;
}
.mind-center {
  grid-column: 1 / 4;
  background: var(--main-color);
  color: #fff;
  border-radius: 16px;
  text-align: center;
  padding: 1.1rem;
  font-weight: 900;
}
.node {
  border: 1px solid var(--border-color);
  border-radius: 14px;
  background: #fff;
  padding: 1rem;
}
@media (max-width: 1100px) {
  .flow { display: block; }
  .flow .step { margin-bottom: .7rem; }
  .flow .step:not(:last-child)::after {
    content: "↓";
    right: 50%;
    top: auto;
    bottom: -.7rem;
    transform: translateX(50%);
  }
  .mindmap { grid-template-columns: 1fr; }
  .mind-center { grid-column: auto; }
}
```

## 図解HTML案1：問題構造フロー

```html
<div class="flow" aria-label="問題構造フロー">
  <div class="step"><span class="step-label">入口</span><div class="step-title">入会申込記録がない</div><p>本人意思を後から検証できない。</p></div>
  <div class="step"><span class="step-label">会費</span><div class="step-title">学校徴収金に混在</div><p>学校会計と団体会計が区別されにくい。</p></div>
  <div class="step"><span class="step-label">情報</span><div class="step-title">学校名簿をPTAへ</div><p>目的外提供・第三者提供の問題が生じる。</p></div>
  <div class="step"><span class="step-label">労務</span><div class="step-title">教職員が回収・督促</div><p>勤務時間内の私的団体事務になる。</p></div>
  <div class="step"><span class="step-label">結果</span><div class="step-title">任意性が見えない</div><p>保護者から学校制度のように見える。</p></div>
</div>
```

## 図解HTML案2：適正運用フロー

```html
<div class="flow" aria-label="適正運用フロー">
  <div class="step"><span class="step-label">1</span><div class="step-title">PTAが説明</div><p>会則・会費額・活動範囲・個人情報利用目的・退会方法を提示。</p></div>
  <div class="step"><span class="step-label">2</span><div class="step-title">入会申込記録</div><p>本人の意思表示をPTAが記録・保存。</p></div>
  <div class="step"><span class="step-label">3</span><div class="step-title">PTA会員名簿</div><p>学校名簿ではなく、PTAが取得した会員情報で管理。</p></div>
  <div class="step"><span class="step-label">4</span><div class="step-title">会費請求</div><p>PTAが会員に対して請求。学校徴収金とは分離。</p></div>
  <div class="step"><span class="step-label">5</span><div class="step-title">活動設計</div><p>加入者・資金・人員に見合う範囲で活動を縮減・再設計。</p></div>
</div>
```

## 図解HTML案3：マインドマップ

```html
<div class="mindmap" aria-label="制度整理マインドマップ">
  <div class="mind-center">PTA運営適正化 ＝ 学校と任意団体の境界を明確にする</div>
  <div class="node"><b>入会申込記録</b><p>会費請求、会員名簿、役員選出、配布対象を支える入口。</p></div>
  <div class="node"><b>個人情報</b><p>学校保有情報をPTA内部事務に使う根拠と同意の確認。</p></div>
  <div class="node"><b>会計分離</b><p>学校徴収金とPTA会費を同一フローに置かない。</p></div>
  <div class="node"><b>職務専念義務</b><p>勤務時間内にPTA会計・督促・名簿・役員選出を扱う危険。</p></div>
  <div class="node"><b>公平性</b><p>非会員児童生徒への不利益、不参加家庭への圧力を防ぐ。</p></div>
  <div class="node"><b>公的媒体</b><p>学校ホームページ・学校メールで私的団体の勧誘をしない。</p></div>
</div>
```

## 本文差し替え例

- 「入学時にPTA加入が当然扱いされ、入会届がない」
  - 修正後：「入学時にPTA加入が当然扱いされ、入会申込記録がない」

- 「加入申込書の有無、未加入者への不利益説明の有無、退会手続の有無」
  - 修正後：「入会申込記録の有無、未加入者への不利益説明の有無、退会手続の有無」

- 「担任が入会届・委任状・会費袋を回収し、未提出者を確認」
  - 修正後：「担任が入会申込記録・委任状・会費袋を回収し、未提出者を確認」

- 「毎年度、各校の配布文書、入会届、会費徴収方法、個人情報提供記録、学校HP掲載、教職員関与の有無を点検する。」
  - 修正後：「毎年度、各校の配布文書、入会申込記録、会費徴収方法、個人情報提供記録、学校HP掲載、教職員関与の有無を点検する。」

## 強調文として追加推奨

```html
<div class="warn-box">
  <span class="box-title">確認の起点</span>
  <p><span class="mark">PTA会費を請求する前提は、入会申込記録の存在です。</span> 入会申込記録が確認できない場合、会費徴収、会員名簿、役員選出、学校からPTAへの情報提供を連鎖的に点検する必要があります。</p>
</div>
```
