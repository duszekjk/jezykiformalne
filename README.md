
## Zajęcia 1

### Informacje na temat przedmiotu

Prowadzący: Jacek Kałużny

mail: duszekjk@gmail.com

#### Wysyłanie zadań 

Proszę stworzyć prywatne repozytorium na https://git.wmi.amu.edu.pl/ o nazwie jfz-2023-sNRINDEKSU oraz dać 
prawa do odczytu dla prowadzącego zajęcia. W NRINDEKSU proszę wpisać swój nr indeksu, np. jfz-2023-s123456.

Następnie w swoim repozytorium proszę spullować niniejsze repozytorium: `git pull git@github.com:duszekjk/jezykiformalne.git`
W ten sposób będziemy aktualizować zadania co zajęcia.

Zadania robimy do końca soboty poprzedzającej zajęcia

Rozwiązanie zapisujemy w pliku run.py


## Zajęcia 2 Wyrażenia regularne

Dokumentacja wyrażeń regularnych w python3: https://docs.python.org/3/library/re.html

### Podstawowe funkcje

search - zwraca pierwsze dopasowanie w napisie

findall - zwraca listę wszystkich dopasowań (nienakładających się na siebie)

match - zwraca dopasowanie od początku string

To tylko podstawowe funkcje, z których będziemy korzystać. W dokumentacji opisane są wszystkie.

### Obiekt match

```
import re
answer = re.search('na','banan')
print(answer)
print(answer.start())
print(answer.end())
print(answer.group())

answer = re.search('na','kabanos')
print(answer)
type(answer)

if answer:
    print(answer.group())
else:
    pass
```

### Metaznaki

 
- [] -  zbiór znaków
- . - jakikolwiek znak

- ^ - początek napisu
- $ - koniec napisu

- ? - znak występuje lub nie występuje
- \* - zero albo więcej pojawień się
- \+ - jeden albo więcej pojawień się
- {} - dokładnie tyle pojawień się

- | - lub
- () - grupa
- \ -znak ucieczki

- \d digit
- \D nie digit
- \s whitespace
- \S niewhitespace


### Flagi

Można użyć specjalnych flag, np: 
`re.search('ma', 'AlA Ma KoTa', re.IGNORECASE)`.

### Przykłady (objaśnienia na laboratoriach)

Do nauki lepiej użyć pythona w wersji interaktywnej, a najlepiej ipython.

```
import re

text = 'Ala ma kota i hamak, oraz 150 bananów.'

re.search('ma',text)
re.match('ma',text)
re.match('Ala ma',text)
re.findall('ma',text)

re.findall('[mn]a',text)
re.findall('[0-9]',text)
re.findall('[0-9abc]',text)
re.findall('[a-z][a-z]ma[a-z]',text)
re.findall('[a-zA-Z][a-zA-Z]ma[a-zA-z0-9]',text)
re.findall('\d',text)

re.search('[0-9][0-9][0-9]',text)
re.search('[\d][\d][\d]',text)

re.search('\d{2}',text)
re.search('\d{3}',text)

re.search('\d+',text)

re.search('\d+ bananów',text)
re.search('\d* bananów','Ala ma dużo bananów')
re.search('\d* bananów',text)
re.search('ma \d? bananów','Ala ma 5 bananów')
re.search('ma ?\d? bananów','Ala ma bananów')
re.search('ma( \d)? bananów','Ala ma bananów') 

re.search('\d+ bananów','Ala ma 10 bananów albo 20 bananów')
re.search('\d+ bananów$','Ala ma 10 bananów albo 20 bananów')

text = 'Ala ma kota i hamak, oraz 150	bananów.'

re.search('\d+ bananów',text)

re.search('\d+\sbananów',text)

re.search('kota . hamak',text)

re.search('kota . hamak','Ala ma kota z hamakiem')

re.search('kota .* hamak','Ala ma kota lub hamak')

re.search('\.',text)

re.search('kota|psa','Ala ma kota lub hamak')

re.findall('kota|psa','Ala ma kota lub psa')

re.search('kota (i|lub) psa','Ala ma kota lub psa')

re.search('mam (kota).*(kota|psa)','Ja mam kota. Ala ma psa.').group(0)

re.search('mam (kota).*(kota|psa)','Ja mam kota. Ala ma psa.').group(1)

re.search('mam (kota).*(kota|psa)','Ja mam kota. Ala ma psa.').group(2)
```







### Przykłady wyrażenia regularne 2 (objaśnienia na laboratoriach)

####  ^
```
re.search('[0-9]+', '123-456-789')
re.search('[^0-9][0-9]+[^0-9]', '123-456-789')
```

#### cudzysłów
'' oraz "" - oznaczają to samo w pythonie

' ala ma psa o imieniu "Burek"'

" ala ma psa o imieniu 'Burek' "

' ala ma psa o imieniu \'Burek\' '

" ala ma psa o imieniu \"Burek\" "

#### multiline string

#### raw string

przy raw string znaki \ traktowane są jako zwykłe znaki \

chociaż nawet w raw string nadal są escapowane (ale wtedy \ pozostają również w stringu bez zmian)

https://docs.python.org/3/reference/lexical_analysis.html

