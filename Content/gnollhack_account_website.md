---
title: Using the GnollHack Account Website
summary: Player guide to account.gnollhack.com — the dashboard, Top Scores, Recent Games, Win Rate statistics, Bones Sharing, dump logs, profile pages, and setting a Junethack username
---

## What the Site Is

**GnollHack Account** at **account.gnollhack.com** is the online home of your GnollHack player account. It records the games you post from the app, ranks them on global leaderboards, tracks bones-file sharing, and publishes win-rate statistics for the whole player base.

You almost certainly already have an account and are logged in: **the Gnoll Overseer uses this same account**, and so does score posting from the game. If you are using the Overseer, registration is behind you.

The site works fine while logged out — leaderboards, statistics, and dump logs are public. Logging in adds your personal dashboard and profile pages.

## Navigating the Site

The top navigation bar is the same on every page.

| Menu | Contains |
|---|---|
| **GnollHack Account** (top-left) | Your dashboard when logged in, the getting-started page when logged out |
| **Results** | **Top Scores**, **Recent Games** |
| **Statistics** | **Win Rates**, **Bones Sharing** |
| **Links** | GnollHack.com, GnollHack Wiki, Gnoll Overseer, the GnollHack GitHub repository, NetHack Scoreboard, Junethack |
| **Contact** | Email and Discord contact details |
| **Logged in as …** (top-right) | **Profile**, **Logout** |
| **Register** / **Login** (top-right, when logged out) | Account creation and sign-in |

A **Privacy** link in the footer points to the GnollHack Account Privacy Policy on the wiki.

## Your Dashboard

Logging in turns the front page into your personal dashboard. The header shows your username and, beneath it, your **global rank**, **played games**, **last active** date, and **joined** date.

Four button groups control what the dashboard lists:

| Group | Choices |
|---|---|
| **Listing** | **Recent** (your latest games) or **Top Scores** (your best, with the rank each holds on the global leaderboard) |
| **Gameplay Mode** | All, Classic, Modern |
| **Game Type** | All, or Ascension only |
| **Layout** | Auto, Table, or Card — Auto picks by screen width; Card is easier to read on a phone |

Each row is one game: time and version, character name, class with race/gender/alignment, difficulty and mode, score with experience and dungeon level, turns and real time played, and how the game ended. Ascensions are highlighted and marked with a crown. **Clicking a row opens that game's dump log.**

If you have just registered and posted nothing yet, the front page instead shows the *Connect In-App* card with the steps for linking the game to your account.

## Top Scores

**Results → Top Scores** is the global leaderboard, showing up to the 1000 highest-scoring games from all players.

The same **Gameplay Mode**, **Game Type**, and **Layout** button groups apply. Choosing *Ascension* under Game Type switches the page to "Top Scores for Ascensions".

Ranks 1, 2, and 3 are shown on gold, silver, and bronze shields. Tied scores share a rank. Only games with scoring enabled and posted by a registered account appear — casual, explore, and debug runs are excluded.

The table is sortable by any column, has its own search box, and is paginated with a page-size selector. Clicking a row opens that game's dump log.

## Recent Games

**Results → Recent Games** is the same table ordered by end time instead of score, showing the most recent 1000 games. The subtitle tells you how many that is out of the total. The Ascension filter turns it into "Recent Ascensions".

This is the page to watch to see what other players are doing right now.

## Win Rate Statistics

**Statistics → Win Rates** shows a matrix of games and ascensions broken down by **role** (across the top) and **difficulty** (down the side), with an *All Roles* column and totals row.

Each cell gives:

- **G** — games played, and that cell's share of the games in its row;
- **A** — ascensions, and that cell's share of the ascensions in its row;
- the resulting **win rate** percentage for the row.

Only games that count are included, and the note under the heading spells out the filter: at least **1000 turns**, played within the last **2 years**, scoring games only, excluding debug and explore modes. The **Gameplay Mode** buttons narrow the whole matrix to All Modes, Classic, or Modern.

This is a good place to check whether a role is genuinely hard or you have simply been unlucky.

## Bones Sharing

**Statistics → Bones Sharing** shows the bones-file exchange. When a character dies, their level can be saved as a "bones file" and later loaded into another player's game, where the dead adventurer appears as a ghost guarding their old equipment.

The page lists, per account: **Bones Uploaded**, **Bones Downloaded**, and **Bones Shared**. Tabs break the figures down by difficulty, with an *All Difficulties* tab first.

Because bones files are only compatible between certain game versions, a **Compatible With** dropdown filters the table to one compatibility range. Change it if the figures look empty for your version.

Bones sharing must be enabled in the game — Settings → Server Posting → **Share Bones Files**.

