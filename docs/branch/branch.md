---
presentationID: 1MWQEtUPdOWkKqo4hzWhQyVkJpIyHxm8ZshtSEJXbWcg
title: ブランチについて
breaks: true
marp: true
---

# 正しいブランチの図

<pre class="mermaid">
gitGraph
    commit id: "初期コミット"
    commit id: "機能追加"

    branch team_a/feature_a
    checkout main
    commit id: "他のチームの変更1"

    checkout team_a/feature_a
    commit id: "feature_a: 実装開始"
    commit id: "feature_a: 機能追加"
    commit id: "feature_a: テスト追加"

    checkout main
    branch team_b/feature_b
    commit id: "feature_b: 実装開始"
    commit id: "feature_b: 機能改善"
    commit id: "feature_b: バグ修正"

    checkout main
    merge team_a/feature_a tag: "マージ成功"

    commit id: "他のチームの変更2"

    checkout main
    merge team_b/feature_b tag: "マージ成功"

    commit id: "最新のコミット"
</pre>

<style>
  .mermaid {
    font-size: 22px !important;
  }
  .mermaid .commit-label {
    font-size: 16px !important;
  }
  .mermaid .branch-label {
    font-size: 22px !important;
  }
  .mermaid .tag-label {
    font-size: 16px !important;
  }
  /* mainブランチとteam_a/feature_aを白抜きに */
  .mermaid .branch-label0,
  .mermaid .branch-label1,
  .mermaid .branch-label2 {
    fill: #ffffff !important;
    stroke: #ffffff !important;
  }
</style>

<script type="module">
  import mermaid from 'https://cdn.jsdelivr.net/npm/mermaid@latest/dist/mermaid.esm.min.mjs';
  mermaid.initialize({
    startOnLoad: true,
    themeVariables: {
      git0: '#0052cc',
      git1: '#d93f0b',
      git2: '#22a06b',
    }
  });
</script>
---

## 間違ったブランチ運用の例

同じチームで同じ機能を別々のブランチで実装してしまうケース。

<pre class="mermaid">
gitGraph
    commit id: "初期コミット"
    commit id: "mainの最新"

    branch team_a/feature_a
    checkout team_a/feature_a
    commit id: "太郎: 機能Aの実装開始"
    commit id: "太郎: 機能Aの実装完了"
    commit id: "太郎: テスト追加"

    checkout main
    branch team_a/feature_a_hanako
    checkout team_a/feature_a_hanako
    commit id: "花子: 機能Aの実装開始"
    commit id: "花子: 機能Aの実装完了"
    commit id: "花子: テスト追加"

    checkout main
    merge team_a/feature_a tag: "マージ成功"

    commit id: "他の変更"

    checkout main
    merge team_a/feature_a_hanako tag: "競合エラー!"
</pre>

**問題点:**
- 太郎さんと花子さんが同じ機能を別々のブランチで実装
- 太郎さんの`team_a/feature_a`が先にマージされる
- 花子さんの`team_a/feature_a_hanako`をマージしようとすると競合(conflict)が発生
- 同じファイルの同じ箇所を両方が変更しているため、Gitがどちらを採用すべきか判断できない
