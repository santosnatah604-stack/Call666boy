const TelegramBot = require('node-telegram-bot-api');
const twilio = require('twilio');
const express = require('express');

const app = express();
app.get('/', (req, res) => res.send('Bot actif'));

const bot = new TelegramBot(process.env.BOT_TOKEN, { polling: true });

const client = twilio(
  process.env.TWILIO_SID,
  process.env.TWILIO_AUTH
);

bot.onText(/\/call (.+)/, async (msg, match) => {
  const chatId = msg.chat.id;
  const number = match[1];

  try {
    await client.calls.create({
      url: 'http://demo.twilio.com/docs/voice.xml',
      to: number,
      from: process.env.TWILIO_NUMBER
    });

    bot.sendMessage(chatId, `📞 Appel lancé vers ${number}`);
  } catch (err) {
    bot.sendMessage(chatId, `❌ ${err.message}`);
  }
});

app.listen(3000, () => console.log("OK"));
