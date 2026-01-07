# Next.js Dashboard Application

このプロジェクトは、**Next.js App Router Course** で学習する **ダッシュボードアプリケーション** です。

## 📋 プロジェクト概要
ダッシュボード管理システムです。以下の機能を備えています：

- **ユーザー認証**：NextAuth.js を使用したセキュアなログイン機能
- **ダッシュボード**：売上チャート、最新の請求書、キャード表示
- **請求書管理**：請求書の作成、編集、削除、ステータス管理（保留中 / 支払済み）
- **顧客管理**：顧客情報の一覧表示と詳細情報
- **レスポンシブデザイン**：モバイル・タブレット・デスクトップに対応

---

## 🛠️ 技術スタック

| カテゴリ | 使用技術 |
|---------|--------|
| **フロントエンド** | Next.js (latest), React (latest), TypeScript 5.7.3 |
| **スタイリング** | Tailwind CSS 3.4.17, PostCSS 8.5.1 |
| **認証** | NextAuth.js 5.0.0-beta.25 |
| **データベース** | PostgreSQL (postgres ^3.4.6) |
| **UIコンポーネント** | Heroicons (React) 2.2.0 |
| **ユーティリティ** | Zod 3.25.17, clsx 2.1.1, use-debounce 10.0.4 |
| **セキュリティ** | bcrypt 5.1.1 |
| **パッケージマネージャー** | pnpm |

---

## 📁 プロジェクト構成

```
nextjs-dashboard/
├── app/                          # Next.js App Router ディレクトリ
│   ├── layout.tsx                # ルートレイアウト（全ページの基本構造）
│   ├── page.tsx                  # ホームページ
│   ├── dashboard/                # ダッシュボードセクション
│   │   ├── layout.tsx            # ダッシュボードレイアウト
│   │   ├── page.tsx              # ダッシュボードメインページ
│   │   ├── customers/
│   │   │   └── page.tsx          # 顧客一覧ページ
│   │   └── invoices/
│   │       └── page.tsx          # 請求書一覧ページ
│   ├── lib/                      # ユーティリティ関数とデータベース関連
│   │   ├── data.ts               # データベース接続とクエリ関数
│   │   ├── definitions.ts        # TypeScript型定義
│   │   ├── placeholder-data.ts   # テスト用ダミーデータ
│   │   └── utils.ts              # ヘルパー関数（通貨フォーマットなど）
│   ├── seed/                     # データベースシーディング
│   │   └── route.ts              # DB初期化エンドポイント
│   ├── query/                    # クエリ関連エンドポイント
│   │   └── route.ts
│   └── ui/                       # UIコンポーネント
│       ├── global.css            # グローバルスタイル
│       ├── fonts.ts              # Google Fonts設定（Inter, Lusitana）
│       ├── button.tsx            # ボタンコンポーネント
│       ├── search.tsx            # 検索フォーム
│       ├── skeletons.tsx         # ローディングスケルトン
│       ├── login-form.tsx        # ログインフォーム
│       ├── acme-logo.tsx         # ロゴコンポーネント
│       ├── dashboard/
│       │   ├── nav-links.tsx     # ナビゲーションリンク
│       │   ├── sidenav.tsx       # サイドナビゲーション
│       │   ├── cards.tsx         # ダッシュボードカード
│       │   ├── revenue-chart.tsx # 売上チャート
│       │   └── latest-invoices.tsx # 最新請求書リスト
│       ├── customers/
│       │   └── table.tsx         # 顧客テーブル
│       └── invoices/
│           ├── table.tsx         # 請求書テーブル
│           ├── create-form.tsx   # 請求書作成フォーム
│           ├── edit-form.tsx     # 請求書編集フォーム
│           ├── breadcrumbs.tsx   # パンくずリスト
│           ├── buttons.tsx       # アクションボタン
│           ├── pagination.tsx    # ページネーション
│           └── status.tsx        # ステータスバッジ
├── public/                       # 静的ファイル
│   ├── favicon.ico
│   ├── hero-desktop.png
│   ├── hero-mobile.png
│   ├── opengraph-image.png
│   └── customers/                # 顧客プロフィール画像
├── .env.example                  # 環境変数テンプレート
├── tsconfig.json                 # TypeScript設定
├── tailwind.config.ts            # Tailwind CSS設定
├── next.config.ts                # Next.js設定
├── postcss.config.js             # PostCSS設定
├── package.json                  # プロジェクト依存関係
└── README.md                     # このファイル
```

