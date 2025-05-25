## Comhréir Patrúin

Sa chuid seo, bailímid an comhréir go léir atá bailí i bpatrúin agus pléimid cén fáth agus cathain a d'fhéadfá gach ceann acu a úsáid.

### Meaitseáil Litreacha

Mar a chonaic tú i gCaibidil 6, is féidir leat patrúin a mheaitseáil le litreacha go díreach. Tugann an cód seo a leanas roinnt samplaí:

```rust
{{#rustdoc_include ../../listings/ch19-patterns-and-matching/no-listing-01-literals/src/main.rs:here}}
```

Priontálann an cód seo `aon` mar go bhfuil an luach in `x` 1. Tá an comhréir seo úsáideach
nuair is mian leat go ndéanfadh do chód gníomh má fhaigheann sé luach coincréite ar leith.

### Athróga Ainmnithe a Mheaitseáil

Is patrúin dhochloíte iad athróga ainmnithe a mheaitseálann aon luach, agus tá siad úsáidte againn
go minic sa leabhar. Mar sin féin, bíonn deacracht ann nuair a úsáideann tú athróga ainmnithe in nathanna `match`, `if let`, nó `while let`. Toisc go dtosaíonn gach ceann de na cineálacha seo raon feidhme nua, cuirfidh athróga a dhearbhaítear mar chuid de phatrún
laistigh den abairt scáth ar na cinn leis an ainm céanna lasmuigh, mar atá
an cás le gach athróg. I Liosta 19-11, dearbhaímid athróg darb ainm
`x` leis an luach `Some(5)` agus athróg `y` leis an luach `10`. Ansin
cruthaímid abairt `match` ar an luach `x`. Féach ar na patrúin sa mheaitseáil
arms agus `println!` ag an deireadh, agus déan iarracht a dhéanamh amach cad a phriontálfaidh an cód
sula ritheann tú an cód seo nó sula léann tú tuilleadh.

<Listing number="19-11" file-name="src/main.rs" caption="A `match` expression with an arm that introduces a new variable which shadows an existing variable `y`">

```rust
{{#rustdoc_include ../../listings/ch19-patterns-and-matching/listing-19-11/src/main.rs:here}}
```

</Listing>

Déanaimis iniúchadh ar a tharlaíonn nuair a ritheann an abairt `match`. Ní mheaitseálann an patrún
sa chéad lámh mheaitseála an luach sainithe de `x`, mar sin leanann an cód
ar aghaidh.

Tugann an patrún sa dara lámh mheaitseála isteach athróg nua darb ainm `y` a
mheaitseálfaidh aon luach laistigh de luach `Some`. Ós rud é go bhfuilimid i raon feidhme nua laistigh
den abairt `match`, is athróg nua `y` í seo, ní an `y` a dhearbhaíomar ag an
tús leis an luach 10. Meaitseálfaidh an ceangal nua `y` seo aon luach
laistigh de `Some`, arb é atá againn in `x`. Dá bhrí sin, ceanglaíonn an `y` nua seo le
luach inmheánach an `Some` in `x`. Is é an luach sin `5`, mar sin forghníomhaítear agus priontálann an abairt don
lámh sin `Matched, y = 5`.

