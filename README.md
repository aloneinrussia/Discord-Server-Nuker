# Discord-Server-Nuker
This was a old project i created myself in python 100% feel free to use it 
## What this project does

This is a Python Discord bot prototype built with `discord.py`. It starts several bot accounts and defines commands for checking that bots are present, renaming bot nicknames, and carrying out a destructive server operation.

That operation attempts to delete the server's channels and roles (except `@everyone`), create replacement channels and roles, and post a configured message repeatedly in text channels. The bot also constructs invitation links requesting administrator permissions.

**Warning:** This behavior can irreversibly destroy server content and disrupt or spam a Discord community. Do not run or deploy this project in a real server. This README intentionally does not provide instructions for deploying or triggering those actions.

## Project files

- `main.py` — bot configuration, command definitions, and asynchronous startup.
- `Requirements.txt` — lists `discord.py` and `aiohttp`.

## Configuration and implementation notes

The `Config` class in `main.py` contains the command prefix, bot tokens and IDs, and the message and counts used by the destructive operation. The values in the checked-in source are placeholders, not usable credentials. Never put real bot tokens in source code or commit them to version control.

There are important inconsistencies in the current prototype:

- The configuration supplies three bot tokens and IDs, but the operation accesses a fourth bot (`bots[3]`) while creating roles. That can raise an `IndexError`.
- The operation assumes particular bots are available in the server and does not check the bot list before using it.
- Errors from many deletion, creation, and message-send tasks are suppressed by `asyncio.gather(..., return_exceptions=True)`, so the operation may fail partially without reporting each failure.
- `main.py` attempts to install dependencies when it starts, even though they are listed in `Requirements.txt`. Installing packages at runtime is not recommended.

This repository is best treated as a code sample for inspection, not as a ready-to-use bot.
