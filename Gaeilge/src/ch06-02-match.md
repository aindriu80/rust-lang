<!-- Sean-cheannteideal. Ná bain amach nó seans go mbrisfidh naisc. -->

<a id="the-match-control-flow-operator"></a>

## An "match" Tógáil Sreabhadh Rialaithe

Tá struchtúr sreafa rialaithe thar a bheith cumhachtach ag Rust ar a dtugtar `match` sin
ligeann duit luach a chur i gcomparáid le sraith patrún agus ansin a fhorghníomhú
cód bunaithe ar an patrún a oireann. Is féidir le patrúin a bheith comhdhéanta de luachanna litriúla,
ainmneacha athraitheacha, saoróga, agus go leor rudaí eile; [Caibidil
19][ch19-00-patterns]<!-- neamhaird --> clúdaíonn sé na cineálacha éagsúla patrún go léir
agus cad a dhéanann siad. Tagann cumhacht `match` as sainiúlacht an
patrúin agus ar an bhfíric go ndeimhníonn an tiomsaitheoir go bhfuil gach cás féideartha
láimhsithe.

Smaoinigh ar shloinneadh `match` a bheith cosúil le meaisín sórtála boinn: sleamhnaíonn boinn
síos rian le poill de mhéideanna éagsúla ar a feadh, agus titeann gach bonn tríd
an chéad pholl a bhuaileann sé a luíonn sé isteach. Ar an mbealach céanna, téann luachanna
trí gach patrún i `match`, agus ag an gcéad phatrún "oireann,"
titeann an luach isteach sa bhloc cód gaolmhar atá le húsáid le linn forghníomhaithe.

Ag labhairt di ar bhoinn, déanaimis iad a úsáid mar shampla ag baint úsáide as `match`! Is féidir linn scríobh a
feidhm a ghlacann bonn SAM anaithnid agus, ar bhealach cosúil leis an gcomhaireamh
meaisín, socraíonn sé cén bonn atá ann agus cuireann sé a luach ar ais ina cent, mar a thaispeántar
i Liosta 6-3.

<Listing number="6-3" caption="An enum and a `match` expression that has the variants of the enum as its patterns">

```rust
{{#rustdoc_include ../../listings/ch06-enums-and-pattern-matching/listing-06-03/src/main.rs:here}}
```

</Listing>

Déanaimis miondealú ar an `match` san fheidhm `value_in_cents`. Ar dtús déanaimid liosta
an eochairfhocal `match` agus slonn ina dhiaidh sin, arb é an luach é sa chás seo
`coin`. Dealraíonn sé seo an-chosúil le slonn coinníollach a úsáidtear le `if`, ach
tá difríocht mhór ann: le `if`, is gá an riocht a mheas go dtí a
Luach Boole, ach anseo is féidir é a bheith de chineál ar bith. An cineál `coin` sa sampla seo
is é an `Coin` enum a shainmhíníomar ar an gcéad líne.

Ina dhiaidh sin tá na hairm `match`. Tá dhá chuid ag lámh: patrún agus roinnt cód. Tá an
tá patrún sa chéad lámh anseo arb é an luach `Coin::Penny` agus ansin an `=>`
oibreoir a scarann ​​an patrún agus an cód a rith. An cód sa chás seo
níl ann ach an luach `1`. Tá gach lámh scartha ón gcéad cheann eile le camóg.

Nuair a fheidhmíonn an slonn `match`, déanann sé an luach iarmhartach a chur i gcomparáid le
patrún gach lámh, in ord. Má mheaitseálann patrún leis an luach, an cód
a bhaineann leis an bpatrún sin a fhorghníomhú. Mura n-oireann an patrún sin leis an
luach, leanann an forghníomhú ar aghaidh go dtí an chéad lámh eile, an oiread agus is i meaisín sórtála mona.
Is féidir linn an oiread arm agus is gá a bheith againn: i Liosta 6-3, tá ceithre lámh ag ár `match`.

Is slonn é an cód a bhaineann le gach lámh, agus an luach iarmhartach de
is é an slonn sa lámh meaitseála an luach a fhaightear ar ais don
abairt `match` ar fad.

De ghnáth ní úsáidimid lúibíní curacha má tá cód lámh an chluiche gearr, mar atá sé
i Liosta 6-3 áit nach dtugann gach lámh ach luach ar ais. Más mian leat a reáchtáil iolrach
línte cód i lámh cluiche, ní mór duit úsáid a bhaint as lúibíní chatach, agus an camóg
Tá leanúint na láimhe roghnach ansin. Mar shampla, priontaí an cód seo a leanas
"Pingin an t-ádh!" gach uair a thugtar an modh le `Coin::Penny`, ach fós
seo ar ais luach deiridh an bhloic, `1`:

