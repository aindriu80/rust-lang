## Téacs Ionchódaithe UTF-8 a Stóráil le Teaghráin

Labhair muid faoi teaghráin i gCaibidil 4, ach féachfaimid orthu níos doimhne anois.
Is minic a théann Rustaceans nua i bhfostú ar theaghráin le haghaidh meascán de thrí
cúiseanna: claonadh Rust chun earráidí féideartha a nochtadh, agus teaghráin níos mó
struchtúr sonraí casta ná go dtugann go leor ríomhchláraitheoirí creidiúint dóibh as, agus
UTF-8. Tagann na fachtóirí seo le chéile ar bhealach a d’fhéadfadh a bheith deacair nuair a bhíonn tú
ag teacht ó theangacha ríomhchlárúcháin eile.

Pléimid teaghráin i gcomhthéacs bailiúcháin toisc go bhfuil teaghráin
curtha i bhfeidhm mar bhailiúchán beart, chomh maith le roinnt modhanna úsáideacha a sholáthar
feidhmiúlacht nuair a léirmhínítear na bearta sin mar théacs. Sa chuid seo, déanfaimid
labhairt faoi na hoibríochtaí ar `String` atá ag gach cineál bailiúcháin, mar shampla
ag cruthú, ag nuashonrú, agus ag léamh. Déanfaimid plé freisin ar na bealaí ina bhfuil `String`
difriúil ó na bailiúcháin eile, is é sin an chaoi a ndéantar innéacsú i `String`
casta ag na difríochtaí idir conas a dhéanann daoine agus ríomhairí léirmhíniú
Sonraí `String`.

### Cad is Teaghrán ann?

Déanfaimid sainmhíniú ar dtús cad atá i gceist againn leis an téarma _string_. Níl ach sreang amháin ag meirge
clóscríobh sa chroítheanga, is é sin an sreangshlis `str` a fheictear go hiondúil
san fhoirm a fuarthas ar iasacht `&str`. I gCaibidil 4, labhair muid faoi _string slices_,
atá ina thagairtí do roinnt sonraí teaghrán ionchódaithe UTF-8 atá stóráilte in áit eile. Teaghrán
Stóráiltear litreacha, mar shampla, i ndénártha an chláir agus mar sin de
slisní teaghrán.

An cineál `String`, a sholáthraíonn leabharlann caighdeánach Rust seachas
códaithe sa teanga lárnach, is growable, mutable, úinéireacht, UTF-8 ionchódaithe
cineál teaghrán. Nuair a thagraíonn Rustaceans do "teaghráin" i Rust, d'fhéadfadh siad a bheith
ag tagairt do na cineálacha `String` nó do na cineálacha sreangán `&str`, ní hamháin ceann amháin
de na cineálacha sin. Cé go mbaineann an chuid seo den chuid is mó le `String`, tá an dá chineál
a úsáidtear go mór i leabharlann caighdeánach Rust, agus 'Teaghrán` agus slisní sreang araon
atá ionchódaithe UTF-8.

### Teaghrán Nua á Chruthú

Tá go leor de na hoibríochtaí céanna atá ar fáil le `Vec<T>` ar fáil le `String`
chomh maith toisc go gcuirtear `String` i bhfeidhm i ndáiríre mar chumhdach timpeall veicteoir
bearta le roinnt ráthaíochtaí breise, srianta, agus cumais. Sampla
d'fheidhm a oibríonn ar an mbealach céanna le `Vec<T>` agus is é `String` an `new`
feidhm chun sampla a chruthú, a thaispeántar i Liostú 8-11.

<Listing number="8-11" caption="Creating a new, empty `String`">

```rust
{{#rustdoc_include ../../listings/ch08-common-collections/listing-08-11/src/main.rs:here}}
```

</Listing>

Cruthaíonn an líne seo teaghrán nua, folamh ar a dtugtar `s`, ar féidir linn a luchtú isteach ansin
sonraí. Go minic, beidh roinnt sonraí tosaigh againn agus ba mhaith linn tús a chur leo
teaghrán. Chuige sin, úsáidimid an modh `to_string`, atá ar fáil ar aon chineál
a chuireann an trait `Display` i bhfeidhm, mar a dhéanann literals teaghrán. Liostáil 8-12 seónna
dhá shampla.

