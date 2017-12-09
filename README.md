# Toadally Awesome  
Toadally Awesome is a [Discord](https://discordapp.com/) bot written in the NodeJS module [discord.io](https://github.com/izy521/discord.io), based off BastionBot by AlphaKretin, with a focus on functions related to the Yu-Gi-Oh! card game and a simulator of it, [YGOPro Percy](http://ygopro.co). All commands are case-insensitive.  
  
[Here's](https://discordapp.com/oauth2/authorize?client_id=388137852132917248&scope=bot&permissions=201849937) the invite link. 
  
### Help  
Usage: `@Toadally Awesome#7968`  
  
Mentioning Toadally Awesome will provide a link to this readme.  
  
### Card Lookup  
Usage: `{card name|ID[,lang,lang]}`  
  
This command searches for a card by the name or YGOPro ID specified in the brackets and returns the card's name, all of its IDs in YGOPro, any archetypes its a member of, its status, its lowest, average, and highest prices if available, its types, its attribute if it's a monster, any stats, and its card text. If you enter two valid language codes (e.g. "en", "ja", "es"), the bot will search by the first language and output in the second.  
  
As an example, `{dark magician}` returns the following output:  
![card output](/readme-images/card.png)  
  
### Card With Image  
Usage: `<card name|ID[,lang,lang]>`  
  
This command works the same way as the above command, but also displays an image of the card's artwork.  
  
As an example, `<stardust dragon>` returns the following output:  
![card image output](/readme-images/card-image.png)  
  
### Individual Property Lookup  
Usage: `.name [card name|ID]`, `.id [card name|ID]`, `.status [card name|ID]`, `.price [card name|ID]`, `.effect [card name|ID]`, `.peffect [card name|ID]`, `.type [card name|ID]`, `.att [card name|ID]`, `.stats [card name|ID]`  
  
Using these commands, you can search for these individual parts of what the above commands return. If the property does not exist, for example the attribute of a Spell Card, nothing will be returned.  
  
### .randcard  
Usage: `.randcard [opts]`  
  
The `.randcard` command will select a random card and display its information as if you searched it. The command accepts options that allow you to specify the status, level, type, or attribute of the card, as well as optionally display an image by including "image" or display cards in different languages by including the language code for that language.  
  
As an example, `.randcard tcg/ocg 4 image` returns the following output:  
![.randcard output](/readme-images/randcard.png)  
  
### .script  
Usage: `.script [name|id]`  
  
The `.script` command searches for a card by name or YGOPro ID and returns a link to its script for YGOPro, as well as embedding it if short enough.  
  
As an example, `.script macro cosmos` returns the following output:  
![.script output](/readme-images/script1.png)  
![.script output 2](/readme-images/script2.png)  
  
### .matches  
Usage: `.matches [name]`  
  
The `.matches` command simulates a search for cards by name and returns the 10 closest matches for your search term, that share a status. This command ignores cards with the same name, for example alternate artworks.  
  
As an example, `.matches junk warrior` returns the following output:  
![.matches output](/readme-images/matches.png)  
  
### .set  
Usage: `.set [name|setcode]`  
  
The `.set` command searches for an archetype, or "setcode" by either its name or its hexadecimal value in YGOPro (`0xba` for example) and returns both.  
  
As an example, `.set 0xba` returns the following output:  
![.set output](/readme-images/set.png)  
  
### Scripting Library  
Usage: `.f [function name]`, `.c [constant name]`, `.param [parameter name]`  
  
Toadally Awesome can return information about YGOPro's Lua API with the above commands. All results that match your query will be displayed, in pages of 9. Type or edit `.p[page number]` to change pages. Entries will be displayed with a corresponding number - type o edit `.d[number]` to see a more detailed description of that entry, if available.  
  
### .trivia  
Usage: `.trivia [options]`  
For fun, Toadally Awesome can play a game where it will provide the art of a card, and players have 30 seconds to give its name, with a hint at 10 seconds. The command accepts any number of the following options:  
**Status**: By default, the game will display TCG/OCG cards, but you can specify `OCG`, `TCG`, `Anime` (which will include Video Game and Illegal cards), and `Custom`.  
**Rounds**: If you include a number as an option, the game will run that many times and track the total scores of each player over the course of the game.  
**Hard Mode**: If you include `hard` as an option, Toadally Awesome will display only a quarter of the card image, for added difficulty.  
You can end the game prematurely by typing ".tq".  
**Language**: If you include a language code as an option, Toadally Awesome will use that language for the card name.  
  
### .tlock  
Usage: `.tlock`  
The `.tlock` command tells Toadally Awesome that on the server you use the command, he should only allow `.trivia` in the channels in which you've used the command. Only users with the "Manage Messages" permission can use the command. You can use the command in multiple channels to allow trivia in multiple channels. Using the command in a channel already registered will remove it from the list. If there are no channels in the list, trivia will be allowed anywhere.  
  
## Installation  
If you so choose, you can run a copy of Toadally Awesome yourself! This section will assume some basic familiarity with NodeJS and the command line.  
  
All of Toadally Awesome's dependencies are properly documented in the package.json, so you can just download that, put it in a folder, and run `npm install`. To run the bot, the script expects some certain files - a configuration file, a shortcuts file, a setcodes file, any number of SQLite databases containing card data, in the format YGOPro uses, and optionally 3 files with information about YGOPro's API with a customizable name. Once it's setup, you can use `node Toadally Awesome.js` to run it once, or on Windows, use `autorun.bat` to have it automatically restart upon a crash.  
  
### Configuration  
By default, the configuration file is called `config.json`, and is expected to be found in a subfolder of the local directory called `config`, i.e. `config/config.json`. The script expects `config.json` to contain a JSON object with the following properties:  
```json  
{  
	"token": "",  
	"prefix": ".",  
	"longStr": "...\n__Type \".long\" to be PMed the rest!__",  
	"maxSearches": 3,  
	"imageUrl": "",  
	"imageUrlAnime": "",  
	"imageUrlCustom": "",  
	"imageSize": 100,  
	"scriptUrl": "",  
	"scriptUrlAnime": "",  
	"scriptUrlCustom": "",  
	"dbs": {  
		"en": [ "cards.cdb" ]  
	},
	"dbMemory": 33554432,
	"triviaTimeLimit": 30000,  
	"triviaHintTime": 10000,  
	"triviaMaxRounds": 20,  
	"triviaLocks": {},  
	"botOwner": "169299769695535105",  
	"scriptFunctions": "functions.json",  
	"scriptConstants": "constants.json",  
	"scriptParams": "parameters.json"  
}  
```  
`token` is the Discord User token that the discord.io module will use to log in to Discord. You can obtain a bot token through the [Discord Developers website](https://discordapp.com/developers/applications/me/). This field is required.  
  
`prefix` is the text that Toadally Awesome will look for at the start of messages to indicate that it's a bot command. For example, if `prefix` is "b$", `.randcard` becomes `b$randcard`. This field is optional - if it is missing, Toadally Awesome will default to what you see above.  
  
`longStr` is the message Toadally Awesome will append to an output that's split up due to violating Discord's character limit, instructing the user how to see the rest. This field is optional - if it is missing, Toadally Awesome will default to what you see above.  
  
`maxSearches` is the number of different cards Toadally Awesome will allow a user to search at once - if a message contains more queries, Toadally Awesome won't search anything, instead returning an error message. This field is optional - if it is missing, Toadally Awesome will default to what you see above.  
  
`imageUrl` is a link to a source for card images - either official ones, or all of them. Toadally Awesome will append the ID of the card, then ".png". This field is optional - if it is missing, functions that require images will be disabled and the following fields will be ignored: `imageUrlAnime`, `imageUrlCustom`, `imageSize`, `triviaTimeLimit`, `triviaHintTime`, `triviaMaxRounds` and `triviaLocks`.  
  
`imageUrlAnime` is a link to a source for anime card images. Toadally Awesome will append the ID of the card, then ".png". This field is optional - if it is missing, Toadally Awesome will default to `imageUrl`.  
  
`imageUrlCustom` is a link to a source for custom card images. Toadally Awesome will append the ID of the card, then ".png". This field is optional - if it is missing, Toadally Awesome will default to `imageUrl`.  
  
`scriptUrl` is a link to a source for card scripts - either official ones, or all of them. Toadally Awesome will append the ID of the card, then ".lua". This field is optional - if it is missing, functions that require scripts will be disabled and the following fields will be ignored: `scriptUrlAnime`, and `scriptUrlCustom`.  
  
`scriptUrlAnime` is a link to a source for anime card scripts. Toadally Awesome will append the ID of the card, then ".lua". This field is optional - if it is missing, Toadally Awesome will default to `scriptUrl`.  
  
`scriptUrlCustom` is a link to a source for custom card scripts. Toadally Awesome will append the ID of the card, then ".lua". This field is optional - if it is missing, Toadally Awesome will default to `scriptUrl`.  
  
`scriptUrlBackup` is a link to a source for backup card scripts - if Toadally Awesome doesn't find a script at the first source specified, he'll try again here. Toadally Awesome will append the ID of the card, then ".lua". This field is optional - if it is missing, Toadally Awesome will not try to find backup scripts.  
  
`dbs` is an object of arrays of filenames for card databases Toadally Awesome will read, to be found in a folder called `dbs`. The keys of the object are language codes. This field is optional - if it is missing, Toadally Awesome will default to what you see above.  

`dbMemory` is the size allocated in memory for Toadally Awesome to load card database, in bytes. If you get the error "Cannot adjust memory arrays" in the middle of loading databases, you need to increase this. This field is optional - if it is missing, Toadally Awesome will default to what you see above.
  
`triviaTimeLimit` is the time a player has to guess the answer in the trivia game, in milliseconds. This field is optional - if it is missing, Toadally Awesome will default to what you see above.  
  
`triviaHintTime` is the time at which Toadally Awesome will provide a hint for the player in the trivia game, in milliseconds. If it is greater than `triviaTimeLimit`, the hint will never display, which may be behaviour you desire. This field is optional - if it is missing, Toadally Awesome will default to what you see above.  
  
`triviaMaxRounds` is the maximum number of rounds a player can set the trivia game to run for, to prevent someone from forcing it to run for an arbitrarily long time. This field is optional - if it is missing, Toadally Awesome will default to what you see above.  
  
`triviaLocks` is an object with server IDs as keys and an array of channel IDs as the properties. If a server is in the object, the trivia game can only be player in the channels listed in the array. This field is optional - if it is missing, Toadally Awesome will default to what you see above, and you can configure it through Toadally Awesome even if you don't run the copy using the `.tlock` command.  
  
`botOwner` is the Discord user ID of the user you consider to own the bot, likely yourself, for the sake of administrative functions. This field is optional - if it is missing, such functions will be disabled.  
  
`scriptFunctions` is the name of the JSON file Toadally Awesome will load containing information about the YGOPro API's functions - details on this file below. This field is optional - if it is missing, searching for functions will be disabled.  
  
`scriptConstants` is the name of the JSON file Toadally Awesome will load containing information about the YGOPro API's constants - details on this file below. This field is optional - if it is missing, searching for constants will be disabled.  
  
`scriptParams` is the name of the JSON file Toadally Awesome will load containing information about the YGOPro API's parameters - details on this file below. This field is optional - if it is missing, searching for parameters will be disabled.  
  
### Shortcuts  
By default, the shortcut file is called `shortcuts.json`, and is expected to be found in a subfolder of the local directory called `config`, i.e. `config/shortcuts.json`. The script expects `shortcut.json` to contain a JSON array of arrays, with contents like the following:  
```json  
[  
	[  
		"A0",  
		"AbZ.",  
		"AbZ",  
		"Elemental HERO Absolute Zero"  
	],  
	[  
		"AGGD",  
		"Ancient Gear Gadjiltron Dragon"  
	]  
]  
```  
The final entry in each array should be the full name of a card, for which all other entries are a shortened form of. Toadally Awesome splits queries up by spaces when checking for shortcuts, so shortcuts with a space will never be matched.  
  
### Setcodes  
By default, the setcode file is called `setcodes.json`, and is expected to be found in a subfolder of the local directory called `config`, i.e. `config/setcodes.json`. The script expects `setcodes.json` to contain a object, with hexadecimal setcodes as the keys and the names of the corresponding archetypes as the values, like so:  
```json  
{  
	"0x1": "Ally of Justice",  
	"0x2": "Genex"  
}  
```  
  
### Database  
  
Toadally Awesome reads card databases from SQLite databases formatted the same way as those YGOPro uses. Because of this similarity, you can copy databases from YGOPro or edit them with programs like [DataEditorX](https://github.com/247321453/DataEditorX), so it should not be necessary to document the format here. If you do want to learn more about it, you can read [MichaelLawrenceDee's tutorial](https://www.ygopro.co/Forum/tabid/95/g/posts/t/16781/Scripting-Tutorial--CURRENTLY-INCOMPLETE#post88202) on custom card creation for YGOPro, which covers making Card Databases manually. The schema for a card database is as follows:  
```sql  
CREATE TABLE IF NOT EXISTS "datas" (  
	`id`	integer,  
	`ot`	integer,  
	`alias`	INTEGER,  
	`setcode`	integer,  
	`type`	integer,  
	`atk`	integer,  
	`def`	integer,  
	`level`	integer,  
	`race`	integer,  
	`attribute`	integer,  
	`category`	integer,  
	PRIMARY KEY(id)  
);  
CREATE TABLE IF NOT EXISTS "texts" (  
	`id`	integer,  
	`name`	TEXT,  
	`desc`	TEXT,  
	`str1`	TEXT,  
	`str2`	TEXT,  
	`str3`	TEXT,  
	`str4`	TEXT,  
	`str5`	TEXT,  
	`str6`	TEXT,  
	`str7`	TEXT,  
	`str8`	TEXT,  
	`str9`	TEXT,  
	`str10`	TEXT,  
	`str11`	TEXT,  
	`str12`	TEXT,  
	`str13`	TEXT,  
	`str14`	TEXT,  
	`str15`	TEXT,  
	`str16`	TEXT,  
	PRIMARY KEY(id)  
);  
```  
  
### API  
  
Toadally Awesome expects 3 files in the `dbs` folder containing JSON arrays of objects detailing the functions, constants, and parameters in YGOPro's API. Examples of their format below.  
  
#### functions.json  
```json  
[  
	{  
		"sig": "int,int",  
		"name": "Card.GetOriginalCodeRule(Card c)",  
		"desc": "Gets the original code of a Card (Card c) (used for wording \"original name\")"  
	},  
	{  
		"sig": "bool",  
		"name": "Card.IsFusionCode(Card c, int code)",  
		"desc": "Checks if a Card (Card c) has a specific code (int code) (for Fusion Summons)"  
	}  
]  
```  
  
#### constants.json  
```json  
[  
	{  
		"val": "0x01",  
		"name": "LOCATION_DECK",  
		"desc": ""  
	},  
	{  
		"val": "0x02",  
		"name": "LOCATION_HAND",  
		"desc": ""  
	}  
]  
```  
  
#### parameters.json  
```json  
[  
{  
		"type": "string",  
		"name": "any msg",  
		"desc": "A string in parantheses (can also include variables: 'Debug.Message(\"string1\"..var1..\"string2\")')"  
	},  
	{  
		"type": "bool",  
		"name": "cancel",  
		"desc": "Determines if it's cancelled or not"  
	}  
]  
```  