## Dump Logs

Every posted game has a **dump log**: the end-of-game record with your character's final attributes, inventory, discoveries, conduct, and the last messages before death or ascension.

Reach one by clicking any row in Top Scores, Recent Games, or your dashboard. The address is `account.gnollhack.com/dumplog/<id>`, and appending `/plain` gives the same log as plain text instead of HTML — handy for pasting into Discord or attaching to an Overseer chat.

A dump log for a very old game may no longer exist on the server, in which case the page reports that it is gone.

## Your Profile Pages

The **Logged in as …** menu → **Profile** opens the account management area. Its side navigation has these pages:

| Page | What you can do |
|---|---|
| **Profile** | View your username (it cannot be changed) and set a phone number |
| **Email** | View your current email address and change it — a confirmation link is sent to the new address |
| **Password** | Change your password |
| **Personal data** | Download everything the site stores about you, or delete your account permanently |
| **Junethack** | Set your Junethack username — see below |

> **Deleting your account is permanent and cannot be undone.** It removes the account entirely.

## Adding a Junethack Username

[Junethack](https://junethack.net/) is the annual roguelike tournament held every June, in which NetHack variants — GnollHack among them — compete together. Junethack tracks your games across every participating server, but it needs to know which account on this server belongs to which Junethack player.

To link them:

1. Register at **junethack.net** if you have not already, and note the username you chose there.
2. Log in at account.gnollhack.com.
3. Open **Logged in as … → Profile**, then **Junethack** in the side navigation.
4. Type your **Junethack Username** into the field.
5. Press **SAVE**. The page confirms *"Your JunetHack user name has been updated"*.

Rules for the field:

- Only **letters, numbers, and underscores** are allowed. No spaces, dashes, or other punctuation.
- Maximum **255 characters**.
- It is your **Junethack** username, which does not have to match your GnollHack username.
- **Clearing the field and saving unlinks the accounts.**

Once set, the server makes the mapping between your GnollHack account and your Junethack account available to Junethack, so your GnollHack games are credited to you in the tournament. Nothing else changes: your games still appear on the GnollHack leaderboards exactly as before, under your GnollHack name.

You must still be posting your games for anything to be credited — Settings → Server Posting → **Post Top Scores** in the game. The same game-log data also feeds [NetHack Scoreboard](https://nethackscoreboard.org/), which needs no username setup.

> Tournament play has its own requirements in the game client. **Tournament Mode** forces score posting, bones sharing, replay recording, and save-file tracking on, and needs at least Expert difficulty.

## Registering and Logging In

Only needed if you do not yet have an account — using the Overseer already requires one.

**To register**, press **Register** in the top-right and fill in:

| Field | Rules |
|---|---|
| **User Name** | Up to 31 characters, letters, digits, and underscores only, and it cannot start with an underscore. This is the name that appears on the leaderboards. |
| **Email** | Must be a valid address, and each address may be used for only one account |
| **Password** | 6 to 100 characters |
| **Confirm Password** | Must match |

**Email confirmation is required.** After registering you receive a confirmation message; you cannot log in until you follow its link. If it does not arrive, use the **Resend email confirmation** link on the login page and check your spam folder.

**To log in**, press **Login** and enter your username and password. Forgotten passwords are reset with **Forgot Password?**, which mails you a reset link.

**After registering**, link the game to the account: in GnollHack, go to Settings → Server Posting, enter the same **User Name** and **Password**, and enable **Post Top Scores** and/or **Post Bones Files**. The same credentials log you into the Gnoll Overseer.

## Troubleshooting

| Symptom | Cause and fix |
|---|---|
| Your games do not appear anywhere | **Post Top Scores** is off in the game, or the username/password in Settings → Server Posting is wrong. Verify the credentials in the app. |
| A game is missing from Top Scores but shows in Recent Games | Top Scores lists only scoring games; casual, explore, and debug runs are excluded. |
| You cannot log in right after registering | Your email address is not confirmed yet. Use the confirmation link, or resend it from the login page. |
| The Bones Sharing table looks empty | The **Compatible With** filter is set to a version range you have not played. |
| A dump log link reports the log is gone | The dump file for that old game is no longer stored on the server. |
| Your Junethack username will not save | It contains a character other than a letter, digit, or underscore. |

> **See also:** get_knowledge_article("server_account") for setting up score posting, bones sharing, and Tournament Mode inside the game.
> **See also:** get_knowledge_article("overseer_app_guide") for the Gnoll Overseer, which uses this same account.
> **See also:** get_knowledge_article("settings_reference") for the **Server Posting** settings category in the game.
> **Wiki:** For tournament rules, public server details, and the privacy policy, search the wiki for **GnollHack Account**.
