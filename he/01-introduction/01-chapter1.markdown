# מתחילים #

הפרק הזה יעסוק באיך מתחילים עם Git. נתחיל בהתחלה, וניתן מעט רקע על כלים לניהול גרסאות, ומשם נמשיך לכיצד להריץ את Git על המערכת שלך, ולבסוף, כיצד להתקין אותו כדי להתחיל לעבוד. בסוף פרק זה תביני מדוע Git קיים, למה לך להשתמש בו ותהיי מוכנה לעשות זאת.

## ניהול גרסאות ##

מהו ניהול גרסאות, ומדוע שיהיה לך אכפת? ניהול גרסאות הוא מערכת שרושמת שינויים בקובץ או בקבוצת קבצים לאורך זמן כך שמאוחר יותר תוכלי לשחזר גרסאות מסויימות. בדוגמאות בספר זה תשתמשי בקוד תוכנה בקבצים להם ננהל גרסאות, למרות שבמציאות תוכלי לעשות זאת עם כמעט כל סוג קובץ במחשב.

אם את מעצבת גרפיקה או אתרים ותרצי לשמור כל גרסא של כל תמונה או עימוד (layout, שאותו בטוח תרצי לשמור), שימוש במערכת לניהול גרסאות (VCS) יהיה צעד נבון. הוא מאפשר לך להחזיר קבצים למצבם הקודם, להחזיר פרוייקט שלם למצבו הקודם, להשוות שינויים לאורך זמן, לראות מי האחרון  ששינה משהו שאולי גורם לבעיה, מי הכניס נושא מסויים ומתי, ועוד. ניהול גרסאות בדרך כלל אומר גם שאם דפקת משהו או איבדת קבצים, את יכולה להתאושש מהר. בנוסף, את מקבלת את כל זה כשאת משלמת מעט מאוד על כל פעולה.

### ניהול גרסאות מקומי ###

כדי לנהל גרסאות, הרבה אנשים נוקטים בשיטה של העתקת קבצים לספריה אחרת (אם הם נבונים, הם אולי אפילו מתעדים את זמן השמירה). הגישה הזו כה נפוצה מכיוון שהיא כה פשוטה, אבל היא גם מועדת מאוד לטעויות. קל מאוד לשכוח באיזו ספרייה את ולכתוב לתוך קבצים לא נכונים או להעתיק ולדרוס קבצים בלי כוונה.

כדי להתמודד עם הבעיה הזו, מתכנתים פיתחו ממזמן מנהלי גרסאות מקומיים עם בסיסי מידע פשוטים ששמרו את כל השינויים שנעשו בקבצים שעבורם נוהלו השיכתובים (ראי תרשים 1-1).

Insert 18333fig0101.png 
תרשים 1-1. תרשים של ניהול גרסאות מקומי.

אחד מהכלים היותר פופולריים לנהול גרסאות היה מערכת ששמה rcs, שעדיין מופצת היום עם הרבה מחשבים. אפילו מערכת ההפעלה  Mac OS X הפופולרית כוללת את פקודת ה rcs כשאת מתקינה את כלי הפיתוח (Developer Tools). באופן בסיסי, הכלי הזה עובד על ידי שמירת קבוצות של טלאים (כלומר, ההבדלים בין קבצים) משינוי אחד לשני בפורמט מיוחד על הדיסק; כך הוא יכול לשחזר איך כל קובץ נראה בכל נקודת זמן על ידי סיכום כל הטלאים.

### ניהול גרסאות ריכוזי ###

הצורך לשתף פעולה עם מפתחים שעבדו על מערכות אחרות היווה את הבעיה המשמעותית הבאה. כדי להתמודד איתה, פותחו מנהלי גרסאות ריכוזיים (CVCSs). למערכות אלו, כדוגמת CVS, Subversion או Perforce, יש שרת יחיד שמכיל את כל הקבצים המנוהלים, ומספר לקוחות שמוציאים קבצים מאותו מקום מרכזי. במשך שנים ארוכות זה היה ניהול הגרסאות הסטנדרטי (ראי תרשים 1-2).

Insert 18333fig0102.png 
תרשים 1-2. תרשים של ניהול גרסאות ריכוזי.

המבנה הזה הציע יתרונות רבים, במיוחד לעומת גרסאות מקומיות. לדוגמא, כולם יודעים במידה מסויימת מה כל אחד בפרוייקט עושה. למנהלים יש שליטה מדוייקת על מי יכול לעשות מה; וזה קל הרבה יותר לנהל מערכת ריכוזית מאשר להתעסק עם בסיסי מידע מקומיים בכל תחנת קצה.

