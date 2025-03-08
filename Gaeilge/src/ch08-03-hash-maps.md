## Eochracha le Luachanna Gaolmhara a Stóráil i Léarscáileanna Hash

Is é an _hash map_ an ceann deireanach dár mbailiúcháin choiteanna. An cineál `HashMap<K, V>`
stórálann sé mapáil d'eochracha den chineál `K` le luachanna de chineál `V` ag baint úsáide as _hashing
function_, a chinneann conas a chuireann sé na heochracha agus na luachanna seo i gcuimhne.
Tacaíonn go leor teangacha ríomhchláraithe leis an gcineál seo struchtúr sonraí, ach is minic a bhíonn siad
úsáid ainm eile, mar shampla _hash_, _map_, _object_, _hash table_,
_dictionary_, nó _associative array_, gan ach roinnt a ainmniú.

Tá léarscáileanna hash úsáideach nuair is mian leat sonraí a chuardach ní trí innéacs a úsáid, mar
is féidir leat le veicteoirí, ach ag baint úsáide as eochair is féidir a bheith de chineál ar bith. Mar shampla,
i gcluiche, d’fhéadfá súil a choinneáil ar scór gach foirne ar léarscáil hash ina bhfuil
is ainm foirne é gach eochair agus is ionann na luachanna agus scór gach foirne. Tugtar foireann
ainm, is féidir leat a scór a fháil ar ais.

Rachaimid thar an API bunúsach de léarscáileanna hash sa chuid seo, ach go leor rudaí eile
folaithe sna feidhmeanna atá sainmhínithe ar `HashMap<K, V>` ag an leabharlann chaighdeánach.
Mar is gnáth, seiceáil na doiciméid chaighdeánacha leabharlainne le haghaidh tuilleadh eolais.

### Hash Léarscáil Nua a Chruthú

Bealach amháin le léarscáil hash folamh a chruthú ná `new` a úsáid agus gnéithe a chur leis
`insert`. I Liostáil 8-20, táimid ag coinneáil súil ar scóir dhá fhoireann a bhfuil
is iad na hainmneacha _Gorm_ agus _Buí_. Tosaíonn an fhoireann Gorm le 10 bpointe, agus an
Tosaíonn foireann buí le 50.

<Listing number="8-20" caption="Creating a new hash map and inserting some keys and values">

```rust
{{#rustdoc_include ../../listings/ch08-common-collections/listing-08-20/src/main.rs:here}}
```

</Listing>

Tabhair faoi deara go gcaithfimid an `HashMap` a úsáid ar dtús ón gcuid bailiúcháin de
an leabharlann caighdeánach. As ár dtrí bhailiúchán coitianta, is é an ceann seo an ceann is lú
a úsáidtear go minic, mar sin níl sé san áireamh sna gnéithe a thugtar isteach sa raon feidhme
go huathoibríoch sa réamhrá. Tá níos lú tacaíochta ag léarscáileanna hash freisin ó na
leabharlann caighdeánach; níl aon mhacra ionsuite ann chun iad a thógáil, mar shampla.

Díreach cosúil le veicteoirí, stórálann léarscáileanna hash a gcuid sonraí ar an gcarn. Tá an `HashMap` seo
eochracha den chineál `String` agus luachanna an chineáil `i32`. Cosúil le veicteoirí, tá léarscáileanna hash
aonchineálach: caithfidh an cineál céanna a bheith ag gach ceann de na heochracha, agus na luachanna go léir
Ní mór go mbeadh an cineál céanna.

### Ag fáil rochtana ar Luachanna i Hash Léarscáil

Is féidir linn luach a fháil ón léarscáil hash trína eochair don `get`
modh, mar a thaispeántar i Liosta 8-21.

<Listing number="8-21" caption="Accessing the score for the Blue team stored in the hash map">

```rust
{{#rustdoc_include ../../listings/ch08-common-collections/listing-08-21/src/main.rs:here}}
```

</Listing>

