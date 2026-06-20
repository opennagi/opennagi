# OpenNagi

> 嵐を静める。AI から人間への通知を、受け手主権で束ねて届ける。

OpenNagi は、AI が生む通知の洪水と、人間の有限な注意の間に立つレイヤ。自律 AI エージェントが人間に伝えたいことを受け取り、まとめ、選別し、邪魔にならない形に整えてから届ける。

名前は **open**（どんな AI でもどんな通知でも取り込む、開かれた受け口）と、**凪**（風が止み波が静まる状態）を組み合わせたもの。入口で何でも取り込み、出口で静かにして返す。

このリポジトリは OpenNagi 全体の**入口（ハブ）**。全体像と各コンポーネントへの導線を置く。コードは各リポジトリにある。

## いまの状態

構想と MVP 設計の段階。最初に出す機能は束ね（Digest）で、RSS を「最初のエージェント」として受け口プロトコルに写すところから始める。前身は Tutiino という更新通知アプリで、AI 時代に合わせてコンセプトを反転させた経緯がある。

## 構成（リポジトリ）

OpenNagi は4つのリポジトリに分割されている。**`protocol` が契約層の根**で、`server` と `app` はその契約に一方向で依存する。

| リポジトリ | 公開 | 役割 |
| --- | --- | --- |
| [**protocol**](https://github.com/opennagi/protocol) | 🌐 Public | 契約層。受け口エンベロープ（送り手が投げる単一の入力）の Zod スキーマ・型・OpenAPI 片と、公開 SDK（sender SDK・RSS アダプタ）。何にも依存しない根。 |
| [**server**](https://github.com/opennagi/server) | 🔒 Private | バックエンド。受け口（`/intake`）で取り込み、束ね・選別し、定時配信する。`protocol` に依存。設計ドキュメント（concept / mvp / protocol / open-strategy / stack / build-plan）もここ。 |
| [**app**](https://github.com/opennagi/app) | 🔒 Private | 受け手のモバイルクライアント（Expo / React Native）。 |
| [**web**](https://github.com/opennagi/web) | 🔒 Private | 公式サイト [opennagi.com](https://opennagi.com)。Cloudflare Workers（Static Assets）で配信。 |

```
            ┌─────────────┐
            │  protocol   │  契約層（受け口エンベロープ + SDK）
            └──────┬──────┘
                   │ 一方向に依存
        ┌──────────┴──────────┐
        ▼                     ▼
  ┌───────────┐         ┌───────────┐
  │  server   │         │   app     │
  │ 取り込み・ │         │ 受け手の  │
  │ 束ね・配信 │         │ クライアント│
  └───────────┘         └───────────┘

  ┌───────────┐
  │   web     │  opennagi.com（ブランドの公開面）
  └───────────┘
```

## ドキュメント

設計ドキュメントは現状 [`server/docs/`](https://github.com/opennagi/server/tree/main/docs) にある。

- `concept.md` — 正式コンセプト（背景・中核の考え方・スコープ・ブランド）
- `mvp.md` — MVP 計画（最初に出す束ね＝Digest の仕様と検証仮説）
- `protocol.md` — 受け口プロトコルとデータモデルの素案
- `open-strategy.md` — 公開戦略（4層のオープンコア・ライセンス方針）
- `stack.md` — MVP 技術選定
- `build-plan.md` — MVP 実装計画（リポジトリ構成とビルド順）

## ライセンス

[`open-strategy.md`](https://github.com/opennagi/server/blob/main/docs/open-strategy.md) のオープンコア方針に従い、ライセンスはリポジトリごとに定める。`protocol` は公開（OSS）、その他は段階的に公開を検討する。
