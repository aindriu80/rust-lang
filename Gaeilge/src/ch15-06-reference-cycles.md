## Is féidir le Timthriallta Tagartha an Cuimhne a sceitheadh

Mar gheall ar ráthaíochtaí sábháilteachta cuimhne Rust tá sé deacair, ach níl sé dodhéanta
cruthaigh de thaisme cuimhne nach nglantar riamh (ar a dtugtar _memory leak_).
Ní ceann de ráthaíochtaí Rust é sceitheadh ​​cuimhne a chosc go hiomlán, rud a chiallaíonn
tá sceitheadh ​​cuimhne sábháilte cuimhne i Rust. Is féidir linn a fheiceáil go gceadaíonn Rust sceitheadh ​​cuimhne
trí úsáid a bhaint as `Rc<T>` agus `RefCell<T>`: is féidir tagairtí a chruthú nuair a
tagraíonn míreanna dá chéile i dtimthriall. Cruthaíonn sé seo leaks cuimhne mar gheall ar an
Ní bheidh líon tagartha gach míre sa timthriall a bhaint amach 0, agus na luachanna
ní scaoilfear choíche.

### Timthriall Tagartha á Chruthú

Breathnaímid ar conas a d’fhéadfadh timthriall tagartha tarlú agus conas é a chosc,
ag tosú leis an sainmhíniú ar an `List` enum agus modh `tail` sa Liostú
15-25:

<Listing number="15-25" file-name="src/main.rs" caption="A cons list definition that holds a `RefCell<T>` so we can modify what a `Cons` variant is referring to">

```rust
{{#rustdoc_include ../../listings/ch15-smart-pointers/listing-15-25/src/main.rs}}
```

</Listing>

Tá athrú eile á úsáid againn ar an sainmhíniú ar `List` ó Liostú 15-5. Tá an
is é an dara heilimint sa leagan `Cons` anois `RefCell <Rc<List>>`, rud a chiallaíonn go
in ionad a bheith in ann an luach `i32` a mhodhnú mar a rinneamar i Liostú
15-24, ba mhaith linn an luach `List` a bhfuil malairt `Cons` dírithe air a mhodhnú.
Táimid ag cur modh `tail` leis freisin chun é a dhéanamh áisiúil dúinn rochtain a fháil ar an
an dara mír má tá leagan `Cons` againn.

I Liostú 15-26, táimid ag cur `main` leis a úsáideann na sainmhínithe i
Liostáil 15-25. Cruthaíonn an cód seo liosta in `a` agus liosta i `b` a dhíríonn
an liosta in `a`. Ansin athraíonn sé an liosta in `a` chun `b` a chur in iúl, ag cruthú a
timthriall tagartha. Tá ráitis `println!` ar an mbealach chun a thaispeáint cad iad na
tá comhaireamh tagartha ag pointí éagsúla sa phróiseas seo.

<Listing number="15-26" file-name="src/main.rs" caption="Creating a reference cycle of two `List` values pointing to each other">

```rust
{{#rustdoc_include ../../listings/ch15-smart-pointers/listing-15-26/src/main.rs:here}}
```

</Listing>

Cruthaímid sampla `Rc<List>` a bhfuil luach `List` san athróg `a`
le liosta tosaigh de `5, Nil`. Cruthaímid gabháltas mar shampla `Rc<List>` ansin
luach `List` eile san athróg `b` ina bhfuil an luach 10 agus pointí
chuig an liosta in `a`.

Modhnaimid `a` mar sin díríonn sé ar `b` in ionad `Nil`, ag cruthú timthriall. Déanaimid
sin trí úsáid a bhaint as an modh `tail` chun tagairt a fháil don `RefCell<Rc<List>>`
in `a`, a chuireamar san athróg `link`. Ansin úsáidimid an `borrow_mut`
modh ar an `RefCell<Rc<List>>` chun an luach istigh ó `Rc<List>` a athrú
a choinníonn luach `Nil` ar an `Rc<List>` i `b`.

Nuair a rithimid an cód seo, ag coinneáil an `println!` deireanach a dúirt amach le haghaidh an
nóiméad, gheobhaidh muid an t-aschur seo:

```console
{{#include ../../listings/ch15-smart-pointers/listing-15-26/output.txt}}
```