<Listing number="8-12" caption="Using the `to_string` method to create a `String` from a string literal">

```rust
{{#rustdoc_include ../../listings/ch08-common-collections/listing-08-12/src/main.rs:here}}
```

</Listing>

Cruthaíonn an cód seo teaghrán ina bhfuil `initial contents`.

Is féidir linn an fheidhm `String::from` a úsáid freisin chun `String` a chruthú as téad
litriúil. Tá an cód i Liostú 8-13 comhionann leis an gcód i Liostú 8-12
a úsáideann `to_string`.

<Listing number="8-13" caption="Ag baint úsáide as an bhfeidhm `String::from` chun `String` a chruthú as teaghrán litriúil">

``` meirge
{{#rustdoc_include ../../listings/ch08-common-collections/listing-08-13/src/main.rs:here}}
```

</Listing>

Toisc go n-úsáidtear teaghráin le haghaidh an oiread sin rudaí, is féidir linn go leor cineálacha éagsúla a úsáid
APIs le haghaidh teaghráin, ag soláthar dúinn go leor roghanna. Is féidir le cuid acu cosúil
iomarcach, ach tá a n-áit acu go léir! Sa chás seo, `String::from` agus
`to_string` déan an rud céanna, mar sin cén ceann a roghnaíonn tú is ábhar do stíl agus
inléiteacht.

Cuimhnigh go bhfuil teaghráin ionchódaithe UTF-8, ionas gur féidir linn a chur san áireamh aon ionchódaithe i gceart
sonraí iontu, mar a thaispeántar i Liosta 8-14.

<Listing number="8-14" caption="Storing greetings in different languages in strings">

```rust
{{#rustdoc_include ../../listings/ch08-common-collections/listing-08-14/src/main.rs:here}}
```

</Listing>

Is luachanna `String` bailí iad seo go léir.

### Teaghrán á nuashonrú

Is féidir le `String` fás i méid agus féadann a bhfuil ann athrú, díreach mar a bhíonn san ábhar
de `Vec<T>`, má bhrúnn tú tuilleadh sonraí isteach ann. Ina theannta sin, is féidir leat go caothúil
úsáid an t-oibreoir `+` nó an macra `format!` chun luachanna `String` a chomhcheangal.

#### Ag gabháil le Teaghrán le `push_str` agus `push`

Is féidir linn `String` a fhás tríd an modh `push_str` a úsáid chun sreangán a cheangal,
mar a léirítear i Liosta 8-15.

<Listing number="8-15" caption="Appending a string slice to a `String` using the `push_str` method">

```rust
{{#rustdoc_include ../../listings/ch08-common-collections/listing-08-15/src/main.rs:here}}
```

</Listing>

Tar éis an dá líne seo, beidh `foobar` i `s`. Glacann an modh `push_str` a
slisne teaghrán mar ní gá go dteastaíonn uainn úinéireacht a ghlacadh ar an
paraiméadar. Mar shampla, sa chód i Liostú 8-16, ba mhaith linn a bheith in ann úsáid a bhaint as
`s2` tar éis a bhfuil ann a chur i gceangal le `s1`.

<Listing number="8-16" caption="Using a string slice after appending its contents to a `String`">

```rust
{{#rustdoc_include ../../listings/ch08-common-collections/listing-08-16/src/main.rs:here}}
```

</Listing>

Dá nglacfadh an modh `push_str` úinéireacht ar `s2`, ní bheimis in ann priontáil
a luach ar an líne dheireanach. Mar sin féin, oibríonn an cód seo mar a mbeimis ag súil!

Glacann an modh `push` carachtar amháin mar pharaiméadar agus cuireann sé leis an
`String`. Cuireann liostú 8-17 an litir _l_ le `String` ag baint úsáide as an `push`
modh.

<Listing number="8-17" caption="Adding one character to a `String` value using `push`">

```rust
{{#rustdoc_include ../../listings/ch08-common-collections/listing-08-17/src/main.rs:here}}
```