```rust
{{#rustdoc_include ../../listings/ch06-enums-and-pattern-matching/no-listing-08-match-arm-multiple-lines/src/main.rs:here}}
```

### Patrúin a Cheanglaíonn Luachanna

Gné úsáideach eile a bhaineann le hairm mheaitseála ná gur féidir leo ceangal a dhéanamh le codanna an
luachanna a mheaitseálann an patrún. Seo mar is féidir linn luachanna a bhaint as enum
athraithigh.

Mar shampla, déanaimis ceann dár n-athraithigh enum a athrú chun sonraí a choinneáil istigh ann.
Ó 1999 go dtí 2008, bhuail na Stáit Aontaithe cheathrú le éagsúla
dearaí do gach ceann de na 50 stát ar thaobh amháin. Ní bhfuair aon bhoinn eile an stát
dearaí, mar sin níl ach an luach breise seo ag ceathrúna. Is féidir linn an fhaisnéis seo a chur le
ár `enum` tríd an leagan `Quarter` a athrú chun luach `UsState` a chur san áireamh
stóráilte istigh ann, rud atá déanta againn i Liostú 6-4.

<Listing number="6-4" caption="A `Coin` enum in which the `Quarter` variant also holds a `UsState` value">

```rust
{{#rustdoc_include ../../listings/ch06-enums-and-pattern-matching/listing-06-04/src/main.rs:here}}
```

</Listing>

Samhlóimis go bhfuil cara ag iarraidh na 50 ceathrú stáit ar fad a bhailiú. Cé go
Déanaimid ár n-athrú scaoilte a shórtáil de réir cineáil boinn, glaofaimid amach freisin ainm an
luaigh baint aige le gach ráithe ionas más ceann é nach bhfuil ag ár gcara,
is féidir leo é a chur lena mbailiúchán.

Sa slonn meaitseála don chód seo, cuirimid athróg darb ainm `state` leis an
patrún a mheaitseálann luachanna an leagain `Coin::Quarter`. Nuair a
Meaitseálann `Coin::Quarter`, beidh an athróg `state` ina gceangal leis an luach sin
stát ceathrú. Ansin is féidir linn `state` a úsáid sa chód don lámh sin, mar sin:

```rust
{{#rustdoc_include ../../listings/ch06-enums-and-pattern-matching/no-listing-09-variable-in-pattern/src/main.rs:here}}
```

Dá gcuirfimid `value_in_cents(Coin::Quarter(UsState::Alaska))`, `coin`
bheadh ​​`Coin::Quarter(UsState::Alaska)`. Nuair a dhéanaimid an luach sin i gcomparáid le gach ceann acu
de na hairm chluiche, ní mheaitseálann aon cheann acu go dtí go sroicheann muid `Coin::Quarter(state)`. Ag
an pointe sin, is é an luach `UsState::Alaska` a bheidh mar cheangal ar `state`. Is féidir linn
ansin bain úsáid as an gceangal sin sa slonn `println!`, mar sin faigh an taobh istigh
luaigh luach amach as an malairt `coin` enum le haghaidh `Quarter`.

### Ag meaitseáil le `Option<T>`

San alt roimhe seo, bhíomar ag iarraidh an luach `T` istigh a bhaint as an `Some`
cás agus `Option<T>` in úsáid; is féidir linn `Option<T>` a láimhseáil freisin ag baint úsáide as `match`, mar
rinne muid leis an `Coin` enum! In ionad boinn a chur i gcomparáid, déanfaimid comparáid idir na
leaganacha de `Option<T>`, ach fanann an bealach a oibríonn an slonn `match` mar an gcéanna
céanna.

Ligean le rá gur mhaith linn feidhm a scríobh a ghlacann `Option<i32>` agus, más rud é
tá luach istigh, cuireann sé 1 leis an luach sin. Mura bhfuil luach istigh ann,
ba chóir don fheidhm an luach `None` a thabhairt ar ais agus gan iarracht a dhéanamh aon cheann a dhéanamh
oibríochtaí.

Tá an fheidhm seo an-éasca a scríobh, a bhuíochas sin do `match`, agus beidh cuma mhaith
Liostáil 6-5.

<Listing number="6-5" caption="A function that uses a `match` expression on an `Option<i32>`">

```rust
{{#rustdoc_include ../../listings/ch06-enums-and-pattern-matching/listing-06-05/src/main.rs:here}}
```

</Listing>