Is iad comhaireamh tagartha na gcásanna `Rc<List>` sa dá `a` agus `b` ná 2 i ndiaidh
athraíonn muid an liosta in `a` chun `b` a chur in iúl. Ag deireadh `main`, titeann Rust an
athróg `b`, a laghdaíonn comhaireamh tagartha an shampla `b Rc<List>`
ó 2 go 1. Ní ligfear siar an chuimhne atá ag `Rc<List>` ar an gcarn ag
an pointe seo, toisc go bhfuil a chomhaireamh tagartha 1, ní 0. Ansin titeann Rust `a`, a
laghdaítear comhaireamh tagartha an ásc `a Rc<List>` ó 2 go 1 mar
go maith. Ní féidir cuimhne an ásc seo a ísliú ach an oiread, mar gheall ar an gceann eile
Tagraíonn `Rc<List>` shampla dó fós. Déanfaidh an chuimhne a leithdháiltear ar an liosta
fanacht gan bailiú go deo. Chun an timthriall tagartha seo a shamhlú, tá a
léaráid i bhFíor 15-4.

<img alt="Timthriall tagartha na liostaí" src="img/trpl15-04.svg" class="center" />

<span class="caption">Fíor 15-4: Timthriall tagartha liostaí `a` agus `b`
ag tagairt dá chéile</span>

Mura ndéanann tú trácht ar an `println!` deiridh agus má ritheann tú an clár, déanfaidh Rust iarracht é
priontáil an timthriall seo le `a` ag tagairt do `b` ag cur in iúl do `a` agus mar sin de go dtí é
thar maoil an chruach.

I gcomparáid le clár fíor-domhan, na hiarmhairtí a chruthú timthriall tagartha
sa sampla seo níl siad an-dochar: díreach tar éis dúinn an timthriall tagartha a chruthú,
chríochnaíonn an clár. Mar sin féin, má leithdháileadh clár níos casta go leor de chuimhne
i dtimthriall agus coinnithe air ar feadh i bhfad, d'úsáidfeadh an clár níos mó cuimhne
ná mar a bhí de dhíth air agus d'fhéadfadh sé an córas a shárú, rud a fhágann go n-imeodh sé as
cuimhne ar fáil.

Ní furasta timthriallta tagartha a chruthú, ach níl sé dodhéanta ach an oiread.
Má tá luachanna `RefCell<T>` agat ina bhfuil luachanna `Rc<T>` nó a mhacasamhail neadaithe
teaglaim de chineálacha le mutability istigh agus comhaireamh tagartha, ní mór duit
cinntigh nach gcruthaíonn tú timthriallta; ní féidir leat brath ar Rust chun iad a ghabháil.
Is fabht loighce i do chlár é timthriall tagartha a chruthú agus ba cheart duit
tástálacha uathoibrithe, athbhreithnithe cód, agus cleachtais forbartha bogearraí eile a úsáid chun
íoslaghdú.

Réiteach eile chun timthriallta tagartha a sheachaint is ea do shonraí a atheagrú
struchtúir sa chaoi is go gcuireann tagairtí áirithe úinéireacht in iúl agus ní léiríonn roinnt tagairtí.
Mar thoradh air sin, is féidir leat a bheith timthriallta comhdhéanta de roinnt caidreamh úinéireachta agus
roinnt caidreamh neamh-úinéireachta, agus ní dhéanann ach na caidrimh úinéireachta difear
cibé an féidir luach a ísliú nó nach féidir. I Liosta 15-25, ba mhaith linn i gcónaí `Cons`
roghanna eile chun a liosta a shealbhú, mar sin ní féidir an struchtúr sonraí a atheagrú.
Breathnaímid ar shampla ag baint úsáide as graif comhdhéanta de nóid tuismitheora agus nóid linbh
féachaint cén uair is bealach iomchuí chun cosc ​​a chur ar chaidrimh neamhúinéireachta
timthriallta tagartha.

### Timthriallta Tagartha a Chosc: `Rc<T>` á iompú ina `Weak<T>`

Go dtí seo, tá sé léirithe againn go méadaíonn glaoch `Rc::clone` an
Ní ghlantar `strong_count` de shampla `Rc<T>`, agus `Rc<T>` ach
suas más é a `strong_count` ná 0. Is féidir leat tagairt _lag_ a chruthú freisin don
luach laistigh de shampla `Rc<T>` trí `Rc::downgrade` a ghlaoch agus pas a fháil
tagairt don `Rc<T>`. Is tagairtí láidre iad conas is féidir leat úinéireacht a roinnt
mar shampla `Rc<T>`. Ní chuireann tagairtí laga caidreamh úinéireachta in iúl,
agus ní chuireann a n-áireamh isteach nuair a ghlantar sampla `Rc<T>`. siad
ní bheidh sé ina chúis le timthriall tagartha mar gheall ar aon timthriall ina bhfuil roinnt tagairtí laga
Brisfear iad a luaithe is é 0 an comhaireamh láidir tagartha luachanna atá i gceist.