Anseo, beidh an luach a bhaineann leis an bhfoireann Gorm ag `score`, agus an
Beidh an toradh `10`. Filleann an modh `get` `Option<&V>`; mura bhfuil
luach na heochair sin sa léarscáil hash, tabharfaidh `get` ar ais `None`. An clár seo
láimhseálann sé an `Option` trí ghlaoch ar `copied` chun `Option<i32>` a fháil seachas
`Option<&i32>`, ansin `unwrap_or` chun `score` a shocrú go nialas mura bhfuil `scores`
bíodh iontráil agat don eochair.

Is féidir linn athrá a dhéanamh ar gach péire eochairluacha ar léarscáil hash ar an mbealach céanna is a dhéanaimid
Déan le veicteoirí, ag baint úsáide as lúb `for`:

```rust
{{#rustdoc_include ../../listings/ch08-common-collections/no-listing-03-iterate-over-hashmap/src/main.rs:here}}
```

Déanfaidh an cód seo gach péire a phriontáil in ord treallach:

```text
Yellow: 50
Blue: 10
```

### Léarscáileanna Hash agus Úinéireacht

I gcás cineálacha a chuireann an trait `Copy` i bhfeidhm, mar `i32`, déantar na luachanna a chóipeáil
isteach sa léarscáil hash. I gcás luachanna faoi úinéireacht mar `String`, bogfar na luachanna agus
beidh an léarscáil hash ina úinéir ar na luachanna sin, mar a léirítear i Liosta 8-22.

<Listing number="8-22" caption="Showing that keys and values are owned by the hash map once they’re inserted">

```rust
{{#rustdoc_include ../../listings/ch08-common-collections/listing-08-22/src/main.rs:here}}
```

</Listing>

Nílimid in ann na hathróga `field_name` agus `field_value` a úsáid ina dhiaidh
tá siad bogtha isteach sa léarscáil hash leis an nglao `insert`.

Má chuirimid tagairtí do luachanna isteach sa léarscáil hash, ní bhogfar na luachanna
isteach sa léarscáil hash. Ní mór na luachanna a díríonn na tagairtí dóibh a bheith bailí ag
ar a laghad chomh fada agus atá an léarscáil hash bailí. Labhróimid níos mó faoi na ceisteanna seo i
an [“Tagairtí a Bhailíochtú le
Saoil”][bailíochtú-tagairtí-le-saoil]<!-- neamhaird a dhéanamh ar --> alt i
Caibidil 10 .

### Léarscáil Hash á nuashonrú

Cé gur féidir fás ar líon na bpéirí eochair agus luacha, is féidir le gach eochair uathúil
gan ach luach amháin a bheith bainteach leis ag an am (ach ní vice versa: do
Mar shampla, d'fhéadfadh an luach `10` a bheith ag an bhfoireann Gorm agus ag an bhfoireann Bhuí araon
stóráilte sa léarscáil hash `scores`).

Nuair is mian leat na sonraí a athrú i léarscáil hash, caithfidh tú cinneadh a dhéanamh conas
láimhseáil an cás nuair a bhíonn luach sannta ag eochair cheana féin. D'fhéadfá ionad an
luach d'aois leis an luach nua, go hiomlán neamhaird a dhéanamh ar an luach d'aois. D'fhéadfá
choinneáil ar an luach d'aois agus neamhaird a dhéanamh ar an luach nua, ach amháin ag cur an luach nua má tá an
eochair _níl_ luach aici cheana féin. Nó d’fhéadfá an seanluach agus an
luach nua. Breathnaímid ar conas gach ceann díobh seo a dhéanamh!

#### Luach a Fhorscríobh

Má chuirimid eochair agus luach isteach i léarscáil hash agus ansin cuir isteach an eochair chéanna
le luach difriúil, cuirfear an luach a bhaineann leis an eochair sin in ionad.
Cé go nglaonn an cód i Liostú 8-23 `insert` faoi dhó, beidh an léarscáil hash
níl ach péire eochairluacha amháin ann toisc go bhfuil luach an Ghorm á chur isteach againn
eochair na foirne an dá uair.

<Listing number="8-23" caption="Replacing a value stored with a particular key">

```rust
{{#rustdoc_include ../../listings/ch08-common-collections/listing-08-23/src/main.rs:here}}
```

</Listing>

Priontálfaidh an cód seo `{"Blue": 25}`. Tá luach bunaidh `10` curtha
forscríofa.