Déanaimis scrúdú níos mine ar an gcéad fhorghníomhú de `plus_one`. Nuair a ghlaoimid
`plus_one(five)`, beidh an athróg `x` i gcorp `plus_one`
luach `Some(5)`. Déanaimid é sin a chur i gcomparáid le gach lámh cluiche:

```rust,ignore
{{#rustdoc_include ../../listings/ch06-enums-and-pattern-matching/listing-06-05/src/main.rs:first_arm}}
```

Ní mheaitseálann an luach `Some(5)` an patrún `None`, mar sin leanaimid ar aghaidh chuig an
lámh eile:

```rust,ignore
{{#rustdoc_include ../../listings/ch06-enums-and-pattern-matching/listing-06-05/src/main.rs:second_arm}}
```

An meaitseálann `Some(5)``Some(i)`? Déanann sé! Tá an leagan céanna againn. Tá an `i`
ceanglaíonn sé leis an luach atá i `Some`, mar sin glacann `i` an luach `5`. An cód i
déantar lámh an chluiche ansin, mar sin cuirimid 1 le luach `i` agus cruthaímid a
luach `Some` nua lenár `6` iomlán istigh.

Anois déanaimis machnamh ar an dara glao ar `plus_one` i Liostú 6-5, áit a bhfuil `x`
`None`. Cuirimid isteach sa `match` agus cuirimid i gcomparáid leis an gcéad lámh:

```rust,ignore
{{#rustdoc_include ../../listings/ch06-enums-and-pattern-matching/listing-06-05/src/main.rs:first_arm}}
```

Meaitseálann sé! Níl aon luach le cur leis, mar sin stopann an clár agus seolann sé an
luach `none` ar thaobh na láimhe deise de `=>`. Mar gheall ar mheaitseáil an chéad lámh, ní eile
déantar comparáid idir airm.

Tá sé úsáideach 'meaitseáil' agus enums a chomhcheangal i go leor cásanna. Feicfidh tú é seo
patrún go leor sa chód meirge: `match` i gcoinne enum, ceangail athróg leis an
sonraí taobh istigh, agus ansin a fhorghníomhú cód bunaithe ar sé. Tá sé beagán tricky ar dtús, ach
a luaithe a rachaidh tú i dtaithí air, ba mhaith leat go mbeadh sé agat i ngach teanga. Tá sé
go seasta is fearr leat úsáideoir.

### Tá Meaitseálacha Uileghabhálach

Tá gné amháin eile den ‘mheaitseáil’ ar gá dúinn a phlé: ní mór patrúin na n-arm
gach féidearthacht a chlúdach. Smaoinigh ar an leagan seo dár bhfeidhm `plus_one`,
a bhfuil fabht aige agus nach dtiomsóidh:

```rust,ignore,does_not_compile
{{#rustdoc_include ../../listings/ch06-enums-and-pattern-matching/no-listing-10-non-exhaustive-match/src/main.rs:here}}
```

Níor láimhseáil muid an cás `None`, mar sin cruthóidh an cód seo fabht. Ar ámharaí an tsaoil, tá
fabht Tá a fhios ag Rust conas a ghabháil. Má dhéanaimid iarracht an cód seo a thiomsú, gheobhaidh muid é
earráid:

```console
{{#include ../../listings/ch06-enums-and-pattern-matching/no-listing-10-non-exhaustive-match/output.txt}}
```

Tá a fhios ag Rust nár chlúdaigh muid gach cás féideartha, agus tá a fhios aige fiú cé acu
patrún dearmadta againn! Tá meaitseanna meirge _uileghabhálach_: ní mór dúinn gach ceann deireanach a sceite
féidearthacht ionas go mbeidh an cód bailí. Go háirithe i gcás
`Option<T>`, nuair a chuireann Rust cosc ​​orainn dearmad a dhéanamh ar an
‘Gan cás’, cosnaíonn sé sinn ó bheith ag glacadh leis go bhfuil luach againn nuair a d’fhéadfaimis
bheith ar neamhní, rud a fhágann go bhfuil an botún billiún dollar a pléadh níos luaithe dodhéanta.

### Patrúin Catch-All agus an Sealbhóir Áite `_`

