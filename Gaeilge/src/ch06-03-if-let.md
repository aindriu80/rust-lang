## Sreabhadh Rialaithe Gonta le `if let` agus `let else`

Ligeann an chomhréir `if let` duit `if` agus `let` a chur le chéile ar bhealach nach bhfuil chomh briathartha
láimhseáil luachanna a mheaitseálann patrún amháin agus neamhaird á déanamh ar an gcuid eile. Smaoinigh ar an
clár i Liostú 6-6 a mheaitseálann ar luach `Option<u8>` sa
athróg `config_max` ach ní theastaíonn uaidh cód a rith ach amháin más é an luach an `Some`
athraitheach.

<Listing number="6-6" caption="A `match` that only cares about executing code when the value is `Some`">

```rust
{{#rustdoc_include ../../listings/ch06-enums-and-pattern-matching/listing-06-06/src/main.rs:here}}
```

</Listing>

Más `Some` an luach, priontálaimid an luach sa leagan `Some` trí cheangal
an luach don athróg `max` sa phatrún. Nílimid ag iarraidh aon rud a dhéanamh
leis an luach `None`. Chun an slonn `match` a shásamh, caithfimid `_ => 
()` a chur leis tar éis, a phróiseáil ach malairt amháin, a bhfuil cód boilerplate annoying go
cuir.

