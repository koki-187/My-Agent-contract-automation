# テンプレート

このディレクトリには、契約書や請求書などのテンプレートファイルを格納します。

## テンプレート一覧

### 契約書テンプレート

1. **contract-template.md** - Markdown形式の契約書テンプレート
2. **contract-template-basic.md** - 基本的な契約書テンプレート
3. **contract-template-detailed.md** - 詳細な契約書テンプレート

### 請求書テンプレート

1. **invoice-template.md** - Markdown形式の請求書テンプレート
2. **invoice-template-simple.md** - シンプルな請求書テンプレート

### その他のテンプレート

1. **nda-template.md** - 秘密保持契約書テンプレート
2. **agreement-template.md** - 業務委託契約書テンプレート

## テンプレート変数

テンプレート内では以下の変数を使用できます：

### 契約書変数

- `{{CONTRACT_NUMBER}}` - 契約番号
- `{{CONTRACT_DATE}}` - 契約日
- `{{CLIENT_NAME}}` - クライアント名
- `{{CLIENT_ADDRESS}}` - クライアント住所
- `{{CLIENT_REPRESENTATIVE}}` - クライアント代表者名
- `{{COMPANY_NAME}}` - 自社名
- `{{COMPANY_ADDRESS}}` - 自社住所
- `{{COMPANY_REPRESENTATIVE}}` - 自社代表者名
- `{{START_DATE}}` - 契約開始日
- `{{END_DATE}}` - 契約終了日
- `{{CONTRACT_AMOUNT}}` - 契約金額
- `{{PAYMENT_TERMS}}` - 支払条件
- `{{SERVICE_DESCRIPTION}}` - サービス内容

### 請求書変数

- `{{INVOICE_NUMBER}}` - 請求書番号
- `{{INVOICE_DATE}}` - 請求日
- `{{DUE_DATE}}` - 支払期限
- `{{CLIENT_NAME}}` - クライアント名
- `{{CLIENT_ADDRESS}}` - クライアント住所
- `{{COMPANY_NAME}}` - 自社名
- `{{COMPANY_ADDRESS}}` - 自社住所
- `{{ITEMS}}` - 請求項目リスト
- `{{SUBTOTAL}}` - 小計
- `{{TAX_RATE}}` - 税率
- `{{TAX_AMOUNT}}` - 消費税額
- `{{TOTAL_AMOUNT}}` - 合計金額
- `{{BANK_NAME}}` - 銀行名
- `{{BRANCH_NAME}}` - 支店名
- `{{ACCOUNT_TYPE}}` - 口座種別
- `{{ACCOUNT_NUMBER}}` - 口座番号
- `{{ACCOUNT_HOLDER}}` - 口座名義

## 使用方法

### Google Apps Scriptでの使用例

```javascript
function generateContract(contractData) {
  // テンプレートを読み込み
  const template = DriveApp.getFileById('TEMPLATE_FILE_ID').getBlob().getDataAsString();
  
  // 変数を置換
  let document = template;
  document = document.replace('{{CONTRACT_NUMBER}}', contractData.contractNumber);
  document = document.replace('{{CLIENT_NAME}}', contractData.clientName);
  // ... その他の変数を置換
  
  // 新しいドキュメントを作成
  const folder = DriveApp.getFolderById('OUTPUT_FOLDER_ID');
  const newFile = folder.createFile(`契約書_${contractData.contractNumber}.txt`, document);
  
  return newFile.getUrl();
}
```

### Pythonでの使用例

```python
def generate_invoice(invoice_data):
    # テンプレートを読み込み
    with open('templates/invoice-template.md', 'r', encoding='utf-8') as f:
        template = f.read()
    
    # 変数を置換
    document = template
    for key, value in invoice_data.items():
        document = document.replace(f'{{{{{key.upper()}}}}}', str(value))
    
    # ファイルに保存
    output_path = f'output/invoice_{invoice_data["invoice_number"]}.md'
    with open(output_path, 'w', encoding='utf-8') as f:
        f.write(document)
    
    return output_path
```

## テンプレートのカスタマイズ

1. 既存のテンプレートをコピーして新しいファイルを作成
2. 必要に応じて文言や項目を修正
3. 変数名は `{{VARIABLE_NAME}}` の形式で記述
4. システム側で変数の置換処理を実装

## PDF変換

Markdown形式のテンプレートをPDF化する方法：

### 方法1: Pandocを使用

```bash
pandoc contract-template.md -o contract.pdf
```

### 方法2: Google Docsを経由

1. Markdown → Google Docs形式に変換
2. Google DocsのExport機能でPDF化

### 方法3: 専用ツール

- [Markdown PDF](https://marketplace.visualstudio.com/items?itemName=yzane.markdown-pdf) (VS Code拡張機能)
- [md-to-pdf](https://www.npmjs.com/package/md-to-pdf) (Node.jsパッケージ)

## 注意事項

- テンプレートファイルは必ずUTF-8エンコーディングで保存してください
- 変数名は大文字で統一し、単語間はアンダースコアで区切ります
- 法的効力を持つ文書は、弁護士などの専門家にレビューを依頼してください