Ag baint úsáide as enums, is féidir linn a ghlacadh freisin gníomhartha speisialta le haghaidh cúpla luachanna ar leith, ach
do gach luach eile déan beart réamhshocraithe amháin. Samhlaigh go bhfuil cluiche á chur i bhfeidhm againn
más rud é, má rollaíonn tú 3 ar rolla dísle, ní bhogann d'imreoir, ach ina ionad sin
Faigheann hata mhaisiúil nua. Má rollaíonn tú 7, cailleann d'imreoir hata mhaisiúil. Do chách
luachanna eile, bogann d'imreoir an líon sin spásanna ar an gclár cluiche. Seo chugaibh
`match` a chuireann an loighic sin i bhfeidhm, le toradh an rolla dísle
hardcoded seachas luach randamach, agus gach loighic eile ionadaíocht ag
feidhmeanna gan chomhlachtaí toisc go bhfuil cur chun feidhme iarbhír na bhfeidhmeanna sin lasmuigh den scóip le haghaidh
an sampla seo:

```rust
{{#rustdoc_include ../../listings/ch06-enums-and-pattern-matching/no-listing-15-binding-catchall/src/main.rs:here}}
```

Don chéad dá lámh, is iad na patrúin na luachanna litriúla `3` agus `7`. Le haghaidh
an lámh deiridh a chlúdaíonn gach luach féideartha eile, is é an patrún an
athróg atá roghnaithe againn chun `other` a ainmniú. An cód a ritheann don lámh `other`
Úsáideann sé an athróg trína chur ar aghaidh chuig an bhfeidhm `move_player`.

Tiomsaítear an cód seo, cé nach bhfuil na luachanna féideartha go léir liostaithe againn a
Is féidir le `u8` a bheith agat, mar beidh an patrún deireanach ag teacht le gach luach nach bhfuil go sonrach
liostaithe. Comhlíonann an patrún uileghabhálach seo an riachtanas nach mór `match` a bheith ann
uileghabhálach. Tabhair faoi deara go gcaithfimid an lámh iomlán a chur suas go deireanach mar go bhfuil an
déantar patrúin a mheas in ord. Má chuir muid an lámh ghabháil-uile níos luaithe, an ceann eile
ní rithfeadh airm choíche, mar sin tabharfaidh Rust foláireamh dúinn má chuirimid airm leis tar éis gach rud!

Tá patrún ag meirge freisin ar féidir linn a úsáid nuair a theastaíonn uainn go mbeidh gach rud againn ach nach dteastaíonn uainn
_use_ an luach sa phatrún uileghabhálach: Is patrún speisialta é `_` a mheaitseálann
luach ar bith agus ní cheanglaíonn sé leis an luach sin. Insíonn sé seo do Rust nach bhfuilimid chun
bain úsáid as an luach, mar sin ní thabharfaidh Rust rabhadh dúinn faoi athróg nár úsáideadh.

Athróimid rialacha an chluiche: anois, má rollaíonn tú rud ar bith seachas 3 nó
a 7, ní mór duit rolladh arís. Ní gá dúinn an luach uileghabhálach a úsáid a thuilleadh, mar sin ní mór dúinn
Is féidir ár gcód a athrú chun `_` a úsáid in ionad na hathróige darb ainm `other`:

```rust
{{#rustdoc_include ../../listings/ch06-enums-and-pattern-matching/no-listing-16-underscore-catchall/src/main.rs:here}}
```

Comhlíonann an sampla seo an riachtanas uileghabhálachta freisin toisc go bhfuilimid go sainráite
neamhaird a dhéanamh ar gach luach eile sa lámh dheireanach; níl dearmad déanta againn ar rud ar bith.

Ar deireadh, athróimid rialacha an chluiche arís eile ionas nach mbeidh aon rud eile ann
a tharlaíonn ar do sheal má rollaíonn tú rud ar bith seachas 3 nó 7. Is féidir linn a chur in iúl
sin trí úsáid a bhaint as an luach aonaid (an cineál tuple folamh a luaigh muid in [“The Tuple
Cineál”][tuples] <!-- neamhaird a dhéanamh --> alt) mar an cód a théann leis an lámh `_`:

```rust
{{#rustdoc_include ../../listings/ch06-enums-and-pattern-matching/no-listing-17-underscore-unit/src/main.rs:here}}
```

Anseo, táimid ag insint do Rust go sainráite nach bhfuilimid chun aon luach eile a úsáid
nach bhfuil ag teacht le patrún i lámh níos luaithe, agus nílimid ag iarraidh aon cheann a rith
cód sa chás seo.

Tá níos mó faoi phatrúin agus faoi mheaitseáil a chlúdóimid i [Caibidil
19][ch19-00-patterns]<!-- neamhaird a dhéanamh -->. Faoi láthair, táimid ag dul ar aghaidh go dtí an
comhréir `if let`, is féidir a bheith úsáideach i gcásanna ina bhfuil an slonn `match`
rud beag focal.

[tuples]: ch03-02-data-types.html#the-tuple-type
[ch19-00-patterns]: ch19-00-patterns.html
