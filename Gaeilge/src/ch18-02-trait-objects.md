## Úsáid Réada Tréithe a Cheadaíonn Luachanna de Chineálacha Éagsúla

I gCaibidil 8, luaigh muid gur teorannú amháin a bhaineann le veicteoirí ná gur féidir leo
eilimintí de chineál amháin a stóráil. Chruthaíomar réiteach sealadach i Liosta 8-9 inar
shainíomar enum `SpreadsheetCell` a raibh malairtí ann chun slánuimhreacha, snámháin,
agus téacs a shealbhú. Chiallaigh sé seo go bhféadfaimis cineálacha éagsúla sonraí a stóráil i ngach cill agus
veicteoir a bheith againn fós a léirigh sraith cealla. Is réiteach breá maith é seo
nuair is sraith sheasta cineálacha iad ár míreanna inmhalartaithe a bhfuil aithne againn orthu
nuair a chuirtear ár gcód le chéile.

Mar sin féin, uaireanta ba mhaith linn go mbeadh ár n-úsáideoir leabharlainne in ann an tsraith
cineálacha atá bailí i gcás ar leith a leathnú. Chun a thaispeáint conas a d'fhéadfaimis é seo a bhaint amach,
cruthaímid uirlis chomhéadain úsáideora grafach (GUI) samplach a dhéanann athrá
trí liosta míreanna, ag glaoch modh `draw` ar gach ceann acu chun é a tharraingt chuig an
scáileán - teicníc choitianta d'uirlisí GUI. Cruthóimid cliathbhosca leabharlainne ar a dtugtar
`gui` ina bhfuil struchtúr leabharlainne GUI. D’fhéadfadh go mbeadh cineálacha áirithe sa chliathán seo le húsáid ag daoine, amhail ‘Cnaipe’ nó ‘RéimseText’. Ina theannta sin,
beidh úsáideoirí ‘gui’ ag iarraidh a gcineálacha féin a chruthú ar féidir iad a tharraingt: mar
shampla, d’fhéadfadh ríomhchláraitheoir amháin ‘Íomhá’ a chur leis agus d’fhéadfadh duine eile ‘BoscaRoghnaithe’ a chur leis.

Ní chuirfimid leabharlann GUI lánfheidhmiúil i bhfeidhm don sampla seo ach taispeánfaimid
conas a d’oirfeadh na píosaí le chéile. Tráth scríofa na leabharlainne, ní féidir linn
na cineálacha go léir a d’fhéadfadh ríomhchláraitheoirí eile a chruthú a bheith ar eolas againn agus a shainiú. Ach tá a fhios againn
go gcaithfidh ‘gui’ súil a choinneáil ar go leor luachanna de chineálacha éagsúla, agus go gcaithfidh sé modh ‘tarraingthe’ a ghlaoch ar gach ceann de na luachanna seo atá clóscríofa go difriúil. Ní gá dó a fhios a bheith aige go díreach cad a tharlóidh nuair a ghlaonn muid ar an modh ‘tarraingthe’,
ach go mbeidh an modh sin ar fáil dúinn don luach le glaoch air.

Chun seo a dhéanamh i dteanga le hoidhreacht, d’fhéadfaimis rang darb ainm
‘Comhpháirt’ a shainiú a bhfuil modh darb ainm ‘tarraingthe’ air. Gheobhadh na ranganna eile, amhail
`Button`, `Image`, agus `SelectBox`, oidhreacht ó `Component` agus dá bhrí sin
oidhreacht an modh `draw`. D’fhéadfaidís gach ceann acu an modh `draw` a shárú chun a n-iompar saincheaptha a shainiú, ach d’fhéadfadh an creatlach na cineálacha go léir a láimhseáil amhail is dá mba chásanna `Component` iad agus glaoch ar `draw` orthu. Ach toisc nach bhfuil oidhreacht ag Rust, teastaíonn bealach eile uainn chun an leabharlann `gui` a struchtúrú chun
ligean d’úsáideoirí í a leathnú le cineálacha nua.

### Tréith a Shainiú le haghaidh Iompraíochta Coitianta

