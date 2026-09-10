import os

import random

from telegram import Update

from telegram.ext import Application, CommandHandler, ContextTypes

TOKEN = os.getenv("BOT_TOKEN")

if not TOKEN:

    raise ValueError("BOT_TOKEN n'est pas configuré.")

async def start(update: Update, context: ContextTypes.DEFAULT_TYPE):

    await update.message.reply_text(

        "🤖 SEDOSKI PREDICTION BOT\n\n"

        "Bienvenue sur le bot de prédictions football ⚽\n\n"

        "📌 Commandes :\n"

        "/prediction - Prédire un match\n"

        "/today - Matchs du jour\n"

        "/help - Aide"

    )

async def help_command(update: Update, context: ContextTypes.DEFAULT_TYPE):

    await update.message.reply_text(

        "📚 AIDE SEDOSKI\n\n"

        "⚽ /prediction : obtenir une prédiction\n"

        "📅 /today : voir les matchs du jour\n"

        "🏠 /start : menu principal\n\n"

        "⚠️ Les prédictions sont indicatives."

    )

async def prediction(update: Update, context: ContextTypes.DEFAULT_TYPE):

    equipes = [

        ("Équipe A", "Équipe B"),

        ("Équipe C", "Équipe D"),

        ("Équipe E", "Équipe F")

    ]

    equipe1, equipe2 = random.choice(equipes)

    choix = random.choice([

        f"Victoire {equipe1}",

        f"Victoire {equipe2}",

        "Match nul"

    ])

    score1 = random.randint(0, 3)

    score2 = random.randint(0, 3)

    await update.message.reply_text(

        f"⚽ SEDOSKI PREDICTION\n\n"

        f"🏆 {equipe1} 🆚 {equipe2}\n\n"

        f"🔮 Pronostic : {choix}\n"

        f"📊 Score probable : {score1} - {score2}\n\n"

        f"⚠️ Prédiction indicative uniquement."

    )

async def today(update: Update, context: ContextTypes.DEFAULT_TYPE):

    await update.message.reply_text(

        "📅 Les matchs du jour seront bientôt disponibles."

    )

def main():

    app = Application.builder().token(TOKEN).build()

    app.add_handler(CommandHandler("start", start))

    app.add_handler(CommandHandler("help", help_command))

    app.add_handler(CommandHandler("prediction", prediction))

    app.add_handler(CommandHandler("today", today))

    print("🤖 SEDOSKI PREDICTION BOT démarré !")app.run_polling()

if __name__ == "__main__":

    main()