עם זאת, למבנה הזה יש כמה חסרונות רציניים. הבולט מביניהם הוא שהשרת מהווה למעשה נקודת כשל יחידה. אם השרת מושבת למשך שעה, אז במשך שעה זו אף אחד לא יכול לשתף בכלל, או לשמור גרסאות עם שינויים על שום דבר שעובדים עליו. אם הדיסק הקשיח, שבסיס הנתונים עליו, נפגם ולא נשמרו גיבויים סדירים, את פשוט מאבדת את הכל - את כל ההיסטוריה של הפרוייקט, למעט חתכים (snapshots) שיש במקרה לאנשים על המכונות המקומיות שלהם. גרסאות מקומיות סובלות מאותה הבעיה בדיוק - כל זמן שיש לך את כל ההיסטוריה של הפרוייקט במקום אחד, את מסתכנת בכך שתאבדי את כולו.

### ניהול גרסאות מבוזר ###

כאן נכנסות לתמונה מערכות ניהול גרסאות מבוזרות (DVCSs). בניהול גרסאות מבוזר (כגון Git, Mercurial, Bazaar או Darcs), לקוחות לא סתם מוציאים את העותקים האחרונים של הקבצים: הם משקפים את המאגר (repository) במלואו. וכך, אם איזשהו שרת מת, והמערכות האלו שיתפו דרכו, אפשר להעתיק כל אחד ממאגרי הלקוח חזרה לשרת ולשחזר אותו. למעשה, כל גרסא שיוצאת מהשרת היא גיבוי מלא של כל המידע (ראי תרשים 1-3).

Insert 18333fig0103.png 
תרשים 1-3. תרשים של ניהול גרסאות מבוזר.

יתרה מכך, רבים מהכלים האלו מתמודדים די טוב עם עבודה מול מספר מאגרים מרוחקים, כך שאת יכולה לשתף פעולה עם קבוצות אנשים שונות בדרכים שונות באותו פרוייקט בעת ובעונה אחת. כך ניתן לקבוע סוגים של  תהליכי עבודה שאינם אפשריים במערכות ריכוזיות, כגון מודלים היררכיים.

## היסטוריה קצרה של Git ##

כמו הרבה דברים טובים בחיים, Git התחיל עם מעט הרסנות יצירתית וחילוקי דעות לוהטים. הליבה של לינוקס (The Linux kernel) הוא פרוייקט תוכנה בקוד פתוח בקנה מידה די גדול. במשך רוב חיי התחזוקה של הפרוייקט (1991-2002), שינויים בתוכנה נמסרו כטלאים וכקבצי ארכיון. בשנת 2002, הפרוייקט החל להשתמש במערכת גרסאות מבוזרת פרטית (קניינית) שנקראה BitKeepr.

בשנת 2005, הסתיימו היחסים בין הקהילה שפיתחה את הליבה ובין החברה המסחרית שפיתחה את BitKeeper, ובוטלה האפשרות להשתמש בכלי ללא תשלום. מצב זה הביא את קהילת מפתחי לינוקס (ובמיוחד את לינוס טרובלדס, היוצר של לינוקס) לפתח כלי משלהם בהתבסס על כמה מהלקחים שלמדו תוך כדי השימוש ב BitKeeper. מספר מטרות המערכת החדשה היו כדלקמן:

*	מהירות
*	תכנון פשוט
*	תמיכה איתנה בפיתוח לא-לינארי (אלפי ענפים במקביל)
*	מבוזר לחלוטין
*	יכולת להתמודד ביעילות עם פרוייקטים גדולים כדוגמת הליבה של לינוקס (מהירות וכמות המידע)

מאז לידתו ב 2005, Git התפתח והבשיל לכלי קל לשימוש שעדיין שומר על האיכויות הראשוניות האלו. הוא מהיר באופן בלתי יאומן, יעיל ביותר בפרוייקטים רחבי היקף, ובעל מערכת הסתעפויות יוצאת מהכלל עבור פיתוח לא-לינארי.

## יסודות Git ##

