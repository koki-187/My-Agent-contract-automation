# 請求書

---

## 請求書番号: {{INVOICE_NUMBER}}

**請求日**: {{INVOICE_DATE}}

**お支払期限**: {{DUE_DATE}}

---

## 請求先

{{CLIENT_NAME}} 御中

{{CLIENT_ADDRESS}}

---

## 請求元

{{COMPANY_NAME}}

{{COMPANY_ADDRESS}}

TEL: {{COMPANY_PHONE}}

Email: {{COMPANY_EMAIL}}

---

## 請求内容

下記の通りご請求申し上げます。

### ご請求金額

# **¥{{TOTAL_AMOUNT}}**（税込）

---

## 明細

| 項目 | 数量 | 単価 | 金額 |
|------|------|------|------|
{{ITEMS}}

---

## 金額詳細

| 項目 | 金額 |
|------|------|
| 小計 | ¥{{SUBTOTAL}} |
| 消費税（{{TAX_RATE}}%） | ¥{{TAX_AMOUNT}} |
| **合計** | **¥{{TOTAL_AMOUNT}}** |

---

## お支払方法

**銀行振込**

- 銀行名: {{BANK_NAME}}
- 支店名: {{BRANCH_NAME}}
- 口座種別: {{ACCOUNT_TYPE}}
- 口座番号: {{ACCOUNT_NUMBER}}
- 口座名義: {{ACCOUNT_HOLDER}}

※振込手数料はお客様のご負担でお願いいたします。

---

## 備考

{{NOTES}}

---

## お問い合わせ

ご不明な点がございましたら、下記までご連絡ください。

**{{COMPANY_NAME}}**

担当者: {{CONTACT_PERSON}}

TEL: {{COMPANY_PHONE}}

Email: {{COMPANY_EMAIL}}

---

*本請求書は{{INVOICE_DATE}}に発行されました。*
