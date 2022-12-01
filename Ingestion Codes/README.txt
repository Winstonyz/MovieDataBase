akas.csv
	Original Dataset
	- filtered region with US
	- filtered by joining with basics to get rid of data without a startYear(\N)
	- runtimeMinutes > 20

	Contains the following information for titles:
	- titleId (string) - a tconst, an alphanumeric unique identifier of the title
	- ordering (integer) – a number to uniquely identify rows for a given titleId
	- title (string) – the localized title

	<class 'pandas.core.frame.DataFrame'>
	Int64Index: 541142 entries, 12 to 1299537
	Data columns (total 3 columns):
	titleId     541142 non-null object
	ordering    541142 non-null int64
	title       541142 non-null object
	dtypes: int64(1), object(2)
	memory usage: 16.5+ MB

title.basics.csv
	Original Dataset
	- filtered region with US
	- Removed rows with startYear(\N)
	- runtimeMinutes > 20
	- tconst foreign key reference to akas(titleId)

	Contains the following information for titles:
	- tconst (string) - alphanumeric unique identifier of the title
	- titleType (string) – the type/format of the title (e.g. movie, short, tvseries, tvepisode, video, etc)
	- primaryTitle (string) – the more popular title / the title used by the filmmakers on promotional materials at the point of release
	- originalTitle (string) - original title, in the original language
	- isAdult (boolean) - 0: non-adult title; 1: adult title
	- startYear (YYYY) – represents the release year of a title. In the case of TV Series, it is the series start year
	- endYear (YYYY) – TV Series end year. ‘\N’ for all other title types
	- runtimeMinutes – primary runtime of the title, in minutes
	- genres (string array) – includes up to three genres associated with the title

	<class 'pandas.core.frame.DataFrame'>
	Int64Index: 489949 entries, 8 to 8688616
	Data columns (total 9 columns):
	tconst            489949 non-null object
	titleType         489949 non-null object
	primaryTitle      489949 non-null object
	originalTitle     489949 non-null object
	isAdult           489949 non-null object
	startYear         489949 non-null object
	endYear           489949 non-null object
	runtimeMinutes    489949 non-null int32
	genres            489949 non-null object
	dtypes: int32(1), object(8)
	memory usage: 35.5+ MB

crew.csv
	Original Dataset
	- tconst foreign key reference to akas(titleId)

	Contains the director and writer information for all the titles in IMDb. Fields include:
	- tconst (string) - alphanumeric unique identifier of the title
	- directors (array of nconsts) - director(s) of the given title
	- writers (array of nconsts) – writer(s) of the given title

	<class 'pandas.core.frame.DataFrame'>
	Int64Index: 489949 entries, 8 to 8688616
	Data columns (total 3 columns):
	tconst       489949 non-null object
	directors    489949 non-null object
	writers      489949 non-null object
	dtypes: object(3)
	memory usage: 15.0+ MB

episode.csv
	Original Dataset
	- tconst foreign key reference to akas(titleId)
	
	Contains the tv episode information. Fields include:
	- tconst (string) - alphanumeric identifier of episode
	- parentTconst (string) - alphanumeric identifier of the parent TV Series
	- seasonNumber (integer) – season number the episode belongs to
	- episodeNumber (integer) – episode number of the tconst in the TV series

	<class 'pandas.core.frame.DataFrame'>
	Int64Index: 121644 entries, 114 to 6498739
	Data columns (total 4 columns):
	tconst           121644 non-null object
	parentTconst     121644 non-null object
	seasonNumber     121644 non-null object
	episodeNumber    121644 non-null object
	dtypes: object(4)
	memory usage: 4.6+ MB

principals.csv
	Original Dataset
	- tconst foreign key reference to akas(titleId)

	Contains the principal cast/crew for titles
	- tconst (string) - alphanumeric unique identifier of the title
	- ordering (integer) – a number to uniquely identify rows for a given titleId
	- nconst (string) - alphanumeric unique identifier of the name/person
	- category (string) - the category of job that person was in
	- job (string) - the specific job title if applicable, else '\N'
	- characters (string) - the name of the character played if applicable, else '\N'

	<class 'pandas.core.frame.DataFrame'>
	Int64Index: 4032123 entries, 24 to 48828166
	Data columns (total 6 columns):
	tconst        object
	ordering      int64
	nconst        object
	category      object
	job           object
	characters    object
	dtypes: int64(1), object(5)
	memory usage: 215.3+ MB

