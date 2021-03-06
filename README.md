# BakaBT Description Generator
This tool is intended for automated, fast, and most importantly, accurate generation of torrent descriptions for BakaBT tracker.

For now, it's still in very early alpha, but i intend to work on it until it becomes so easy to use that it'll be a nobrainer to go for it instead of manually typing HTML code.

### Usage, installation and updates
#### Linux:
##### Cloning the repo and installing dependencies: 
    git clone https://github.com/w1kl4s/DescriptionGenerator && cd DescriptionGenerator
    pip3 install -r requirements.txt
#### Windows:
Install Python 3 (tested on version 3.7) from https://www.python.org/downloads/windows/ (recommended is web-based Windows x86-64 installer) and Git https://github.com/git-for-windows/git/releases/tag/v2.19.0.windows.1 (recommended is Git-2.19.0-64-bit.exe file). Those may be diffrent if you run 32 bit system (which should be pretty rare these days), and i tested the program using those versions. After installing that, go to your desired application directory, and open up CMD/PowerShell there using shift + right click, and choose "Open Powershell/Command Line here" or something like that. In terminal, execute those commands:
    
     git clone https://github.com/w1kl4s/DescriptionGenerator
     cd  DescriptionGenerator
     py -m pip install -r requirements.txt

After installation is complete, you can close up your terminal.

#### Updating:
Just like you run requirements install , open terminal in directory with program, and type: `git pull`

#### Usage:
Start up `main.py` file, either using `python3 main.py` (Linux and Mac), or `py main.py` (Windows).
Windows also allows to execute py files, so double clicking on `main.py` file should do as well.

You will be prompted with window to enter your AniDB credentials. This is necessary, as AniDB requires authentification in or order to use their API. Entering Client Key is optional, as it's used to encrypt your connection.

After that, another window will open. Choose the folder with anime files you wish to parse, and you are done!

This will create HTML description file in Generated Descriptions folder, according to `basictemplate.html` file in templates folder. Progress of hashing and file query is displayed.

Speed of hashing depends heavily on read speed of directory (For example, i can hash with about 300 MB/s when directory is on my SSD, but if i try it with location over network, it can be as low as single megabytes per second.)

New fancy colored logs and stuff! Preview of what it looks like right now.

Mind that i put black background in HTML file for sake of visibility after generation. After you put proper background image, it will go away.
![Example output:](https://i.imgur.com/1cUl74F.png)


If you wish to use your own template, you can do it pretty easily! If you are here, i imagine you know at least basic principles of HTML. You can swap out `basictemplate.html` in `templates` folder to your own template, just keep the name `basictemplate.html`. In order to make fields properly appear, you will have to replace all curly bracelets in your file with double ones(replace `{` with `{{` and `}` with `}}`). After that, you can put fields in your file. You can look for them in my template, but i'll include it here as well:

    {episode_count}
    {categories}
    {director_link}
    {studio_links}
    {ANN_id}
    {anime_id}
    {MAL_id}
    {group_id}
    {group_name}
    {source}
    {file_format}
    {resolution}
    {video_codec}
    {frame_rate}
    {video_bitrate}
    {color_depth}
    {aspect_ratio}
    {audio_language}
    {audio_channels}
    {audio_codec}
    {audio_sample_rate}
    {audio_bitrate}
    {sub_language}
    {sub_format}
    {english_name}
    
Field names should be easily understood. Just put those in your HTML file, and you are good to go! Brackets around field names are important tho. Don't forget them!

### Current State and TODO

- [ ] Adding GUI and windows release for our not so tech-savvy friends.

- [x] Using collections instead of filthy dictionaries

- [x] Implement logging

- [x] Implement proper exception classes

- [x] Verification of each file with release information

- [x] Fetching of most basic data from AniDB

- [x] Writing obtained data to HTML template

- [x] Acquiring missing data from mediainfo (Framerate, aspect ratio, audio sample rate, channels, subtitle format)

- [x] Parsing every file data to get average values for whole release (video bitrate, audio bitrate)

- [x] Generating links for other sites (Anime News Network, AnimePlanet, MAL) (Partially done i guess, MAL and AnimePlanet need search instead of just pasting ID from AniDB)

- [x] Fetching pages of director and studio

- [ ] Fetching description either from ANN, AP, or MAL (for user to choose)

- [ ] Implementing multithreading for faster hashing and querying rate
### Limitations
Main limitation right now is AniDB API which does not contain all information that is needed. Also, it doesn't allow fast querying (Wiki says that it allows one request per 4 seconds, which is a lot). I'm using Yumemi Client for easier management of this ([Source Code](https://github.com/fpob/yumemi)).

NO FREAKIN' IDEA HOW IT WORKS ON WINDOWS.
I use mainly Ubuntu and Arch as my daily drivers. I have absolutely no idea how it will work on Windows, but it should be fine because Python magic i assume?  Anyway, Windows testers are really appriciated. I am screaming for help.

Right now, it doesn't check for extra files as well (Openings, Endings, etc), since AniDB API doesn't include those in episode number. Hashes of those files are still calculated and they will be fetched just like normal episodes, so having them in checked directory won't interfere with data parsing for main release itself.

Fetching proper MAL page is also tricky because of all the OVAs, extra movie and stuff like that with same title. I'll try to make it more accurate using show type field, but even then i'm not sure how well it will work.

Sadly, fetching data like sub creator is very hard since it's not consistent (on AniDB, it sometimes is in notes of release, but it's rare and not really helpful since it's just a string with group name. Additional search would be required, which would require a lot of work and wouldn't even be useful 99% of the time.)

AnimePlanet would also need some kind of scraper to properly parse since i didn't find any API reference for it. However it's very low on my list, beause let's be honest, who even uses AnimePlanet. 



## Help!

I am by no means a proper developer. I work as a sysadmin, so i have a lot of experience with Python, but not when it comes to writing a proper project from scratch. It would be great if someone who actually knows how to do that stuff properly came here and complained about it. I am open to suggestions how to improve it and make it a proper pythonic application.