Dá mba luach `None` a bhí i `x` in ionad `Some(5)`, ní bheadh ​​na patrúin sna chéad
dhá lámh meaitseáilte, mar sin bheadh ​​an luach meaitseáilte leis an
fo-score. Níor thugamar isteach an athróg `x` i bpatrún na láimhe
fo-score, mar sin is é an `x` sa slonn an `x` seachtrach nach bhfuil
scátháilte. Sa chás hipitéiseach seo, phriontálfadh an `match` an cás `Default`, x = None`.

Nuair a bheidh an slonn `match` déanta, críochnaíonn a raon feidhme, agus mar sin críochnaíonn raon feidhme
an `y` istigh. Táirgeann an `println!` deireanach `at the end: x = Some(5), y = 10`.

Chun slonn `match` a chruthú a dhéanann comparáid idir luachanna an `x` sheachtraigh agus
`y`, seachas athróg nua a thabhairt isteach a scáthaíonn an athróg `y` atá ann cheana féin, bheadh ​​orainn coinníollach garda meaitseála a úsáid ina ionad. Labhróimid faoi ghardaí meaitseála níos déanaí sa chuid [“Coinníollach Breise le Gardaí
Meaitseála”](#extra-conditionals-with-match-guards)<!-- ignore -->.

### Patrúin Ilghnéitheacha

Is féidir leat patrúin iolracha a mheaitseáil ag baint úsáide as an gcomhréir `|`, arb é an t-oibreoir patrún _nó_ é. Mar shampla, sa chód seo a leanas, déanaimid luach `x` a mheaitseáil i gcoinne
na n-arm meaitseála, agus tá rogha _nó_ ag an gcéad cheann acu, rud a chiallaíonn má mheaitseálann luach
`x` ceachtar de na luachanna sa arm sin, rithfidh cód na láimhe sin:

```rust
{{#rustdoc_include ../../listings/ch19-patterns-and-matching/no-listing-02-multiple-patterns/src/main.rs:here}}
```

Priontálann an cód seo `ceann amháin nó dhó`.

### Raonta Luachanna a Mheaitseáil le `..=`

Ligeann comhréir `..=` dúinn raon luachanna cuimsitheacha a mheaitseáil. Sa
chód seo a leanas, nuair a mheaitseálann patrún aon cheann de na luachanna laistigh den raon tugtha, déanfaidh an lámh sin a fhorghníomhú:

```rust
{{#rustdoc_include ../../listings/ch19-patterns-and-matching/no-listing-03-ranges/src/main.rs:here}}
```

Más ionann `x` agus `1`, `2`, `3`, `4`, nó `5`, beidh an chéad lámh comhoiriúnach. Tá an comhréir seo níos áisiúla do luachanna meaitseála iolracha ná an t-oibreoir `|` a úsáid chun an
smaoineamh céanna a chur in iúl; dá n-úsáidfimis `|` bheadh ​​orainn `1 | 2 | 3 | 4 | 5` a shonrú.

Tá sé i bhfad níos giorra raon a shonrú, go háirithe más mian linn, abair, aon uimhir idir 1 agus 1,000 a mheaitseáil!

Seiceálann an tiomsaitheoir nach bhfuil an raon folamh ag am an tiomsaithe, agus toisc gurb iad na
cineálacha amháin ar féidir le Rust a rá an bhfuil raon folamh nó nach bhfuil ná `char` agus
luachanna uimhriúla, ní cheadaítear raonta ach le luachanna uimhriúla nó `char`.

Seo sampla ag baint úsáide as raonta de luachanna `char`:

```rust
{{#rustdoc_include ../../listings/ch19-patterns-and-matching/no-listing-04-ranges-of-char/src/main.rs:here}}
```

Is féidir le Rust a rá go bhfuil `'c'` laistigh de raon an chéad phatrúin agus priontáileann sé `early
ASCII letter`.

### Dístruchtúrú chun Luachanna a Bhriseadh óna chéile

Is féidir linn patrúin a úsáid freisin chun struchtúir, enums, agus tuples a dhístruchtúrú chun
codanna éagsúla de na luachanna seo a úsáid. Siúlaimis trí gach luach.

#### Struchtúir a Bhriseadh óna chéile

Taispeánann Liostáil 19-12 struchtúr `Point` le dhá réimse, `x` agus `y`, ar féidir linn
a bhriseadh óna chéile ag baint úsáide as patrún le ráiteas `let`.

<Listing number="19-12" file-name="src/main.rs" caption="Destructuring a struct’s fields into separate variables">

```rust
{{#rustdoc_include ../../listings/ch19-patterns-and-matching/listing-19-12/src/main.rs}}
```

</Listing>

Cruthaíonn an cód seo na hathróga `a` agus `b` a mheaitseálann luachanna na réimsí `x`
agus `y` den struchtúr `p`. Taispeánann an sampla seo nach gá go mbeadh ainmneacha na n-athróg sa phatrún ag teacht le hainmneacha réimsí an struchtúir.
Mar sin féin, is gnách ainmneacha na n-athróg a mheaitseáil le hainmneacha na réimsí chun go mbeidh sé
éasca cuimhneamh cé na hathróga a tháinig ó réimsí éagsúla. Mar gheall ar an
úsáid choitianta seo, agus toisc go bhfuil go leor dúblála i scríobh `let Point { x: x, y: y } = p;`, tá giorrúchán ag Rust do phatrúin a mheaitseálann réimsí struchtúir:
ní gá duit ach ainm an réimse struchtúir a liostáil, agus beidh na hainmneacha céanna ar na hathróga a cruthaíodh
ón bpatrún. Iompraíonn Liostáil 19-13 ar an mbealach céanna
leis an gcód i Liostáil 19-12, ach is iad na hathróga a cruthaíodh sa phatrún `let` ná `x` agus `y` in ionad `a` agus `b`.

<Listing number="19-13" file-name="src/main.rs" caption="Destructuring struct fields using struct field shorthand">

```rust
{{#rustdoc_include ../../listings/ch19-patterns-and-matching/listing-19-13/src/main.rs}}
```

</Listing>

Cruthaíonn an cód seo na hathróga `x` agus `y` a mheaitseálann na réimsí `x` agus `y` den athróg `p`. Is é an toradh ná go bhfuil na
luachanna ón struchtúr `p` sna hathróga `x` agus `y`.

Is féidir linn dístruchtúrú a dhéanamh le luachanna liteartha mar chuid den phatrún struchtúir
seachas athróga a chruthú do na réimsí go léir. Trí sin a dhéanamh, is féidir linn
cuid de na réimsí a thástáil le haghaidh luachanna áirithe agus athróga á gcruthú againn chun
na réimsí eile a dhístruchtúrú.

I Liosta 19-14, tá léiriú `match` againn a scarann ​​luachanna `Point`
i dtrí chás: pointí atá suite go díreach ar ais `x` (rud atá fíor nuair a
`y = 0`), ar ais `y` (`x = 0`), nó ceachtar acu.

<Listing number="19-14" file-name="src/main.rs" caption="Destructuring and matching literal values in one pattern">

```rust
{{#rustdoc_include ../../listings/ch19-patterns-and-matching/listing-19-14/src/main.rs:here}}
```

</Listing>

Déanfaidh an chéad lámh aon phointe atá suite ar an ais `x` a mheaitseáil trí shonrú go bhfuil an réimse `y` ag teacht leis má tá a luach ag teacht leis an liteartha `0`. Cruthaíonn an patrún athróg `x` fós is féidir linn a úsáid sa chód don lámh seo.

Ar an gcaoi chéanna, déanann an dara lámh aon phointe ar an ais `y` a mheaitseáil trí shonrú go bhfuil an réimse `x` ag teacht leis má tá a luach `0` agus cruthaíonn sí athróg `y` do luach an réimse `y`. Ní shonraíonn an tríú lámh aon liteartha, mar sin déanann sí aon `Point` eile a mheaitseáil agus cruthaíonn sí athróga do na réimsí `x` agus `y` araon.

Sa sampla seo, déanann an luach `p` an dara lámh a mheaitseáil de bhua `x` ina bhfuil 0, mar sin priontálfaidh an cód seo `On the y axis at 7`.

Cuimhnigh go stopann abairt `match` seiceáil arm a luaithe a aimsítear an
chéad phatrún meaitseála, mar sin cé go bhfuil `Point { x: 0, y: 0}` ar an ais `x`
agus an ais `y`, ní phriontálfadh an cód seo ach  `On the x axis at 0`.

#### Dístruchtúrú Áinimí

Tá dístruchtúrú déanta againn ar áinimí sa leabhar seo (mar shampla, Liostáil 6-5 i gCaibidil 6),
ach níor phléamar go sainráite fós go gcomhfhreagraíonn an patrún chun áinim a dhístruchtúrú
don chaoi a sainmhínítear na sonraí atá stóráilte laistigh den áinim. Mar
shampla, i Liostáil 19-15 úsáidimid an t-áinim `Message` ó Liostáil 6-2 agus scríobhaimid
`match` le patrúin a dhístruchtúróidh gach luach inmheánach.

<Listing number="19-15" file-name="src/main.rs" caption="Destructuring enum variants that hold different kinds of values">

```rust
{{#rustdoc_include ../../listings/ch19-patterns-and-matching/listing-19-15/src/main.rs}}
```

</Listing>

Priontálfaidh an cód seo `Change the color to red 0, green 160, and blue 255`. Bain triail as
luach `msg` a athrú chun an cód ó na hairm eile a fheiceáil.

I gcás malairtí enum gan aon sonraí, cosúil le `Message::Quit`, ní féidir linn an luach a dhístruchtúrú
tuilleadh. Ní féidir linn meaitseáil ach ar an luach liteartha `Message::Quit`,
agus níl aon athróga sa phatrún sin.

I gcás malairtí enum cosúil le struchtúr, mar shampla `Message::Move`, is féidir linn patrún a úsáid
cosúil leis an patrún a shonraímid chun struchtúir a mheaitseáil. Tar éis ainm an athraithe, cuirimid
lúibíní casta agus ansin liostaímid na réimsí le hathróga ionas go mbrisfimid óna chéile
na píosaí le húsáid sa chód don lámh seo. Anseo úsáidimid an fhoirm ghiorraithe mar
a rinneamar i Liostáil 19-13.

I gcás malairtí enum cosúil le tuplaí, cosúil le `Message::Write` a bhfuil tupla le heilimint amháin ann agus `Message::ChangeColor` a bhfuil tupla le trí eilimint ann, tá an
patrún cosúil leis an patrún a shonraímid chun tuplaí a mheaitseáil. Caithfidh líon na
n-athróg sa phatrún a bheith ag teacht le líon na n-eilimintí sa malairt atá á
mheaitseáil againn.

#### Struchtúir agus Enumaí Neadaithe a Scriosadh

Go dtí seo, bhí ár samplaí go léir ag meaitseáil struchtúir nó enumaí leibhéal amháin domhain,
ach is féidir meaitseáil a dhéanamh ar mhíreanna neadaithe freisin! Mar shampla, is féidir linn an
cód i Liostáil 19-15 a athfhachtóireacht chun tacú le dathanna RGB agus HSV sa teachtaireacht `ChangeColor`, mar a thaispeántar i Liostáil 19-16.

<Listing number="19-16" caption="Matching on nested enums">

```rust
{{#rustdoc_include ../../listings/ch19-patterns-and-matching/listing-19-16/src/main.rs}}
```

</Listing>

Meaitseálann patrún na chéad láimhe san abairt `match` malairt enum `Message::ChangeColor` ina bhfuil malairt `Color::Rgb`; ansin
ceanglaíonn an patrún leis na trí luach istigh `i32`. Meaitseálann patrún an dara
láimh malairt enum `Message::ChangeColor` freisin, ach meaitseálann an enum istigh `Color::Hsv` ina ionad. Is féidir linn na coinníollacha casta seo a shonrú in aon abairt amháin
`match`, cé go bhfuil dhá enum i gceist.

#### Struchtúir agus Tuplaí a Scriosadh

Is féidir linn patrúin dístruchtúrtha a mheascadh, a mheaitseáil agus a neadú ar bhealaí níos casta fós.
Léiríonn an sampla seo a leanas dístruchtúrú casta ina neadaímid struchtúir agus
tuplaí laistigh de thupla agus na luachanna primitive go léir a dhístruchtúrú amach:

```rust
{{#rustdoc_include ../../listings/ch19-patterns-and-matching/no-listing-05-destructuring-structs-and-tuples/src/main.rs:here}}
```

This code lets us break complex types into their component parts so we can use
the values we’re interested in separately.

Destructuring with patterns is a convenient way to use pieces of values, such
as the value from each field in a struct, separately from each other.

### Ignoring Values in a Pattern

You’ve seen that it’s sometimes useful to ignore values in a pattern, such as
in the last arm of a `match`, to get a catchall that doesn’t actually do
anything but does account for all remaining possible values. There are a few
ways to ignore entire values or parts of values in a pattern: using the `_`
pattern (which you’ve seen), using the `_` pattern within another pattern,
using a name that starts with an underscore, or using `..` to ignore remaining
parts of a value. Let’s explore how and why to use each of these patterns.

#### Ignoring an Entire Value with `_`

We’ve used the underscore as a wildcard pattern that will match any value but
not bind to the value. This is especially useful as the last arm in a `match`
expression, but we can also use it in any pattern, including function
parameters, as shown in Listing 19-17.

<Listing number="19-17" file-name="src/main.rs" caption="Using `_` in a function signature">

```rust
{{#rustdoc_include ../../listings/ch19-patterns-and-matching/listing-19-17/src/main.rs}}
```

</Listing>

Déanfaidh an cód seo neamhaird iomlán ar an luach `3` a ritheadh ​​mar an chéad argóint,
agus priontáilfidh sé `This code only uses the y parameter: 4`.

I bhformhór na gcásanna nuair nach bhfuil paraiméadar feidhme áirithe ag teastáil uait a thuilleadh,
d'athrófá an síniú ionas nach n-áireofar an paraiméadar neamhúsáidte ann. Is féidir neamhaird a dhéanamh ar
pharaiméadar feidhme a bheith úsáideach go háirithe i gcásanna nuair, mar shampla,
atá tú ag cur tréith i bhfeidhm nuair a bhíonn síniú cineáil áirithe ag teastáil uait ach nach bhfuil ceann de na paraiméadair ag teastáil ó
chorp na feidhme i do chur i bhfeidhm. Seachnaíonn tú ansin rabhadh tiomsaitheora a fháil faoi pharaiméadair feidhme neamhúsáidte, mar a dhéanfá
dá n-úsáidfeá ainm ina ionad.

#### Neamhaird a dhéanamh ar Chodanna de Luach le `_` Neadaithe

Is féidir linn `_` a úsáid laistigh de phatrún eile chun neamhaird a dhéanamh ar chuid de luach amháin,
mar shampla, nuair is mian linn tástáil a dhéanamh ar chuid de luach amháin ach nach bhfuil aon úsáid againn as na
codanna eile sa chód comhfhreagrach is mian linn a rith. Taispeánann liostú 19-18 an cód
atá freagrach as luach socraithe a bhainistiú. Is iad na ceanglais ghnó ná nach gceadaítear don úsáideoir saincheapadh atá ann cheana féin ar shocrú a athscríobh ach gur féidir leis an socrú a dhíshocrú agus luach a thabhairt dó mura bhfuil sé socraithe faoi láthair.

<Listing number="19-18" caption=" Using an underscore within patterns that match `Some` variants when we don’t need to use the value inside the `Some`">

```rust
{{#rustdoc_include ../../listings/ch19-patterns-and-matching/listing-19-18/src/main.rs:here}}
```

</Listing>

Priontálfaidh an cód seo `Can't overwrite an existing customized value` agus ansin
`setting is Some(5)` Sa chéad lámh mheaitseála, ní gá dúinn meaitseáil a dhéanamh ar na luachanna laistigh de cheachtar den dá chineál `Some` ná iad a úsáid, ach ní mór dúinn tástáil a dhéanamh don chás
nuair is iad `setting_value` agus `new_setting_value` an cineál `Some`. Sa
chás sin, priontálaimid an chúis gan `setting_value` a athrú, agus ní
athraítear é.

I ngach cás eile (más rud é go bhfuil `setting_value` nó `new_setting_value`
`None`) arna léiriú ag an bpatrún `_` sa dara lámh, ba mhaith linn ligean do
`new_setting_value` a bheith ina `setting_value`.

Is féidir linn fo-línte a úsáid in áiteanna éagsúla laistigh de phatrún amháin chun neamhaird a dhéanamh ar
luachanna ar leith. Taispeánann liostú 19-19 sampla de neamhaird a dhéanamh ar an dara agus an
ceathrú luach i dtuple de chúig mhír.

<Listing number="19-19" caption="Ignoring multiple parts of a tuple">

```rust
{{#rustdoc_include ../../listings/ch19-patterns-and-matching/listing-19-19/src/main.rs:here}}
```

</Listing>

Priontálfaidh an cód seo `Some numbers: 2, 8, 32`, agus déanfar neamhaird de na luachanna 4 agus 16.

#### Neamhaird a Thabhairt d'Athróg Neamhúsáidte trína hainm a thosú le `_`

Má chruthaíonn tú athróg ach mura n-úsáideann tú í in áit ar bith, eiseoidh Rust rabhadh de ghnáth toisc go bhféadfadh fabht a bheith in athróg neamhúsáidte. Mar sin féin, uaireanta bíonn sé
úsáideach a bheith in ann athróg nach n-úsáidfidh tú fós a chruthú, amhail nuair a bhíonn tú ag
fréamhshamáiriú nó ag tosú tionscadail. Sa chás seo, is féidir leat a rá le Rust
gan rabhadh a thabhairt duit faoin athróg neamhúsáidte trí ainm na hathróige a thosú
le fo-líne. I Liosta 19-20, cruthaímid dhá athróg neamhúsáidte, ach nuair a
thiomsaíonn muid an cód seo, níor cheart dúinn ach rabhadh a fháil faoi cheann acu.

<Listing number="19-20" file-name="src/main.rs" caption="Starting a variable name with an underscore to avoid getting unused variable warnings">

```rust
{{#rustdoc_include ../../listings/ch19-patterns-and-matching/listing-19-20/src/main.rs}}
```

</Listing>

Anseo faighimid rabhadh faoi gan an athróg `y` a úsáid, ach ní fhaighimid rabhadh faoi gan `_x` a úsáid.

Tabhair faoi deara go bhfuil difríocht bheag idir `_` amháin a úsáid agus ainm a úsáid a thosaíonn le fo-líne. Ceanglaíonn an comhréir `_x` an luach leis an
athróg fós, ach ní cheanglaíonn `_` ar chor ar bith. Chun cás a thaispeáint ina bhfuil an
idirdhealú seo tábhachtach, cuirfidh Liostáil 19-21 earráid ar fáil dúinn.

<Listing number="19-21" caption="An unused variable starting with an underscore still binds the value, which might take ownership of the value">

```rust,ignore,does_not_compile
{{#rustdoc_include ../../listings/ch19-patterns-and-matching/listing-19-21/src/main.rs:here}}
```

</Listing>

Gheobhaimid earráid mar go mbogfar an luach `s` isteach i `_s` fós,
rud a chuireann cosc ​​orainn `s` a úsáid arís. Mar sin féin, ní cheanglaíonn úsáid an fho-línte leis féin leis an luach riamh. Tiomsófar Liostáil 19-22 gan aon earráidí
toisc nach mbogtar `s` isteach i `_`.

<Listing number="19-22" caption="Using an underscore does not bind the value">

```rust
{{#rustdoc_include ../../listings/ch19-patterns-and-matching/listing-19-22/src/main.rs:here}}
```

</Listing>

Oibríonn an cód seo go breá mar ní cheanglaímid `s` le haon rud riamh; ní bhogtar é.

#### Neamhaird a dhéanamh ar na Codanna atá fágtha de Luach le `..`

Le luachanna a bhfuil go leor codanna iontu, is féidir linn comhréir `..` a úsáid chun codanna sonracha a úsáid agus neamhaird a dhéanamh den chuid eile, ag seachaint an ghá le fo-línte a liostáil do gach luach
a ndéantar neamhaird de. Déanann an patrún `..` neamhaird d'aon chodanna de luach nach bhfuil
meaitseáilte go sainráite againn sa chuid eile den phatrún. I Liostáil 19-23, tá struchtúr
`Point` againn a choinníonn comhordanáid i spás tríthoiseach. Sa
sloinnt `match`, ba mhaith linn oibriú ar an gcomhordanáid `x` amháin agus neamhaird a dhéanamh ar na luachanna sna réimsí `y` agus `z`.

<Listing number="19-23" caption="Ignoring all fields of a `Point` except for `x` by using `..`">

```rust
{{#rustdoc_include ../../listings/ch19-patterns-and-matching/listing-19-23/src/main.rs:here}}
```

</Listing>

Liostaímid an luach `x` agus ansin ní chuireann muid ach an patrún `..` san áireamh. Tá sé seo níos tapúla ná `y: _` agus `z: _` a liostáil, go háirithe nuair a bhíonn muid ag obair le
struchtúir a bhfuil a lán réimsí iontu i gcásanna nach bhfuil ach réimse amháin nó dhó ábhartha.

Leathnóidh an comhréir `..` go dtí an oiread luachanna agus is gá. Taispeánann liostú 19-24
conas `..` a úsáid le tuple.

<Listing number="19-24" file-name="src/main.rs" caption="Matching only the first and last values in a tuple and ignoring all other values">

```rust
{{#rustdoc_include ../../listings/ch19-patterns-and-matching/listing-19-24/src/main.rs}}
```

</Listing>

Sa chód seo, déantar an chéad luach agus an luach deireanach a mheaitseáil le `first` agus `last`. Déanfaidh an `..` meaitseáil agus neamhaird a dhéanamh ar gach rud sa lár.

Mar sin féin, ní mór úsáid `..` a bheith neamhbhríoch. Mura bhfuil sé soiléir cé na luachanna atá beartaithe le haghaidh meaitseáil agus cé acu ba chóir neamhaird a dhéanamh orthu, tabharfaidh Rust earráid dúinn.
Léiríonn liostú 19-25 sampla d'úsáid `..` go débhríoch, mar sin ní
thiomsóidh sé.

<Listing number="19-25" file-name="src/main.rs" caption="An attempt to use `..` in an ambiguous way">

```rust,ignore,does_not_compile
{{#rustdoc_include ../../listings/ch19-patterns-and-matching/listing-19-25/src/main.rs}}
```

</Listing>

Nuair a dhéanaimid an sampla seo a thiomsú, faighimid an earráid seo:

```console
{{#include ../../listings/ch19-patterns-and-matching/listing-19-25/output.txt}}
```

Tá sé dodhéanta do Rust a chinneadh cé mhéad luach sa tuple le neamhaird a dhéanamh orthu
sula ndéantar luach a mheaitseáil le `second` agus ansin cé mhéad luach eile le
neamhaird a dhéanamh orthu ina dhiaidh sin. D’fhéadfadh an cód seo a chiallaíonn gur mian linn neamhaird a dhéanamh de `2`, `second` a cheangal le `4`, agus ansin neamhaird a dhéanamh de `8`, `16`, agus `32`; nó gur mian linn neamhaird a dhéanamh de
`2` agus `4`, `second` a cheangal le `8`, agus ansin neamhaird a dhéanamh de `16` agus `32`; agus mar sin de.
Ní chiallaíonn an t-ainm athróg `second` aon rud speisialta do Rust, mar sin faighimid
earráid tiomsaitheora toisc go bhfuil sé débhríoch `..` a úsáid in dhá áit mar seo.

### Coinníollacha Breise le Gardaí Meaitseála

Is coinníoll breise `má` é _garda meaitseála_, a shonraítear tar éis an phatrúin i
lámh `match`, a chaithfidh a bheith oiriúnach freisin chun go roghnófar an lámh sin. Tá gardaí meaitseála
úsáideach chun smaointe níos casta a chur in iúl ná mar a cheadaíonn patrún ina aonar. Níl siad ar fáil ach amháin i léirithe `match`, ní i léirithe `if let` nó `while let`.

Is féidir leis an gcoinníoll athróga a cruthaíodh sa phatrún a úsáid. Taispeánann Liostáil 19-26 `match` ina bhfuil an patrún `Some(x)` ag an gcéad lámh agus ina bhfuil garda meaitseála `if x % 2 == 0` aici freisin (a bheidh fíor má tá an uimhir cothrom).

<Listing number="19-26" caption="Adding a match guard to a pattern">

```rust
{{#rustdoc_include ../../listings/ch19-patterns-and-matching/listing-19-26/src/main.rs:here}}
```

</Listing>

Priontálfaidh an sampla seo `The number 4 is even`. Nuair a dhéantar comparáid idir `num` agus an
patrún sa chéad lámh, meaitseálann sé, mar go meaitseálann `Some(4)` `Some(x)`. Ansin
seiceálann an garda meaitseála an bhfuil an chuid eile de roinnt `x` ar 2 cothrom le
0, agus toisc go bhfuil, roghnaítear an chéad lámh.

Dá mba rud é go raibh `num` ina `Some(5)` ina ionad, bheadh ​​an garda meaitseála sa chéad lámh
bréagach mar go bhfuil an chuid eile de 5 roinnte ar 2 cothrom le 1, nach
comhionann le 0. Ansin rachadh an meirge go dtí an dara lámh, a mheaitseálfadh mar nach bhfuil garda meaitseála ag an
dara lámh agus dá bhrí sin meaitseálann sé aon athraitheach `Some`.

Níl aon bhealach ann an coinníoll `if x % 2 == 0` a chur in iúl laistigh de phatrún, mar sin
tugann an garda meaitseála an cumas dúinn an loighic seo a chur in iúl. Is é an míbhuntáiste a bhaineann leis an
léiritheacht bhreise seo ná nach ndéanann an tiomsaitheoir iarracht seiceáil le haghaidh
uileghabhálachta nuair a bhíonn léirithe garda meaitseála i gceist.

I Liostáil 19-11, luaigh muid go bhféadfaimis gardaí meaitseála a úsáid chun ár
fhadhb scáthú patrún a réiteach. Cuimhnigh gur chruthaíomar athróg nua laistigh den
phatrún san abairt `match` in ionad an athróg lasmuigh den
`match` a úsáid. Chiallaigh an athróg nua sin nach bhféadfaimis tástáil a dhéanamh i gcoinne luach na
hathróige seachtraí. Taispeánann Liostáil 19-27 conas is féidir linn gardaí meaitseála a úsáid chun an
fhadhb seo a réiteach.

<Listing number="19-28" caption="Combining multiple patterns with a match guard">

```rust
{{#rustdoc_include ../../listings/ch19-patterns-and-matching/listing-19-28/src/main.rs:here}}
```

</Listing>

Deir an coinníoll meaitseála nach n-oireann an lámh ach amháin má tá luach `x` cothrom le `4`, `5`, nó `6` _agus_ má tá `y` fíor. Nuair a ritheann an cód seo, oibríonn patrún na chéad láimhe mar go bhfuil `x` cothrom le `4`, ach tá an garda meaitseála `if y` bréagach, mar sin ní roghnaítear an chéad lámh. Bogann an cód ar aghaidh go dtí an dara lámh,
a mheaitseálann, agus priontáileann an clár seo `no`. Is é an chúis atá leis ná go mbaineann an coinníoll `if` leis an patrún iomlán `4 | 5 | 6`, ní hamháin leis an luach deireanach
`6`. I bhfocail eile, iompraíonn tosaíocht garda meaitseála i ndáil le patrún mar seo:

```text
(4 | 5 | 6) if y => ...
```

seachas seo:

```text
4 | 5 | (6 if y) => ...
```

Tar éis an cód a rith, is léir an t-iompar tosaíochta: dá gcuirfí an garda meaitseála i bhfeidhm ar an luach deiridh sa liosta luachanna a shonraítear ag baint úsáide as an oibreoir `|` amháin, bheadh ​​an lámh meaitseáilte agus bheadh ​​an clár tar éis `yes` a phriontáil.

### Ceangail `@`

Ligeann an t-oibreoir _ag_ `@` dúinn athróg a chruthú a choinníonn luach ag an am céanna
agus muid ag tástáil an luacha sin le haghaidh meaitseáil patrún. I Liostáil 19-29, ba mhaith linn
tástáil a dhéanamh go bhfuil réimse `Message::Hello` `id` laistigh den raon `3..=7`. Ba mhaith linn freisin
an luach a cheangal leis an athróg `id_variable` ionas gur féidir linn é a úsáid sa
chód a bhaineann leis an lámh. D'fhéadfaimis an t-athróg seo a ainmniú `id`, mar an gcéanna leis an
réimse, ach don sampla seo úsáidfimid ainm difriúil.

<Listing number="19-29" caption="Using `@` to bind to a value in a pattern while also testing it">

```rust
{{#rustdoc_include ../../listings/ch19-patterns-and-matching/listing-19-29/src/main.rs:here}}
```

</Listing>

Priontálfaidh an sampla seo `Found an id in range: 5`. Trí `id_variable @` a shonrú roimh an raon `3..=7`, táimid ag gabháil cibé luach a mheaitseálann an raon
agus ag tástáil freisin an raibh an luach ag teacht leis an bpatrún raoin.

Sa dara lámh, áit nach bhfuil ach raon sonraithe sa phatrún, níl aon athróg sa chód
a bhaineann leis an lámh ina bhfuil luach iarbhír
an réimse `id`. D’fhéadfadh luach an réimse `id` a bheith 10, 11, nó 12, ach
níl a fhios ag an gcód a théann leis an bpatrún sin cé acu é. Níl an cód patrún
in ann an luach ón réimse `id` a úsáid, mar nach bhfuil an luach
`id` sábháilte againn in athróg.

Sa lámh dheireanach, áit ar shonraigh muid athróg gan raon, tá an luach againn ar fáil le húsáid i gcód na láimhe in athróg darb ainm `id`. Is é an
cúis ná gur úsáid muid comhréir giorraithe an réimse struchtúr. Ach níor
chuireamar aon tástáil i bhfeidhm ar an luach sa réimse `id` sa bhrainse seo, mar a rinneamar leis an
dhá bhrainse tosaigh: bheadh ​​aon luach ag teacht leis an bpatrún seo.

Trí `@` a úsáid, is féidir linn luach a thástáil agus é a shábháil in athróg laistigh d'aon phatrún amháin.

## Achoimre

Tá patrúin Rust an-úsáideach chun idirdhealú a dhéanamh idir cineálacha éagsúla
sonraí. Nuair a úsáidtear iad i léirithe `match`, cinntíonn Rust go gclúdaíonn do phatrúin gach
luach is féidir, nó ní thiomsóidh do chlár. Déanann patrúin i ráitis `let` agus
paraiméadair feidhme na coincheapa sin níos úsáidí, rud a chuireann ar chumas
luachanna a athstruchtúrú i gcodanna níos lú ag an am céanna le hathróga a shannadh. Is féidir linn patrúin shimplí nó chasta a chruthú chun freastal ar ár riachtanais.

Ansin, don dara caibidil dheireanach den leabhar, féachfaimid ar roinnt gnéithe ardleibhéil de ghnéithe éagsúla Rust.