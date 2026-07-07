# Telegram Crypto Digital Store Bot — Railway Ready

A ready-to-run Telegram digital store bot with crypto payment verification and instant digital delivery using NOWPayments.

## Features

- Railway-ready deployment: `railway.json` + `Procfile`
- Product catalog from `products.json`
- Telegram inline buy buttons
- NOWPayments crypto payment creation
- Signed IPN/webhook verification
- SQLite order database
- Automatic delivery after verified crypto confirmation
- Admin commands inside Telegram
- Add/remove products from Telegram
- File, key, or text delivery

## 1. Create your Telegram bot

1. Open Telegram and message `@BotFather`.
2. Send `/newbot`.
3. Copy the bot token.

To get your Telegram numeric admin ID, run the bot after deployment and send `/myid`.

## 2. Deploy on Railway

1. Upload this project to a GitHub repository.
2. Go to Railway and choose **New Project**.
3. Choose **Deploy from GitHub Repo**.
4. Select your repository.
5. Open the Railway project settings and generate a public domain.
6. Copy the public domain. It will look like:

```text
https://your-project-name.up.railway.app
```

## 3. Add Railway variables

In Railway, open **Variables** and add:

```env
BOT_TOKEN=your_telegram_bot_token
STORE_NAME=My Digital Store
BASE_URL=https://your-project-name.up.railway.app
ADMIN_TELEGRAM_IDS=your_numeric_telegram_id
NOWPAYMENTS_API_KEY=your_nowpayments_api_key
NOWPAYMENTS_IPN_SECRET=your_nowpayments_ipn_secret
NOWPAYMENTS_PRICE_CURRENCY=usd
NOWPAYMENTS_PAY_CURRENCY=btc
```

Important: `BASE_URL` must be your Railway public URL with no slash at the end.

## 4. Set NOWPayments webhook/IPN

In NOWPayments, set the IPN/Webhook callback URL to:

```text
https://your-project-name.up.railway.app/webhooks/nowpayments
```

Use the same IPN secret in Railway as `NOWPAYMENTS_IPN_SECRET`.

## 5. Start using your bot

Open your Telegram bot and send:

```text
/start
```

Admin commands:

```text
/myid
/admin
/orders
/listproducts
/addfileproduct id|name|price|filePath|description
/addtextproduct id|name|price|delivery text
/removeproduct id
```

Examples:

```text
/addfileproduct ebook1|Premium PDF|9.99|files/premium.pdf|Instant PDF delivery
/addtextproduct vip1|VIP Access Code|19.99|YOUR-CODE-HERE
/removeproduct ebook1
```

## Product setup

### File product

Put the file inside the `files/` folder and add it to `products.json`:

```json
{
  "id": "ebook-basic",
  "name": "Premium PDF Guide",
  "description": "Delivered instantly after crypto confirmation.",
  "price": 10,
  "filePath": "files/sample-product.txt"
}
```

### Text/key product

```json
{
  "id": "license-key-pack",
  "name": "License Key Pack",
  "description": "Example key delivery product.",
  "price": 15,
  "deliveryText": "YOUR-LICENSE-KEY-HERE"
}
```

## Local test

```bash
npm install
cp .env.example .env
npm start
```

For local webhooks, use ngrok:

```bash
npx ngrok http 3000
```

Then set `BASE_URL` to your ngrok HTTPS URL.

## Important notes

- Do not sell illegal, stolen, or unauthorized digital goods.
- The bot only delivers after a signed NOWPayments IPN says the payment is confirmed/finished.
- Keep `.env`, API keys, database files, and private files safe.
- Railway ephemeral storage can reset on redeploys depending on plan/config. For serious stores, use Railway Volumes or PostgreSQL for persistent order history.