dobra praktyka - wszędzie escapować

```
'\\'
print('\\')

r'\\'
print(r'\\')


print("abcd")
print("ab\cd")
print(r"ab\cd")

print("ab\nd")
print(r"ab\nd")


print("\"")
print(r"\"")

print("\")
print(r"\")

re.search('\\', r'a\bc')
re.search(r'\\', r'a\bc')
re.search('\\\\', r'a\bc')
```

#### RE SUB
```
re.sub(pattern, replacement, string)

re.sub('a','b', 'ala ma kota')
```

#### backreferencje:

```

re.search(r' \d+ \d+', 'ala ma 41 41 kota')
re.search(r' \d+ \d+', 'ala ma 41 123 kota')
re.search(r' (\d+) \1', 'ala ma 41 41 kota')
re.search(r' (\d+) \1', 'ala ma 41 123 kota')
```

#### lookahead ( to sa takie assercje):
```
re.search(r'ma kot', 'ala ma kot')
re.search(r'ma kot(?=[ay])', 'ala ma kot')
re.search(r'ma kot(?=[ay])', 'ala ma kotka')
re.search(r'ma kot(?=[ay])', 'ala ma koty')
re.search(r'ma kot(?=[ay])', 'ala ma kota')

re.search(r'ma kot(?![ay])', 'ala ma kot')
re.search(r'ma kot(?![ay])', 'ala ma kotka')
re.search(r'ma kot(?![ay])', 'ala ma koty')
re.search(r'ma kot(?![ay])', 'ala ma kota')
```

#### named groups
```
r = re.search(r'ma (?P<ilepsow>\d+) kotow i (?P<ilekotow>\d+) psow', 'ala ma 100 kotow i 200 psow')
r.groups()
r.groups('ilepsow')
r.groups('ilekotow')
```

#### re.split
```
('a,b.c,d').split(',')
('a,b.c,d').split(',')
('a,b.c,d').split(',.')
re.split(r',', 'a,b.c,d') 
re.split(r'[.,]', 'a,b.c,d') 
```
#### \w word character
```
\w - matchuje Unicod word character , jeżeli flaga ASCII to [a-zA-Z0-9_]
\w - odwrotne do \W, jezeli flaga ASCI to [^a-zA-Z0-9_]

re.findall(r'\w+', 'ala ma 3 koty.')
re.findall(r'\W+', 'ala ma 3 koty.')
```
#### początek albo koniec słowa | word boundary
```
re.search(r'\bkot\b', 'Ala ma kota')
re.search(r'\bkot\b', 'Ala ma kot')
re.search(r'\bkot\b', 'Ala ma kot.')
re.search(r'\bkot\b', 'Ala ma kot ')

re.search(r'\Bot\B', 'Ala ma kot ')
re.search(r'\Bot\B', 'Ala ma kota ')
```
#### MULTILINE
```
re.findall(r'^Ma', 'Ma kota Ala\nMa psa Jacek') 
re.findall(r'^Ma', 'Ma kota Ala\nMa psa Jacek', re.MULTILINE)
```
#### RE.COMPILE




## zajęcia 6

instalacja https://pypi.org/project/google-re2/

### DFA i NDFA

```
import re2 as re
n = 50
regexp =  "a?"*n+"a"*n
s = "a"*n
re.match(regexp, s)
```

```
re.match(r"(\d)abc\1", "3abc3") # re2 nie obsługuje backreferencji
```


re2 max memory - podniesienie limitu
time # mierzenie czasu działania


gdyby ktoś chciał poczytać więcej:
https://swtch.com/~rsc/regexp/regexp1.html

### UTF-8
```
c = "ℋ"
ord(c)
chr(8459)
8* 16**2 + 0 * 16**(1) + 0*16**(0)
15*16**3 + 15* 16**2 + 15 * 16**(1) + 15*16**(0)
```

```
xxd -b file
xxd  file
```

termin oddawania zadań - 15. listopada


## Zajęcia 7
https://www.openfst.org/twiki/bin/view/GRM/Thrax

https://www.cs.jhu.edu/~jason/465/hw-ofst/hw-ofst.pdf

Wszystkie zadania proszę robić na wzór `TaskH00`. Proszę umieszczać gramatykę w pliku `grammar.grm` oraz
opisywać finalną regułę nazwą `FinalRule`.



## KOLOKWIUM
Operatory, obowiązujące na kolokwium
====================================

* kwantyfikatory `-` `*` `+` `?` `{n}` `{n,}` `{n, m}`
* alternatywa — `|`
* klasy znaków — `[...]`
* zanegowane klasy znaków — `[^...]`
* dowolny znak — `.`
* unieważnianie znaków specjalnych — \
* operatory zakotwiczające — `^` `$`


Na kolokwium do każdego z 4 pytań będą 3 podpunkty. Na każdy podpunkt odpowiadamy TAK/NIE. Czas trwania to 15 minut.

- zawsze daszek i dolar
- nie bierzemy pod uwagę capturing (jeżeli są pytania o równoważne)
- proponuję wydrukować cały test w wersji bez opdowiedzi i sprawdzać


Do zaliczenia należy zdobyć conajmniej 10 punktów.