---

## 🚀 セットアップとインストール

### 前提条件

- Node.js 18.0 以上
- npm / yarn / pnpm
- PostgreSQL データベース

### インストール手順

1. **リポジトリをクローン**

```bash
git clone <repository-url>
cd nextjs-dashboard
```

2. **依存関係をインストール**

```bash
pnpm install
```

3. **環境変数を設定**

`.env.example` を参考に `.env.local` を作成します：

```bash
cp .env.example .env.local
```

`.env.local` に以下の情報を入力：

```env
# PostgreSQL接続情報（Vercel PostgreSQLの場合）
POSTGRES_URL=postgresql://user:password@host:5432/database
POSTGRES_PRISMA_URL=postgresql://user:password@host:5432/database
POSTGRES_URL_NON_POOLING=postgresql://user:password@host:5432/database
POSTGRES_USER=your_username
POSTGRES_HOST=your_host
POSTGRES_PASSWORD=your_password
POSTGRES_DATABASE=your_database

# NextAuth.js設定
AUTH_SECRET=<openssl rand -base64 32で生成>
AUTH_URL=http://localhost:3000/api/auth
```

> **ジェネレータ：** `openssl rand -base64 32` で AUTH_SECRET を生成してください。

4. **データベースを初期化**

```bash
curl http://localhost:3000/api/seed
```

または開発サーバー起動後、ブラウザで `http://localhost:3000/seed` にアクセスします。

5. **開発サーバーを起動**

```bash
pnpm dev
```

ブラウザで `http://localhost:3000` を開きます。

---

## 📚 利用可能なスクリプト

```bash
# 開発サーバーを起動（Turbopack有効）
pnpm dev

# 本番用にビルド
pnpm build

# 本番サーバーを起動
pnpm start
```

---

## 🔐 ログイン認証

### テストアカウント

データベースシーディングにより、以下のテストユーザーが作成されます：

| メール | パスワード |
|--------|----------|
| `user@nextmail.com` | `123456` |

### NextAuth.js設定

- **認証方式**：Email/Password（bcryptでハッシュ化）
- **セッション管理**：JWT
- **パッケージ**：`next-auth@5.0.0-beta.25`

---

## 📊 主要機能

### 1. ダッシュボード
- 売上チャートの可視化（月別売上）
- 最新の5件の請求書表示
- 顧客・請求書サマリーカード

### 2. 請求書管理（Invoices）
- 請求書一覧（テーブル表示）
- ページネーション機能
- 請求書作成（新規）
- 請求書編集
- ステータス変更（保留中 ↔ 支払済み）
- ステータスバッジ表示

### 3. 顧客管理（Customers）
- 顧客一覧表示
- 顧客ごとの請求書統計
  - 総請求書数
  - 支払済み金額
  - 保留中金額

### 4. 認証・セキュリティ
- ログインページ
- パスワードのbcryptハッシュ化
- NextAuth.js によるセッション管理
- ダッシュボード保護（ログイン必須）

---

## 🎨 スタイリングと設計

### Tailwind CSS カスタマイズ

`tailwind.config.ts` で定義されたカスタムカラー：

```typescript
colors: {
  blue: {
    400: '#2589FE',
    500: '#0070F3',
    600: '#2F6FEB',
  }
}
```

グリッド設定：

```typescript
gridTemplateColumns: {
  '13': 'repeat(13, minmax(0, 1fr))',
}
```

### Heroicons UIアイコン