<!-- Old headings. Do not remove or links may break. -->

<a id="only-inserting-a-value-if-the-key-has-no-value"></a>

#### Ag Cur Eochair agus Luach Leis Mura bhfuil Eochair i Láthair

Is gnách seiceáil an bhfuil eochair ar leith sa léarscáil hash cheana féin
le luach agus ansin na gníomhartha seo a leanas a dhéanamh: má tá an eochair ann i
an léarscáil hash, ba cheart go bhfanfadh an luach reatha mar atá sé; má tá an eochair
nach bhfuil ann, cuir isteach é agus luach air.

Tá API speisialta ag léarscáileanna hash don `entry` seo a thógann an eochair duit
ag iarraidh a sheiceáil mar pharaiméadar. Is énum luach aischuir an mhodha `entry`
ar a dtugtar `Entry` a léiríonn luach a d'fhéadfadh a bheith ann nó nach bhféadfadh. Déarfainn
ba mhaith linn a sheiceáil an bhfuil luach ag baint leis an eochair don fhoireann Bhuí
leis. Mura ndéanann sé, ba mhaith linn an luach `50` a chur isteach, agus mar an gcéanna le haghaidh an
Foireann gorm. Ag baint úsáide as an `entry` API, tá an chuma ar an gcód Liostú 8-24.

<Listing number="8-24" caption="Using the `entry` method to only insert if the key does not already have a value">

```rust
{{#rustdoc_include ../../listings/ch08-common-collections/listing-08-24/src/main.rs:here}}
```

</Listing>

Sainmhínítear an modh `or_insert` ar `Entry` chun tagairt shochorraithe a thabhairt ar ais dó
an luach don eochair 'Iontráil' chomhfhreagrach má tá an eochair sin ann, agus mura bhfuil, é
cuireann sé an paraiméadar isteach mar an luach nua don eochair seo agus cuireann sé mutable ar ais
tagairt don luach nua. Tá an teicníc seo i bhfad níos glaine ná mar a scríobh an
loighic féin agus, ina theannta sin, imríonn níos nicely leis an seiceálaí iasachtaí.

Má ritheann tú an cód i Liostú 8-24, priontálfar `{"Yellow": 50, "Blue": 10}`. Tá an
cuirfidh an chéad ghlao ar `entry` isteach an eochair don fhoireann Bhuí leis an luach
`50` toisc nach bhfuil luach ag an bhfoireann Buí cheana féin. An dara glaoch chuig
Ní athróidh `entry` an léarscáil hash mar tá an t-ainm ag an bhfoireann Gorm cheana féin
luach `10`.

#### Luach Bunaithe ar an Seanluach a Nuashonrú

Cás úsáide coitianta eile le haghaidh léarscáileanna hash ná luach eochair a chuardach agus ansin
é a nuashonrú bunaithe ar an seanluach. Mar shampla, taispeánann Liostú 8-25 cód sin
comhaireamh cé mhéad uair gach focal le feiceáil i roinnt téacs. Bainimid úsáid as léarscáil hash le
na focail mar eochracha agus incrimint an luach súil a choinneáil ar cé mhéad uair atá againn
chonaic an focal sin. Más é seo an chéad uair a bhfuil focal feicthe againn, cuirfimid isteach ar dtús
an luach `0`.

<Listing number="8-25" caption="Counting occurrences of words using a hash map that stores words and counts">

```rust
{{#rustdoc_include ../../listings/ch08-common-collections/listing-08-25/src/main.rs:here}}
```

</Listing>

Priontálfaidh an cód seo `{"world": 2, "hello": 1, "wonderful": 1}`. Seans go bhfeicfeá
na péirí eochairluacha céanna priontáilte in ord difriúil: aisghairm ón
[“Luachanna a Rochtana i Hash Map”][access]<!-- neamhaird a dhéanamh ar --> alt sin
tarlaíonn atriall thar léarscáil hash in ord treallach.

