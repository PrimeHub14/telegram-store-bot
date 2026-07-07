# Telegram Crypto Digital Store Bot

Ready-to-deploy Telegram digital store bot with NOWPayments crypto payment verification and instant delivery.

## Features

- Telegram product catalog
- NOWPayments crypto invoice creation
- Secure IPN/webhook signature verification
- Instant delivery after confirmed payment
- SQLite order database
- Admin commands inside Telegram
- Railway-ready config

## Deploy on Railway

1. Upload this project to GitHub.
2. In Railway, click **New Project** → **Deploy from GitHub Repo**.
3. Choose your repository.
4. Go to **Variables** and add:

```env
BOT_TOKEN=your_botfather_token
ADMIN_IDS=your_telegram_numeric_user_id
PUBLIC_URL=https://your-railway-domain.up.railway.app
NOWPAYMENTS_API_KEY=your_nowpayments_api_key
NOWPAYMENTS_IPN_SECRET=your_nowpayments_ipn_secret
PAY_CURRENCY=usd
PRICE_CURRENCY=usd
DATABASE_PATH=./data/store.db
```

5. Set NOWPayments IPN/Webhook URL to:

```text
https://your-railway-domain.up.railway.app/nowpayments-webhook
```

6. Open your Telegram bot and send `/start`.

## Admin commands

Send `/admin` to the bot.

Add product:

```text
/addproduct ebook1 | My Ebook | 9.99 | text | https://your-download-link.com/file.pdf | My ebook description
```

For file delivery from server path:

```text
/addproduct pack1 | Template Pack | 14.99 | file | ./deliveries/template-pack.zip | ZIP template pack
```

Then upload the file to the `deliveries` folder before deployment.

Delete/disable product:

```text
/deleteproduct ebook1
```

List orders:

```text
/orders
```

## Important

Do not put `.env` into GitHub. Add secrets only in Railway Variables.
Only deliver products you own or have permission to sell.
