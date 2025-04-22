## Cód Rith ar Ghlantachán leis an Trait `Drop`

Is é an dara tréith atá tábhachtach don phatrún pointeoir cliste ná `Drop`, rud a ligeann
shaincheapann tú cad a tharlaíonn nuair a bhíonn luach ar tí dul as an raon feidhme. Is féidir leat
cur i bhfeidhm a sholáthar don tréith `Drop` ar aon chineál, agus is féidir leis an gcód sin
a úsáid chun acmhainní cosúil le comhaid nó naisc líonra a scaoileadh.

Táimid ag tabhairt isteach `Drop` i gcomhthéacs leideanna cliste mar go bhfuil an
is beagnach i gcónaí a úsáidtear feidhmiúlacht na tréithe `Drop` agus a
pointeoir cliste. Mar shampla, nuair a scaoiltear `Box<T>` díroinnfidh sé an
spás ar an gcarn a díríonn an bosca air.

I dteangacha áirithe, i gcás cineálacha áirithe, ní mór don ríomhchláraitheoir cód a ghlaoch chun cuimhne saor in aisce
nó acmhainní gach uair a chríochnaíonn siad ag baint úsáide as sampla de na cineálacha sin. Samplaí
cuir láimhseálacha comhaid, soicéid nó glais san áireamh. Má dhéanann siad dearmad, d'fhéadfadh an córas
éirí ró-ualaithe agus tuairteála. I Rust, is féidir leat a shonrú go bhfuil beagán áirithe de
cód a rith aon uair a théann luach as raon feidhme, agus cuirfidh an tiomsaitheoir isteach
an cód seo go huathoibríoch. Mar thoradh air sin, ní gá duit a bheith cúramach faoi
cód glanta a chur i ngach áit i gclár a chuireann cás ar leith
tá an cineál críochnaithe - ní bheidh tú ag sceitheadh ​​acmhainní fós!

Sonraíonn tú an cód le rith nuair a théann luach as raon feidhme trí chur i bhfeidhm an
Tréith `drop`. Éilíonn an tréith `Drop` ort modh amháin ainmnithe a chur i bhfeidhm
`drop` a thógann tagairt mutable do `self`. Chun féachaint nuair a ghlaonn Rust 'titim',
cuirimis ráitis `drop` le `println!` i bhfeidhm faoi láthair.

Léiríonn liostú 15-14 struchtúr `CustomSmartPointer` nach bhfuil ach saincheaptha aige
feidhmiúlacht ná go ndéanfaidh sé `Dropping CustomSmartPointer!` a phriontáil nuair a bheidh an
mar shampla téann as raon feidhme, chun a thaispeáint nuair a ritheann Rust an fheidhm `drop`.

<Listing number="15-14" file-name="src/main.rs" caption="A `CustomSmartPointer` struct that implements the `Drop` trait where we would put our cleanup code">

```rust
{{#rustdoc_include ../../listings/ch15-smart-pointers/listing-15-14/src/main.rs}}
```

</Listing>

Tá an trait `Drop` san áireamh sa réamhrá, mar sin ní gá dúinn é a thabhairt isteach
scóip. Cuirimid an tréith `Drop` ar `CustomSmartPointer` i bhfeidhm agus soláthraímid an
cur i bhfeidhm don mhodh `drop` ar a dtugtar `println!`. An comhlacht ar an
Is éard is feidhm `drop` ann ná áit a gcuirfeá aon loighic a theastaigh uait a rith
téann sampla de do chineál as raon feidhme. Táimid ag priontáil roinnt téacs anseo chun
léiriú go radhairc cathain a ghlaonn Rust 'titim'.

I `main`, cruthaímid dhá chás de `CustomSmartPointer` agus ansin priontáil
`CustomSmartPointers created`. Ag deireadh `main`, ár gcásanna de
Rachaidh `CustomSmartPointer` as an scóip, agus cuirfidh Rust glaoch ar an gcód a chuireamar
sa mhodh `drop`, ár dteachtaireacht deiridh a phriontáil. Tabhair faoi deara nár ghá dúinn
glaoigh ar an modh `drop` go sainráite.

Agus an clár seo á rith againn, feicfidh muid an t-aschur seo a leanas:

```rust
{{#rustdoc_include ../../listings/ch15-smart-pointers/listing-15-14/src/main.rs}}
```

Thug Rust `drop` orainn go huathoibríoch nuair a chuaigh ár gcásanna amach as an scóip,
ag glaoch ar an gcód a shonraigh muid. Cuirtear athróga in ord droim ar ais de
a greadadh, mar sin thit `d` roimh `c`. Is é cuspóir an tsampla seo ná
treoir amhairc a thabhairt duit ar conas a oibríonn an modh `drop`; de ghnáth dhéanfá
sonraigh an cód glanta nach mór do do chineál a rith seachas prionta
teachtaireacht.

### Luach a ísliú go luath le `std::mem::drop`

