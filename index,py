import random
import discord
import pymongo
import asyncio
from better_profanity import profanity
from discord.ext import commands

token = 'discord_bot_token'
client = pymongo.MongoClient("Mongo_URI")
db = client.get_database('database_name')
auth = db.register

client = commands.Bot(command_prefix='.', intents=discord.Intents.all())
admin_id = #admin id here, make sure its an integer


@client.event
async def on_ready():
    print(f'{client.user.name} is ready')  

    while True:
        userCount = auth.count_documents({})  #reads count of documents in the register collection so that it can know how many users there are.
        await client.change_presence(activity=discord.Activity(type=discord.ActivityType.watching, name=f'{userCount} user(s) using Qubed!'))
        await asyncio.sleep(30)  #keeps on relooping and checks the collection every 30 seconds

@client.event
async def on_message(message):
    text = message.content
    profanity.load_censor_words()
    if profanity.contains_profanity(text):
        await message.delete()
    else:
        print(f'{message.author} can say that')


@client.command()
async def embed(ctx, title, *, desc):
    title = title
    desc = str(desc)
    embedVar = discord.Embed(title=title, description=desc, color=0x00ff00)
    if ctx.author.id == admin_id:
        await ctx.send(embed=embedVar)
    else:
       await ctx.reply('You are not permitted to use this command.')

client.run(token)
