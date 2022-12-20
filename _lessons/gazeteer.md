---
layout: page
title: Finding Places in Text with the World Historical Gazeteer 
description: Details how to programmatically search documents for a list of terms, including place names and then how to obtain coordinates and map historical place names with the World Historical Gazetteer. 
---
## Source
[Susan Grunewald, Andrew Janco, "Finding Places in Text with the World Historical Gazeteer," Programming Historian 7 (2022), https://doi.org/10.46430/phen0096.](https://programminghistorian.org/en/lessons/finding-places-world-historical-gazetteer)

## Reflection

Through this tutorial, I learned how to use Python to search a corpus of texts for place names from a defined list. It specifically uses German cities and towns as an example, using named entity recognition and a service that locates and maps historic place names. It also teaches how to create maps depicting historical information in a largely point and click interface. Throughout the lesson, I learned how to use the pathlib library to load a directory of texxt files, how to create a list of term matches and their locations in a text, and how to create a TSV file to upload to the World Historical Gazetteer. 

I was able to follow along with the code, but as usual, the trickiest part was getting used to all the new syntax from new, unfamiliar libraries like Counter and Matcher. While I don't think that I could do everything from memory, I could understand what was happening as I was reading the tutorial. The other challenge I faced was debugging, since sometimes I would get errors that I wasn't sure how to fix, but after spending some time on them, I realized that it was the misplacing of a file in the wrong directory or other small mistakes like that. Lastly, the last few steps with the visualization were unable to load on jupyter notebooks, so I don't have the resulting visualizations, just the code that I wrote. 

This lesson could be applied to projects that involve analyzing and visualizing data based off locations in a text. For example, if you wanted to look at texts from a book or a database, you could extract the names of locations to pinpoint general trends or historical patterns in the texts, analyzing frequency of occurence and connotations to the most frequent locations. For my final project, I'll be doing this with songs, so by looking at locations that are mentioned frequently, you can draw meaningful conclusions abotu the contents of the text. 


```python
text = "Siberia has many rivers."
for index, char in enumerate(text):
    print(index, char)
```

    0 S
    1 i
    2 b
    3 e
    4 r
    5 i
    6 a
    7  
    8 h
    9 a
    10 s
    11  
    12 m
    13 a
    14 n
    15 y
    16  
    17 r
    18 i
    19 v
    20 e
    21 r
    22 s
    23 .



```python
text = "Siberia has many rivers."
text.find("rivers")
```




    17




```python
pip install spacy
```

    Requirement already satisfied: spacy in /opt/anaconda3/lib/python3.9/site-packages (3.4.2)
    Requirement already satisfied: tqdm<5.0.0,>=4.38.0 in /opt/anaconda3/lib/python3.9/site-packages (from spacy) (4.64.0)
    Requirement already satisfied: cymem<2.1.0,>=2.0.2 in /opt/anaconda3/lib/python3.9/site-packages (from spacy) (2.0.7)
    Requirement already satisfied: jinja2 in /opt/anaconda3/lib/python3.9/site-packages (from spacy) (2.11.3)
    Requirement already satisfied: requests<3.0.0,>=2.13.0 in /opt/anaconda3/lib/python3.9/site-packages (from spacy) (2.27.1)
    Requirement already satisfied: thinc<8.2.0,>=8.1.0 in /opt/anaconda3/lib/python3.9/site-packages (from spacy) (8.1.5)
    Requirement already satisfied: setuptools in /opt/anaconda3/lib/python3.9/site-packages (from spacy) (61.2.0)
    Requirement already satisfied: pydantic!=1.8,!=1.8.1,<1.11.0,>=1.7.4 in /opt/anaconda3/lib/python3.9/site-packages (from spacy) (1.10.2)
    Requirement already satisfied: spacy-loggers<2.0.0,>=1.0.0 in /opt/anaconda3/lib/python3.9/site-packages (from spacy) (1.0.3)
    Requirement already satisfied: numpy>=1.15.0 in /opt/anaconda3/lib/python3.9/site-packages (from spacy) (1.21.5)
    Requirement already satisfied: murmurhash<1.1.0,>=0.28.0 in /opt/anaconda3/lib/python3.9/site-packages (from spacy) (1.0.9)
    Requirement already satisfied: spacy-legacy<3.1.0,>=3.0.10 in /opt/anaconda3/lib/python3.9/site-packages (from spacy) (3.0.10)
    Requirement already satisfied: typer<0.5.0,>=0.3.0 in /opt/anaconda3/lib/python3.9/site-packages (from spacy) (0.4.2)
    Requirement already satisfied: preshed<3.1.0,>=3.0.2 in /opt/anaconda3/lib/python3.9/site-packages (from spacy) (3.0.8)
    Requirement already satisfied: wasabi<1.1.0,>=0.9.1 in /opt/anaconda3/lib/python3.9/site-packages (from spacy) (0.10.1)
    Requirement already satisfied: packaging>=20.0 in /opt/anaconda3/lib/python3.9/site-packages (from spacy) (21.3)
    Requirement already satisfied: langcodes<4.0.0,>=3.2.0 in /opt/anaconda3/lib/python3.9/site-packages (from spacy) (3.3.0)
    Requirement already satisfied: catalogue<2.1.0,>=2.0.6 in /opt/anaconda3/lib/python3.9/site-packages (from spacy) (2.0.8)
    Requirement already satisfied: pathy>=0.3.5 in /opt/anaconda3/lib/python3.9/site-packages (from spacy) (0.6.2)
    Requirement already satisfied: srsly<3.0.0,>=2.4.3 in /opt/anaconda3/lib/python3.9/site-packages (from spacy) (2.4.5)
    Requirement already satisfied: pyparsing!=3.0.5,>=2.0.2 in /opt/anaconda3/lib/python3.9/site-packages (from packaging>=20.0->spacy) (3.0.4)
    Requirement already satisfied: smart-open<6.0.0,>=5.2.1 in /opt/anaconda3/lib/python3.9/site-packages (from pathy>=0.3.5->spacy) (5.2.1)
    Requirement already satisfied: typing-extensions>=4.1.0 in /opt/anaconda3/lib/python3.9/site-packages (from pydantic!=1.8,!=1.8.1,<1.11.0,>=1.7.4->spacy) (4.1.1)
    Requirement already satisfied: charset-normalizer~=2.0.0 in /opt/anaconda3/lib/python3.9/site-packages (from requests<3.0.0,>=2.13.0->spacy) (2.0.4)
    Requirement already satisfied: idna<4,>=2.5 in /opt/anaconda3/lib/python3.9/site-packages (from requests<3.0.0,>=2.13.0->spacy) (3.3)
    Requirement already satisfied: certifi>=2017.4.17 in /opt/anaconda3/lib/python3.9/site-packages (from requests<3.0.0,>=2.13.0->spacy) (2021.10.8)
    Requirement already satisfied: urllib3<1.27,>=1.21.1 in /opt/anaconda3/lib/python3.9/site-packages (from requests<3.0.0,>=2.13.0->spacy) (1.26.9)
    Requirement already satisfied: blis<0.8.0,>=0.7.8 in /opt/anaconda3/lib/python3.9/site-packages (from thinc<8.2.0,>=8.1.0->spacy) (0.7.9)
    Requirement already satisfied: confection<1.0.0,>=0.0.1 in /opt/anaconda3/lib/python3.9/site-packages (from thinc<8.2.0,>=8.1.0->spacy) (0.0.3)
    Requirement already satisfied: click<9.0.0,>=7.1.1 in /opt/anaconda3/lib/python3.9/site-packages (from typer<0.5.0,>=0.3.0->spacy) (8.0.4)
    Requirement already satisfied: MarkupSafe>=0.23 in /opt/anaconda3/lib/python3.9/site-packages (from jinja2->spacy) (2.0.1)
    Note: you may need to restart the kernel to use updated packages.



```python
from spacy.lang.de import German
```


```python
nlp = German()
doc = nlp("Berlin ist eine Stadt in Deutschland.")
for token in doc:
    print(token.i, token.text)
```

    0 Berlin
    1 ist
    2 eine
    3 Stadt
    4 in
    5 Deutschland
    6 .



```python
from pathlib import Path

gazetteer = Path("gazetteer.txt").read_text()
gazetteer = gazetteer.split("\n")
print(gazetteer)

```

    ['Armenien', 'Aserbaidshan', 'Aserbaidshen', 'Estland', 'Georgien', 'Kasachstan', 'Kirgisien', 'Lettland', 'Litauen', 'Moldawien', 'Russland', 'RSFSR', 'Kazakhstan', 'Turkmenien', 'Usbekistan', 'Ukraine', 'Weißrussland', 'Weissrussland', 'Abchasien', 'Akmola', 'Aktjubinsk', 'Alma Ata', 'Gurjew', 'Karaganda', 'Kostai', 'Ostkasachstan', 'Sudkasachstan', 'Siidkasachstan', 'DshalaLAbad', 'Frunse', 'Osch', 'Basarabeasca', 'Adygejien', 'Altai', 'Archangelsk', 'Astrachan', 'Baschkirien', 'Brjansk', 'Burjatien', 'Dagestan', 'Gorki', 'Gorkif Tschkalowsk', 'Irkutsk', 'Iwanowo', 'Jaroslawl', 'KabardinienBalkarien', 'Kalinin', 'Kaliningrad', 'Kalmykien', 'Kaluga', 'KaratschaiTscherkessien', 'Karelien', 'Kemerowo', 'Kislar', 'Kingissepp', 'Kirow', 'Komi', 'Krasnodar', 'Krasnoyarsk', 'Krim', 'Kuibyschew', 'Kurgan', 'Kursk', 'Leningrad', 'Marij El', 'Molotow', 'Mordowien', 'Moskau', 'Murmansk', 'Nordossetien', 'Nowgorod', 'Nowosibirsk', 'Omsk', 'Ordshonikidse', 'Orjol', 'Oijol', 'Pensa', 'Perm', 'Primorje', 'Pskow', 'Rjasan', 'Rostow am Don', 'Saratow', 'Smolensk', 'Stalingrad', 'Stawropol', 'Swerdlowsk', 'Tambow', 'Tatarstan', 'Tjumen', 'Tula', 'T ula', 'Udmurtien', 'Uljanowsk', 'Tscheljabinsk', 'Tscheijabinsk', 'Tscherkessien', 'TschetschenoInguschetien', 'Tschkalow', 'Tschuwaschien', 'Wladimir', 'Wologda', 'Woronesh', 'Aschchabad', 'Andishan', 'Ferga', 'Taschkent', 'Taschkentj', 'Charkow', 'Chmelnizki', 'Dnepropetrowsk', 'Dnepropetrovsk', 'Drogobytsch', 'KamenezPodolski', 'Kiew', 'Kirowograd', 'Lwow', 'Nikolajew', 'Odessa', 'Poltawa', 'Rowno', 'Saporoshje', 'Shitomir', 'Stalino', 'Stanislaw', 'Sumy', 'Su my', 'Tschernigow', 'Winniza', 'Wolynien', 'Woroschilowgrad', 'Gomel', 'Grodno', 'Minsk', 'Mogiljow', 'Pinsk', 'PoLessje', 'Polozk', 'Wilejka', 'Witebsk', 'Alawerdi', 'Arthik', 'Jerewan', 'Oktemberjan', 'Sewan', 'Talin', 'Chanlar', 'Chilly', 'Daschkesan', 'Nucha', 'Samuch', 'Stadt Baku', 'Stadt Kirowabad', 'Harjumaa', 'MorskoiStadtbezirk Tallinn', 'Paide', 'Parnu', 'Raplamaa', 'Valga', 'Otschamtschira', 'Agbulach', 'Macharadse', 'Tbilissi', 'ZaLendshicha', 'Zchaltubo', 'Wischnjowka', 'TaLdykorgan', 'Makat', 'BalchaschStadt', 'Karsakpai', 'Leninogorsk', 'Syrjanowsk', 'Lenger', 'Pachtaaral', 'Turkestan', 'TaschKumyr', 'Kemin', 'Bauska', 'Cesis', 'Jekabpils', 'Jelgava', 'Liepaja', 'Ogre', 'Riga', 'Saldus', 'Talsi', "Talsi'", 'Tukums', 'Akmene', 'Kaus', 'Siauliai', 'Vilkaviskis', 'Kischinjow', 'Vadul Lui Voda', 'BaruL', 'Sorokino', 'Troizkoje', 'Krasnoborsk', 'Oneshski', 'Plessezk', 'Primorski', 'Wolodarski', 'Belorezk', 'Birsk', 'Djatkowo', 'wlja', 'Potschep', 'Susemka', 'Trubtschewsk', 'Iwolginsk', 'PribaikalskiKreis', "Sa'igrajewo", "Sai'grajewo", 'Selenga', 'Tarbagatai', 'Buiksk', 'Balach', 'Bogorodsk', 'Bor', 'Dsershinsk', 'Linda', 'Kulebaki', 'waschino', 'Schachunja', 'Tonschajewo', 'Tschistoje', 'Uren', 'Worotynez', 'Sljudjanka', 'Gawrilow Possad', 'Jurjewez', 'Jusha', 'Kirshatsch', 'Leshnewo', 'Palech', 'Sereda', 'Tejkowo', 'Brejtowo', 'Nerechta', 'PereslawlSalesski', 'UgLitsch', 'ltschik', 'Firowo', 'Mednoje', 'Rshew', 'Sawidowo', 'Spirowo', 'Torshok', 'Wyschni Wolotschok', 'Lagan', 'Wyssokinitschi', 'MikojanKreis', 'UstDsheguta', 'Belomorsk', 'Kalewaly', 'Medweshjegorsk', 'Pitkaranta', 'Prioneshski', 'Pudosh', 'Segesha', 'Wolossowo', 'Kai', 'Kilmes', 'Werchnekamski', 'Wjatskije Poljany', 'Knjashpogost', 'UstWym', 'Beloretschensk', 'Gelendshik', 'Krasnoarmejskaja', 'Kuschtschewskaja', 'Neftegorsk', 'Pawlowskaja', 'Sewerskaja', 'Sowetskaja', 'Uspenskoje', 'Aluschta', 'Balaklawa', 'Bachtschissarai', 'Jalta', 'JaLtaStadt', 'KarassuBasar', 'Kolai', 'Krasnogwardejskoje', 'Krasnoperekopsk', 'MajakSalynski', 'Saki', 'Seitlerski', 'SewastopolStadt', 'Simferopol', 'Stary Krym', 'Sudak', 'Suja', 'MolotowKreis', 'Schigony', 'Shiguijowsk', 'GLuschkowo', 'Mikojanowka', 'Schebekino', 'Borowitschi', 'Ljubytino', 'Lodejnoje Pole', 'Malaja Wischera', 'Okulowka', 'Opetschenski', 'Pargolowo', 'Pestowo', 'Podporoshje', 'Sluzk', 'Tichwin', 'Utorgosch', 'Wolchow', 'Wsewoloshsk', 'JoschkarOla', 'Jurino', 'Kilemary', 'KiseLStadt', 'Kungur', 'MolotowStadt', 'Ochansk', 'Solikamsk', 'TschussowoiStadt', 'Subowa Polja', 'Temnikow', 'Balaschicha', 'Istra', 'Kaschira', 'Kolom', 'Krasnogorsk', 'Krasja Pachra', 'Krasja Polja', 'Kriwandino', 'Leninski', 'Moshaisk', 'Mytischtschi', 'roFominsk', 'Nowopetrowskoje', 'Osjory', 'Reutow', 'Reutov. Kutschino', 'Rusa', 'Schatura', 'Schtscholkowo', 'Solnetschnogorsk', 'StalinogorskStadt', 'Swenigorod', 'Uchtomski', 'Uwarowka', 'Wolokolamsk', 'Kirowsk', 'Kola', 'Dargkoch', 'Digora', 'AnsheroSudshensk', 'Assino', 'Gurjewsk', 'Jurga', 'Kusedejewo', 'Taiga', 'Taschtagol', 'Tjashinski', 'Apasjenkowskoje', 'Gorjatschewodski', 'Kursawka', 'Nowoalexandrowsk', 'Petrowskoje', 'Komaritschi', 'Urizki', 'Bolschoi Wjass', 'Kondolj Kondol', 'Mokschan', 'Gdow', 'Dankow', 'Kawerino', 'Lebedjan', 'Lew Tolstoi', 'Rybnoje', 'SoLotschinski', 'SpassKLepiki', 'Belaja Kalitwa', 'Matwejew Kurgan', 'NowoschachtinskStadt', 'Oktjabrski', 'Remontnoje', 'Simowniki', 'Swerjewo', 'Atkarsk', 'Kamenka', 'Krasnopartisansld', 'Krasny Kut', 'Rtischtschewo', 'Tatischtschewo', 'Woroschilowsk', 'Gshatsk', 'Isdeschkowo', 'Jarzewo', 'Krasny', 'Tumanowo', 'Balyklej', 'Frolowo', 'Gorodischtsche', 'Kotelnikowo', 'Krasja Sloboda', 'Georgijewsk', 'Isobilny', 'Suworowskaja', 'Alapajewsk', 'Aramil', 'AsbestStadt', 'AsbestĀ« Stadt', 'BerjosowskiStadt', 'Iss', 'Iwdel', 'Jegorschino', 'KirowgradStadt', 'Kirowgrad', 'Krasnoufimsk', 'Newjansk', 'Nishnjaja Saida', 'Nishnije Sergi', 'Nowaja Ljalja', 'PoLewskoi', 'Resh', 'RewdaStadt', 'Sysert', 'Tugulym', 'Werchnjaja Tura', 'Bondjushski', 'Kukmor', 'Nurlaty', 'Takanysch', 'Sawodoukowsk', 'Alexin', 'BogorodizkStadt', 'Bolochowo', 'Donskoi', 'Jepifan', 'Kimowsk', 'Laptewo', 'Mordwess', 'Schtschokino', 'Towarkowski', 'Tschern', 'TulaStadt', 'Uslowaja', 'Pudem', 'Uwa', 'Tscherdakly', 'Jetkul', 'Kussa', 'Minjar', 'Satka', "Atagi'", 'Atschaluki', 'AtschchoiMartan', 'dteretschnoje', 'Prigorodny', 'UrusMartan', 'Busuluk', 'KosLowka', 'GusChrustalny', 'Kameschkowo', 'Kurlowski', 'Sudogda', 'Wjasniki', 'Tschagoda', 'Tscherepowez', 'UstKubinski', 'Grjasi', 'JelanKolenowski', 'Dshalalkuduk', 'Isbaskan', 'Begowat', 'Tschis', 'Tschirtschik', 'IBogoduchow', 'Kegitschowka', 'Nowaja Wodolaga', 'Polonnoje', 'Baryschewka', 'Beresan', 'Christinowka', 'Jagotin', 'Alexandrowka', 'Malaja Wiska', 'Busk', 'Nowy Bug', 'Gaiworon', 'Gruschka', 'Globino', 'Lochwiza', 'Genitschesk', 'Michajlowka', 'Berditschew', 'PopoLnja', 'Charzyssk', 'GorLowkaStadt', 'Krasnoarmejsk', 'MakejewkaStadt', 'Selidowo', 'Jampot', 'Nedrigaitow', 'Utjanowka', 'Neshin', 'PriLuki', 'Litin', 'Turbow', 'Tywrow', 'Perwomaisk Stadt', 'Krasny Lutsch Stadt', 'Uwarowitschi', 'WoLkowysk', 'Puchowitschi', 'Saslawl', 'Beresino', 'Bobruisk', 'Ganzewitschi', 'Orscha', 'Sirotino', 'Ejlar', 'Armlu', 'Ararat', 'Etschmiadsin', 'Molotja', 'Kirowakan', 'Werchni Talin', 'Tumanjan', 'Alabaschly', 'Bajan', 'Baku', 'Kugitschu', 'Nishni Daschkesan', 'Werchni Daschkesan', 'Karadag', 'Kirowobad', 'Kirowabad', 'Kysyldsha', 'Kyrychly', 'Mingetschewir', 'Quba', 'Sabuntschi', 'Saljan', 'Schemacha', 'Sych', 'Adshikent', 'Sumgait', 'Ahtme', 'Loksa', 'Johvi', 'Kivioli', 'KohtlaJarve', 'Kuttejou', 'Lehtse', 'Maardu', 'Narva', 'JarvaJaani', 'Lavassaare', 'Rakvere', 'Jarvakandi', 'Sonda', 'Tallinn', 'Tammiku', 'Tapa', 'Tartu', 'Ulila', 'Loosi', 'Nudrezowo', 'Podra', 'Kingu', 'Vasalemma', 'Vontkula', 'Suchumi', 'Kelasuri', 'Miussera', 'Tkwartscheli', 'Manglissi', 'Awtschala', 'Bachmaro', 'Bergwerkssiedlung Nr. 2', 'Bolnissi', 'Bulutschauri', 'ChezerTeesowchos', 'ChramiWasser kraftwerkssiedlung', 'Dsegwi', 'Dwiri', 'Ingiri', 'Kluchori', 'Ksani', 'KutaĆÆssi', 'KutaTssi', 'Kutaiā€™ssi', 'Kutaissi', 'Kwareli', 'Sairme', 'Mukusani', 'wtLugi', 'Poti', 'Rustawi', 'Samgori', 'Sugdidi', 'Supsa', 'Barmaksis', 'Teegenossenschaft Didatschkon', 'Teegenossenschaft raseni', 'Tk', 'Tschaladidi', 'Tschubrin', 'Ureki', 'Wedjanka', 'Zulukidse', 'Atbassar', 'Jessil', 'Koluton', 'Ko Luton', 'Makinka', 'TekeLi', 'Baischoss', 'DshambuL', 'Agadyr', 'Ar', 'Kounradski', 'Bergwerksiedlung 2626 BIS', 'Bergwerksiedlung 4243', 'KaragandaSortirowotschja', 'Dsheskasgan', 'Kokusek', 'MaiKuduk', 'Nurinskaja', 'Saran', 'SpasskiWerkssiedlung', 'Temirtau', 'Dshetygara', 'Kuschmurun', 'Kysylorda', 'Irtyschgesstroi', 'Beloussowka', 'Jerofejewka', 'Syrjanowskoje', 'UstKamenogorsk', 'Syrdarjinskaja', 'Tschimkent', 'Atschissaj', 'Kantagi', 'KjokDshangak', 'DsheLAryk', 'KisKyja', 'Bystrowka', 'Maimak', 'KysylKyja', 'Suljukta', 'Auce', 'Iecava', 'LIgatne', 'Daugavpils', 'Dzukste', 'Eglaine', 'Jaunjelgava', 'Krustpils', 'Garoza', 'Misa', 'Turmali', 'Jugla', 'Kraslava', 'Kuldiga', 'Pavilosta', 'Satinskoje', 'LTgatne', 'Murjani', 'Kegums', 'Olaine', 'Priedaine', 'Purmsati', 'Rampa', 'Rezekne', 'Balozi', 'Salaspils', 'Stopini', 'Broceni', 'Sarkandaugava', 'Skulte', 'Sloka', 'Suntazi', 'Stende', 'Taurupe', 'T ukums', 'Valmiera', 'Ventspils', 'Bicionys', 'Gaideliai', 'Kaisiadorys', 'Ezerelis', 'Raudelino', 'Samaniai', 'Klaipeda', 'Kretinga', 'Mauruciai', 'ujoji Vilnia', 'Palemos', 'RadviLiskis', 'Taurage', 'Telsiai', 'Kybartai', 'Vilnius', 'Abaklia', 'Balti', 'Tiraspol', 'Orhei', 'Ungheni', 'Maikop', 'Tschesnokowka', 'Bisk', 'Blinowo', 'Rubzowsk', 'Newerowskaja', 'Sarinskaja', 'Schpagino', 'Smasnewo', 'Borowljanka', 'Jemza', 'Jerzewo', 'Jura', 'Kargopol', 'Kisema', 'Kostyljowo', 'Kotlas', 'Ustjewo', 'Molotowsk', 'Moschnoje', 'Njandoma', 'Oboserski', 'wolok', 'Podjuga', 'Solsa', 'Schalakuscha', 'Tschekamino', 'Welsk', 'Kapustin Jar', 'Nikolskoje', 'Perwomaiski', 'Tumanny', 'Werchni Baskuntschak', 'Wladimirowka', 'Wolodarowka', 'Beljagusch', 'Inser', 'Nukatowo', 'Sorwicha', 'Karlaman', 'Manjawa', 'Tschernikowka', 'Tschernikowsk', 'Ufa', 'Besymjanka', 'Bijansk', 'Brjansk1', 'Brjansl<2', 'Brjansk2', 'Bytosch', 'Iwot', 'Star', 'Zementny', 'Karatschew', 'Kletnja', 'KLinzy', 'Altuchowo', 'Nowosybkow', 'Ordshonikidsegrad', 'Palushje', 'Pogreby', 'Ramassucha', 'Selzo', 'Kokorewka', 'Belaja Berjoska', 'Unetscha', 'Wygonitschi', 'Dshida', 'Gorchon', 'Gorodok', 'Sawodskoi', 'JushlagSiedlung', 'Nowoiljinsk', 'Onochoi', 'Pedshino', 'Turka', 'Sagustai', 'Surgalej', 'Schabur', 'Werchnije Talzy', 'Saudinski', 'Gussinoje Osero', 'Oronchoj', 'Selenduma', 'Suchaja Padj', 'UlanUde', 'Werchnjaja Mojsa', 'Chabarowsk', 'Karamachi', 'Derbent', 'Gedshuch', 'Isberbasch', 'Machatschkala', 'Mamedkala', 'Rubas', 'Arja', 'Awarijny', 'Prawdinsk', 'Oranki', 'Kershenez', 'Orlowo', 'Bystrucha', 'Pyra', 'Gluchaja', 'Igumnowo', 'Kiselicha', 'Kolchosny', 'Korelka', 'Krasnenki', 'Manturowo', 'Mochowye gory', 'Mostyrka', 'Mursizy', 'Tjoscha', 'Obchod', 'Sjawa', 'Scharja', 'Schemanicha', 'Sejma', 'Serebrjanka', 'Suchobeswodnoje', 'Tschornoje', 'Usta', 'Michailowski', 'Uwarowskaja', 'Rasneshje', 'Wyksa', 'Baischoss NOTE: Error in book. Makat is in Kazakhstan', 'Sagis. NOTE: Error in book. Makat is in Kazakhstan. Book said RSFSR', 'Siedlung des Werks Nr. 39', 'Strecke IrkutskSljudjanka', 'Strecke PosolskUlanUde', 'Strecke SljudjankaWydrino', 'Listwjanka', 'Strecke WydrinoPosolsk', 'Taischet', 'Demidowo', 'Furmanow', 'Iwankowo', 'Michailowo', 'Mugrejewo', 'Talizy', 'Kineschma', 'Kochma', 'Komsomolsk', 'Kowrow', 'Petrowski', 'Rodniki', 'Schuja', 'Jakowlewskoje', 'Siedlung des SchalowZiegelwerkes', 'Textilny', 'Witschuga', 'Iwkino', 'Chmelniki', 'Gawrilow Jam', 'Jakschanga', 'Kostroma', 'Lorn', 'Neja', 'Kosmynino', 'Perebory', 'Pereslawl', 'Rogosinino', 'Ussolje', 'Petrowsk', 'PriwoLshje', 'Rodionowo', 'Rybinsk', 'Schestichino', 'Schtschelkanskoje Torfopredprijatije', 'Semibratowo', 'Silnizy', 'Suprotiwny', 'Tichmenewo', 'Tutajew', 'Tschernizyno', 'WauLowo', 'Wspolje', 'AksautGretscheski', 'Kenshe', 'Akademitscheskaja', 'Beshezk', 'Bologoje', 'Emmaus', 'Wassiljewski Moch', 'Kimry', 'Kokowo', 'Kuwschinowo', 'Leontjewo', 'Maksaticha', 'Malyschewo', 'rotschino', 'Nelidowo', 'Nowossokolniki', 'Ossetschenka', 'Ostaschkow', 'Poddubki', 'Ranzewo', 'Redkino', 'Konyschewo', 'Olenino', 'Selisharowo', 'Semzy', 'Wydropushsk', 'Staraja Toropa', 'Dmitrowskoje', 'Dumanowo', 'Tschernogubowo', 'Tschorny Dor', 'Udomlja', 'Welikije Luki', 'Krasnomaiski', 'Konigsberg', 'Bagration owsk', 'Gut Romitten', 'Gwardejsk', 'Insterburg', 'Kaukiemis', 'Metgethen', 'Pillau', 'Preu&ischEylau', 'Ragnit', 'Seckenburg', 'Tilsit', 'Trammen', 'Tschernjachowsk', 'Wehlau', 'UlanChol', 'Kanukowo', 'Fajansowaja', 'Kusmitschi', 'Ljudinowo', 'Malojaroslawez', 'Suchinitschi', 'DurowSowchos', 'Chumara', 'Tscherkessk', 'Washnoje', 'Malenga', 'Letneretschenski', 'Saliwy', 'Tegosero', 'Iljinskaja', 'Kepa', 'Kondopoga', 'Medweshja Gora', 'arlahti', 'Pai', 'Petrosawodsk', 'Harlu', 'Laskela', 'Suojarvi', 'Pjashijewa Selga', 'Derewjanka', 'Botschilowo', 'Kolowo', 'Kubowskaja', 'NowoStekljannoje', 'Pjalma', 'Porschta', 'Schala', 'Schalski', 'Tschernoretschenski', 'Petrowski Jam', 'Polga', 'Uchta', 'Uuksu', 'Jurga1', 'Prokopjewsk', 'Stalinsk', 'Kikerino', 'Ardaschi', 'Besboshnik', 'Fosforitja', 'Ima', 'Werchnekamskaja', 'Latyschski', 'Loiga', 'Ljangassowo', 'Omutninsk', 'Posdino', 'Slobodskoi', 'Sosnowka', 'Stalja', 'Suslowka', 'Sosimski', "N. BeLoi'rka", 'WoshajeL', 'Lemju', 'Sewsheldorlag', 'Syktywkar', 'Sheschart', 'Adler', 'Apa', 'Apscheronsk', 'Armawir', 'Chadyshensk', 'Dshugba', 'Gluchari', 'Jurjewka', 'Mogilnoje', 'Kropotkin', 'Krymsk', 'Mogilny', 'Abchasskaja', 'Chadyshenskaa', 'Noworossisk', 'Ilski', 'Sotschi', 'Tichorezk', 'Tuapse', 'BogotoL', 'Sowchos Kastel', 'Belbek', "Tai'r", 'Dshankoi', 'Feodossija', 'Inkerman', 'AiWa nil', 'Alupka', 'Foros', "Korei's", 'Liwadija', 'Oreanda', 'Partenit', 'Jewpatorija', 'Mariano', 'Kertsch', 'Sowchos Bolschewik', 'Bagerowo', 'BuLgak', 'Eschkine', 'Sowchos Tschoschty', 'Tamak', 'Sewastopol', 'Sevastopol', 'Katscha', 'Sowchos KaraKijat', 'Sirenj', 'Siwasch', 'Sowchos AiDani', 'Sowchos Krasny', 'Koktebel', 'Sowchos 1. Fiinfjahrplan', 'Otusy', 'Sowchos Krymskaja Rosa', "Ta'ir", 'Bachilowa Polja', 'Batraki', 'Jablonowy Owrag', 'Jablonewy Owrag', 'Kadej', 'Kinel', 'Krjash', 'Melekess', 'Otwashnoje', 'Nikolajewka', 'Pochwistnewo', 'Sabdowka', 'Petscherskoje', 'Solnoje', 'Solonez', 'Sysran', 'Schadrinsk', 'Belgorod', 'Blagodatenski', 'Derjugino', 'Fatesh', 'Tjotkino', 'Gotnja', 'ShurawLjowka', 'Obojanj', 'Ryschkowo', 'NowoTawoLshanka', 'Tros', 'Waluiki', 'Besborodowo', 'Boksitogorsk', 'Jegla', 'Schibotowo', 'Ustje', 'Chotzy', 'Dibuny', 'Ishora', 'Jedrowo', 'Johannes', 'Kakisalmi', 'Kaskowo', 'Koli', 'Kolpino', 'Kowanko', 'Krasja Mysa', 'Krasnoje Selo', 'Krestzy', 'Kronstadt', 'LadogaSee', 'Ljalizy', 'Komarowo', 'Swirstroi', 'Luga', 'Lungatschi', 'Bolschoje Saborowje', 'Mga', 'Neboltschi', 'ParachinoPoddubje', 'Opetschenski Posad', 'Pesotschny', 'Petrodworez', 'PikaLjowo', 'Washiny', 'Pontonja', 'Puschkin', 'Rautu', 'Rogawka', 'Rudnitschja', 'Sestrorezk', 'Shichaijowo', 'Shicharjowo', 'Antropschino', 'UstIshora', 'Spasskaja Polistj', 'Staraja Russa', 'Stroganowo', 'Swir', 'Taizy', 'Terebutenez', 'Terioki', 'Tosno', 'Tschudowo', 'Turgosch', 'Uglowka', 'Waldaj', 'Sjasstroj', 'Wolchowstroi', 'Wolchowstroi2', 'MorosowSiedlung', 'Rachja', 'Golowino', 'SusLonger', 'Kosmodemjansk', 'Wolshsk', 'Baskaja', 'Beresniki', 'Gremjatschinski', 'Kisel', 'Gubacha', 'Jushny Kospaschski', 'Polowinka', 'Sewerny Kospaschski', 'Uswa', 'WsewolodoWilwa', 'Krasnokamsk', 'Kurja', 'Lyswa', 'Lewschino', 'Obogatitel', 'Obogatitelja', 'JugoKamski', 'Owerjata', 'Ponysch', 'Borowsk', 'Kalijez', 'Tscherdyn', 'Tschussowskaja', 'Paschia', 'Tjoplaja Gora', 'UrizkiBergwerke', 'Potma', 'Saransk', 'Sweshenkaja', 'Baratjewo', 'Akinschino', 'Aprelewka', 'Baranowo', 'Barmino', 'Bogorodskoje', 'Bronnizy', 'Butowo', 'Chimki', 'Chlebnikowo', 'Cholschtschewiki', 'Chotkowo', 'Chowrino', 'Chrapunowo', 'Dmitrow', 'Dolgoprudny', 'Dorochowo', 'Dres', 'Dulewo', 'Elektrostal', 'Fill', 'Golizyno', 'Golutwin', 'Gubanowo', 'Gutschkowo', 'Nowojerusalimskaja', 'Iwantejewka', 'Jegorjewsk', 'KaganowitschWerke', 'Osherelje', 'Katuar', 'Kisseljowo', 'Klin', 'Schtschurowo', 'Kolotsch', 'Koptjewo', 'Kossino', 'Iljinskoje', 'Pawschino', 'Tuschino', 'GosplanLandsiedlung', 'Lunjowo', 'Krasny Stroitel', 'Krjukowo', 'Lebsino', 'Tscherjomuschki', 'Lianosowo', 'Ljuberzy', 'Ljublino', 'Lobnja', 'Lopasnja', 'Luchowizy', 'Jurlowo', 'Obljanischtschewo', 'Schalikowo', 'Moskworezkaja', 'Mosshinka', 'Textilschtschik', 'Noginsk', 'Nowogorsk', 'OrechowoSujewo', 'Ostankino', 'Otdych', 'Otschakowo', 'Perowo', 'Planerja', 'Podlipki', 'Podolsk', 'PokrowskojeStreschnjewo', 'PtscheLowodnoje', 'Puschkino', 'Kutschino', 'Reutowo', 'Reschetnikowo', 'Rumjanzewo', 'Tutschkowo', 'Saraisk', 'Sasonowo', 'Frjasino', 'Semjonowskoje', 'Serebijany Bor', 'Serpuchow', 'Silikatja', 'Snegiri', 'Sorewnowanie', 'Sofrino', 'Rshawka', 'Kijukowo', 'Bergwerkssiedlung 28', 'Stroika', 'Stupino', 'Tomilino', 'Tscherkisowo', 'Tscherusti', 'Tschuchlinka', 'Kraskowo', 'Lytkarino', 'Ugreschskaja', 'Gorbuny', 'Kisseljowka', 'Poretschje', 'Werbilki', 'Wolololamsk', 'Woskressensk', 'Wyssokowsk', 'Kandalakscha', 'Saschejek', 'Kildinstroi', 'Murmaschi', 'Ku', 'Montschegorsk', 'Nikel', 'Olenja', 'Padun', 'Pautscha', 'Werchnjaja Simba', 'Nekrylowo', 'Beslan', 'Kardshin', 'Ursdon', 'Dsaudshikau', 'Krasnowodsk', 'Sadon', 'Wosnessensk', 'Perniza', 'Novosibirsk', 'Abagurowski', 'Alambai', 'Jaja', 'Ansherskaja', 'Artyschta', 'Barabinsk', 'Belowo', 'Bergwerke Jushja', "Salai'r", 'Inskoi', 'Kisseljowsk', 'Kriwoschtschokowo', 'Schuschtalep', 'LeninskKusnezki', 'Myski', 'Nowokusnezk', 'Berdsk', 'Ossinnilci', 'Ossinniki', 'Jaschkino', 'Tatarsk', 'Tjashin', 'Tschulym', 'Ussjaty', 'Issilkul', 'Kulomsino', 'Diwnoje', 'Mineralnyje Wody', 'Newinnomyssk', 'NowoALexandrowka', 'Pjatigorsk', 'Prijutnoje', 'Belyje Berega', 'Fokino', 'Jelez', 'Oelez', 'Mzensk', 'Pogar', 'Polushje', 'Assejewskaja', 'Bednodemjanowsk', 'Tschaadajewka', 'Kusnezk', 'Nikolajewski chutor', 'Nishni Lomow', 'Seliksa', 'Simanschtschino', 'Wertuhowka', 'Jar', 'Bauobjekt 500', 'Slanzy', 'Nowosselje', 'Pljussa', 'Toroschino', 'Tschorskaja', 'Birlcino', 'Chruschtschowo', 'Sowchos Kuibyschew', 'Djagilewo', 'Grotowski', 'Iswest', 'Jambirino', 'Kurscha', 'Sowchos 15 Jahre Oktober', 'Sowchos Agronom', 'Sowchos Gorki', 'sarowka', 'Pronja', 'Kanischtschewskije Wysselki', 'Kriuscha', 'KanischtschewsIcije WysseLki', 'Murmino', 'Wyschgorod', 'Wyssokoje', 'Roshdestwenskoje', 'Roshdestwo', 'Schazk', 'StaroshiLowo', 'Zementja', 'Artjom', 'Bataisk', 'Bogdanowka', 'Bergwerkssiedlung SapadnoKapitalja', 'Bergwerkssiedlung ā€˛0GPU"', 'Gukowo', 'Gundorowski', 'Krasny Sulin', 'Nowikowka', 'RawnopoL', 'deshda', 'Mi ch aj Lo Leo n tj ewskaj a', 'Mich aj Lo Leo n tj e ws kaj a', 'Mi c h aj Lo Le o n tj e ws kaj a', 'MichajLoLeontjewskaja', 'chitschewanDonskaja', 'Nowotscherkassk', 'Nowoschachtinsk', 'MolotowSiedlung', 'Kamenolomni', 'Salsk', 'Schachtja', 'Schachty', 'Sinjawskaja', 'Taganrog', 'Tazinski', 'Arkadak', 'Podgorenka', 'Strecke Atkarsk...', 'Bagajewwka', 'Bagajewka', 'Balakowo', 'Chwalynsk', 'Engels', 'Grimm', 'Jekaterinowka', 'Jelschanka', 'Kologriwowka', 'Gorny', 'Kurdjum', 'Marx', 'Pudowkino', 'Pugatschow', 'Tamala', 'Toptulino', 'Trofimowski', 'Wertunowka', 'Wolsk', 'Dorogobush', 'Durowo', 'Gussino', 'Kolesniki', 'Kolesniki Swischtschewo', 'Kondrowo', 'Kuprino', 'Nikitinka', 'Pjatowskaja', 'Polotnjany Sawod', 'Priselskaja', 'Roslawl', 'Saretschje', 'Semlewo', 'Wjasma', 'Artscheda', 'Gorny Balyklej', 'Beketowka', 'Beketowskaja', 'Dubowka', 'Ilowlja', 'Kamyschin', 'Keller', 'Kotelnikowski', 'Sadowaja', 'Sarepta', 'Staraja Otrada', 'Urjupinsk', 'Wesjolaja Balka', 'Georgijewsk.', 'Neslobja', 'Jessentuki', 'Kislowodsk', 'Kumarinskie Schachty', 'Skatschki', 'Adui', 'Werchnjaja Sinjatschicha', 'Bobrowka', 'Mostyr', 'Altyi', 'Apparatja', 'Asanka', 'Asbest', 'Isumrud', 'Bashenowo', 'Belyje Baraki', 'Beresit', 'Berjosowski', 'Lossiny', 'Bogoslowsk', 'Chabartschicha', 'ChmyLowka', 'Chrompik', 'Chudjakowo', 'Degtjarsk', 'GLucharny', 'GorobLagodatskaja', 'Irbit', 'Kytlym', 'Isset', 'Istok', 'Iwdel2', 'Artjomowski', 'Krasnogwardejski', 'Jeshewaja', 'KamenskUralski', 'Kamyschlow', 'Karpinsk', 'Lewicha', 'Kolzowo', 'Kossulino', 'Kourowka', 'Krasnoturjinsk', 'Krasnotuijinsk', 'Koschai', 'Krasnouralsk', 'Krasny Alut', 'Krasny Jar', 'Krasny Shelesnjak', 'Maly Istok', 'Maramsino', 'Medja Schachta', 'Molwa', 'Monetny', 'Moroskowo', 'Mramorskaja', 'Mugai', 'deshdinsk', 'NejwoSchaitanski', 'WerchNejwinski', 'Basjanowski', 'Werchnije Sergi', 'Nishni Issetsk', 'Nishni Istok', 'Nishni Tagil', 'Nishnjaja Tura', 'Lobwa', 'Perschino', 'PerwouraLsk', 'PodwoLoschja', 'PokLjowskaja', 'Sewerski', 'Rasjesd 173', 'Rewda', 'Degtjarka', 'Sadanije', 'Samozwet', 'Schabrowski', 'Schaitan', 'Schartasch', 'Schuwakisch', 'Seredowi', 'Serow', 'Sewerouralsk', 'Sinjatschicha', 'Soswa', 'SredneuraLsk', 'Suchoi Log', 'BoLschoi Istok', 'TaLy Kljutsch', 'Tawda', 'TjopLy Kljutsch', 'Tschorja Retschka', 'Jertarski', 'Turin sk', 'Turinsk', 'Turinskie rudniki', 'Uktus', 'Urai', 'Werchnjaja Pyschma', 'Werchnjaja Saida', 'Otradnowo', 'Werchoturje', 'Wessjolowka', 'Woltschansk', 'Chobotowo', 'Inshawino', 'Kirsanow', 'Mitschurinsk', 'Morschansk', 'Oboro', 'Rada', 'Sampur', 'Wjashli', 'Kokschan', 'Bugulma', 'Buinsk', 'Jelabuga', 'Kamskoje Ustje', 'Kasan', 'Lubjany', 'Schemordan', 'SelenodoLsk', 'Tschistopol', 'Jalutorowsk', 'Lebedewka', 'WinsiLi', 'Myschega', 'BobrikDonskoi', 'Begitschewski', 'Suchodolski', 'Chomjakowo', 'Dedilowo', 'Sadonje', 'Smorodinka', 'Gorbatschowo', 'Granki', 'Jasja Polja', 'Wladimirskoje', 'Kasanowka', 'Lwowo', 'Maklez', 'Majenki', 'Obidimo', 'Obolenskoje', 'Plawsk', 'Polunino', 'Prisady', 'Sbrodowo', 'Schepeljowo', 'Ogarjowka', 'Serebrjanyje Prudy', 'Shdanka', 'Stalinogorsk', 'Tarusskaja', 'Towarkowo', 'Kossaja Gora', 'Bergwerkssiedlung Nr. 5', 'Torbejewka', 'Wenjow', 'Glasow', 'Ishewsk', 'Lynga', 'NjurdorKotja', 'Perwomaisk', 'Rjabowo', 'Wischur', 'Kondakowka', 'Poliwanowo', 'Taschla', 'Ai', 'Ascha', 'Bischkil', 'JemansheLinka', 'Korkino', 'Kamensk', 'Kamyschinka', 'Karabasch', 'Kartaly', 'Kopejsk', 'Kropatschowo', 'Magnitka', 'Kyschtym', 'Magnitogorsk', 'Mauk', 'Miass', 'Rosa', 'BakaL', 'Sawodskaja', 'Slatoust', 'Tajandy', 'Ufalej', 'Urshumka', 'Wawilowo', 'TschetschenAul', 'Samaschki', 'Gora Gorskaja', 'Grosny', 'AliJurt', 'sran', 'Basorkino', 'Scholkowskaja', 'TangiTschu', 'Tschita', 'Buguruslan', 'Koltubanka', 'Nowotroizk', 'Nowotroizki Maksai', 'Orsk', 'SoLILezk', 'ALatyr', 'Kasch', 'TjurLema', 'SawoLshskoje Torfopredprijatije', 'Tscheboksary', 'Butylizy', 'Anopino', 'Krasnoje Echo', 'Chrapowizkaja 1', 'Chrapowizkaja 2', 'Karabanowo', 'Koltschugino', 'Komissarowka', 'Iljitschowo', 'Melenki', 'Sarja', 'Sobinka', 'Andrejewo', 'Susdal', 'Tschulkowo', 'Undol', 'Mstjora', 'Woschod', 'Wtorowo', "Buschui'cha", 'Charowskaja', 'Dedowo Pole', 'Grjasowez', 'Jadricha', 'Jawenga', 'Kadnikow', 'Kirillow', 'Lesha', 'Petschatkino', 'Scheks', 'Schelomowo', 'Semigorodnjaja', 'Sokol', 'Suda', 'Ustjush', 'Wolonga', 'Woshega', 'Borissoglebsk', 'Chrenowaja', 'Ertil', 'Grafskaja', 'Gribanowka', 'Lipezk', 'Liski', 'Poworino', 'Rossosch', 'Usman', 'Tedshen', 'Jushny Alamyschik', 'Tschuama', 'Kokand', 'Skobelewo', 'Taschkent Tientjaksai', 'Achangaran', 'Angren', 'Angrenschachtstroi', 'Farchad', 'Jangijul', 'Gwardejski', 'Schirin', 'Charkow Ukraine', 'Anjewo', 'Perwuchino', 'Isjum', 'Krasnograd', 'Kupjansk', 'Ljubotin', 'Merefa', 'Nowaja Bawarija', 'Osnowa', 'Panjutino', 'Parchomowka', 'Pokotilowka', 'Rogan', 'Sokolniki', 'Tschugujew', 'Kriwin', 'Poninka', 'Schepetowka', 'Slawuta', 'Baglej', 'Baustelle des SamaraBergwerkes', 'Dneprodsershinsk', 'Dolginzewo', 'Kanderopol', 'Kriwoi Rog', 'Marganez', 'Nikopol', 'Nishnedneprowsk', 'Nowomoskowsk', 'Pereschtschepino', 'Prossjaja', 'Raduschja', 'Tschertomlyk', 'Tscherwonoje', 'Borislaw', 'Chodorow', 'Gelsendorf', 'Morschin', 'Shidatschow', 'Skole', 'Stryj', 'Tschernowizy', 'Belaja Zerkow', 'Borispol', 'Browary', 'Werchnjatschka', 'Darniza', 'Fastow', 'Sgurowka', 'Panfily', 'Schewtschenkowo', 'Schpola', 'Smela', 'Talnoje', 'Tscherkassy', 'Uman', 'Alexandria', 'Alexandrija', 'Kapitanowka', 'Wiska', 'Pantajewka', 'Sacharja', 'Scharowka', 'Schestakowka', 'Negrebki', 'Peremyschljany', 'Rudno', 'Salush', 'Sknilow', 'Skoschlow', 'SoLotschew', 'Berislaw', 'Cherson', 'Jurizino', 'Kopani', 'Partisany', 'SaLkowo', 'SokoLogornoje', 'Ternowka', 'Tschitschkarowka', 'NowoBorissow', 'Ismail', 'Kotowsk', 'Reni', 'Pestschanka', 'Abasowka', 'Chorol', 'Grebjonka', 'Oagotin', 'dagotin', 'Karlowka', 'Kononowka', 'Kotschubejewka', 'Krementschug', 'StaLinZuckerwerk', 'Lubny', 'Mechedowka', 'Pirjatin', 'Romodan', 'Skorochodowo', 'Wesjoly Podol', 'Sarny', 'Sdolbunow', 'Balabi no', 'Bolschoi Tokmak', 'Bolschoi Utljug', 'Georgijewski', 'Grigorjewka', 'Nowoalexejewka', 'Rosowka', 'Matwejewski', 'Melitopol', 'PetroMichajlowka', 'Mokraja', 'Nowogrigorjewka', 'Rodionowka', 'Terpenije', 'Belokorowitschi', 'Lyssaja Gora', 'Skomorochi', 'Chajtschnorin', 'Igtopol', 'Igtpot', 'Jemetjanowka', 'Korosten', 'Kriwoje', 'Matin', 'NowogradWolynski', 'Penisewitschi', 'Kornin', 'Radomyschl', 'Weledniki', 'Artjoma', 'Artjomowsk', 'Bairak', 'Chanshonkowo', 'Sujewka', 'Cholodja Balka', 'Debalzewo', 'Dobropolje', 'Dronowo', 'Drushkowka', 'FenoLja', 'GorLowka', 'Kondratjewski', 'Grechow', 'Jama', 'Jassinowka', 'Jekijewo', 'Kalmius', 'Katyk', 'Konstantinowka', 'Kramatorsk', 'Nowoekonomitscheskoje', 'Krasnoarmejskoe', 'Krasnogorowka', 'Kurachowka', 'Lutugino', 'Magdalinowka', 'Makejewka', 'Pantelejmonowka', 'Mospino', 'Motschalino', 'Motschalinski', 'Muschketowo', 'Nikitowka', 'Nowy Donbass', 'Orlowa Sloboda', 'Petrowka', 'Postnikowo', 'Roja', 'Rutschenkowo', 'Bergwerkssiedlung 12', 'Bergwerkssiedlung 31', 'Bergwerkssiedlung 56', 'Bergwerkssiedlung 78 BIS', 'Bergwerkssiedlung Dsershinka', 'Bergwerkssiedlung imeni Leni', 'Bergwerkssiedlung Kisseljow', 'Schtscheglowka', 'Shdanow', 'Skossyrskaja', 'Slawjansk', 'Smoljanka', 'Sol', 'Studgorodok', 'TroizkoCharzyssk', 'Trudowaja', 'Tschassow Jar', 'Tschistjakowo', 'Tschumakowo', 'Woskressenskaja', 'Zukuricha', 'Kolomyja', 'Lawotschnoje', 'Achtyrka', 'Gluchow', 'Konotop', 'Nepljujewo', 'Terny', 'Neptjujewo', 'PrawdinskiZuckerfabrik', 'Putiwt', 'Toropitowka', 'Torochtjany', 'Ternopot', 'Bobrowizy', 'T schernigow', 'Linowizy', 'Ladan', 'Perelowka', 'Safonowo Guta', 'SafonowoGuta', 'Semjonowka', 'Sorokatitschi', 'Tolsty Les', 'Wiltscha', 'Tschernjowka', 'Tschernowzy', 'GLuchowzy', 'Kasatin', 'Shmerinka', 'Gniwan', 'Manewitschi', 'Almasja', 'Altschewsk', 'Awdakowo', 'Bergwerk 2', 'Darjewka', 'Djakowo', 'Dolshanskaja', 'Golubowka', 'Gorskoje', 'Irmino', 'Iswarino', 'Kadijewka', 'Kamyschewacha', 'Karakas', 'KrasnopoLje', 'Krasny Lutsch', 'Krindatschowka', 'KrupskajaBergwerk', 'Lissitschansk', 'Kriworoshje', 'Manuilowka', 'Ovvragi', 'Parishskaja Kommu', 'Perejesdja', 'Popasja', 'Rowenki', 'Rubeshnoje', 'Schtschotowo', 'Schterowka', 'Sentjanowka', 'Sifonja', 'Simogorje', 'Waljanowski', 'Werchneje', 'Wiljanowo', 'Wolodarsk', 'ZentralnoBokowskoi', 'Chojniki', 'Dobrusch', 'Jelsk', 'Kostjukowka', 'Nowobelizkaja', 'Retschiza', 'Rogatschow', 'Shlobin', 'Sjabrowka', 'Usa', 'Wassilewitschi', 'Lida', 'Mosty', 'SLonim', 'PawLinowo', 'Ross', 'Borissow', 'Fanipol', 'Kolodischtschi', 'Krasnoje Smja', 'Maiji Gorka', 'Sedtscha', 'Shodino', 'SmoLewitschi', 'TaLka', 'Uretschje', 'Gluscha', 'Brosha', 'Bychow', 'Grodsjanka', 'Jasen', 'Kershenka', 'Kopzewitschi', 'Kritschew', 'Ossipowitschi', 'Mosyr', 'Barawucha', 'Tatarka', 'Schklow', 'Timkowitschi', 'Molodetschno', 'Oschmjany', 'Chljustino', 'Krasja', 'Obol', 'Osinowka', 'Ossipowka', 'Borkowitschi', 'Kriste', 'Tolotschin', 'Tschaschniki', 'Ulga', 'Koschtschu', 'Bernjaschen', 'Armenikend', 'Konju', 'Kukruse', 'Ereda', 'Aseri', 'Ellamaa', 'Jeschera', 'Agudseri', 'Gori', 'Borshomi', 'Inguri', 'SaganLugi', 'Sandary', 'MolotowStadtbezirk', 'Didube', 'wtlugi1 ā€¢', 'wibuli', 'Dshalombet', 'Giiterbahnhof', 'Ridder', 'Saschtschita', 'Kflkas', 'Sesava', 'Kalgi', 'Bukas', 'Spopane', 'Rembazkoje', 'Petrasiui', 'Seredzius', 'Lustberg', 'Airiogola', 'Klemiske', 'MaimaksanskiStadtbezirk', 'P ro leta rs ki Sta dtbezi rk', 'Stadtteil Beshiza', 'I wot', 'Kokino', 'Sakamensk', 'Nishnjaja Arakorka', 'Onochoj', 'AwtosawodskiStadtbezirk', 'SormowoStadtbezirk', 'SchumLewaja', 'Sejm a', 'Tschernoramenka', 'Gorschenino', 'not RSFSR as book says', 'Chlebowo', 'Krasny Orjol', 'Berendejewo', 'Karasch', 'Gusjatino', 'Migalewo', 'Grinino', 'Smoschje', 'Gontscharowo', 'Kotarowo', 'Tapiau', 'Jasnoje', 'Prochladja', 'Baltisk', 'Bagrationowsk', 'Neman', 'Sowetsk', 'Tramischen', 'Smensk', 'Sjassosero', 'Kappesalka', 'Kutichosskaja', 'Solomennoje', 'Kukowka', 'Witschka', 'Bessow Nos', 'Wolosniza', 'Pschada', 'Jejsk', 'Turgenewka', 'Subtschaninowka', 'Stary OskoL', 'Schemilowka', 'Ljamisa', 'Mstinski Most', 'Sowetski', 'Priosjorsk', 'Kin', 'Lissi Nos', 'Iwangorod', 'Kamenskoje', 'Seliwanowo', 'KowaLko', 'Dubowizkoje', 'Sosnowo', 'Selenogorsk', 'Kerest', 'UstSchora', 'UstSchory', 'Filippowka', 'Molebny Owrag', 'Stadtteil Rostokino', 'Werchnije Kotly', 'Nishnije Kotly', 'NowoGirejewo', 'Panki', 'Perowo Pole', 'Kurkino', 'Marfino', 'Alexino', 'Beskudnikowo', 'Guba', 'Nishnjaja Simba', 'Wladikawkas', 'Bugry', 'Kriwoschtschowoko', 'MBystraja', 'Dorogoi', 'Bolotowo', 'Kjutschiki', 'Raswilka', 'Jewlaschewo', 'Achuny', 'Machalino', 'Kripun', 'Rasjesd', 'Turns kaja', 'Turn a', 'Lesnoje', 'Sals k', 'NowoAsowka', 'Rostowka', 'Marzewo', 'Peschtschany', 'Sokolowaja Gora', 'Sudowka', 'km 282', 'DsershinskiStadtbezirk', 'JermanskiStadtbezirk', 'J e r m a n s ki Stad tbezi rk', 'TraktorosawodskiStadtbezirk', 'Sowchos Priwolshski', 'Shirnowsk', 'Abgenowo', 'Rasjesd Owrashny', 'Ajat', 'Turjinski', 'Kuschwa', 'Rudnitschny', 'Woltschanka', 'Bergwerk 23', 'Patotschja', 'Rogoshinski', 'Bergwerk 6', 'Stali nogorsk', 'Bergwerk 19', 'Dsjakino', 'Sareka', 'Moissejewka', 'Mjassnikowo', 'Nowoschalaschowo', 'Maksai', 'Korjakino', 'ski', 'Alexejewskoje', 'Makarji Roschtscha', 'Silno', 'Kokawino', 'Ljubomirskaja', 'Wassilkow', 'PostWolynski', 'Kowachino', 'Olesko', 'Sinilow', 'Rabotschi', 'Wetka', 'Kalinowka', 'PetrowoLidijewka', 'DonezkoAmwrossijewka', 'Shelanja', 'Schachtjorsk', 'Ilowaisk', 'Kriwoi Torez', 'Lidijewka', 'IwanoFrankowsk', 'Wiry', 'Jazewo', 'Shidinitschi', 'Uditschew', 'Uditschewo', 'Brjanka', 'DsershinskiBergwerk', 'Toschkowka', 'Maksimowka', 'Bergwerk Nr. 8', 'GLuboki', 'IljitschBergwerk', 'Petrowenki', 'Bergwerkssiedlung Nr. 7', 'Kosyrewo', 'Kasimirowka', 'Norio', 'Dshambejty', 'Komsomolski', 'Spass Saulok', 'B. Saborje', 'Werksiedlung Sulash Gora', 'Kudama', 'Repjowka', 'Sibrowo', 'Lopatkowo', 'Solnjetschja', 'Perewoloki', 'Alexejewka', 'Bachilowo', 'Uman', 'Owrutsch', 'Mariupol', 'Mokwa', 'Massy', 'Lahta', 'Sapjorja', 'Roshdestwennoje', 'Rybniza', 'Brno', 'Sibirien', 'Ural', 'Workuta', 'Magadan', 'Kolyma', 'Norilsk', 'Lubjanka', 'Butyrka', 'Kaliningrad', 'Lager Nr.', 'Lager Nummer']



```python
from spacy.lang.de import German
from spacy.matcher import Matcher

nlp = German()

doc = nlp("Karl-Heinz Quade ist von März 1944 bis August 1948 im Lager 150 in Grjasowez interniert.")

matcher = Matcher(nlp.vocab)
for place in gazetteer:
    pattern = [{'LOWER': place.lower()}]
    matcher.add(place, [pattern])

matches = matcher(doc)
for match_id, start, end in matches:
    print(start, end, doc[start:end].text)
```

    13 14 Grjasowez



```python
pattern = [{'LOWER': 'lager'},  
           {'LIKE_NUM': True}] 
matcher.add("LAGER_PATTERN", [pattern])
```


```python
for file in Path('german').iterdir():
    doc = nlp(file.read_text())
    matches = matcher(doc)
    for match_id, start, end in matches:
        print(file.name, start, end, doc[start:end].text)
```

    germantext.txt 16 17 Stalingrad
    germantext.txt 33 34 Workuta
    germantext.txt 35 36 Astrachan
    germantext.txt 65 66 Stalingrad
    germantext.txt 77 78 Stalingrad
    germantext.txt 104 105 Stalingrad
    germantext.txt 106 107 Saratow
    germantext.txt 180 181 Stalingrad
    germantext.txt 190 191 Jelabuga
    germantext.txt 193 194 Stalingrad
    germantext.txt 222 223 Stalingrad
    germantext.txt 240 241 Jelabuga
    germantext.txt 382 383 Stalingrad
    germantext.txt 396 397 Stalingrad
    germantext.txt 416 417 Stalingrad
    germantext.txt 456 457 Stalingrad
    germantext.txt 483 484 Stalingrad
    germantext.txt 521 522 Stalingrad
    germantext.txt 600 601 Moskau
    germantext.txt 649 650 Stalingrad
    germantext.txt 663 664 Stalingrad
    germantext.txt 715 716 Stalingrad
    germantext.txt 730 731 Stalingrad
    germantext.txt 794 795 Stalingrad
    germantext.txt 825 826 Russland
    germantext.txt 861 862 Stalingrad
    germantext.txt 880 881 Stalingrad
    germantext.txt 971 972 Stalingrad
    germantext.txt 1056 1057 Stalingrad
    germantext.txt 1081 1082 Stalingrad
    germantext.txt 1119 1120 Stalingrad
    germantext.txt 1140 1141 Stalingrad
    germantext.txt 1166 1167 Stalingrad
    germantext.txt 1186 1187 Stalingrad
    germantext.txt 1241 1242 Stalingrad
    germantext.txt 1275 1276 Stalingrad
    germantext.txt 1336 1337 Stalingrad
    germantext.txt 1456 1457 Stalingrad
    germantext.txt 1483 1484 Russland
    germantext.txt 1506 1507 Stalingrad
    germantext.txt 1563 1564 Stalingrad
    germantext.txt 1631 1632 Stalingrad
    germantext.txt 1682 1683 Stalingrad
    germantext.txt 1744 1745 Stalingrad
    germantext.txt 1769 1770 Russland
    germantext.txt 1795 1796 Stalingrad
    germantext.txt 1830 1831 Stalingrad
    germantext.txt 1919 1920 Stalingrad
    germantext.txt 1931 1932 Stalingrad
    germantext.txt 1940 1941 Russland
    germantext.txt 1949 1950 Stalingrad
    germantext.txt 1977 1978 Stalingrad
    germantext.txt 1985 1986 Stalingrad
    germantext.txt 2133 2134 Stalingrad
    germantext.txt 2364 2365 Keller
    germantext.txt 2484 2485 Stalingrad
    germantext.txt 2516 2517 Stalingrad
    germantext.txt 2558 2559 Gorki
    germantext.txt 2570 2571 Moskau
    germantext.txt 2592 2593 Stalingrad
    germantext.txt 2594 2595 Saratow
    germantext.txt 2596 2597 Wolsk
    germantext.txt 2598 2599 Sysran
    germantext.txt 2600 2601 Kuibyschew
    germantext.txt 2604 2605 Uljanowsk
    germantext.txt 2606 2607 Kasan
    germantext.txt 2610 2611 Kasan
    germantext.txt 2612 2613 Moskau
    germantext.txt 2714 2715 Kasan
    germantext.txt 2765 2766 Stalingrad
    germantext.txt 2834 2835 Stalingrad
    germantext.txt 3002 3003 Kasan
    germantext.txt 3039 3040 Kasan
    germantext.txt 3079 3080 Kasan
    germantext.txt 3113 3114 Tscheboksary
    germantext.txt 3139 3140 Tula
    germantext.txt 3193 3194 Russland
    germantext.txt 3259 3260 Moskau
    germantext.txt 3267 3268 Jelabuga
    germantext.txt 3520 3521 Kaluga
    germantext.txt 3529 3530 Tula
    germantext.txt 3553 3554 Moskau
    germantext.txt 3570 3571 Derbent
    germantext.txt 3574 3575 Baku
    germantext.txt 3587 3588 Astrachan
    germantext.txt 3592 3593 Moskau
    germantext.txt 3608 3609 Pugatschow
    germantext.txt 3626 3627 Moskau
    germantext.txt 3714 3715 Ural
    germantext.txt 3721 3722 Ural
    germantext.txt 3730 3731 Kasan
    germantext.txt 3733 3734 Pugatschow
    germantext.txt 3738 3739 Moskau
    germantext.txt 4066 4067 Moskau
    germantext.txt 4121 4122 Smolensk
    germantext.txt 4139 4140 Smolensk
    germantext.txt 4237 4238 Workuta
    germantext.txt 4239 4240 Astrachan
    germantext.txt 4311 4312 Smolensk
    germantext.txt 4323 4324 Sibirien
    germantext.txt 4466 4467 Smolensk
    germantext.txt 4494 4495 Smolensk
    germantext.txt 4568 4569 Smolensk
    germantext.txt 4596 4597 Johannes
    germantext.txt 4604 4605 Smolensk
    germantext.txt 4627 4628 Smolensk
    germantext.txt 5097 5098 Borowitschi
    germantext.txt 5121 5122 KALININ
    germantext.txt 5127 5128 Borissow
    germantext.txt 5130 5131 MINSK
    germantext.txt 5132 5133 Orscha
    germantext.txt 5138 5139 WITEBSK
    germantext.txt 5156 5157 LWOW
    germantext.txt 5167 5168 Stanislaw
    germantext.txt 5180 5181 Winniza
    germantext.txt 5182 5183 Tscherkassy
    germantext.txt 5184 5185 Molotowsk
    germantext.txt 5193 5194 SMOLENSK
    germantext.txt 5196 5197 MOSKAU
    germantext.txt 5200 5201 KALUGA
    germantext.txt 5217 5218 BRJANSK
    germantext.txt 5221 5222 Lebedjan
    germantext.txt 5224 5225 ARCHANGELSK
    germantext.txt 5227 5228 Temnikow
    germantext.txt 5230 5231 PENSA
    germantext.txt 5232 5233 Wolsk
    germantext.txt 5248 5249 Kineschma
    germantext.txt 5257 5258 Susdal
    germantext.txt 5263 5264 WLADIMIR
    germantext.txt 5294 5295 KURSK
    germantext.txt 5297 5298 Sumy
    germantext.txt 5312 5313 ODESSA
    germantext.txt 5319 5320 POLTAWA
    germantext.txt 5320 5321 CHARKOW
    germantext.txt 5325 5326 Kupjansk
    germantext.txt 5329 5330 Atkarsk
    germantext.txt 5331 5332 SARATOW
    germantext.txt 5333 5334 Urjupinsk
    germantext.txt 5335 5336 Lissitschansk
    germantext.txt 5341 5342 Rjasan
    germantext.txt 5346 5347 Potma
    germantext.txt 5348 5349 Saransk
    germantext.txt 5351 5352 Morschansk
    germantext.txt 5355 5356 Kramatorsk
    germantext.txt 5360 5361 MAKEJEWKA
    germantext.txt 5364 5365 STALINO
    germantext.txt 5370 5371 Melitopol
    germantext.txt 5373 5374 Taganrog
    germantext.txt 5381 5382 SIMFEROPOL
    germantext.txt 5394 5395 Armawir
    germantext.txt 5401 5402 Nowotscherkassk
    germantext.txt 5442 5443 Rustawi
    germantext.txt 5451 5452 TASCHKENT
    germantext.txt 5453 5454 Tschuama
    germantext.txt 5459 5460 Kokand
    germantext.txt 5467 5468 Begowat
    germantext.txt 5717 5718 Kertsch
    germantext.txt 5771 5772 Maikop
    germantext.txt 5878 5879 Baku
    germantext.txt 5944 5945 Stalingrad
    germantext.txt 5991 5992 Astrachan
    germantext.txt 6057 6058 Tichorezk
    germantext.txt 6082 6083 Stalingrad
    germantext.txt 6087 6088 Astrachan
    germantext.txt 6100 6101 Stalingrad
    germantext.txt 6108 6109 Astrachan
    germantext.txt 6188 6189 Baku
    germantext.txt 6297 6298 Kertsch
    germantext.txt 6343 6344 Kertsch
    germantext.txt 6440 6441 Leningrad
    germantext.txt 6497 6498 Krasnogorsk
    germantext.txt 6499 6500 Moskau
    germantext.txt 6622 6623 Moskau
    germantext.txt 6653 6654 Moskau
    germantext.txt 6671 6672 Moskau
    germantext.txt 6826 6827 Jelabuga
    germantext.txt 6884 6885 Engels
    germantext.txt 6951 6952 Engels
    germantext.txt 7051 7052 Moskau
    germantext.txt 7064 7065 Moskau
    germantext.txt 7074 7075 Moskau
    germantext.txt 7139 7140 Moskau
    germantext.txt 7154 7155 Moskau
    germantext.txt 7177 7178 Krasnogorsk
    germantext.txt 7201 7202 Moskau
    germantext.txt 7309 7310 Marx
    germantext.txt 7364 7365 Gorki
    germantext.txt 7425 7426 Nowgorod
    germantext.txt 7428 7429 Gorki
    germantext.txt 7448 7449 Wladimir
    germantext.txt 7472 7473 Kasan
    germantext.txt 7497 7498 Nowgorod
    germantext.txt 7525 7526 Nowgorod
    germantext.txt 7557 7558 Moskau
    germantext.txt 7620 7621 Susdal
    germantext.txt 7631 7632 Moskau
    germantext.txt 7638 7639 Jelabuga
    germantext.txt 7719 7720 Gorki
    germantext.txt 7722 7723 Moskau
    germantext.txt 7724 7725 Leningrad
    germantext.txt 7732 7733 RSFSR
    germantext.txt 7901 7902 Gorki
    germantext.txt 7949 7950 Nowgorod
    germantext.txt 7955 7956 Gorki
    germantext.txt 7985 7986 Gorki
    germantext.txt 7988 7989 Nowgorod
    germantext.txt 8044 8045 Nowgorod
    germantext.txt 8050 8051 Moskau
    germantext.txt 8093 8094 Gorki
    germantext.txt 8235 8236 Jelabuga
    germantext.txt 8468 8469 Jelabuga
    germantext.txt 8484 8485 Jelabuga
    germantext.txt 8518 8519 Jelabuga
    germantext.txt 8535 8536 Jelabuga
    germantext.txt 8561 8562 Selenodolsk
    germantext.txt 8567 8568 Kasan
    germantext.txt 8573 8574 Selenodolsk
    germantext.txt 8580 8581 Selenodolsk
    germantext.txt 8587 8588 Selenodolsk
    germantext.txt 8602 8603 Moskau
    germantext.txt 8604 8605 Jarzewo
    germantext.txt 8610 8611 Jarzewo
    germantext.txt 8623 8624 Charkow
    germantext.txt 8635 8636 Charkow
    germantext.txt 8637 8638 Ukraine
    germantext.txt 9831 9832 Ukraine
    germantext.txt 9841 9842 Litauen
    germantext.txt 9843 9844 Estland
    germantext.txt 9980 9981 Wladimir
    germantext.txt 10114 10115 Moskau
    germantext.txt 10129 10130 Leningrad
    germantext.txt 10319 10320 Ural
    germantext.txt 10325 10326 Sibirien
    germantext.txt 10404 10405 Stalingrad
    germantext.txt 10590 10591 RSFSR
    germantext.txt 10597 10598 Ukraine
    germantext.txt 10601 10602 Usbekistan
    germantext.txt 10603 10604 Kasachstan
    germantext.txt 10605 10606 Georgien
    germantext.txt 10609 10610 Litauen
    germantext.txt 10611 10612 Estland
    germantext.txt 10617 10618 Armenien
    germantext.txt 10623 10624 Lettland
    germantext.txt 10791 10792 Kyschtym
    germantext.txt 10795 10796 Tscheljabinsk
    germantext.txt 10803 10804 Beketowka
    germantext.txt 10834 10835 Orscha
    germantext.txt 10836 10837 Beketowka
    germantext.txt 10838 10839 Wolsk
    germantext.txt 10865 10866 Kasan
    germantext.txt 10867 10868 Stalingrad
    germantext.txt 10878 10879 Workuta
    germantext.txt 10893 10894 Moskau
    germantext.txt 10895 10896 Workuta
    germantext.txt 10948 10949 Riga
    germantext.txt 10969 10970 Suchumi
    germantext.txt 10981 10982 Nowoschachtinsk
    germantext.txt 10993 10994 Brjansk
    germantext.txt 11009 11010 Stalingrad
    germantext.txt 11045 11046 Ragnit
    germantext.txt 11047 11048 Sibirien
    germantext.txt 11066 11067 Orsk
    germantext.txt 11085 11086 Moskau
    germantext.txt 11087 11088 Krasnogorsk
    germantext.txt 11390 11391 Moskau
    germantext.txt 11505 11506 Moskau
    germantext.txt 11519 11520 Moskau
    germantext.txt 11598 11599 Moskau
    germantext.txt 11617 11618 Moskau
    germantext.txt 11642 11643 Moskau
    germantext.txt 11659 11660 Krjukowo
    germantext.txt 11661 11662 Kaschira
    germantext.txt 11671 11672 Moskau
    germantext.txt 11690 11691 Moskau
    germantext.txt 11753 11754 Moskau
    germantext.txt 11963 11964 Moskau
    germantext.txt 11976 11977 Ural
    germantext.txt 11981 11982 Moskau
    germantext.txt 12049 12050 Moskau
    germantext.txt 12367 12368 Ar
    germantext.txt 12400 12401 Stalingrad
    germantext.txt 12431 12432 Stalingrad
    germantext.txt 12514 12515 Keller
    germantext.txt 12632 12633 Stalingrad
    germantext.txt 12645 12646 Stalingrad
    germantext.txt 12787 12788 Stalingrad
    germantext.txt 12867 12868 Russland
    germantext.txt 13011 13012 STALINGRAD
    germantext.txt 13055 13056 Stalingrad
    germantext.txt 13288 13289 Nowotroizk
    germantext.txt 13290 13291 Maksai
    germantext.txt 13608 13609 Moskau
    germantext.txt 13694 13695 Stalingrad
    germantext.txt 13715 13716 Rshew
    germantext.txt 13748 13749 Bor
    germantext.txt 13754 13755 Smolensk
    germantext.txt 13767 13768 Rshew
    germantext.txt 13772 13773 Gshatsk
    germantext.txt 13783 13784 Brjansk
    germantext.txt 13785 13786 Orjol
    germantext.txt 13793 13794 Smolensk
    germantext.txt 13821 13822 Witebsk
    germantext.txt 13833 13834 Roslawl
    germantext.txt 13845 13846 Brjansk
    germantext.txt 13852 13853 Smolensk
    germantext.txt 13875 13876 Minsk
    germantext.txt 13963 13964 Jelabuga
    germantext.txt 13995 13996 Kasan
    germantext.txt 14013 14014 Selenodolsk
    germantext.txt 14036 14037 Jelabuga
    germantext.txt 14078 14079 Kasan
    germantext.txt 14093 14094 Kasan
    germantext.txt 14111 14112 Selenodolsk
    germantext.txt 14123 14124 Selenodolsk
    germantext.txt 14148 14149 Kasan
    germantext.txt 14197 14198 Kasan
    germantext.txt 14231 14232 Kasan
    germantext.txt 14246 14247 Kasan
    germantext.txt 14267 14268 Kasan
    germantext.txt 14321 14322 Kasan
    germantext.txt 14370 14371 Selenodolsk
    germantext.txt 14533 14534 Selenodolsk
    germantext.txt 14607 14608 Selenodolsk
    germantext.txt 14654 14655 Selenodolsk
    germantext.txt 14721 14722 Riga
    germantext.txt 14736 14737 Selenodolsk
    germantext.txt 14769 14770 Selenodolsk
    germantext.txt 14846 14847 Selenodolsk
    germantext.txt 14944 14945 Tiraspol
    germantext.txt 14994 14995 Nikolajew
    germantext.txt 15108 15109 Odessa
    germantext.txt 15149 15150 Nikolajew
    germantext.txt 15195 15196 Nikolajew
    germantext.txt 15237 15238 Nikolajew
    germantext.txt 15311 15312 Nikolajew
    germantext.txt 15419 15420 Odessa
    germantext.txt 15437 15438 Odessa
    germantext.txt 15490 15491 Nikolajew
    germantext.txt 15498 15499 Odessa
    germantext.txt 15506 15507 Odessa
    germantext.txt 15523 15524 Odessa
    germantext.txt 15534 15535 Krim
    germantext.txt 15547 15548 Odessa
    germantext.txt 15613 15614 Odessa
    germantext.txt 15618 15619 Krim
    germantext.txt 15639 15640 Sibirien
    germantext.txt 15653 15654 Krim
    germantext.txt 15667 15668 Krim
    germantext.txt 15685 15686 Siwasch
    germantext.txt 15689 15690 Kertsch
    germantext.txt 15956 15957 Selenodolsk
    germantext.txt 16021 16022 Selenodolsk
    germantext.txt 16150 16151 Selenodolsk
    germantext.txt 16201 16202 Selenodolsk
    germantext.txt 16257 16258 Selenodolsk
    germantext.txt 16291 16292 Selenodolsk
    germantext.txt 16407 16408 Selenodolsk
    germantext.txt 16512 16513 Jelabuga
    germantext.txt 16536 16537 Jelabuga
    germantext.txt 16550 16551 Jelabuga
    germantext.txt 16571 16572 Selenodolsk
    germantext.txt 16580 16581 Jelabuga
    germantext.txt 16598 16599 Selenodolsk
    germantext.txt 16611 16612 Selenodolsk
    germantext.txt 16628 16629 Moskau
    germantext.txt 16639 16640 Jarzewo
    germantext.txt 16652 16653 Merefa
    germantext.txt 16677 16678 Charkow
    germantext.txt 16779 16780 Jelabuga
    germantext.txt 16863 16864 Moskau
    germantext.txt 16865 16866 Workuta
    germantext.txt 17127 17128 Moskau
    germantext.txt 17136 17137 Lubjanka
    germantext.txt 17140 17141 Butyrka
    germantext.txt 17159 17160 Moskau
    germantext.txt 17162 17163 Workuta
    germantext.txt 17249 17250 Karaganda
    germantext.txt 17251 17252 Workuta
    germantext.txt 17256 17257 Karaganda
    germantext.txt 17269 17270 Workuta
    germantext.txt 17338 17339 Workuta
    germantext.txt 17477 17478 Moskau
    germantext.txt 17660 17661 Workuta
    germantext.txt 17684 17685 Stalingrad
    germantext.txt 17805 17806 Moskau
    germantext.txt 17810 17811 USA
    germantext.txt 17877 17878 Jelabuga
    germantext.txt 18119 18120 Gorodischtsche
    germantext.txt 18213 18214 Stalingrad
    germantext.txt 18243 18244 Stalingrad
    germantext.txt 18276 18277 Stalingrad
    germantext.txt 18331 18332 Kasan
    germantext.txt 18359 18360 Jelschanka
    germantext.txt 18428 18429 Jelschanka
    germantext.txt 18455 18456 Gorodischtsche
    germantext.txt 18471 18472 Jelschanka
    germantext.txt 18540 18541 Stalingrad
    germantext.txt 18836 18837 Johannes
    germantext.txt 18877 18878 Krasnodar
    germantext.txt 18882 18883 Charkow
    germantext.txt 18899 18900 Minsk
    germantext.txt 18904 18905 Kiew
    germantext.txt 18907 18908 Jar
    germantext.txt 18958 18959 Nikolajew
    germantext.txt 19020 19021 Johannes
    germantext.txt 19024 19025 Stalingrad
    germantext.txt 19030 19031 Stalingrad
    germantext.txt 19261 19262 Jelabuga
    germantext.txt 20017 20018 ar
    germantext.txt 20370 20371 Stalingrad
    germantext.txt 20411 20412 Stalingrad
    germantext.txt 20452 20453 Stalingrad
    germantext.txt 20529 20530 Stalingrad
    germantext.txt 20591 20592 Stalingrad
    germantext.txt 20640 20641 Stalingrad
    germantext.txt 20739 20740 Stalingrad
    germantext.txt 20761 20762 Stalingrad
    germantext.txt 20818 20819 Russland
    germantext.txt 20906 20907 Stalingrad
    germantext.txt 20941 20942 Russland
    germantext.txt 20963 20964 Stalingrad
    germantext.txt 21021 21022 Stalingrad
    germantext.txt 21069 21070 Jelabuga
    germantext.txt 21089 21090 Stalingrad
    germantext.txt 21233 21234 Stalingrad
    germantext.txt 21284 21285 Stalingrad
    germantext.txt 21897 21898 Adler
    germantext.txt 22069 22070 Adler
    germantext.txt 22083 22084 Adler
    germantext.txt 22253 22254 Kursk
    germantext.txt 22333 22334 Wjasma
    germantext.txt 22335 22336 Gshatsk
    germantext.txt 22339 22340 Smolensk
    germantext.txt 22350 22351 Kursk
    germantext.txt 22371 22372 Smolensk
    germantext.txt 22394 22395 Smolensk
    germantext.txt 22396 22397 Roslawl
    germantext.txt 22410 22411 Roslawl
    germantext.txt 22448 22449 Smolensk
    germantext.txt 22450 22451 Roslawl
    germantext.txt 22477 22478 Smolensk
    germantext.txt 22500 22501 Gomel
    germantext.txt 22570 22571 Witebsk
    germantext.txt 22737 22738 Witebsk
    germantext.txt 22739 22740 Borissow
    germantext.txt 22741 22742 Bobruisk
    germantext.txt 23209 23210 Moskau
    germantext.txt 23413 23414 Stalingrad
    germantext.txt 23506 23507 Stalingrad
    germantext.txt 23790 23791 Dwiri
    germantext.txt 23795 23796 Georgien
    germantext.txt 23996 23997 Jelabuga
    germantext.txt 24018 24019 Jelabuga
    germantext.txt 24077 24078 Stalingrad
    germantext.txt 24103 24104 Kasan
    germantext.txt 24173 24174 Jelabuga
    germantext.txt 24321 24322 Stalingrad
    germantext.txt 24329 24330 Stalingrad
    germantext.txt 24486 24487 Jelabuga
    germantext.txt 24529 24530 Jelabuga
    germantext.txt 24538 24539 Kasan
    germantext.txt 24932 24933 Stalingrad
    germantext.txt 24991 24992 Workuta
    germantext.txt 24993 24994 Astrachan
    germantext.txt 25029 25030 Stalingrad
    germantext.txt 25072 25073 Johannes
    germantext.txt 25605 25606 jelabuga
    germantext.txt 25638 25639 Selenodolsk
    germantext.txt 25670 25671 Jelabuga
    germantext.txt 25688 25689 Moskau
    germantext.txt 25690 25691 Jarzewo
    germantext.txt 25696 25697 Moskau
    germantext.txt 25702 25703 Minsk
    germantext.txt 25717 25718 Jarzewo
    germantext.txt 25763 25764 Merefa
    germantext.txt 25767 25768 Charkow
    germantext.txt 26099 26100 Jelabuga
    germantext.txt 26101 26102 Selenodolsk
    germantext.txt 26108 26109 Jelabuga
    germantext.txt 26391 26392 Stalingrad
    germantext.txt 26407 26408 Stalingrad
    germantext.txt 26440 26441 Stalingrad
    germantext.txt 26518 26519 Kasan
    germantext.txt 26533 26534 Stalingrad
    germantext.txt 26688 26689 Pensa
    germantext.txt 26694 26695 Pensa
    germantext.txt 26724 26725 Moskau
    germantext.txt 26737 26738 Pensa
    germantext.txt 26762 26763 Moskau
    germantext.txt 26825 26826 Moskau
    germantext.txt 26827 26828 Kuibyschew
    germantext.txt 26838 26839 Kuibyschew
    germantext.txt 26860 26861 Moskau
    germantext.txt 26898 26899 Stalingrad
    germantext.txt 26909 26910 Pensa
    germantext.txt 26911 26912 Kuibyschew
    germantext.txt 26990 26991 Jelabuga
    germantext.txt 27096 27097 Moskau
    germantext.txt 27160 27161 Jelabuga
    germantext.txt 27165 27166 Kasan
    germantext.txt 27167 27168 Pensa
    germantext.txt 27337 27338 Ukraine
    germantext.txt 27366 27367 Fastow
    germantext.txt 27368 27369 Shitomir
    germantext.txt 27372 27373 Owrutsch
    germantext.txt 27484 27485 Kursk
    germantext.txt 27486 27487 Orjol
    germantext.txt 27561 27562 Kiew
    germantext.txt 27575 27576 Kiew
    germantext.txt 27775 27776 Pronja
    germantext.txt 27804 27805 Gomel
    germantext.txt 27826 27827 Bobruisk
    germantext.txt 27837 27838 Moskau
    germantext.txt 27846 27847 Gomel
    germantext.txt 27853 27854 Retschiza
    germantext.txt 27864 27865 Shlobin
    germantext.txt 27866 27867 Mosyr
    germantext.txt 27885 27886 Retschiza
    germantext.txt 28076 28077 Krasnogorsk
    germantext.txt 28122 28123 Stalingrad
    germantext.txt 28126 28127 Kameschkowo
    germantext.txt 28184 28185 Stalingrad
    germantext.txt 28382 28383 Stalingrad
    germantext.txt 28397 28398 Stalingrad
    germantext.txt 28403 28404 Kameschkowo
    germantext.txt 28489 28490 Kasan
    germantext.txt 28504 28505 Kameschkowo
    germantext.txt 28659 28660 Stalingrad
    germantext.txt 28684 28685 STALINGRAD



    ---------------------------------------------------------------------------

    IsADirectoryError                         Traceback (most recent call last)

    Input In [44], in <cell line: 1>()
          1 for file in Path('german').iterdir():
    ----> 2     doc = nlp(file.read_text())
          3     matches = matcher(doc)
          4     for match_id, start, end in matches:


    File /opt/anaconda3/lib/python3.9/pathlib.py:1266, in Path.read_text(self, encoding, errors)
       1262 def read_text(self, encoding=None, errors=None):
       1263     """
       1264     Open the file in text mode, read it, and close the file.
       1265     """
    -> 1266     with self.open(mode='r', encoding=encoding, errors=errors) as f:
       1267         return f.read()


    File /opt/anaconda3/lib/python3.9/pathlib.py:1252, in Path.open(self, mode, buffering, encoding, errors, newline)
       1246 def open(self, mode='r', buffering=-1, encoding=None,
       1247          errors=None, newline=None):
       1248     """
       1249     Open the file pointed by this path and return a file object, as
       1250     the built-in open() function does.
       1251     """
    -> 1252     return io.open(self, mode, buffering, encoding, errors, newline,
       1253                    opener=self._opener)


    IsADirectoryError: [Errno 21] Is a directory: 'german/.ipynb_checkpoints'



```python
from collections import Counter

count_list = []
for match_id, start, end in matches:
    count_list.append(doc[start:end].text)

counter = Counter(count_list)

for term, count in counter.most_common(10):
    print(term,count)
```

    Stalingrad 100
    Moskau 55
    Jelabuga 30
    Selenodolsk 26
    Kasan 25
    Smolensk 16
    Workuta 11
    Russland 8
    Gorki 8
    Odessa 8



```python
pip install spacy
```

    Requirement already satisfied: spacy in /opt/anaconda3/lib/python3.9/site-packages (3.4.2)
    Requirement already satisfied: pydantic!=1.8,!=1.8.1,<1.11.0,>=1.7.4 in /opt/anaconda3/lib/python3.9/site-packages (from spacy) (1.10.2)
    Requirement already satisfied: numpy>=1.15.0 in /opt/anaconda3/lib/python3.9/site-packages (from spacy) (1.21.5)
    Requirement already satisfied: requests<3.0.0,>=2.13.0 in /opt/anaconda3/lib/python3.9/site-packages (from spacy) (2.27.1)
    Requirement already satisfied: langcodes<4.0.0,>=3.2.0 in /opt/anaconda3/lib/python3.9/site-packages (from spacy) (3.3.0)
    Requirement already satisfied: catalogue<2.1.0,>=2.0.6 in /opt/anaconda3/lib/python3.9/site-packages (from spacy) (2.0.8)
    Requirement already satisfied: jinja2 in /opt/anaconda3/lib/python3.9/site-packages (from spacy) (2.11.3)
    Requirement already satisfied: wasabi<1.1.0,>=0.9.1 in /opt/anaconda3/lib/python3.9/site-packages (from spacy) (0.10.1)
    Requirement already satisfied: spacy-legacy<3.1.0,>=3.0.10 in /opt/anaconda3/lib/python3.9/site-packages (from spacy) (3.0.10)
    Requirement already satisfied: packaging>=20.0 in /opt/anaconda3/lib/python3.9/site-packages (from spacy) (21.3)
    Requirement already satisfied: preshed<3.1.0,>=3.0.2 in /opt/anaconda3/lib/python3.9/site-packages (from spacy) (3.0.8)
    Requirement already satisfied: spacy-loggers<2.0.0,>=1.0.0 in /opt/anaconda3/lib/python3.9/site-packages (from spacy) (1.0.3)
    Requirement already satisfied: pathy>=0.3.5 in /opt/anaconda3/lib/python3.9/site-packages (from spacy) (0.6.2)
    Requirement already satisfied: srsly<3.0.0,>=2.4.3 in /opt/anaconda3/lib/python3.9/site-packages (from spacy) (2.4.5)
    Requirement already satisfied: thinc<8.2.0,>=8.1.0 in /opt/anaconda3/lib/python3.9/site-packages (from spacy) (8.1.5)
    Requirement already satisfied: cymem<2.1.0,>=2.0.2 in /opt/anaconda3/lib/python3.9/site-packages (from spacy) (2.0.7)
    Requirement already satisfied: typer<0.5.0,>=0.3.0 in /opt/anaconda3/lib/python3.9/site-packages (from spacy) (0.4.2)
    Requirement already satisfied: setuptools in /opt/anaconda3/lib/python3.9/site-packages (from spacy) (61.2.0)
    Requirement already satisfied: tqdm<5.0.0,>=4.38.0 in /opt/anaconda3/lib/python3.9/site-packages (from spacy) (4.64.0)
    Requirement already satisfied: murmurhash<1.1.0,>=0.28.0 in /opt/anaconda3/lib/python3.9/site-packages (from spacy) (1.0.9)
    Requirement already satisfied: pyparsing!=3.0.5,>=2.0.2 in /opt/anaconda3/lib/python3.9/site-packages (from packaging>=20.0->spacy) (3.0.4)
    Requirement already satisfied: smart-open<6.0.0,>=5.2.1 in /opt/anaconda3/lib/python3.9/site-packages (from pathy>=0.3.5->spacy) (5.2.1)
    Requirement already satisfied: typing-extensions>=4.1.0 in /opt/anaconda3/lib/python3.9/site-packages (from pydantic!=1.8,!=1.8.1,<1.11.0,>=1.7.4->spacy) (4.1.1)
    Requirement already satisfied: certifi>=2017.4.17 in /opt/anaconda3/lib/python3.9/site-packages (from requests<3.0.0,>=2.13.0->spacy) (2021.10.8)
    Requirement already satisfied: charset-normalizer~=2.0.0 in /opt/anaconda3/lib/python3.9/site-packages (from requests<3.0.0,>=2.13.0->spacy) (2.0.4)
    Requirement already satisfied: urllib3<1.27,>=1.21.1 in /opt/anaconda3/lib/python3.9/site-packages (from requests<3.0.0,>=2.13.0->spacy) (1.26.9)
    Requirement already satisfied: idna<4,>=2.5 in /opt/anaconda3/lib/python3.9/site-packages (from requests<3.0.0,>=2.13.0->spacy) (3.3)
    Requirement already satisfied: blis<0.8.0,>=0.7.8 in /opt/anaconda3/lib/python3.9/site-packages (from thinc<8.2.0,>=8.1.0->spacy) (0.7.9)
    Requirement already satisfied: confection<1.0.0,>=0.0.1 in /opt/anaconda3/lib/python3.9/site-packages (from thinc<8.2.0,>=8.1.0->spacy) (0.0.3)
    Requirement already satisfied: click<9.0.0,>=7.1.1 in /opt/anaconda3/lib/python3.9/site-packages (from typer<0.5.0,>=0.3.0->spacy) (8.0.4)
    Requirement already satisfied: MarkupSafe>=0.23 in /opt/anaconda3/lib/python3.9/site-packages (from jinja2->spacy) (2.0.1)
    Note: you may need to restart the kernel to use updated packages.



```python
import spacy
nlp = spacy.load("de_core_news_sm")

doc = nlp("Karl-Heinz Quade ist von März 1944 bis August 1948 im Lager 150 in Grjasowez interniert.")
for ent in doc.ents:
    print(ent.text, ent.label_, ent.start, ent.end)
```

    Karl-Heinz Quade PER 0 2
    Grjasowez LOC 13 14



```python
from spacy import displacy
displacy.serve(doc, style="ent")
```


```python
displacy.render(doc, jupyter=True, style="ent")

```


```python
displacy.render(doc, jupyter=True, style="dep")

```


```python
from pathlib import Path

svg = displacy.render(doc, style="dep")
output_path = Path("sentence.svg")
output_path.write_text(svg)
```


```python
import spacy
nlp = spacy.load('de_core_news_sm')
nlp.add_pipe('dbpedia_spotlight', config={'language_code': 'de'})

doc = nlp("Karl-Heinz Quade ist von März 1944 bis August 1948 im Lager 150 in Grjasowez interniert.")
for ent in doc.ents:
    print(ent.text, ent.label_, ent.kb_id_)
```


```python
import requests
data = requests.get("http://de.dbpedia.org/data/Grjasowez.json").json()
```


```python
start_date = "1800" #YYYY-MM-DD
end_date = "2000"
source_title = "Karl-Heinz Quade Diary"

output_text = ""
column_header = "id\ttitle\ttitle_source\tstart\tend\n"  
output_text += column_header  

places_list = []
if matches:
    places_list.extend([ doc[start:end].text for match_id, start, end in matches ])
if doc.ents:
    places_list.extend([ ent.text for ent in doc.ents if ent.label_ == "GPE" or ent.label_ == "LOC"])

# remove duplicate place names by creating a list of names and then converting the list to a set
unique_places = set(places_list)

for id, place in enumerate(unique_places):
    output_text += f"{id}\t{place}\t{source_title}\t{start_date}\t{end_date}\n"

filename = source_title.lower().replace(' ','_') + '.tsv'
Path(filename).write_text(output_text)
print('created: ', filename)
```


```python

```


```python

```