ratings.csv
	Original Dataset
	- tconst foreign key reference to akas(titleId)

	Contains the IMDb rating and votes information for titles
	- tconst (string) - alphanumeric unique identifier of the title
	- averageRating – weighted average of all the individual user ratings
	- numVotes - number of votes the title has received

	<class 'pandas.core.frame.DataFrame'>
	Int64Index: 323057 entries, 8 to 1213971
	Data columns (total 3 columns):
	tconst           323057 non-null object
	averageRating    323057 non-null float64
	numVotes         323057 non-null int64
	dtypes: float64(1), int64(1), object(1)
	memory usage: 9.9+ MB

name.basics.csv
	Original Dataset
	- nconst foreign key reference to principals(nconst)

	Contains the following information for names:
	- nconst (string) - alphanumeric unique identifier of the name/person
	- primaryName (string)– name by which the person is most often credited
	- birthYear – in YYYY format
	- deathYear – in YYYY format if applicable, else '\N'
	- primaryProfession (array of strings)– the top-3 professions of the person
	- knownForTitles (array of tconsts) – titles the person is known for

	<class 'pandas.core.frame.DataFrame'>
	Int64Index: 1106616 entries, 0 to 11407035
	Data columns (total 6 columns):
	nconst               1106616 non-null object
	primaryName          1106616 non-null object
	birthYear            1106616 non-null object
	deathYear            1106616 non-null object
	primaryProfession    996906 non-null object
	knownForTitles       1106616 non-null object
	dtypes: object(6)
	memory usage: 59.1+ MB


--------------------------------------

	genres.info();
	1. obtain from title.basics
	2. drop duplicates

<class 'pandas.core.frame.DataFrame'>
RangeIndex: 29 entries, 0 to 28
Data columns (total 1 columns):
Genre    29 non-null object
dtypes: object(1)
memory usage: 312.0+ bytes

	genreOf.info();

<class 'pandas.core.frame.DataFrame'>
RangeIndex: 903153 entries, 0 to 903152
Data columns (total 2 columns):
tconst    903153 non-null object
Genre     903153 non-null object
dtypes: object(2)
memory usage: 13.8+ MB

	movie.info();

<class 'pandas.core.frame.DataFrame'>
RangeIndex: 489949 entries, 0 to 489948
Data columns (total 8 columns):
tconst            489949 non-null object
titleType         489949 non-null object
primaryTitle      489949 non-null object
originalTitle     489949 non-null object
isAdult           489949 non-null int64
startYear         489949 non-null int64
endYear           489949 non-null object
runtimeMinutes    489949 non-null int64
dtypes: int64(3), object(5)
memory usage: 29.9+ MB

	ratings.info();

<class 'pandas.core.frame.DataFrame'>
RangeIndex: 323057 entries, 0 to 323056
Data columns (total 3 columns):
tconst           323057 non-null object
averageRating    323057 non-null float64
numVotes         323057 non-null int64
dtypes: float64(1), int64(1), object(1)
memory usage: 7.4+ MB

	persons.info();
	1. drop ones without primareyProfession
	2. drop ones without knownForTitles
	3. drop ones without birthYear

<class 'pandas.core.frame.DataFrame'>
RangeIndex: 220816 entries, 0 to 220815
Data columns (total 6 columns):
nconst               220816 non-null object
primaryName          220816 non-null object
birthYear            220816 non-null int64
deathYear            220816 non-null object
primaryProfession    212910 non-null object
knownForTitles       220816 non-null object
dtypes: int64(1), object(5)
memory usage: 10.1+ MB

	writers.info();
	1. drop ones without primareyProfession
	2. drop ones without knownForTitles
	3. drop ones without birthYear

<class 'pandas.core.frame.DataFrame'>
RangeIndex: 61171 entries, 0 to 61170
Data columns (total 1 columns):
nconst    61171 non-null object
dtypes: object(1)
memory usage: 478.0+ KB

	director.info();
	1. drop ones without primareyProfession
	2. drop ones without knownForTitles
	3. drop ones without birthYear

<class 'pandas.core.frame.DataFrame'>
RangeIndex: 46719 entries, 0 to 46718
Data columns (total 1 columns):
nconst    46719 non-null object
dtypes: object(1)
memory usage: 365.1+ KB

	actor.info();
	1. drop ones without primareyProfession
	2. drop ones without knownForTitles
	3. drop ones without birthYear