Chun an t-iompar is mian linn a bheith ag `gui` a chur i bhfeidhm, sainmhínímid tréith darb ainm
`Draw` a mbeidh modh amháin darb ainm `draw` aige. Ansin is féidir linn veicteoir a shainiú a
ghlacann _trait object_. Díríonn réad tréithe ar chás de chineál
a chuireann ár dtréith shonraithe i bhfeidhm agus tábla a úsáidtear chun modhanna tréithe a chuardach ar
an gcineál sin ag am rite. Cruthaímid réad tréithe trí chineál éigin pointeora a shonrú, amhail tagairt `&` nó pointeoir cliste `Box<T>`, ansin an eochairfhocal `dyn`, agus ansin an tréith ábhartha a shonrú. (Pléifimid faoin gcúis
a gcaithfidh réada tréithe pointeoir a úsáid i gCaibidil 20 sa chuid [“Cineálacha Méide Dinimiciúla agus an Tréith ‘Méide’.”][dinimiciúil-mhéide]<!-- neamhaird a dhéanamh -->) Is féidir linn
réada tréithe a úsáid in ionad cineáil ghinearálta nó coincréite. Pé áit a n-úsáidimid
réad tréithe, cinnteoidh córas cineáil Rust ag am tiomsaithe go gcuirfidh aon luach
a úsáidtear sa chomhthéacs sin tréith an réada tréithe i bhfeidhm. Dá bhrí sin, ní gá dúinn na cineálacha féideartha go léir a bheith ar eolas againn ag am tiomsaithe.

Luaigh muid, i Rust, nach nglaoimid ar struchtúir agus ar enums
“réada” chun iad a idirdhealú ó réada teangacha eile. I struchtúr nó
enum, déantar na sonraí sna réimsí struchtúr agus an t-iompar i mbloic `impl` a
scaradh, ach i dteangacha eile, is minic a lipéadaítear an sonraí agus an t-iompar a chuirtear le chéile i gcoincheap amháin mar réad. Mar sin féin, tá réada tréithe níos cosúla
le réada i dteangacha eile sa mhéid is go gcomhcheanglaíonn siad sonraí agus iompar.
Ach tá réada tréithe difriúil ó réada traidisiúnta sa mhéid is nach féidir linn sonraí a chur le
réad tréithe. Níl réada tréithe chomh húsáideach le réada i dteangacha
eile: is é a gcuspóir sonrach ná ligean do bhaint amach trasna
iompar
coitianta.

Léiríonn Liostáil 18-3 conas tréith darb ainm `Draw` a shainiú le modh amháin darb ainm
`draw`:

<Listing number="18-3" file-name="src/lib.rs" caption="Definition of the `Draw` trait">

```rust,noplayground
{{#rustdoc_include ../../listings/ch18-oop/listing-18-03/src/lib.rs}}
```

</Listing>

Ba chóir go mbeadh an comhréir seo eolach ónár bplé ar conas tréithe a shainiú i gCaibidil 10. Ansin tagann roinnt comhréir nua: Sainmhíníonn Liostáil 18-4 struchtúr darb ainm `Screen` a bhfuil veicteoir darb ainm `components` ann. Is de chineál `Box<dyn Draw>` an ​​veicteoir seo, arb é réad tréithe é; is ionadaí é d'aon chineál laistigh de `Box` a chuireann an tréith `Draw` i bhfeidhm.

<Listing number="18-4" file-name="src/lib.rs" caption="Definition of the `Screen` struct with a `components` field holding a vector of trait objects that implement the `Draw` trait">

```rust,noplayground
{{#rustdoc_include ../../listings/ch18-oop/listing-18-04/src/lib.rs:here}}
```

</Listing>

Ar an struchtúr `Screen`, sainmhínímid modh darb ainm `run` a ghlaofaidh ar an modh `draw` ar gach ceann dá `components`, mar a thaispeántar i Liostáil 18-5:	


<Listing number="18-5" file-name="src/lib.rs" caption="A `run` method on `Screen` that calls the `draw` method on each component">

```rust,noplayground
{{#rustdoc_include ../../listings/ch18-oop/listing-18-05/src/lib.rs:here}}
```

</Listing>

Oibríonn sé seo ar bhealach difriúil ó struchtúr a shainiú a úsáideann paraiméadar cineál cineálach le teorainneacha tréithe. Ní féidir paraiméadar cineál cineálach a chur in ionad ach cineál coincréite amháin ag an am, ach ceadaíonn réada tréithe do chineálacha coincréite iolracha a líonadh isteach don réad tréithe ag am rite. Mar shampla, d'fhéadfaimis an struchtúr `Screen` a shainiú ag baint úsáide as cineál cineálach agus teorainn tréithe mar atá i Liostáil 18-6:

<Listing number="18-6" file-name="src/lib.rs" caption="An alternate implementation of the `Screen` struct and its `run` method using generics and trait bounds">

```rust,noplayground
{{#rustdoc_include ../../listings/ch18-oop/listing-18-06/src/lib.rs:here}}
```

</Listing>

Cuireann sé seo srian orainn go dtí sampla `Screen` ina bhfuil liosta comhpháirteanna den chineál `Button` nó den chineál `TextField`. Más rud é nach mbeidh ach bailiúcháin aonchineálacha agat, is fearr cineálacha agus teorainneacha tréithe a úsáid mar go ndéanfar na
sainmhínithe a mhonamorfú ag am tiomsaithe chun na cineálacha coincréiteacha a úsáid.