Ar an drochuair, níl sé éasca an `drop` uathoibríoch a dhíchumasú
feidhmiúlacht. De ghnáth ní gá ‘titim’ a dhíchumasú; pointe iomlán an
Is éard atá i gceist le tréithe “titim” go dtugtar aire uathoibríoch dó. Ó am go chéile, áfach,
b'fhéidir gur mhaith leat luach a ghlanadh go luath. Sampla amháin is ea nuair a úsáidtear cliste
leideanna a bhainistíonn glais: b'fhéidir gur mhaith leat an modh `drop` a chur i bhfeidhm
scaoileann sé an glas ionas gur féidir le cód eile sa raon feidhme céanna an glas a fháil.
Ní ligeann Rust duit modh ‘titim’ na trait ‘Drop’ a ghlaoch de láimh; ina ionad
caithfidh tú glaoch ar an bhfeidhm `std::mem::drop` a sholáthraíonn an leabharlann chaighdeánach
más mian leat iallach a chur ar luach a ísliú roimh dheireadh a scóip.

Má dhéanaimid iarracht modh 'titim' an trait `Drop` a ghlaoch de láimh trí athrú a dhéanamh ar an
`príomhfheidhm' ó Liostú 15-14, mar a thaispeántar i Liostú 15-15, gheobhaidh muid
earráid tiomsaithe:

<Listing number="15-16" file-name="src/main.rs" caption="Calling `std::mem::drop` to explicitly drop a value before it goes out of scope">

```rust
{{#rustdoc_include ../../listings/ch15-smart-pointers/listing-15-16/src/main.rs:here}}
```

</Listing>

Nuair a dhéanaimid iarracht an cód seo a thiomsú, gheobhaidh muid an earráid seo:

```console
{{#include ../../listings/ch15-smart-pointers/listing-15-16/output.txt}}
```

Deir an teachtaireacht earráide seo nach bhfuil cead againn ‘titim’ a ghlaoch go sainráite. Tá an
Úsáideann teachtaireacht earráide an téarma _destructor_, arb é an téarma ríomhchlárúcháin ginearálta é
le haghaidh feidhm a ghlanann sampla. Tá _destructor_ ar aon dul le a
_constructor_, rud a chruthaíonn sampla. Is é an fheidhm `drop` i Rust amháin
scriostóir ar leith.

Ní ligeann Rust dúinn ‘titim’ a ghlaoch go sainráite mar go mbeadh Rust fós
glaoigh go huathoibríoch ar `drop` ar an luach ag deireadh `main`. Chuirfeadh sé seo faoi deara a
earráid _double free_ toisc go mbeadh Rust ag iarraidh an luach céanna a ghlanadh
faoi ​​dhó.

Ní féidir linn ionsá uathoibríoch `drop` a dhíchumasú nuair a théann luach as
scóip, agus ní féidir linn an modh `drop` a ghlaoch go sainráite. Mar sin, más gá dúinn bhfeidhm
luach atá le glanadh suas go luath, úsáidimid an fheidhm `std::mem::drop`.

Tá an fheidhm `std::mem::drop` difriúil ón modh `drop` sa `Drop`
trait. Tugaimid é trí rith mar argóint an luach ba mhaith linn a bhrú chun titim.
Tá an fheidhm sa réamhrá, ionas /../listings/gur féidir linn `main` i Liostú 15-15 a mhodhnú go
cuir glaoch ar an bhfeidhm `drop`, mar a thaispeántar i Liostú 15-16:

<Listing number="15-16" file-name="src/main.rs" caption="Ag glaoch ar `std::mem::drop` chun luach a laghdú go sainráite sula dtéann sé as an scóip">

```rust
{{#rustdoc_include ../../listings/ch15-smart-pointers/listing-15-16/src/main.rs:here}}
```

</Listing>

Má ritheann tú an cód seo, déanfar na rudaí seo a leanas a phriontáil:

```console
{{#include ../../listings/ch15-smart-pointers/listing-15-16/output.txt}}
```

Tá an téacs ``Dropping CustomSmartPointer with data `some data`!`` clóite
idir an `CustomSmartPointer created.` agus `CustomSmartPointer dropped
before the end of main.` a thaispeánann go dtugtar an cód modha `drop` ar
titim `c` ag an bpointe sin.

Is féidir leat cód sonraithe i gcur i bhfeidhm tréithe `Drop` a úsáid ar go leor bealaí chun
glantachán a dhéanamh áisiúil agus sábháilte: mar shampla, d'fhéadfá é a úsáid chun do chuid féin a chruthú
leithdháilteoir cuimhne féin! Leis an tréith `Drop` agus córas úinéireachta Rust, tusa
ní gá cuimhneamh ar ghlanadh suas toisc go ndéanann Rust é go huathoibríoch.

Ní gá freisin a bheith buartha faoi fhadhbanna a eascraíonn de thaisme
glanadh suas luachanna atá fós in úsáid: an córas úinéireachta a dhéanann cinnte
tá tagairtí bailí i gcónaí cinntíonn sé freisin nach nglaofar `drop` ach uair amháin nuair
níl an luach á úsáid a thuilleadh.

Anois agus `Box<T>` agus roinnt de thréithe an chliste scrúdaithe againn
leideanna, breathnaímis ar roinnt leideanna cliste eile atá sainmhínithe sa chaighdeán
leabharlann.