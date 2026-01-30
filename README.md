import os
import discord
from discord.ext import commands
from datetime import datetime

# Enable member intent
intents = discord.Intents.default()
intents.members = True

bot = commands.Bot(command_prefix="!", intents=intents)

@bot.event
async def on_ready():
    print(f"Logged in as {bot.user}")

@bot.event
async def on_member_join(member):
    username = f"{member.name}#{member.discriminator}"
    join_time = datetime.utcnow().strftime("%Y-%m-%d %H:%M:%S")

    with open("new_users.txt", "a", encoding="utf-8") as f:
        f.write(f"{username} joined at {join_time}\n")

# Start bot using Railway environment variable
bot.run(os.getenv("BOT_TOKEN"))