Ar an láimh eile, leis an modh a úsáideann réada tréithe, is féidir le sampla amháin `Screen` `Vec<T>` a shealbhú ina bhfuil `Box<Button>` chomh maith le
`Box<TextField>`. Féachfaimid ar an gcaoi a n-oibríonn sé seo, agus ansin labhróimid faoi na
impleachtaí feidhmíochta ag an am rith.

### An Tréith a Chur i bhFeidhm

Anois cuirfimid roinnt cineálacha leis a chuireann an tréith `Draw` i bhfeidhm. Soláthróimid an cineál
`Button`. Arís, tá cur i bhfeidhm leabharlann GUI lasmuigh de raon feidhme
an leabhair seo, mar sin ní bheidh aon chur i bhfeidhm úsáideach ag an modh `draw` ina
chorp. Chun a shamhlú cén chuma a bheadh ​​ar an gcur i bhfeidhm, d'fhéadfadh réimsí le haghaidh `width`, `height`, agus `label` a bheith i struchtúr `Button`, mar a thaispeántar i Liostáil 18-7:

<Listing number="18-7" file-name="src/lib.rs" caption="A `Button` struct that implements the `Draw` trait">

```rust,noplayground
{{#rustdoc_include ../../listings/ch18-oop/listing-18-07/src/lib.rs:here}}
```

</Listing>

Beidh na réimsí `width`, `height`, agus `label` ar `Button` difriúil ó na
réimsí ar chomhpháirteanna eile; mar shampla, d'fhéadfadh na
réimsí céanna sin móide réimse `placeholder` a bheith ag cineál `TextField`. Cuirfidh gach ceann de na cineálacha ar mhaith linn a tharraingt ar
an scáileán an tréith `Draw` i bhfeidhm ach úsáidfidh siad cód difriúil sa
mhodh `draw` chun a shainiú conas an cineál sin a tharraingt, mar atá ag `Button` anseo
(gan an cód GUI iarbhír, mar a luadh). D'fhéadfadh bloc breise `impl` a bheith ag an gcineál `Button`, mar shampla, ina bhfuil modhanna a bhaineann leis an méid
a tharlaíonn nuair a chliceálann úsáideoir an cnaipe. Ní bheidh feidhm ag na cineálacha modhanna seo maidir le
cineálacha cosúil le `TextField`.

Má chinneann duine atá ag baint úsáide as ár leabharlann struchtúr `SelectBox` a chur i bhfeidhm a bhfuil
réimsí `width`, `height`, agus `options` ann, cuirfidh siad an tréith `Draw` i bhfeidhm ar an
chineál
`SelectBox` chomh maith, mar a thaispeántar i Liostáil 18-8:

<Listing number="18-8" file-name="src/main.rs" caption="Another crate using `gui` and implementing the `Draw` trait on a `SelectBox` struct">

```rust,ignore
{{#rustdoc_include ../../listings/ch18-oop/listing-18-08/src/main.rs:here}}
```

</Listing>

Is féidir le húsáideoir ár leabharlainne a bhfeidhm `main` a scríobh anois chun sampla `Screen` a chruthú. Leis an sampla `Screen`, is féidir leo `SelectBox` agus `Button` a chur leis trí gach ceann acu a chur i `Box<T>` chun réad tréithe a bheith ann. Ansin is féidir leo glaoch ar an modh `run` ar an sampla `Screen`, a ghlaoidh `draw` ar gach ceann de na comhpháirteanna. Taispeánann Liostáil 18-9 an cur i bhfeidhm seo:

<Listing number="18-9" file-name="src/main.rs" caption="Using trait objects to store values of different types that implement the same trait">

```rust,ignore
{{#rustdoc_include ../../listings/ch18-oop/listing-18-09/src/main.rs:here}}
```

</Listing>

Nuair a scríobhamar an leabharlann, ní raibh a fhios againn go bhféadfadh duine éigin an cineál `SelectBox` a chur leis, ach bhí ár gcur i bhfeidhm `Screen` in ann oibriú ar an
gcineál nua agus é a tharraingt toisc go gcuireann `SelectBox` an tréith `Draw` i bhfeidhm, rud a chiallaíonn go gcuireann sé an modh `draw` i bhfeidhm.

Tá an coincheap seo - a bheith ag plé leis na teachtaireachtaí a bhfreagraíonn luach dóibh amháin - cosúil le cineál coincréiteach an luacha - cosúil le coincheap clóscríofa _duck_ i dteangacha clóscríofa go dinimiciúil: má shiúlann sé cosúil le lacha agus má dhéanann sé gáire
cosúil le lacha, ansin caithfidh sé a bheith ina lacha! I gcur i bhfeidhm `run` ar `Screen` i Liosta 18-5, ní gá do `run` a bheith ar an eolas faoi chineál coincréiteach gach
comhpháirte. Ní dhéanann sé seiceáil an sampla de `Button`
nó de `SelectBox` atá i gcomhpháirt, glaonn sé ar an modh `draw` ar an gcomhpháirt. Trí `Box<dyn Draw>` a shonrú mar chineál na luachanna sa veicteoir `components`, tá `Screen` sainmhínithe againn chun luachanna a theastaíonn uainn ar féidir linn an modh `draw` a ghlaoch orthu.

