# A complete guide on how to create and add a custom character to Vampire Survivors

# Introduction
*So, you want to add your own custom characters to Vampire Survivors, either using your own art, or ported from a spritesheet from a different game.*

## Preface
This guide is written in the hopes that modding snowballs and more and more people get involved with creating custom content for this awesome game. I personally have 'ported' over 30 custom characters from various spritesheets of characters from mostly older retro console games. I have created a few weapons, an accessory and inadvertently a unique powerup, with plans to get more into different modding avenues like map creation.

That all being said, I sincerely hope this guide helps someone!

# Preparation

> In order to mod Vampire Survivors you need to be able to read the file you will be editing 99% of the time.

This file is named `main.bundle.js` and it is located in your Vampire Survivors game directory, located here;

 `SteamLibrary\steamapps\common\Vampire Survivors\resources\app\.webpack\renderer`

Locate this file. It will need to be 'formatted' to be legible. Otherwise, the entire file is on a single line. There are multiple ways to do this depending on what software you have/want to use.

I use Visual Studio Code personally, and highly recommend utilizing this text editor to get the job done.

### [Visual Studio Code](https://code.visualstudio.com/)


*Follow these steps to Format your `main.bundle.js`.*

1. Open Your `main.bundle.js` with VS Code. It will have all of the code on a[ single line.](https://i.imgur.com/v9M1Jcp.png)

2. Click the sidebar Icon that resembles 4 squares, and in the search bar that appeared near the top of VS Code enter; [JSTOOL](https://i.imgur.com/TZxeStt.png)

3. Install/Enable the JSTOOL plugin.

4. Highlight all of the text in `main.bundle.js` with CTRL+A and then enter in ALT+SHIFT+F.

5. You may be asked which formatter you would like to use, select JSTOOL.

6. Your file should now be [legible.](https://i.imgur.com/TZxeStt.png)

7. CTRL+S to save the file, and launch your game to ensure it still works. (If done right, it should)


# First Steps

> This section will guide you through locating and identifying sections you need to copy/modify for a custom character.

## Locating Art

I use numerous websites, along with google and bing image search to find sprite sheets that others' have ported or created.

*Some popular sites:*

* https://www.spritedatabase.net

* https://www.spriters-resource.com

* https://www.deviantart.com/

* https://itch.io/game-assets/free

*Tools Used:*

* [TexturePackerGUI](https://www.codeandweb.com/texturepacker)

* [GIMP](https://www.gimp.org/)

## Editing the Sheet



For a simple rundown though, I essentially look for sprite sheets that have models on them that arent too large, have a left/right facing directional model, with included walking animation.

[For example](https://i.imgur.com/EJjx5uT.png)

Keep in mind, the character selection screen has specific dimensions inside the [window.](https://i.imgur.com/JrHgIUQ.png) 'Smaller' characters are at max `30-32px` tall, and larger characters like Death or Leda are up to `47px` tall. I try to stay within `47px` tall.

1. I use GIMP to then zoom in on the sheet, copy the walk animation frames [\(they are usually grouped together\)](https://i.imgur.com/TaDsywn.png)

2. You can see on the left hand the size of my selection (150x81) just above my cursor.

3. CTRL+C to copy your selection, and then CTRL+N to make a new file. [Input the size from your selection previously.](https://i.imgur.com/AApxTJq.png)

4. [Delete the existing default background before pasting your clipboard into the new file.](https://i.imgur.com/Zow5kzP.png)

5. You will then have a new canvas with [just your walking animations.](https://i.imgur.com/kt7xhpw.png) 
 * Repeat this process for each ['frame'.](https://i.imgur.com/f4tmFNL.png)

6. If your model's height exceeds the `47px`, you may need to [shrink it](https://i.imgur.com/3iaqnlQ.png) to [fit.](https://i.imgur.com/NTXfA7A.png) Adjusting the Height here will automatically adjust the width to keep its' aspect ratio.

7. Export each frame as individual `.png` files, naming convention seemed to be sort of specific. An example;
 * goku_01.png
 * goku_02.png
 * goku_03.png

> Make sure your export has [no compression](https://i.imgur.com/P5j6SJe.png)

8. The game will play them in sequence, so naming them in proper order is important. It is also important to take note how many 'frames' a character uses.

**We are now done with GIMP.**
________________________________
## Packing the Sheet

> TexturePackerGUI has a trial, and a free version. I have found both work just fine.

Open TexturePacker, it may ask you to enable a trial, or just use the free version, it's up to you if you want to use the trial. The trial does offer the ability to split sprite sheets, but that an also be done elsewhere, [even online.](https://ezgif.com/sprite-cutter)

1. Drag all of your new .png files [into TexturePacker](https://i.imgur.com/OItlzNW.png)
 * Make sure 'Framework' is set to (JSON Array)
 * Algorithm is set to 'Basic'
 * Texture Format can be either `PNG-32` or `PNG-8` *(PNG-8 is only available in premium)*
 * Pixel Format `RGBA8888`

Underneath Framework, where it should now say JSON (Array) and to the right of `Data File` click the folder and assign a [save location.](https://i.imgur.com/y25iRvK.png) (This isn't important as you can simply move the files to your game folder later)

I name main plainly as shown for ease. Once saved, it should then show text outputs in both[`Data File` and `Texture File` [fields.](https://i.imgur.com/eKVeBXg.png)

Clicking `Publish Sheet` will create your new PNG spritesheet and the .JSON file with [all of it's data.](https://i.imgur.com/3fpW6BQ.png)
______________________

**We are now done with TexturePackerGUI.**

# Editing the Code

## Character Load

First place I start when adding a new character is making sure it is set to load. In your `main.bundle,js` there is a list of all characters you will need to extend. To locate this, the easiest way is to simply search for an existing character's name. 

1. Go to to top of your file (you may be at the bottom after formatting)
2. CTRL+F and in the window that popped up in the top right enter; `'ODDEEO'`.
3. This should bring you to the [character load list.](https://i.imgur.com/tFDenIS.png)
4. Insert your new custom character. You can follow the formula of other characters.

 This entry on the end has a `;` and whatever character is on the end, *must* keep that semicolon.


 `_0x52d938['ODDEEO'] = 'ODDEEO';`
 
 keep in mind - the beginning hex code  `_0x52d938` will change with every update, so if you plan on sustaining mods, you will have to change this with every update!

5. You can follow this formula to add additional characters. For example;
 
 `_0x52d938['GOKU'] = 'GOKU',`

6. Make sure to add your custom character above the character on the end of the list, or if you are adding it to the end of the list, make sure to include the `;`

7. Your addition should look like [this.](https://i.imgur.com/UvRIeqd.png)

**We are now done with Character Load Data.**

## Character Stat/Gear Data

We will be basically doing the same thing as before, locating the list where the character data is stored and copying/extending that table.

1. Do a search for `'ANTONIO'`, you should see a result not far away from where you already were that [looks like this.](https://i.imgur.com/ROR3rlQ.png)
 * This is the data set for the character. Here you can modify things like their starting stats, starting weapon(s) or accessories, Name, and the gains they get either per level or at each milestone.
 * The showcase line with all the jargon is for Debug mode, when enabling showcase, it gives all of those items.
 * For ease of update through version changes, I recommend [removing this from your custom characters.](https://i.imgur.com/ixUdPFs.png)

2. Copy the entire string shown in the first step. Make sure you have the `,` on the end after the final bracket. Your game *will* break without it.

3. Paste what you copied where you want your character to be on the loading list. They appear to load sequentially. I try to keep my custom characters near the bottom of the list, but it is up to you where to insert them. In this example we are just going to insert our new character directly [underneath Antonio and directly above Imelda.](https://i.imgur.com/XWun8On.png)

4. This image is our current custom character, [Goku.](https://i.imgur.com/h20BNfq.png)
 * I have noted best I can what every entry will do and how to modify them.
 * There are some entries you may want to remove, or may not have when copied from Antonio. I tried to cover them all.
 * Make sure the naming convention for your `textureName` is specific and you remember it. You will need it later for the Atlas.

5. I would hold off on editing any of the attributes for our custom character for now, except for `textureName` `spriteName` and `walkingFrames`. Ensure `walkingFrames` matches how many total frames your character has. In this example, we have 3. Using `0x3` or `3` works the same.

**We are now done with editing the Character** *for now*.

## Character Atlas

> Now that your character Data Set is... set you can now make sure the images you meticulously crafted will load!

This is likely the easiest step in the process, we are in the home stretch!

1. Do a search in your `main.bundle.js` for `GameOver.png` There is only [one entry in the entire file.](https://i.imgur.com/40GsyHc.png)

2. You want to insert a string to tell the game to load your textures.
 * `this['load']['atlas']('GOKU', 'mod/CharBundle/goku/goku.png', 'mod/CharBundle/goku/goku.json'),`
 * The game loads files from the `renderer` folder. So, if you want to tell it to load a file in say the `mod` folder like shown above, it must be told to do so.
 * It can be told to navigate to any folder you want inside `renderer` I chose to have my personal mods reside in `/mod/CharBundle/` as shown above, with breakout folders from there for each specific character.
 * Following this formula, we want to place the `.JSON` and `.PNG` files generated from TexturePacker into [whatever folder you are using in the Character Atlas.](https://i.imgur.com/2V7pShS.png)


**We are now done with Character Atlas.**

## Testing

> CTRL+S inside your `main.bundle.js`

> Launch your game!


Depending on where you placed you custom character in your list, they should now load! Granted everything was done properly, you now have your own custom character!

### Troubleshooting
 * If your game does not start/opens to a black screen the most likely cause of this is a missing comma, or an extra comma, or a failed ending to a bracket.




# Conclusion 

This has been a guide on how to install a custom character! Expect this guide to be updated as best I can.

Thanks for reading, happy modding!