Ina áit sin, d'fhéadfaimis é seo a scríobh ar bhealach níos giorra ag baint úsáide as `if let`. Seo a leanas
Iompraíonn an cód mar an gcéanna leis an `match`` i Liostú 6-6:

```rust
{{#rustdoc_include ../../listings/ch06-enums-and-pattern-matching/no-listing-12-if-let/src/main.rs:here}}
```

Glacann an chomhréir `if let` patrún agus slonn scartha le cothrom
comhartha. Oibríonn sé ar an mbealach céanna le `match`, áit a dtugtar an abairt do na
`match` agus is é an patrún a chéad lámh. Sa chás seo, tá an patrún
`Some(max)`, agus ceanglaíonn an `max` leis an luach taobh istigh den `Some`. Is féidir linn ansin
úsáid `max` i gcorp an bhloic `if let` ar an mbealach céanna a d'úsáid muid `max` in
an lámh `match` comhfhreagrach. Ní ritheann an cód sa bhloc `if let` ach amháin má tá an
meaitseálann luach an patrún.

Ciallaíonn úsáid `if let` níos lú clóscríobh, níos lú eangú, agus níos lú cód pláta coire.
Mar sin féin, caillfidh tú an seiceáil uileghabhálach a fhorfheidhmíonn `match`. Ag roghnú
idir `match` agus `if let` ag brath ar a bhfuil ar siúl agat i do chuid féin
an staid agus an bhfuil comhbhrón oiriúnach dó nó nach bhfuil
seiceáil uileghabhálach a chailleadh.

I bhfocail eile, is féidir leat smaoineamh ar `if let` mar shiúcra comhréire le haghaidh `match` sin
ritheann cód nuair a mheaitseálann an luach patrún amháin agus ansin neamhaird ar gach luach eile.

Is féidir linn `else` a chur san áireamh le `if let`. An bloc cód a théann leis an
is ionann `else` agus an bloc cód a rachadh leis an tuiseal `_` sa
`match` atá comhionann leis an abairt `if let` agus `else`. Athghairm an
Sainmhíniú `Coin` enum i Liosta 6-4, áit a raibh an leagan `Quarter`
luach `UsState`. Dá dteastódh uainn gach bonn neamhcheathrún a chomhaireamh feicimid agus sinn freisin
ag fógairt staid na ceathrún, d’fhéadfaimis é sin a dhéanamh le `match`
abairt, mar seo:

```rust
{{#rustdoc_include ../../listings/ch06-enums-and-pattern-matching/no-listing-13-count-and-announce-match/src/main.rs:here}}
```

Nó d’fhéadfaimis nath `if let` agus `else` a úsáid, mar seo:

```rust
{{#rustdoc_include ../../listings/ch06-enums-and-pattern-matching/no-listing-14-count-and-announce-if-let-else/src/main.rs:here}}
```

## Ag fanacht ar an “cosán sásta” le `let else`

Patrún coitianta amháin is ea roinnt ríomh a dhéanamh nuair a bhíonn luach i láthair agus
cuir luach réamhshocraithe ar ais ar shlí eile. Ag leanúint ar aghaidh lenár sampla de bhoinn le a
luach `UsState`, dá mbeimis ag iarraidh rud éigin greannmhar a rá ag brath ar cén aois an
stáit ar an ráithe a bhí, d'fhéadfadh muid a thabhairt isteach modh ar `UsState` a sheiceáil leis an
aois stáit, mar seo:

```rust
{{#rustdoc_include ../../listings/ch06-enums-and-pattern-matching/listing-06-07/src/main.rs:state}}
```

Ansin d'fhéadfaimis `if let` a úsáid chun an cineál bonn a mheaitseáil, agus `state` á thabhairt isteach
athraitheach laistigh de chorp an choinníll, mar atá i Liosta 6-7.

<Listing number="6-7" caption="Using" file-name="src/main.rs">

```rust
{{#rustdoc_include ../../listings/ch06-enums-and-pattern-matching/listing-06-07/src/main.rs:describe}}
```

</Listing>

Déanann sé sin an jab, ach tá sé tar éis an obair a bhrú isteach i gcorp an `if let`
ráiteas, agus má tá an obair atá le déanamh níos casta, b'fhéidir go mbeadh sé deacair
lean go beacht mar a bhaineann na craobhacha barrleibhéil. D’fhéadfaimis leas a bhaint as freisin
den fhíric go mbíonn luach ag na habairtí chun an `state` a tháirgeadh ó
an `if let` nó le filleadh go luath, mar atá i Liosta 6-8. (D'fhéadfá a leithéid a dhéanamh le a
`match`, ar ndóigh!)

<Listing number="6-8" caption="Using `if let` to produce a value or return early." file-name="src/main.rs">

```rust
{{#rustdoc_include ../../listings/ch06-enums-and-pattern-matching/listing-06-08/src/main.rs:describe}}
```

</Listing>

Tá sé seo beagán annoying a leanúint ina bhealach féin, áfach! Táirgeann brainse 
amháin den `if let` luach, agus filleann an ceann eile ón bhfeidhm go hiomlán.

Chun an patrún coitianta seo a dhéanamh níos deise a chur in iúl, tá `let`-`else` ag Rust. Tá an
glacann comhréir `let`-`else` patrún ar an taobh clé agus slonn ar an
ceart, an-chosúil le `if let`, ach níl brainse `if` aige, ach an
brainse `else`. Má mheaitseálann an patrún, ceangailfidh sé an luach ón bpatrún
sa raon feidhme lasmuigh. Má mheaitseálann an patrún _not_, sruthóidh an clár isteach
an lámh `else`, a chaithfidh filleadh ón bhfeidhm.

I Liostú 6-9, is féidir leat a fheiceáil conas a bhreathnaíonn Liostú 6-8 agus `let` -`else` in úsáid agat
áit `if let`. Tabhair faoi deara go bhfanann sé “ar an gcosán sona” i bpríomhchorp na
an fheidhm ar an mbealach seo, gan sreabhadh rialaithe go suntasach difriúil le haghaidh
dhá chraobh ar an mbealach a rinne an `if let`.

<Listing number="6-9" caption="Using `let`-`else` to clarify the flow through the function." file-name="src/main.rs">

```rust
{{#rustdoc_include ../../listings/ch06-enums-and-pattern-matching/listing-06-09/src/main.rs:describe}}
```

</Listing>

Má tá cás agat ina bhfuil loighic ag do chlár atá ró-bhriathartha le
cuir in iúl ag baint úsáide as `match`, cuimhnigh go bhfuil `if let` agus `let else` i do Rust
bosca uirlisí chomh maith.

## Achoimre

Táimid clúdaithe anois conas enums a úsáid chun cineálacha saincheaptha a chruthú a d’fhéadfadh a bheith mar cheann de a
sraith de luachanna áirimh. Thaispeánamar conas `Option<T>` na leabharlainne caighdeánach
cabhraíonn cineál leat an córas cineáil a úsáid chun earráidí a chosc. Nuair a bhíonn luachanna enum
sonraí taobh istigh díobh, is féidir leat `match` nó `if let` a úsáid chun iad sin a bhaint agus a úsáid
luachanna, ag brath ar cé mhéad cás is gá duit a láimhseáil.

Is féidir le do chláir Rust coincheapa a chur in iúl i d'fhearann ​​anois ag baint úsáide as struchtúir agus
éinim. Cinntíonn cruthú cineálacha saincheaptha le húsáid i do API sábháilteacht cineáil: an
Beidh tiomsaitheoir a dhéanamh cinnte do fheidhmeanna a fháil ach amháin luachanna den chineál gach
feidhm ag súil.

D'fhonn API dea-eagraithe a sholáthar do d'úsáideoirí atá simplí
a úsáid agus ní nochtar ach an méid go díreach a bheidh de dhíth ar d’úsáideoirí, déanaimis casadh anois air
Modúil meirge.

