Is é an buntáiste a bhaineann le húsáid réada tréithe agus córas cineáil Rust chun cód a scríobh
cosúil le cód ag baint úsáide as clóscríobh lachan ná nach gá dúinn a sheiceáil riamh an gcuireann luach modh áirithe i bhfeidhm ag am rite ná a bheith buartha faoi earráidí a fháil
mura gcuireann luach modh i bhfeidhm ach go nglaoimid air ar aon nós. Ní thiomsóidh Rust
ár gcód mura gcuireann na luachanna na tréithe a theastaíonn ó na réada tréithe i bhfeidhm.

Mar shampla, taispeánann Liostáil 18-10 cad a tharlaíonn má dhéanaimid iarracht `Screen` a chruthú
le `String` mar chomhpháirt:


<Listing number="18-10" file-name="src/main.rs" caption="Attempting to use a type that doesn’t implement the trait object’s trait">

```rust,ignore,does_not_compile
{{#rustdoc_include ../../listings/ch18-oop/listing-18-10/src/main.rs}}
```

</Listing>

Gheobhaimid an earráid seo mar nach gcuireann `String` an tréith `Draw` i bhfeidhm:

```console
{{#include ../../listings/ch18-oop/listing-18-10/output.txt}}
```

Cuireann an earráid seo in iúl dúinn go bhfuil rud éigin á chur ar aghaidh againn chuig `Screen` nach raibh sé i gceist againn a chur ar aghaidh agus mar sin ba chóir dúinn cineál difriúil a chur ar aghaidh nó ba chóir dúinn `Draw` a chur i bhfeidhm ar `String` ionas go mbeidh `Screen` in ann glaoch ar `draw` air.

### Trait Objects Perform Dynamic Dispatch

Meabhraigh sa chuid [“Performance of Code Using
Generics”][performance-of-code-using-generics]<!-- ignore --> i gCaibidil
10 ár bplé ar an bpróiseas monamórfúcháin a dhéantar ar ghinearálacha ag an
comhdaitheoir: gineann an comhdaitheoir cur i bhfeidhm neamhghinearálacha feidhmeanna agus
modhanna do gach cineál coincréite a úsáidimid in ionad paraiméadar cineáil ghinearálta.
Tá an cód a eascraíonn as monamórfúchán ag déanamh _static dispatch_, is é sin
nuair a bhíonn a fhios ag an comhdaitheoir cén modh atá á ghlaoch agat ag am an chomdaithe. Tá sé seo
i gcodarsnacht le _dynamic dispatch_, is é sin nuair nach féidir leis an comhdaitheoir a rá ag am an chomdaithe
cé acu modh atá á ghlaoch agat. I gcásanna seolta dinimiciúla, astaíonn an tiomsaitheoir
cód a chinnfidh ag am rith cén modh atá le glaoch.

Nuair a úsáidimid réada tréithe, ní mór do Rust seolta dinimiciúil a úsáid. Níl a fhios ag an tiomsaitheoir
na cineálacha go léir a d'fhéadfaí a úsáid leis an gcód atá ag úsáid réada tréithe,
mar sin níl a fhios aige cén modh atá curtha i bhfeidhm ar cén cineál atá le glaoch. Ina áit sin, ag
am rith, úsáideann Rust na pointeoirí taobh istigh den réad tréithe chun a fháil amach cén modh atá le
ghlao. Tabhaíonn an cuardach seo costas rith-ama nach dtarlaíonn le seolta
statach. Cuireann seolta dinimiciúil cosc ​​​​ar an tiomsaitheoir freisin cód modh a ionchló, rud a chuireann cosc ​​​​ar roinnt optamuithe, agus tá roinnt rialacha ag Rust faoi cá háit ar féidir agus nach féidir leat seolta dinimiciúil a úsáid, ar a dtugtar [_dyn compatibility_][dyn-compatibility]. Mar sin féin, fuair muid solúbthacht bhreise sa chód
a scríobhamar i Liostáil 18-5 agus a raibh muid in ann tacú leis i Liostáil 18-9, mar sin is
trábhlóid le breithniú é.

[performance-of-code-using-generics]: ch10-01-syntax.html#performance-of-code-using-generics
[dynamically-sized]: ch20-03-advanced-types.html#dynamically-sized-types-and-the-sized-trait
[dyn-compatibility]: https://doc.rust-lang.org/reference/items/traits.html#dyn-compatibility	