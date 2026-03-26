# Dc.2.0
main.py

import discord from discord import app_commands from discord.ext import commands import os

Get token from environment variable

TOKEN = os.environ.get('TOKEN')

intents = discord.Intents.default() bot = commands.Bot(command_prefix="!", intents=intents)

Slash command tree

tree = bot.tree

@bot.event async def on_ready(): await tree.sync() print(f"Logged in as {bot.user}")

@tree.command(name="send", description="Send anonymous message multiple times") @app_commands.describe(message="Message to send", count="How many times to send") async def send(interaction: discord.Interaction, message: str, count: int): if count > 10: await interaction.response.send_message("❌ Max limit is 10!", ephemeral=True) return

await interaction.response.send_message(f"✅ Sending message {count} time(s)...", ephemeral=True)

for i in range(count):
    await interaction.channel.send(message)

bot.run(TOKEN)