אז מה זה Git על רגל אחת? זאת פסקה שחשוב להפנים, מכיוון שאם הבנת מהו Git ואת היסודות לאיך שהוא עובד, אז כנראה יהיה לך הרבה יותר קל להשתמש ב Git ביעילות. תוך כדי שאת לומדת את Git, השתדלי לנקות את הראש משאר הדברים שאולי את יודעת על מנהלי גרסאות אחרים כמו Subversion או Perforce; זה יעזור לך להימנע מלהתבלבל בדקויות של שימוש בכלי. האופן בו Git שומר וחושב על מידע שונה באופן מהותי מהכלים האחרים, למרות שממשק המשתמש די דומה; הבנת ההבדלים תעזור לך שלא להתבלבל בזמן השימוש בו.

### חתכים, לא הבדלים ###

ההבדל המרכזי בין Git ובין מערכות אחרות (כולל Subversion וחבריו) הוא הדרך בה Git חושב על מידע. כתפיסה, רוב המערכות האחרות אוצרות מידע במעין רשימה של שינויים עבור קובץ מסויים. מערכות אלו (CVS, Subversion, Perforce, Bazaar וכך הלאה) חושבות על המידע שהן שומרות כצירוף של קבוצת קבצים והשינויים שנעשו בקבצים אלו לאורך זמן, כפי שמדגם בתרשים 1-4.

Insert 18333fig0104.png 
תרשים 1-4. מערכות אחרות נוטות לאגור מידע כשינויים לגרסת בסיס של כל קובץ.

Git לא חושב על או שומר מידע בדרך זו. לחלופין, Git חושב על המידע שלו כקבוצת חתכים של מערכת קבצים מיניאטורית. באופן בסיסי, כל פעם שאת מכניסה (commit), או שומרת את המצב של הפרוייקט שלך ב Git, הוא מצלם חתך של איך שהקבצים שלך נראים באותו רגע ושומר הפניה אל החתך. לשם היעילות, אם קבצים לא השתנו, Git לא שומר את הקובץ שוב - רק קישור (link) לקובץ הזהה שכבר נשמר קודם. Git חושב על המידע שלו בדומה לתרשים 1-5.

Insert 18333fig0105.png 
תרשים 1-5. Git שומר מידע כחתכים של הפרוייקט לאורך זמן.

זוהי הבחנה חשובה בין Git וכמעט כל שאר מנהלי הגרסאות. זה מכריח את Git לשקול מחדש כמעט כל היבט של ניהול גרסאות שרוב המערכות האחרות העתיקו מקודמיהן. כך Git נעשה יותר דומה למערכת קבצים קטנה עם כמה כלים חזקים להפליא שבנויים לתוכה, מאשר סתם כלי לניהול גרסאות. נחקור כמה מהיתרונות הגלומים בתפיסת כזו של מידע כשנלמד על הסתעפות ענפים ב Git בפרק 3.

### כמעט כל פעולה היא מקומית ###

רוב הפעולות ב Git צריכות רק קבצים ומשאבים מקומיים בכדי להתבצע - באופן כללי, אין כלל צורך במידע ממחשב אחר ברשת שלך. אם את רגילה למערכות ריכוזיות, שברוב הפעולות בהן, תשלמי את המחיר ההוא של גישה לרשת, הרי שהצד הזה של Git יגרום לך לחשוב שאלוהי המהירות ברכו את Git בכוחות על טבעיים. מכיוון שכל ההיסטוריה של הפרוייקט נמצא ממש כאן על הדיסק המקומי שלך, רוב הפעולות יראו לך כמעט מיידיות.

For example, to browse the history of the project, Git doesn’t need to go out to the server to get the history and display it for you—it simply reads it directly from your local database. This means you see the project history almost instantly. If you want to see the changes introduced between the current version of a file and the file a month ago, Git can look up the file a month ago and do a local difference calculation, instead of having to either ask a remote server to do it or pull an older version of the file from the remote server to do it locally.

This also means that there is very little you can’t do if you’re offline or off VPN. If you get on an airplane or a train and want to do a little work, you can commit happily until you get to a network connection to upload. If you go home and can’t get your VPN client working properly, you can still work. In many other systems, doing so is either impossible or painful. In Perforce, for example, you can’t do much when you aren’t connected to the server; and in Subversion and CVS, you can edit files, but you can’t commit changes to your database (because your database is offline). This may not seem like a huge deal, but you may be surprised what a big difference it can make.

### Git Has Integrity ###

Everything in Git is check-summed before it is stored and is then referred to by that checksum. This means it’s impossible to change the contents of any file or directory without Git knowing about it. This functionality is built into Git at the lowest levels and is integral to its philosophy. You can’t lose information in transit or get file corruption without Git being able to detect it.

