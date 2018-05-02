hey, thanks for using the plugin! :3



INSTALLATION
	- just extract in the game directory and replace all files


TEXT SYSTEM ORDER


	TEXT LINE SYNTAX

		Single Line Comment:
		// text

		Normal Line:
		key = value
		key=value

		Regex Line:
		R(pattern) = replace
		R(pattern)=replace
		R (pattern) = replace
		R (pattern)=replace

		When using regex:
		* try ALWAYS to avoid regex as possible, each regex search may costs 10ms per call per frame
		* try ALWAYS to avoid regex backtracking¹ this increase the engine searching time killing FPS
		* try ALWAYS to avoid optional quantifiers like *, *?, +, +?, ?, {n}, {n}?, {n,}, {n,}?, {n,m} and {n,m}?
		* try ALWAYS to avoid conditional matching like "|"
		* try ALWAYS to make sure your pattern only has one way to match

		¹ Backtracking occurs when a regular expression pattern contains optional quantifiers or alternation constructs,
		  and the regular expression engine returns to a previous saved state to continue its search for a match.


	IGNORED LINES

		- empty
		- double slash (//)
		- no equal sign (=) (Error)
		- more then one equal sign (=) (Error)
		- ignores trailing white spaces


	AUDIO FILES DIRECTORIES

		1- ". \ Plugins \ UITranslation \ <app> \ Audio \ *.txt"
		or ". \ Plugins \ UITranslation \ <app> \ <language> \ Audio \ *.txt"
		2- ". \ Plugins \ UITranslation \ Audio \ *.txt"
		or ". \ Plugins \ UITranslation \ <language> \ Audio \ *.txt"

		* <app> and <language> are defined in ". \ Plugins \ UITranslation \ Translation.ini" under ApplicationName_Folder and sLanguage respectively


	IMAGE FILES DIRECTORIES

		1- ". \ Plugins \ UITranslation \ <app1> \ Image \ <app2> \ <*>"
		or ". \ Plugins \ UITranslation \ <app1> \ <language> \ Image \ <app2> \ <*>"
		2- ". \ Plugins \ UITranslation \ Image \ <app2> \ <*>"
		or ". \ Plugins \ UITranslation \ <language> \ Image \ <app2> \ <*>"

		* <app1> and <language> are defined in ". \ Plugins \ UITranslation \ Translation.ini" under ApplicationName_Folder and sLanguage respectively
		* <app2> is defined in ". \ Plugins \ UITranslation \ <app1> \ Image \ ApplicationName.ini" under sMainFolder
		* <*> is any directory with ".png", ".jpg", ".jpeg", ".tga", ".dds" file types


	TEXT FILES DIRECTORIES

		1- ". \ Plugins \ UITranslation \ <app> \ Translation.txt"
		or ". \ Plugins \ UITranslation \ <app> \ Translation.<language>.txt"
		2- ". \ Plugins \ UITranslation \ <app> \ Text \ *.txt"
		or ". \ Plugins \ UITranslation \ <app> \ <language> \ Text \ *.txt"
		3- ". \ Plugins \ UITranslation \ Text \ *.txt"
		or ". \ Plugins \ UITranslation \ <language> \ Text \ *.txt"

		* <app> and <language> are defined in ". \ Plugins \ UITranslation \ Translation.ini" under ApplicationName_Folder and sLanguage respectively


	FILE TYPE

		Ignored = ".<name>.txt"
		Leveled = "<name>.<number>.txt", "<name>.<number>.regex.txt", "<name>.<number>.noregex.txt"
		Globalized = "<name>.txt", "<name>.regex.txt", "<name>.noregex.txt"

		* number is the same as the game level number


	LOAD ORDER

		ignores any file that starts with dot like ".log.txt"

		Regex On:
		1 - "Translation.txt" or "Translation.<language>.txt" and loads regex syntax
		2 - "Text \ <name>.<number>.txt" and "Text \ <name>.txt" (no overrides between each other) and loads regex syntax
		3 - "Text \ <name>.<number>.regex.txt" and "Text \ <name>.regex.txt" (no overrides between each other) and loads normal/regex syntax

		Regex Off:
		1 - "Translation.txt" or "Translation.<language>.txt" and ignore regex syntax
		2 - "Text \ <name>.<number>.txt" and "Text \ <name>.txt" (no overrides between each other) and ignore regex syntax
		3 - "Text \ <name>.<number>.noregex.txt" and "Text \ <name>.noregex.txt" (no overrides between each other) and ignore regex syntax

		* the greater order overrides the lower order
		* regex is defined in ". \ Plugins \ UITranslation \ Translation.ini" under bUseRegEx


TRANSLATION ORDER


	REGEX AND PREDICTIONS ON

		First Try:
		1 - Leveled normal translations
		2 - Leveled regex translations
		3 - Globalized normal translations
		4 - Globalized regex translations

		Second Try:
		1 - Predictions normal translations


	REGEX AND PREDICTIONS OFF

		First Try:
		1 - Leveled normal translations
		2 - Globalized normal translations

		* regex and prediction are defined in ". \ Plugins \ UITranslation \ Translation.ini" under bUseRegEx and bUseTextPrediction respectively 


Changes v0.16
- fixed default flip for dds files
- fixed double image loading
- added psd image support

Changes v0.15
- always load items from global path
- v0.15.1 fixed multiple load calls caused by global path

Changes v0.14
- added subtitle support

Changes v0.13
- do not translate input text

Changes v0.12
- changed the folder structure
- added support to load translations by level
- reloads translations upon changing sLanguage and bUseRegEx settings
- retranslates upon changing bFindText setting
- fixed only the first image object got dumped and missing the rest
- fixed several other small bugs
- v0.12.3 fixed several other small bugs
- v0.12.4 fixed some image override bugs

Changes v0.11
- code optimizations
- fixed not finding existing translation on loading
- fixed several other small bugs
- v0.11.1 added text prediction mode
- v0.11.1 renamed bCopy2Clipboard to bUseCopy2Clipboard
- v0.11.1 renamed iCopyTime(ms) to iCopy2ClipboardTime(ms)
- v0.11.1 fixed story fast click not translating
- v0.11.1 fixed reloading text before finishing loading the translations files
- v0.11.4 improved text prediction performance
- v0.11.6 improved text prediction wrap
- v0.11.8 adds back what was removed from the original text
- v0.11.10 adds ability to replace cursor
- v0.11.11 fixed some image cache bugs
- v0.11.12 fixed log writer

Changes v0.10
- show errors only in FindMore mode
- apply translation on reload
- added load external images
- added copy to clipboard support
- added support to comment lines
- v0.10.1 fixed regex incompatibility
- v0.10.2 fixed memory leak
- v0.10.3 fixed section repeating
- v0.10.4 fixed sprite override
- v0.10.4 fixed some cases of textures not unloading
- v0.10.4 image cache improvements
- v0.10.4 moved files to "Plugins\UITranslation"
- v0.10.4 moved texts to "Plugins\UITranslation\Text"
- v0.10.5 renamed bFindMore to bFindText
- v0.10.5 added DebugMode to log plugin like errors
- v0.10.5 added a flip back option in Image\ini file for .dds files
- v0.10.5 fixed encode/decode special text characters
- v0.10.5 fixed rawimage not loading
- v0.10.5 fixed reload translation not getting the right text to translate back
- v0.10.5 fixed multiple lines wrapped not getting translated
- v0.10.5 fixed several other small bugs
- v0.10.6 added changing bFindText from False to True at run-time now will dump untranslated text
- v0.10.6 fixed untranslated text not returning the original text

Changes v0.9
- first fixed story mode
- v0.9.1 fixed word wrap [-reverted]
- v0.9.3 fixed missing null regex check
- v0.9.4~v0.9.5 fixed the wrap for good
- v0.9.6 forced wrap to all
- v0.9.7 fixed some null errors
- v0.9.7 adjusted translate code
- v0.9.7 compile regex at startup
- v0.9.7 fixed error report

Changes v0.8
- v0.8b regex search check optimization
- v0.8b added ability to toggle regex in settings by setting bUseRegEx to True or False
- v0.8b does not load regex strings if it is disabled
- v0.8.3 skip invalid character before even start to search
- v0.8.4 optimizations for regex disabled
- v0.8.5 cache last translation (speeds up fps)
- v0.8.5 parse regex at game startup (speeds up regex/fps)
- v0.8.5 thank kruparker for helping me
- v0.8.6 optimization for the translation cache
- v0.8.6 added Readme.txt file
- v0.8.7 changed the load order
- v0.8.8 fixed language directory path
- v0.8.9 caches regex to match the regex list size (speeds up regex/fps)

Changes v0.7:
- fixed memory leak

Changes v0.6:
- v0.6a added listener to ini file
- v0.6b support to multiple files (more info to come)
- v0.6 fixed missing sLanguage setting
- v0.6 fixed duplicated log

Changes v0.5:
- removed white-space characters (trim)

Changes v0.4:
- small adjustment to font size

Changes v0.3:
- code optimization
- log file for duplicate entries
- added regex support with "R([TEXT])" or "R ([TEXT])" e.g.:
R (パターン(\d\d)) = Pattern $1
R (読み込み中・・([\d]+?)%) = Loading... $1%

Changes v0.2:
-  fixed font size

Changes v0.1:
- no need any plugin injector
- translator can now auto reload (not translate) if the translation.txt file is modified
- new translations will appear in game as you load new stuff