Nuair a ghlaonn tú ar `Rc::downgrade`, gheobhaidh tú pointeoir cliste den chineál `Weak<T>`.
In ionad an `count_strong_count` sa chás `Rc<T>` a mhéadú faoi 1, cuir glaoch
Méadaíonn `Rc::downgrade` an `weak_count` faoi 1. Úsáideann an cineál `Rc<T>`
`weak_count` chun súil a choinneáil ar cé mhéad tagairt `Weak<T>` atá ann, cosúil le
`strong_count`. Is é an difríocht ná ní gá don `count_lag` a bheith 0 don
`Rc<T>` shampla le glanadh suas.

Toisc go mb’fhéidir gur thit an luach a d’fhéadfadh tagairtí `Weak<T>` a dhéanamh, le déanamh
rud ar bith leis an luach a bhfuil `Lag<T>` ag díriú air, caithfidh tú a chinntiú go bhfuil an
luach ann fós. Déan é seo trí ghlao a chur ar an modh `upgrade` ar `Weak<T>`
mar shampla, a thabharfaidh ar ais `Option<Rc<T>>`. Gheobhaidh tú toradh ar `Some`
mura bhfuil an luach `Rc<T>` tite fós agus toradh ar `None` mura bhfuil an
Tá luach `Rc<T>` tite. Toisc go dtugann `upgrade` `Option<Rc<T>>` ar ais,
Cinnteoidh Rust go láimhseálfar an cás `Some` agus an cás `None`, agus
ní bheidh pointeoir neamhbhailí ann.

Mar shampla, seachas liosta a úsáid nach bhfuil a fhios ag a míreanna ach faoin gcéad cheann eile
mír, cruthóimid crann a bhfuil a fhios ag na míreanna faoina leanaí míreanna _agus_
míreanna a dtuismitheoirí.

#### Struchtúr Sonraí Crann a Chruthú: `Node` le Nóid Leanaí

Chun tús a chur leis, tógfaimid crann le nóid a bhfuil eolas acu ar a nóid linbh.
Cruthóimid struchtúr darb ainm `Node` a shealbhaíonn a luach `i32` féin chomh maith le
tagairtí dá luachanna `Node` a leanaí:

<span class="filename">Ainm comhaid: src/main.rs</span>

```rust
{{#rustdoc_include ../../listings/ch15-smart-pointers/listing-15-27/src/main.rs:here}}
```

Teastaíonn uainn `Node` a mbeadh úinéireacht ag a leanaí air, agus ba mhaith linn an úinéireacht sin a roinnt linn
athróg ionas gur féidir linn rochtain a fháil ar gach `Node` sa chrann go díreach. Chun seo a dhéanamh, táimid
sainmhínigh na míreanna `Vec<T>` mar luachanna den chineál `Rc<Node>`. Ba mhaith linn freisin
modhnaigh cé na nóid atá ina bpáistí de nód eile, ionas go mbeidh `RefCell<T>` againn isteach
`children` timpeall an `Vec<Rc<Node>>`.

Ansin, úsáidfimid ár sainmhíniú struchtúr agus cruthóimid sampla amháin `Node` ainmnithe
`leaf` leis an luach 3 agus gan leanaí, agus cás eile darb ainm `branch`
leis an luach 5 agus `leaf` mar dhuine dá leanaí, mar a thaispeántar i Liosta 15-27:

<Listing number="15-27" file-name="src/main.rs" caption="Cruthú nód `leaf` gan chlann agus nód `branch` le `leaf` mar dhuine dá leanaí">

```rust
{{#rustdoc_include ../../listings/ch15-smart-pointers/listing-15-27/src/main.rs:there}}
```

</Listing>

Clónaimid an `Rc<Node>` i `leaf` agus stóráilimid é sin sa `branch`, rud a chiallaíonn an
Tá beirt úinéirí ag `Node` i `leaf` anois: `leaf` agus `branch`. Is féidir linn a fháil ó
`branch` go `leaf` trí `branch.children`, ach níl aon bhealach le fáil ó
`leaf` go `branch`. Is é an fáth nach bhfuil aon tagairt ag `leaf` do `branch` agus
ní fios go bhfuil gaol acu leis. Ba mhaith linn go mbeadh a fhios ag `leaf` gurb é `branch` a chuid
tuismitheoir. Déanfaimid é sin chugainn.

#### Tagairt ó Pháiste á Chur lena Thuismitheoir