The mechanism that Git uses for this checksumming is called a SHA-1 hash. This is a 40-character string composed of hexadecimal characters (0–9 and a–f) and calculated based on the contents of a file or directory structure in Git. A SHA-1 hash looks something like this:

	24b9da6552252987aa493b52f8696cd6d3b00373

You will see these hash values all over the place in Git because it uses them so much. In fact, Git stores everything not by file name but in the Git database addressable by the hash value of its contents.

### Git Generally Only Adds Data ###

When you do actions in Git, nearly all of them only add data to the Git database. It is very difficult to get the system to do anything that is not undoable or to make it erase data in any way. As in any VCS, you can lose or mess up changes you haven’t committed yet; but after you commit a snapshot into Git, it is very difficult to lose, especially if you regularly push your database to another repository.

This makes using Git a joy because we know we can experiment without the danger of severely screwing things up. For a more in-depth look at how Git stores its data and how you can recover data that seems lost, see Chapter 9.

### The Three States ###

Now, pay attention. This is the main thing to remember about Git if you want the rest of your learning process to go smoothly. Git has three main states that your files can reside in: committed, modified, and staged. Committed means that the data is safely stored in your local database. Modified means that you have changed the file but have not committed it to your database yet. Staged means that you have marked a modified file in its current version to go into your next commit snapshot.

This leads us to the three main sections of a Git project: the Git directory, the working directory, and the staging area.

Insert 18333fig0106.png 
Figure 1-6. Working directory, staging area, and git directory.

The Git directory is where Git stores the metadata and object database for your project. This is the most important part of Git, and it is what is copied when you clone a repository from another computer.

The working directory is a single checkout of one version of the project. These files are pulled out of the compressed database in the Git directory and placed on disk for you to use or modify.

The staging area is a simple file, generally contained in your Git directory, that stores information about what will go into your next commit. It’s sometimes referred to as the index, but it’s becoming standard to refer to it as the staging area.

The basic Git workflow goes something like this:

1.	You modify files in your working directory.
2.	You stage the files, adding snapshots of them to your staging area.
3.	You do a commit, which takes the files as they are in the staging area and stores that snapshot permanently to your Git directory.

If a particular version of a file is in the git directory, it’s considered committed. If it’s modified but has been added to the staging area, it is staged. And if it was changed since it was checked out but has not been staged, it is modified. In Chapter 2, you’ll learn more about these states and how you can either take advantage of them or skip the staged part entirely.

## Installing Git ##

Let’s get into using some Git. First things first—you have to install it. You can get it a number of ways; the two major ones are to install it from source or to install an existing package for your platform.

### Installing from Source ###

If you can, it’s generally useful to install Git from source, because you’ll get the most recent version. Each version of Git tends to include useful UI enhancements, so getting the latest version is often the best route if you feel comfortable compiling software from source. It is also the case that many Linux distributions contain very old packages; so unless you’re on a very up-to-date distro or are using backports, installing from source may be the best bet.

To install Git, you need to have the following libraries that Git depends on: curl, zlib, openssl, expat, and libiconv. For example, if you’re on a system that has yum (such as Fedora) or apt-get (such as a Debian based system), you can use one of these commands to install all of the dependencies:

	$ yum install curl-devel expat-devel gettext-devel \
	  openssl-devel zlib-devel

	$ apt-get install libcurl4-gnutls-dev libexpat1-dev gettext \
	  libz-dev libssl-dev
	
When you have all the necessary dependencies, you can go ahead and grab the latest snapshot from the Git web site:

	http://git-scm.com/download
	
Then, compile and install:

	$ tar -zxf git-1.7.2.2.tar.gz
	$ cd git-1.7.2.2
	$ make prefix=/usr/local all
	$ sudo make prefix=/usr/local install

After this is done, you can also get Git via Git itself for updates:

	$ git clone git://git.kernel.org/pub/scm/git/git.git
	
### Installing on Linux ###

If you want to install Git on Linux via a binary installer, you can generally do so through the basic package-management tool that comes with your distribution. If you’re on Fedora, you can use yum:

	$ yum install git-core

Or if you’re on a Debian-based distribution like Ubuntu, try apt-get:

	$ apt-get install git-core

### Installing on Mac ###

