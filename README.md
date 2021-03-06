# ilparser-api
An API for Parsing Indic Languages

Installing Dependencies (Ubuntu):
```bash
$ sudo -E apt-get install autoconf cpanminus gcc git libgdbm-dev libglib2.0-dev make python-numpy \
  python-pydot python-urllib3 python-pip
```

Installing Dependencies (Fedora):
```bash
$ sudo -E dnf install autoconf git gcc gdbm-devel glib2-devel make numpy pydot perl-App-cpanminus \
  python-urllib3 python-pip
```

Installing Perl Dependencies:
```bash
$ cpanm Data::Dumper Dir::Self IPC::Run List::Util Config::IniFiles Mojolicious::Lite
```

Install CRF++
```bash
$ curl https://github.com/ltrc/ilparser-api/releases/download/0.1/CRF.-0.58.tar.gz | tar -xf -
$ cd CRF++-0.58
$ ./configure ; sudo make install
$ echo "/usr/local" | sudo tee /etc/ld.so.conf.d/crfpp.conf
$ sudo ldconfig
```

Setting up the repo:
```bash
$ git clone https://github.com/ltrc/ilparser-api.git
$ ./setup.sh
```

To run the api server:
```
$ perl api.pl prefork
```

Example use of the API:
```bash
$ curl -s localhost:3000/parse --data lang=hin \
    --data data="माना जाता है कि अमृतमंथन के बाद अमृत की कुछ बूँदें यहाँ गिरी थीं , इसलिए इसे ब्रह्मकुंड कहा जाता है ." | \
    jq '.["dependencyparse-11"]' | \
    sed -e 's/\\t/\t/g' -e 's/\\n/\n/g'  -e 's/\\"/\"/g' -e 's/^"//' -e 's/"$//'
1	माना	मान	v	VM	case-|vib-या_जा+ता_है|psd-|chunkId-VGF|pers-2|num-sg|tam-yA|sem-|cp-|gen-m	0	root	_	_
2	जाता	जा	v	VAUX	case-|vib-ता|psd-|chunkId-VGF|pers-any|num-sg|tam-wA|sem-|cp-|gen-m	1	lwg__vaux	_	_
3	है	है	v	VAUX	case-|vib-है|psd-|chunkId-VGF|pers-2|num-sg|tam-hE|sem-|cp-|gen-any	1	lwg__vaux	_	_
4	कि	कि	avy	CC	case-|vib-|psd-|chunkId-CCP|pers-|num-|tam-|sem-|cp-|gen-	1	k2	_	_
5	अमृतमंथन	अमृतमंथन	n	NNP	case-o|vib-०_का_बाद|psd-|chunkId-NP|pers-3|num-sg|tam-0|sem-|cp-|gen-m	14	k7t	_	_
6	के	का	psp	PSP	case-o|vib-का|psd-|chunkId-NP|pers-|num-sg|tam-kA|sem-|cp-|gen-m	5	lwg__psp	_	_
7	बाद	बाद	adv	NST	case-|vib-|psd-|chunkId-NP|pers-|num-|tam-|sem-|cp-|gen-	5	lwg__psp	_	_
8	अमृत	अमृत	n	NNP	case-o|vib-०_का|psd-|chunkId-NP2|pers-3|num-sg|tam-0|sem-|cp-|gen-m	11	r6	_	_
9	की	का	psp	PSP	case-d|vib-का|psd-|chunkId-NP2|pers-|num-sg|tam-kA|sem-|cp-|gen-f	8	lwg__psp	_	_
10	कुछ	कुछ	adj	QF	case-any|vib-|psd-|chunkId-NP3|pers-|num-any|tam-|sem-|cp-|gen-any	11	nmod__adj	_	_
11	बूँदें	बूँद	n	NN	case-d|vib-0|psd-|chunkId-NP3|pers-3|num-pl|tam-0|sem-|cp-|gen-f	14	k1	_	_
12	यहाँ	यहाँ	adv	PRP	case-|vib-|psd-|chunkId-NP4|pers-|num-|tam-|sem-|cp-|gen-	14	k7p	_	_
13	गिरी	गिरी	adj	JJ	case-any|vib-|psd-|chunkId-JJP|pers-|num-any|tam-|sem-|cp-|gen-f	14	k1s	_	_
14	थीं	था	v	VM	case-|vib-था|psd-|chunkId-VGF2|pers-any|num-pl|tam-WA|sem-|cp-|gen-f	4	ccof	_	_
15	,	&चोम्म	punc	SYM	case-|vib-|psd-|chunkId-VGF2|pers-|num-|tam-|sem-|cp-|gen-	14	rsym	_	_
16	इसलिए	इसलिए	adv	PRP	case-|vib-|psd-|chunkId-NP5|pers-|num-|tam-|sem-|cp-|gen-	19	rh	_	_
17	इसे	यह	pn	PRP	case-o|vib-को|psd-|chunkId-NP6|pers-3|num-sg|tam-ko|sem-|cp-|gen-any	19	k2	_	_
18	ब्रह्मकुंड	ब्रह्मकुंड	n	NNP	case-d|vib-0|psd-|chunkId-NP7|pers-3|num-pl|tam-0|sem-|cp-|gen-m	19	k1	_	_
19	कहा	कहा	v	VM	case-|vib-०_जा+ता_है|psd-|chunkId-VGF3|pers-2|num-sg|tam-0|sem-|cp-|gen-m	4	ccof	_	_
20	जाता	जा	v	VAUX	case-|vib-ता|psd-|chunkId-VGF3|pers-any|num-sg|tam-wA|sem-|cp-|gen-m	19	lwg__vaux	_	_
21	है	है	v	VAUX	case-|vib-है|psd-|chunkId-VGF3|pers-2|num-sg|tam-hE|sem-|cp-|gen-any	19	lwg__vaux	_	_
22	.	.	punc	SYM	case-|vib-|psd-|chunkId-BLK|pers-|num-|tam-|sem-|cp-|gen-	1	rsym	_	_
```
Querying the API through browser (output rendered using a JSON plugin):

![GoogleChromeILParserAPI](https://cloud.githubusercontent.com/assets/1779189/14066994/6e405a26-f477-11e5-8d6d-ed26bf3a7f2c.png)

Querying the API through browser (♥ pretty print!):

Enter into the browser: `http://localhost:3000/parse?lang=hin&data=देश के टूरिजम में राजस्थान&pretty`

![PrettyPrint](https://cloud.githubusercontent.com/assets/1779189/14067826/0dfd6fd6-f48c-11e5-8d88-73ab4ad30076.png)

In case of port conflicts, edit the file(s): `./lib/${lang}/daemons.ini`