Filleann an modh `split_whitespace` atriator thar fhomhíreanna, scartha le
spás bán, den luach i `text`. Filleann an modh `or_insert` comhshó
tagairt (`&mut V`) don luach don eochair shonraithe. Anseo, déanaimid é sin a stóráil
tagairt chomhshóite san athróg `count`, mar sin chun an luach sin a shannadh,
ní mór dúinn ar dtús tagairt a dhéanamh do `count` ag baint úsáide as an réiltín (`*`). An mutable
téann an tagairt as an scóip ag deireadh na lúb `for`, mar sin seo go léir
tá athruithe sábháilte agus ceadaithe ag na rialacha iasachtaithe.

### Feidhmeanna Hashing

De réir réamhshocraithe, úsáideann `HashMap` feidhm hashing ar a dtugtar _SipHash_ is féidir a sholáthar
frithsheasmhacht in aghaidh ionsaithe diúltaithe seirbhíse (DoS) a bhaineann le hash
táblaí[^siphash] <!-- neamhaird a dhéanamh -->. Ní hé seo an algartam hashing is tapúla
ar fáil, ach an trádáil-uaire le haghaidh slándála níos fearr a thagann leis an titim isteach
feidhmíocht is fiú é. Má tá tú próifíl do chód agus a fháil go bhfuil an réamhshocraithe
tá feidhm hash ró-mhall chun do chuspóirí, is féidir leat aistriú go feidhm eile
trí hasher difriúil a shonrú. Is cineál é _hasher_ a chuireann an
Tréith `BuildHasher`. Labhróimid faoi thréithe agus conas iad a chur i bhfeidhm
[Caibidil 10][traits]<!-- déan neamhaird de -->. Ní gá duit a chur i bhfeidhm
do hasher féin ón tús; [crates.io]( https://crates.io/) <!-- neamhaird -->
tá leabharlanna roinnte ag úsáideoirí Rust eile a sholáthraíonn hashers a chuireann go leor i bhfeidhm
halgartaim hashing coitianta.

[^siphash]: [ https://en.wikipedia.org/wiki/SipHash]( https://en.wikipedia.org/wiki/SipHash)

## Achoimre

Soláthróidh veicteoirí, teaghráin, agus léarscáileanna hash cuid mhór feidhmiúlachta
riachtanach i gcláir nuair is gá duit sonraí a stóráil, a rochtain agus a mhodhnú. Seo iad
roinnt cleachtaí ba chóir duit a bheith feistithe anois le réiteach:

1. Nuair a thugtar liosta slánuimhreacha, úsáid veicteoir agus cuir ar ais an t-airmheán (agus é sórtáilte,
 an luach sa suíomh lár) agus mód (an luach is mó a tharlaíonn
 go minic ; beidh léarscáil hash ina chuidiú anseo) den liosta.
1. Teaghráin a thiontú go Laidin muc. Bogtar an chéad chonsan de gach focal go dtí
 cuirtear deireadh an fhocail agus _ay_ leis, mar sin déantar _irst-fay_. Focail
 a thosaíonn le guta tar éis _hay_ a chur leis an deireadh ina ionad sin (éiríonn _apple_
 _apple-hay_). Coinnigh i gcuimhne na sonraí faoi ionchódú UTF-8!
1. Ag baint úsáide as léarscáil hash agus veicteoirí, cruthaigh comhéadan téacs chun ligean d'úsáideoir cur leis
 ainmneacha fostaithe do roinn i gcuideachta; mar shampla, “Cuir Sally le
 Innealtóireacht" nó "Cuir Amir le Díolacháin." Ansin lig an t-úsáideoir a fháil ar liosta de na
 daoine i roinn nó gach duine sa chuideachta de réir roinne, curtha in eagar
 in ord aibítre.

Déanann doiciméadú caighdeánach API na leabharlainne cur síos ar mhodhanna a veicteálann, teaghráin,
agus tá léarscáileanna hash a bheidh ina gcuidiú do na cleachtaí seo!

Táimid ag dul isteach i gcláir níos casta ina dteipfidh ar oibríochtaí, mar sin de
am iontach chun láimhseáil earráidí a phlé. Déanfaimid é sin chugainn!

[validating-references-with-lifetimes]: ch10-03-lifetime-syntax.html#validating-references-with-lifetimes
[access]: #accessing-values-in-a-hash-map
[traits]: ch10-02-traits.html