</Listing>

Mar thoradh air sin, beidh `lol` i `s`.

#### Comhghaolú leis an Oibreoir `+` nó an `format!` Macra

Go minic, beidh tú ag iarraidh dhá theaghrán atá ann cheana féin a chur le chéile. Bealach amháin chun é sin a dhéanamh ná úsáid a bhaint as
an t-oibreoir `+`, mar a thaispeántar i Liostú 8-18.

<Listing number="8-18" caption="Using the `+` operator to combine two `String` values into a new `String` value">

```rust
{{#rustdoc_include ../../listings/ch08-common-collections/listing-08-18/src/main.rs:here}}
```

</Listing>

Beidh `Hello, world!` sa teaghrán `s3`. Is é an chúis `s1` a thuilleadh
bailí tar éis an Chomh maith, agus an chúis a úsáid againn tagairt do `s2`, tá a dhéanamh
le síniú an mhodha a thugtar air nuair a úsáidimid an t-oibreoir `+`.
Úsáideann an t-oibreoir `+` an modh `add`, a bhfuil cuma rud éigin ar a shíniú
seo:

```rust,ignore
fn add(self, s: &str) -> String {
```

Sa leabharlann chaighdeánach, feicfidh tú 'cuir' sainithe ag baint úsáide as cineálacha agus gaolmhara
cineálacha. Anseo, tá cineálacha nithiúla curtha ina n-ionad againn, agus is é sin a tharlaíonn nuair a dhéanaimid
glaoigh ar an modh seo le luachanna `String`. Pléifimid cúrsaí cineálacha i gCaibidil 10.
Tugann an síniú seo na leideanna a theastaíonn uainn chun tuiscint a fháil ar na rudaí casta
píosaí den oibreoir `+`.

Ar dtús, tá `&` ag `s2`, rud a chiallaíonn go bhfuil muid ag cur _reference_ den dara ceann
teaghrán go dtí an chéad teaghrán. Tá sé seo mar gheall ar an bparaiméadar `s` sa `add`
feidhm: ní féidir linn ach `&str` a chur le `String`; ní féidir linn dhá `String` a chur leis
luachanna le chéile. Ach fan - is é an cineál `&s2` ná `&String`, ní `&str`, mar
sonraithe sa dara paraiméadar le `add` leis. Mar sin cén fáth a gcuirtear Liostú 8-18 le chéile?

Is é an fáth go bhfuilimid in ann `&s2` a úsáid sa ghlao chun `add` ná go bhfuil an tiomsaitheoir
an féidir an argóint `&String` a _chomhéigean_ go `&str`. Nuair a thugaimid an `add`
modh, úsáideann Rust comhéigean _deref_, a thiontaíonn anseo `&s2` go `&s2[..]`.
Déanfaimid plé níos doimhne ar chomhéigean deref i gCaibidil 15. Toisc go ndéanann `add`
gan úinéireacht a ghlacadh ar an bparaiméadar `s`, beidh `s2` fós ina `String` bailí
tar éis na hoibríochta seo.

Ar an dara dul síos, is féidir linn a fheiceáil sa síniú go nglacann `add` úinéireacht ar `self`
toisc go bhfuil `&` ag `self`. Ciallaíonn sé seo go mbeidh `s1` i Liosta 8-18
bhog sé isteach sa ghlao `add` agus ní bheidh sé bailí ina dhiaidh sin. Mar sin, cé go
Breathnaíonn `let s3 = s1 + &s2;` go ndéanfaidh sé an dá theaghrán a chóipeáil agus ceann nua a chruthú,
glacann an ráiteas seo úinéireacht ar `s1`, cuireann cóip den ábhar leis
de `s2`, agus ansin filleann úinéireacht an toraidh. I bhfocail eile, tá sé
cosúil go bhfuil sé ag déanamh go leor cóipeanna, ach níl; tá an cur i bhfeidhm níos mó
éifeachtach ná cóipeáil.

Más gá dúinn a concatenate teaghráin iolrach, iompar an oibreora `+`
éiríonn anacair:

```rust
{{#rustdoc_include ../../listings/ch08-common-collections/no-listing-01-concat-multiple-strings/src/main.rs:here}}
```
Ag an bpointe seo, beidh `s` `tic-tac-toe`. Le gach ceann de na `+` agus `"`
carachtair, tá sé deacair a fheiceáil cad atá ar siúl. Chun teaghráin a chomhcheangal i
bealaí níos casta, is féidir linn an macra `format!` a úsáid ina ionad sin:


```rust
{{#rustdoc_include ../../listings/ch08-common-collections/no-listing-02-format/src/main.rs:here}}
```

Socraíonn an cód seo `s` go `tic-tac-toe` freisin. Oibríonn an macra `format!` mar
`println!`, ach in ionad an t-aschur a phriontáil go dtí an scáileán, filleann sé a
`String` leis an ábhar. Is mór an leagan den chód a úsáideann `format!`
níos éasca le léamh, agus úsáideann an cód ginte ag an macra `format!` tagairtí
ionas nach mbeidh úinéireacht ag an nglao seo ar aon cheann dá pharaiméadair.

### Innéacsú i Teaghráin

I go leor teangacha ríomhchlárúcháin eile, is féidir rochtain a fháil ar charachtair aonair in a
Is oibríocht bhailí agus choiteann é sreang trí thagairt a dhéanamh dóibh de réir innéacs. Mar sin féin,
má dhéanann tú iarracht codanna de `String` a rochtain ag baint úsáide as comhréir innéacsaithe i Rust, déanfaidh tú
earráid a fháil. Smaoinigh ar an gcód neamhbhailí i Liostú 8-19.

<Listing number="8-19" caption="Attempting to use indexing syntax with a String">

```rust,ignore,does_not_compile
{{#rustdoc_include ../../listings/ch08-common-collections/listing-08-19/src/main.rs:here}}
```

</Listing>

Beidh an earráid seo a leanas mar thoradh ar an gcód seo:

```console
{{#include ../../listings/ch08-common-collections/listing-08-19/output.txt}}
```

Insíonn an earráid agus an nóta an scéal: Ní thacaíonn teaghráin meirge le hinnéacsú. Ach
cén fáth nach bhfuil? Chun an cheist sin a fhreagairt, ní mór dúinn plé a dhéanamh ar an gcaoi a stórálann Rust teaghráin isteach
cuimhne.

#### Ionadaíocht Inmheánach

Is éard is `String` ann ná cumhdach thar `Vec<u8>`. Breathnaímis ar chuid dár gcuid i gceart
teaghráin shamplacha UTF-8 ionchódaithe ó Liostú 8-14. Ar dtús, an ceann seo:

```rust
{{#rustdoc_include ../../listings/ch08-common-collections/listing-08-14/src/main.rs:spanish}}
```

Sa chás seo, beidh `len` `4`, rud a chiallaíonn an veicteoir a stórálann an teaghrán
Tá `"Hola"` 4 byte ar fad. Tógann gach ceann de na litreacha seo beart amháin nuair a ionchódaítear iad
UTF-8. Féadfaidh an líne seo a leanas, áfach, iontas ort (tabhair faoi deara go bhfuil an teaghrán seo
Tosaíonn leis an bpríomhlitir Choireallach _Ze_, ní uimhir 3):

```rust
{{#rustdoc_include ../../listings/ch08-common-collections/listing-08-14/src/main.rs:russian}}
```

Dá gcuirfí ceist ort cé chomh fada is atá an téad, b’fhéidir go ndéarfá 12. Go deimhin, Rust’s
Is é 24 an freagra: sin líon na mbeart a thógann sé chun “Здравствуйте” a ionchódú i
UTF-8, toisc go dtógann gach luach scálach Unicode sa téad sin 2 byte de
stórála. Mar sin, ní bheidh comhghaolú i gcónaí ag innéacs isteach i mbeart na sreinge
chuig luach scálach Unicode bailí. Chun a léiriú, smaoinigh ar an meirge neamhbhailí seo
cód:

```rust,ignore,does_not_compile
let hello = "Здравствуйте";
let answer = &hello[0];
```