<class 'pandas.core.frame.DataFrame'>
RangeIndex: 46719 entries, 0 to 46718
Data columns (total 1 columns):
nconst    46719 non-null object
dtypes: object(1)
memory usage: 365.1+ KB

	actor_by.info();

<class 'pandas.core.frame.DataFrame'>
RangeIndex: 181994 entries, 0 to 181993
Data columns (total 2 columns):
nconst    181994 non-null object
Title     181994 non-null object
dtypes: object(2)
memory usage: 2.8+ MB

	directed_by.info();

<class 'pandas.core.frame.DataFrame'>
RangeIndex: 181994 entries, 0 to 181993
Data columns (total 2 columns):
nconst    181994 non-null object
Title     181994 non-null object
dtypes: object(2)
memory usage: 2.8+ MB

	writtent_by.info();

<class 'pandas.core.frame.DataFrame'>
RangeIndex: 231788 entries, 0 to 231787
Data columns (total 2 columns):
nconst    231788 non-null object
Title     231788 non-null object
dtypes: object(2)
memory usage: 3.5+ MB



- - - - - - - - - - - - - - - - 

genres.info()
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 28 entries, 0 to 27
Data columns (total 1 columns):
Genre    28 non-null object
dtypes: object(1)
memory usage: 304.0+ bytes


genreOf.info()
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 903153 entries, 0 to 903152
Data columns (total 2 columns):
tconst    903153 non-null object
Genre     903153 non-null object
dtypes: object(2)
memory usage: 13.8+ MB


movie.info()
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 489949 entries, 0 to 489948
Data columns (total 8 columns):
tconst            489949 non-null object
titleType         489949 non-null object
primaryTitle      489949 non-null object
originalTitle     489949 non-null object
isAdult           489949 non-null int64
startYear         489949 non-null int64
endYear           489949 non-null object
runtimeMinutes    489949 non-null int64
dtypes: int64(3), object(5)
memory usage: 29.9+ MB


rating.info()
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 323057 entries, 0 to 323056
Data columns (total 3 columns):
tconst           323057 non-null object
averageRating    323057 non-null float64
numVotes         323057 non-null int64
dtypes: float64(1), int64(1), object(1)
memory usage: 7.4+ MB


person.info()
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 220816 entries, 0 to 220815
Data columns (total 6 columns):
nconst               220816 non-null object
primaryName          220816 non-null object
birthYear            220816 non-null int64
deathYear            220816 non-null object
primaryProfession    212910 non-null object
knownForTitles       220816 non-null object
dtypes: int64(1), object(5)
memory usage: 10.1+ MB


writer.info()
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 61171 entries, 0 to 61170
Data columns (total 1 columns):
nconst    61171 non-null object
dtypes: object(1)
memory usage: 478.0+ KB


director.info()
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 46719 entries, 0 to 46718
Data columns (total 1 columns):
nconst    46719 non-null object
dtypes: object(1)
memory usage: 365.1+ KB


actor.info()
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 89919 entries, 0 to 89918
Data columns (total 1 columns):
nconst    89919 non-null object
dtypes: object(1)
memory usage: 702.6+ KB


actress.info()
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 60325 entries, 0 to 60324
Data columns (total 1 columns):
nconst    60325 non-null object
dtypes: object(1)
memory usage: 471.4+ KB


actor_by.info()
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 347574 entries, 0 to 347573
Data columns (total 2 columns):
nconst    347574 non-null object
Title     347574 non-null object
dtypes: object(2)
memory usage: 5.3+ MB


actress_by.info()
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 231644 entries, 0 to 231643
Data columns (total 2 columns):
nconst    231644 non-null object
Title     231644 non-null object
dtypes: object(2)
memory usage: 3.5+ MB


directed_by.info()
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 181994 entries, 0 to 181993
Data columns (total 2 columns):
nconst    181994 non-null object
Title     181994 non-null object
dtypes: object(2)
memory usage: 2.8+ MB


writtent_by.info()
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 231788 entries, 0 to 231787
Data columns (total 2 columns):
nconst    231788 non-null object
Title     231788 non-null object
dtypes: object(2)
memory usage: 3.5+ MB

























