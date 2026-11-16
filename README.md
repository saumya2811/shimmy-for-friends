# Shimmy for friends

A tiny social network for a small group of friends.

I made Shimmy for my three college friends and me. We live across the ocean from each other, and this is our little corner to stay close. It's social media only for the things that matter to us, and only for the four of us. You're welcome to take it and make one for your own people.

**Watch how it was made:** https://claude.ai/artifact/QhrB4JZLxVMfEDZhFQbT8E

## What's inside

- **Shimmy shimmy shimmy**: log what you did to move each day. Everyone's jiggles add up on one shared shimmy meter, and you choose the rewards together.
- **Did you eat?**: a tiny Instagram for meals. Post a few photos at once, react, comment and share recipes.
- **Fill your cup**: one small thing a day that calms you down, plus a shared list of ideas.

The house rules are built in: doing it is the only target, you win together, and nobody gets ranked.

## Make your own

Shimmy runs as a Claude artifact, a web page inside Claude that saves shared data for your group. You and each of your friends need a Claude account.

**The easy way:** open this repo in Claude Code and say something like:

> Make this my own Shimmy for Mira, Tanvi, Rhea and me, and publish it as a new artifact.

Claude reads `CLAUDE.md`, which explains how the app works and how to publish it.

**By hand:**

1. In `index.html`, find `FRIENDS` near the top of the script and put in your names (up to four). Add square photos if you like, or leave them out and everyone gets a pastel initial.
2. Publish `index.html` as a Claude artifact with the `db` and `user` capabilities and the access rules listed in `CLAUDE.md`.
3. Share the page with your friends as Editors. Everyone picks her face on the "Who are you?" screen and can only write in her own column.

## Make it yours

Swap the tabs for whatever your group cares about: books, plants, dog photos. The colors are tokens at the top of `index.html`. Keep it cute.

## Credits

Made with love by Saumya, with Claude, for Lata, Kriti and Sarigama. MIT licensed: use it, change it and share it, and keep the license note.