Chun an nód leanbh a chur ar an eolas faoina thuismitheoir, ní mór dúinn réimse `parent` a chur leis
ár sainmhíniú ar struchtúr `Node`. Is é an deacracht cinneadh a dhéanamh cén cineál
ba cheart go mbeadh `parent`. Tá a fhios againn nach féidir `Rc<T>` a bheith ann, mar bheadh
cruthaigh timthriall tagartha le `leaf.parent` ag tagairt don `branch` agus
`branch.children` ag tagairt do `leaf`, rud a chuirfeadh lena `count_strong`
luachanna gan a bheith 0 riamh.

Ag smaoineamh ar na caidrimh ar bhealach eile, ba cheart go mbeadh úinéireacht ag nód tuismitheora ar a chuid féin
leanaí: má thittear nód tuismitheora, ba chóir a nóid linbh a thit mar
go maith. Mar sin féin, níor cheart go mbeadh úinéireacht ag leanbh ar a thuismitheoir: má scaoilimid nód linbh, beidh an
ba chóir go mbeadh tuismitheoir ann fós. Is cás é seo le haghaidh tagairtí laga!

Mar sin in ionad `Rc<T>`, bainfimid úsáid as `Weak<T>` don chineál `parent`,
go sonrach `RefCell<Weak<Node>>`. Anois breathnaíonn ár sainmhíniú ar struchtúr `Node`
mar seo:

<span class="filename">Filename: src/main.rs</span>

```rust
{{#rustdoc_include ../../listings/ch15-smart-pointers/listing-15-28/src/main.rs:here}}
```

Beidh nód in ann tagairt a dhéanamh dá mháthairnód ach ní leis a thuismitheoir é.
I Liosta 15-28, déanaimid `main` a nuashonrú chun an sainmhíniú nua seo a úsáid mar sin an `leaf`
beidh bealach ag nód tagairt a dhéanamh dá thuismitheoir, `branch`:

<Listing number="15-28" file-name="src/main.rs" caption="A `leaf` node with a weak reference to its parent node `branch`">

```rust
{{#rustdoc_include ../../listings/ch15-smart-pointers/listing-15-28/src/main.rs:there}}
```

</Listing>

Breathnaíonn cruthú an nód `leaf` cosúil le Liostú 15-27 cé is moite de
an réimse `parent`: Tosaíonn `leaf` amach gan tuismitheoir, mar sin cruthaímid ceann nua,
folamh `Weak<Node>` mar shampla tagartha.

Ag an bpointe seo, nuair a dhéanaimid iarracht tagairt a fháil do thuismitheoir `leaf` trí úsáid a bhaint as
an modh `upgrade`, faigheann muid luach `None`. Feicimid é seo san aschur ó na
an chéad ráiteas `println!`:

```text
leaf parent = None
```

Nuair a chruthaímid an nód `branch`, beidh `Weak<Node>` nua aige freisin
tagairt sa réimse `parent`, toisc nach bhfuil nód tuismitheora ag `branch`.
Tá `leaf` fós againn mar dhuine de chlann `branch`. Nuair a bheidh an
Mar shampla `Node` i `branch`, is féidir linn `leaf` a mhionathrú chun `Weak<Node>` a thabhairt dó
tagairt dá thuismitheoir. Úsáidimid an modh `borow_mut` ar an
`RefCell<Weak<Node>>` sa réimse `parent` ar `leaf`, agus ansin úsáidimid an
Feidhm `Rc::downgrade` chun tagairt `Weak<Node>` a chruthú do `branch` ó
an `Rc<Node>` sa `branch`.

Nuair a phriontáilimid tuismitheoir `leaf` arís, gheobhaidh muid leagan `Some` an uair seo
shealbhú `branch`: anois is féidir le `leaf` rochtain a fháil ar a thuismitheoir! Nuair a phriontáilimid `leaf`, déanaimid
seachain freisin an timthriall a chríochnaigh sa deireadh le cur thar maoil stoic mar a bhí againn i
Liostáil 15-26; clóitear na tagairtí `Weak<Node>` mar `(Weak)`:

```text
leaf parent = Some(Node { value: 5, parent: RefCell { value: (Weak) },
children: RefCell { value: [Node { value: 3, parent: RefCell { value: (Weak) },
children: RefCell { value: [] } }] } })
```

Léiríonn an easpa aschuir gan teorainn nár chruthaigh an cód seo tagairt
timthriall. Is féidir linn é seo a insint freisin trí bhreathnú ar na luachanna a fhaighimid ó ghlaoch
`Rc::strong_count` agus `Rc::weak_count`.

#### Amharcléiriú Athruithe ar `strong_count` agus `weak_count`

