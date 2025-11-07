# API仕様書

## 概要

本ドキュメントは、エージェント契約自動化システムのAPI仕様を定義します。

## ベースURL

```
/api/v1
```

## 認証

すべてのAPIリクエストには認証が必要です。

```
Authorization: Bearer {token}
```

## エンドポイント一覧

### 契約管理

#### 契約一覧取得

```
GET /contracts
```

**パラメータ**
- `status` (optional): 契約状態でフィルタ
- `page` (optional): ページ番号
- `limit` (optional): 1ページあたりの件数

**レスポンス**
```json
{
  "contracts": [
    {
      "id": "contract-001",
      "clientName": "クライアント名",
      "startDate": "2024-01-01",
      "endDate": "2024-12-31",
      "amount": 1000000,
      "status": "active"
    }
  ],
  "total": 100,
  "page": 1,
  "limit": 20
}
```

#### 契約作成

```
POST /contracts
```

**リクエストボディ**
```json
{
  "clientId": "client-001",
  "startDate": "2024-01-01",
  "endDate": "2024-12-31",
  "amount": 1000000,
  "terms": "契約条件"
}
```

**レスポンス**
```json
{
  "id": "contract-001",
  "clientId": "client-001",
  "startDate": "2024-01-01",
  "endDate": "2024-12-31",
  "amount": 1000000,
  "status": "draft",
  "createdAt": "2024-01-01T00:00:00Z"
}
```

#### 契約詳細取得

```
GET /contracts/{contractId}
```

**レスポンス**
```json
{
  "id": "contract-001",
  "clientId": "client-001",
  "clientName": "クライアント名",
  "startDate": "2024-01-01",
  "endDate": "2024-12-31",
  "amount": 1000000,
  "status": "active",
  "terms": "契約条件",
  "createdAt": "2024-01-01T00:00:00Z",
  "updatedAt": "2024-01-01T00:00:00Z"
}
```

#### 契約更新

```
PUT /contracts/{contractId}
```

**リクエストボディ**
```json
{
  "endDate": "2025-12-31",
  "amount": 1200000,
  "status": "active"
}
```

#### 契約削除

```
DELETE /contracts/{contractId}
```

### 請求書管理

#### 請求書一覧取得

```
GET /invoices
```

**パラメータ**
- `contractId` (optional): 契約IDでフィルタ
- `status` (optional): 支払状態でフィルタ
- `page` (optional): ページ番号
- `limit` (optional): 1ページあたりの件数

**レスポンス**
```json
{
  "invoices": [
    {
      "id": "invoice-001",
      "contractId": "contract-001",
      "issueDate": "2024-01-01",
      "dueDate": "2024-01-31",
      "amount": 100000,
      "status": "paid"
    }
  ],
  "total": 50,
  "page": 1,
  "limit": 20
}
```

#### 請求書作成

```
POST /invoices
```

**リクエストボディ**
```json
{
  "contractId": "contract-001",
  "issueDate": "2024-01-01",
  "dueDate": "2024-01-31",
  "amount": 100000,
  "items": [
    {
      "description": "月額利用料",
      "quantity": 1,
      "unitPrice": 100000
    }
  ]
}
```

#### 請求書詳細取得

```
GET /invoices/{invoiceId}
```

#### 請求書更新

```
PUT /invoices/{invoiceId}
```

**リクエストボディ**
```json
{
  "status": "paid",
  "paidDate": "2024-01-15"
}
```

### クライアント管理

#### クライアント一覧取得

```
GET /clients
```

#### クライアント作成

```
POST /clients
```

**リクエストボディ**
```json
{
  "name": "クライアント名",
  "email": "client@example.com",
  "phone": "03-1234-5678",
  "address": "東京都..."
}
```

#### クライアント詳細取得

```
GET /clients/{clientId}
```

#### クライアント更新

```
PUT /clients/{clientId}
```

#### クライアント削除

```
DELETE /clients/{clientId}
```

## エラーレスポンス

すべてのエラーは以下の形式で返されます：

```json
{
  "error": {
    "code": "ERROR_CODE",
    "message": "エラーメッセージ",
    "details": {}
  }
}
```

### エラーコード一覧

| コード | HTTPステータス | 説明 |
|--------|----------------|------|
| UNAUTHORIZED | 401 | 認証エラー |
| FORBIDDEN | 403 | アクセス権限エラー |
| NOT_FOUND | 404 | リソースが見つからない |
| VALIDATION_ERROR | 400 | バリデーションエラー |
| INTERNAL_ERROR | 500 | サーバーエラー |

## レート制限

- 1分間に60リクエストまで
- 制限を超えた場合、429 Too Many Requestsが返されます