There are two easy ways to install Git on a Mac. The easiest is to use the graphical Git installer, which you can download from the Google Code page (see Figure 1-7):

	http://code.google.com/p/git-osx-installer

Insert 18333fig0107.png 
Figure 1-7. Git OS X installer.

The other major way is to install Git via MacPorts (`http://www.macports.org`). If you have MacPorts installed, install Git via

	$ sudo port install git-core +svn +doc +bash_completion +gitweb

You don’t have to add all the extras, but you’ll probably want to include +svn in case you ever have to use Git with Subversion repositories (see Chapter 8).

### Installing on Windows ###

Installing Git on Windows is very easy. The msysGit project has one of the easier installation procedures. Simply download the installer exe file from the Google Code page, and run it:

	http://code.google.com/p/msysgit

After it’s installed, you have both a command-line version (including an SSH client that will come in handy later) and the standard GUI.

## First-Time Git Setup ##

Now that you have Git on your system, you’ll want to do a few things to customize your Git environment. You should have to do these things only once; they’ll stick around between upgrades. You can also change them at any time by running through the commands again.

Git comes with a tool called git config that lets you get and set configuration variables that control all aspects of how Git looks and operates. These variables can be stored in three different places:

*	`/etc/gitconfig` file: Contains values for every user on the system and all their repositories. If you pass the option` --system` to `git config`, it reads and writes from this file specifically. 
*	`~/.gitconfig` file: Specific to your user. You can make Git read and write to this file specifically by passing the `--global` option. 
*	config file in the git directory (that is, `.git/config`) of whatever repository you’re currently using: Specific to that single repository. Each level overrides values in the previous level, so values in `.git/config` trump those in `/etc/gitconfig`.

On Windows systems, Git looks for the `.gitconfig` file in the `$HOME` directory (`C:\Documents and Settings\$USER` for most people). It also still looks for /etc/gitconfig, although it’s relative to the MSys root, which is wherever you decide to install Git on your Windows system when you run the installer.

### Your Identity ###

The first thing you should do when you install Git is to set your user name and e-mail address. This is important because every Git commit uses this information, and it’s immutably baked into the commits you pass around:

	$ git config --global user.name "John Doe"
	$ git config --global user.email johndoe@example.com

Again, you need to do this only once if you pass the `--global` option, because then Git will always use that information for anything you do on that system. If you want to override this with a different name or e-mail address for specific projects, you can run the command without the `--global` option when you’re in that project.

### Your Editor ###

Now that your identity is set up, you can configure the default text editor that will be used when Git needs you to type in a message. By default, Git uses your system’s default editor, which is generally Vi or Vim. If you want to use a different text editor, such as Emacs, you can do the following:

	$ git config --global core.editor emacs
	
### Your Diff Tool ###

Another useful option you may want to configure is the default diff tool to use to resolve merge conflicts. Say you want to use vimdiff:

	$ git config --global merge.tool vimdiff

Git accepts kdiff3, tkdiff, meld, xxdiff, emerge, vimdiff, gvimdiff, ecmerge, and opendiff as valid merge tools. You can also set up a custom tool; see Chapter 7 for more information about doing that.

### Checking Your Settings ###

If you want to check your settings, you can use the `git config --list` command to list all the settings Git can find at that point:

	$ git config --list
	user.name=Scott Chacon
	user.email=schacon@gmail.com
	color.status=auto
	color.branch=auto
	color.interactive=auto
	color.diff=auto
	...

You may see keys more than once, because Git reads the same key from different files (`/etc/gitconfig` and `~/.gitconfig`, for example). In this case, Git uses the last value for each unique key it sees.

You can also check what Git thinks a specific key’s value is by typing `git config {key}`:

	$ git config user.name
	Scott Chacon

## Getting Help ##

If you ever need help while using Git, there are three ways to get the manual page (manpage) help for any of the Git commands:

	$ git help <verb>
	$ git <verb> --help
	$ man git-<verb>

For example, you can get the manpage help for the config command by running

	$ git help config

These commands are nice because you can access them anywhere, even offline.
If the manpages and this book aren’t enough and you need in-person help, you can try the `#git` or `#github` channel on the Freenode IRC server (irc.freenode.net). These channels are regularly filled with hundreds of people who are all very knowledgeable about Git and are often willing to help.

## Summary ##

You should have a basic understanding of what Git is and how it’s different from the CVCS you may have been using. You should also now have a working version of Git on your system that’s set up with your personal identity. It’s now time to learn some Git basics.