- `ArrowRightIcon` - リンク矢印
- `AtSymbolIcon` - メールフィールド
- `KeyIcon` - パスワードフィールド
- その他各種アイコン

### フォント

- **Inter** - サンセリフフォント（本文）
- **Lusitana** - セリフフォント（見出し）

---

## 🗄️ データベススキーマ

### Users テーブル

```sql
CREATE TABLE users (
  id UUID PRIMARY KEY DEFAULT uuid_generate_v4(),
  name VARCHAR(255) NOT NULL,
  email TEXT NOT NULL UNIQUE,
  password TEXT NOT NULL
);
```

### Invoices テーブル

```sql
CREATE TABLE invoices (
  id UUID PRIMARY KEY DEFAULT uuid_generate_v4(),
  customer_id UUID NOT NULL,
  amount INT NOT NULL,
  status VARCHAR(255) NOT NULL,
  date DATE NOT NULL,
  FOREIGN KEY (customer_id) REFERENCES customers(id)
);
```

### Customers テーブル

```sql
CREATE TABLE customers (
  id UUID PRIMARY KEY DEFAULT uuid_generate_v4(),
  name VARCHAR(255) NOT NULL,
  email TEXT NOT NULL,
  image_url VARCHAR(255) NOT NULL
);
```

### Revenue テーブル

```sql
CREATE TABLE revenue (
  month VARCHAR(4) NOT NULL UNIQUE,
  revenue INT NOT NULL
);
```

---

## 📝 型定義（TypeScript）

主要な型は `app/lib/definitions.ts` に定義：

- `User` - ユーザー情報
- `Customer` - 顧客情報
- `Invoice` - 請求書情報（ステータス: 'pending' | 'paid'）
- `Revenue` - 月別売上
- `LatestInvoice` - 最新請求書
- `InvoicesTable` - テーブル表示用請求書
- `CustomersTableType` - テーブル表示用顧客

---

## 🔄 データベースクエリ関数

`app/lib/data.ts` で定義されたデータ取得関数：

```typescript
export async function fetchRevenue()           // 売上データ
export async function fetchLatestInvoices()    // 最新請求書
export async function fetchCardData()          // サマリーカードデータ
export async function fetchFilteredInvoices()  // フィルター付き請求書
export async function fetchInvoiceById()       // 請求書詳細
export async function fetchCustomers()         // 顧客リスト
export async function fetchFilteredCustomers() // フィルター付き顧客
export async function fetchCustomerById()      // 顧客詳細
export async function getUser()                // ユーザー認証
```

---

## ⚙️ ユーティリティ関数

`app/lib/utils.ts`：

- `formatCurrency(amount)` - 金額をUSD形式にフォーマット
- `formatDateToLocal(date)` - 日付をローカル形式に変換
- `generateYAxis(revenue)` - グラフのY軸データを生成

---

## 🧪 データシーディング

`app/seed/route.ts` では、以下のテーブルを初期化・シーディング：

1. **Users** - テストユーザーを作成
2. **Customers** - サンプル顧客データ
3. **Invoices** - サンプル請求書データ
4. **Revenue** - 月別売上データ

> ⚠️ このエンドポイントは開発時のみ使用します。本番環境では無効にしてください。

---

## 🚢 デプロイ

### Vercelへのデプロイ

1. GitHub にプッシュ
2. Vercel に接続
3. 環境変数を設定（`.env.local` の内容をVercelダッシュボードに追加）
4. デプロイ実行

```bash
vercel deploy
```

---

## 📖 参考資料

- [Next.js 公式ドキュメント](https://nextjs.org/docs)
- [Next.js Learn Course](https://nextjs.org/learn)
- [Tailwind CSS ドキュメント](https://tailwindcss.com/docs)
- [NextAuth.js ドキュメント](https://next-auth.js.org)

---

## 📝 ライセンス

このプロジェクトは Next.js Learning Course の一部です。

---

## 🤝 貢献

このはプロジェクトは学習用リポジトリです。改善提案やバグ報告は Issue として提出してください。

---

**最終更新**: 2026年1月8日