Breathnaímid ar an gcaoi a bhfuil na luachanna `strong_count` agus `count_count_lag` an `Rc<Node>`
athraíonn cásanna trí raon feidhme inmheánach nua a chruthú agus cruthú na
`branch` isteach sa raon feidhme sin. Trí sin a dhéanamh, is féidir linn a fheiceáil cad a tharlaíonn nuair a bhíonn `branch` cruthaithe agus ansin thit nuair a théann sé as raon feidhme. Taispeántar na modhnuithe
i Liosta 15-29:


<Listing number="15-29" file-name="src/main.rs" caption="Creating `branch` in an inner scope and examining strong and weak reference counts">

```rust
{{#rustdoc_include ../../listings/ch15-smart-pointers/listing-15-29/src/main.rs:here}}
```

</Listing>

Tar éis `leaf` a chruthú, tá comhaireamh láidir 1 agus lag ag a `Rc<Node>`
comhaireamh 0. Sa scóip inmheánach, cruthaímid `branch` agus déanaimid é a nascadh le
`leaf`, ag an bpointe nuair a phriontáilimid na comhaireamh, an `Rc<Node>` sa `branch`
beidh comhaireamh láidir de 1 agus comhaireamh lag de 1 (do phointeáil `leaf.parent`
go `branch` le `Weak<Node>`). Nuair a phriontáilimid na háirimh i `leaf`, feicfimid
beidh líon láidir de 2 aige, toisc go bhfuil clón de na
`Rc<Node>` de `leaf` arna stóráil i `branch.children`, ach beidh lag aige fós
comhaireamh 0.

Nuair a chríochnaíonn an raon feidhme istigh, téann `branch` as raon feidhme agus an comhaireamh láidir de
laghdaítear an `Rc<Node>` go 0, mar sin laghdaítear a `Node`. An líon lag de 1
ó `leaf.parent` nach bhfuil aon tionchar ar cibé an bhfuil nó nach bhfuil `Node` thit, mar sin againn
ná faigh aon sceitheadh ​​cuimhne!

Má dhéanaimid iarracht rochtain a fháil ar thuismitheoir `leaf` tar éis dheireadh an scóip, gheobhaidh muid
`None` arís. Ag deireadh an chláir, tá an `Rc<Node>` i `leaf` láidir
comhaireamh de 1 agus comhaireamh lag de 0, toisc go bhfuil an athróg `leaf` an t-aon anois
tagairt don `Rc<Node>` arís.

Tá an loighic ar fad a bhainistíonn an comhaireamh agus an titim luacha ionsuite
`Rc<T>` agus `Weak<T>` agus a gcur i bhfeidhm ar an trait `Drop`. Le
ag sonrú gur chóir go mbeadh an gaol ó leanbh lena thuismitheoir a
Tagairt `Weak<T>` sa sainmhíniú ar `Node`, is féidir leat tuismitheoir a bheith agat
díríonn nóid ar nóid linbh agus vice versa gan timthriall tagartha a chruthú
agus sceitheadh ​​cuimhne.

## Achoimre

Chlúdaigh an chaibidil seo conas leideanna cliste a úsáid chun ráthaíochtaí éagsúla a dhéanamh agus
comhbhabhtáil ó na cinn a dhéanann Rust de réir réamhshocraithe le tagairtí rialta. Tá an
Tá méid aitheanta ag an gcineál `Box<T>` agus pointí ar na sonraí a leithdháileadh ar an gcarn. Tá an
Coinníonn cineál `Rc<T>` líon na dtagairtí do shonraí ar an gcarn mar sin de
is féidir go mbeadh úinéirí iolracha ag na sonraí sin. An cineál `RefCell<T>` lena taobh istigh
Tugann mutability cineál dúinn gur féidir linn a úsáid nuair a theastaíonn uainn cineál do- immutable ach
gá luach inmheánach den chineál sin a athrú; cuireann sé an iasacht i bhfeidhm freisin
rialacha ag am rite seachas ag am tiomsaithe.

Pléadh freisin na tréithe `Deref` agus `Drop`, a chuireann ar chumas go leor de na
feidhmiúlacht na dtreoir cliste. Rinneamar iniúchadh ar thimthriallta tagartha is féidir a bheith ina chúis
sceitheanna cuimhne agus conas iad a chosc trí úsáid a bhaint as `Weak<T>`.

Má tá do spéis sa chaibidil seo agus gur mhaith leat do chuid féin a chur i bhfeidhm
leideanna cliste, seiceáil amach [“The Rustonomicon”][nomicon] le haghaidh níos úsáidí
eolas.

Next, beidh muid ag caint faoi concurrency i Rust. Foghlaimeoidh tú fiú faoi chúpla rud nua
leideanna cliste.

[nomicon]: ../nomicon/index.html