Tá a fhios agat cheana féin nach `З` a bheidh i `answer`, an chéad litir. Nuair a ionchódaithe
in UTF-8, is é `208` an chéad bheart de `З` agus`151` an dara beart, mar sin bheadh
is cosúil gur cheart go mbeadh `208` mar `answer`, ach ní carachtar bailí é `208`
ar a shon féin. Is dócha nach mbeadh an t-úsáideoir ag iarraidh dá n-iarrfadh siad `208` a thabhairt ar ais
don chéad litir den téad seo; áfach, sin iad na sonraí amháin go Rust
tá ag innéacs beart 0. Go ginearálta ní bhíonn úsáideoirí ag iarraidh an luach beart a thabhairt ar ais, fiú
mura bhfuil sa teaghrán ach litreacha Laidine: dá mba chód bailí é `&"hi"[0]` sin
ar ais an luach beart, thabharfadh sé ar ais `104`, ní `h`.

Is é an freagra, mar sin, ná chun luach agus cúis gan choinne a sheachaint
fabhtanna nach bhfaighfear amach láithreach, ní thiomsaíonn Rust an cód seo
ar chor ar bith agus seachnaíonn sé míthuiscintí go luath sa phróiseas forbartha.

#### Beart agus Luachanna Scalaracha agus Cnuasaigh Ghraifim! Ó Mo!

Pointe eile faoi UTF-8 ná go bhfuil trí bhealach ábhartha ann i ndáiríre
breathnú ar teaghráin ó thaobh Rust: mar bhearta, luachanna scálach, agus grapheme
cnuasaigh (an rud is gaire don rud a thabharfaimis _letters_).

Má bhreathnaíonn muid ar an bhfocal Hiondúis “नमस्ते” scríofa sa script Devanagari, is é
stóráilte mar veicteoir de luachanna `u8` a bhreathnaíonn mar seo:

```text
[224, 164, 168, 224, 164, 174, 224, 164, 184, 224, 165, 141, 224, 164, 164,
224, 165, 135]
```

Sin 18 beart agus sin é an chaoi a stórálann ríomhairí na sonraí seo ar deireadh. Má táimid ar
iad mar luachanna scálacha Unicode, agus is iad sin an cineál `char` atá ag Rust, iad sin
Breathnaíonn bytes mar seo:

```text
['न', 'म', 'स', '्', 'त', 'े']
```

Tá sé luach `char` anseo, ach ní litreacha iad an ceathrú agus an séú ceann:
is diacritics iad nach bhfuil ciall acu leo ​​féin. Ar deireadh, má táimid ar
iad mar bhraislí grapheme, gheobhaimid an rud a thabharfadh duine ar na ceithre litir
a dhéanann suas an focal Hiondúis:

```text
["न", "म", "स्", "ते"]
```

Soláthraíonn meirge bealaí éagsúla chun na sonraí teaghrán amh a dhéanann ríomhairí a léirmhíniú
stóráil ionas gur féidir le gach clár an léiriú a theastaíonn uaidh a roghnú, is cuma
cén teanga dhaonna ina bhfuil na sonraí.

Cúis dheiridh nach ligeann Rust dúinn innéacsú a dhéanamh i `String` chun a
Is é an carachtar ná go bhfuiltear ag súil go dtógfaidh oibríochtaí innéacsaithe am seasta i gcónaí
(O(1)). Ach ní féidir a ráthú go bhfuil feidhmíocht le `String`,
toisc go mbeadh ar Rust siúl tríd an ábhar ón tús go dtí an
innéacs lena fháil amach cé mhéad carachtar bailí a bhí ann.

### Teaghráin slicing

Is minic gur droch-smaoineamh é innéacsú i sreang mar ní léir cad é an
ba cheart go mbeadh cineál aischuir na hoibríochta innéacsaithe teaghrán mar seo a leanas: luach beart, a
carachtar, braisle grapheme, nó slisne teaghrán. Más gá duit a úsáid i ndáiríre
innéacsanna chun slisní teaghrán a chruthú, mar sin, iarrann Rust ort a bheith níos sainiúla.

Seachas `[]` a úsáid le huimhir shingil, is féidir leat `[]` a úsáid le a
raon chun sliseog teaghrán a chruthú ina mbeidh bearta ar leith:

```rust
let hello = "Здравствуйте";

let s = &hello[0..4];
```

Anseo, beidh `s` ina `&str` ina mbeidh na chéad cheithre beart den téad.
Níos luaithe, luaigh muid go raibh gach ceann de na carachtair dhá bytes, rud a chiallaíonn
beidh `s` `Зд`.

Dá ndéanfaimis iarracht gan ach cuid de bhearta carachtar a ghearradh le rud éigin mar
`&hello[0..1]`, bheadh ​​scaoll ar Rust faoin am rite ar an mbealach céanna agus dá mbeadh sé neamhbhailí
Rinneadh rochtain ar innéacs i veicteoir:

```console
{{#include ../../listings/ch08-common-collections/output-only-01-not-char-boundary/output.txt}}
```

Ba chóir duit a bheith cúramach nuair a chruthú slices teaghrán le raonta, mar gheall ar a dhéanamh
mar sin is féidir tuairteála do chlár.

### Modhanna chun atriall thar Teaghráin

Is é an bealach is fearr chun oibriú ar phíosaí teaghráin ná a bheith soiléir faoi cé acu an bhfuil nó nach bhfuil
tá carachtair nó beart uait. Le haghaidh luachanna scálacha Unicode aonair, bain úsáid as an
modh `chars`. Má ghlaoitear `chars` ar “Зд” scartar amach agus cuireann sé ar ais dhá luach de
clóscríobh `char`, agus is féidir leat an toradh a athrá chun rochtain a fháil ar gach eilimint:

```rust
for c in "Зд".chars() {
    println!("{c}");
}
```

Déanfaidh an cód seo na rudaí seo a leanas a phriontáil:

```text
З
д
```

De rogha air sin, cuireann an modh `bytes` gach beart amh ar ais, agus b'fhéidir gurb é sin
oiriúnach do d'fhearann:

```rust
for b in "Зд".bytes() {
    println!("{b}");
}
```

Déanfaidh an cód seo na ceithre bheart a chuimsíonn an teaghrán seo a phriontáil:

```text
208
151
208
180
```

Ach a bheith cinnte a mheabhrú go bhféadfadh luachanna scálach Unicode bailí a bheith comhdhéanta de níos mó
ná beart amháin.

Is éard atá i gceist le braislí grapheme a fháil ó theaghráin, mar atá le script Devanagari
casta, mar sin ní sholáthraíonn an leabharlann chaighdeánach an fheidhmiúlacht seo. cliathbhoscaí
ar fáil ar [crates.io]( https://crates.io/) <!-- neamhaird --> más é seo an
feidhmiúlacht atá uait.

### Níl Teaghráin Chomh Simplí sin

Mar achoimre, tá teaghráin casta. Déanann teangacha cláir éagsúla
roghanna éagsúla maidir le conas an chastacht seo a chur i láthair don ríomhchláraitheoir. Meirge
roghnaigh láimhseáil cheart sonraí `String` an t-iompar réamhshocraithe
do gach clár Rust, rud a chiallaíonn go gcaithfidh ríomhchláraitheoirí níos mó machnaimh a dhéanamh
láimhseáil sonraí UTF-8 roimh ré. Léiríonn an chomhbhabhtáil seo níos mó de chastacht na
teaghráin ná mar is léir i dteangacha ríomhchlárúcháin eile, ach cuireann sé cosc ​​ort
ó bheith ort earráidí a bhaineann le carachtair neamh-ASCII a láimhseáil níos déanaí i do
saolré forbartha.

Is é an dea-scéal ná go dtugann an leabharlann chaighdeánach go leor feidhmiúlacht tógtha
as na cineálacha `String` agus `&str` chun cabhrú leis na cásanna casta seo a láimhseáil
i gceart. Bí cinnte a sheiceáil amach an doiciméadú le haghaidh modhanna úsáideacha mar
`contains` le haghaidh cuardach i teaghrán agus `replace` chun codanna de a
téad le teaghrán eile.

Aistrímid chuig rud éigin nach bhfuil chomh casta: léarscáileanna hash!