## Patrún Dearaidh Dírithe ar Réada a Chur i bhFeidhm

Is patrún dearaidh dírithe ar réada é an _patrún stáit_. Is é croílár an
phatrúin ná go sainmhínímid sraith stát a d'fhéadfadh a bheith ag luach go hinmheánach. Léirítear na
stáit le sraith de _réada stáit_, agus athraíonn iompar an luacha
bunaithe ar a staid. Oibreoimid trí shampla de struchtúr
post bhlag a bhfuil réimse ann chun a staid a choinneáil, a bheidh ina réad stáit
ón tsraith "dréacht", "athbhreithniú", nó "foilsithe".

Roinneann na réada stáit feidhmiúlacht: i Rust, ar ndóigh, úsáidimid struchtúir agus
tréithe seachas réada agus oidhreacht. Tá gach réad stáit freagrach
as a iompar féin agus as rialú cathain ba chóir dó athrú go stát
eile. Níl a fhios ag an luach a shealbhaíonn réad stáit aon rud faoi iompar difriúil na stát ná cathain is ceart aistriú idir stáit.

Is é an buntáiste a bhaineann le patrún an stáit a úsáid ná, nuair a athraíonn
riachtanais ghnó an chláir, nach mbeidh orainn cód an
luacha ina bhfuil an stát ná an cód a úsáideann an luach a athrú. Ní bheidh orainn ach an cód a nuashonrú taobh istigh de cheann de na réada stáit chun a rialacha a athrú nó b'fhéidir
níos mó réada stáit a chur leis.

Ar dtús, cuirfimid patrún an stáit i bhfeidhm ar bhealach níos traidisiúnta
atá dírithe ar réada, ansin úsáidfimid cur chuige atá beagán níos nádúrtha i
Rust. Déanaimis iniúchadh ar shreabhadh oibre post blag a chur i bhfeidhm de réir a chéile ag baint úsáide as an
patrún stáit.

Beidh an fheidhmiúlacht dheireanach mar seo a leanas:

1. Tosaíonn post blag mar dhréacht folamh.
2. Nuair a bheidh an dréacht déanta, iarrtar athbhreithniú ar an bpost.
3. Nuair a cheadaítear an post, foilsítear é.
4. Ní thugann ach poist bhlag foilsithe ábhar ar ais le priontáil, mar sin ní féidir poist neamhcheadaithe a fhoilsiú de thaisme.

Níor cheart go mbeadh aon éifeacht ag aon athruithe eile a dhéantar ar phost. Mar shampla, má dhéanaimid iarracht dréachtphost blag a cheadú sula n-iarraimid athbhreithniú, ba chóir go bhfanfadh an post ina dhréacht neamhfhoilsithe.

Léiríonn Liostáil 18-11 an sreabhadh oibre seo i bhfoirm cóid: seo sampla úsáide den
API a chuirfimid i bhfeidhm i gcliathbhosca leabharlainne darb ainm `blog`. Ní thiomsófar é seo fós
toisc nach bhfuil an cliathbhosca `blog` curtha i bhfeidhm againn.

<Listing number="18-11" file-name="src/main.rs" caption="Code that demonstrates the desired behavior we want our `blog` crate to have">

```rust,ignore,does_not_compile
{{#rustdoc_include ../../listings/ch18-oop/listing-18-11/src/main.rs:all}}
```

</Listing>

Ba mhaith linn ligean don úsáideoir dréachtphost nua blag a chruthú le `Post::new`. Ba mhaith linn ligean do théacs a chur leis an bpost blag. Má dhéanaimid iarracht ábhar an phoist a fháil láithreach, roimh cheadú, níor cheart dúinn aon téacs a fháil mar go bhfuil an post fós ina dhréacht. Chuireamar `assert_eq!` leis an gcód chun críocha taispeána. Bheadh ​​tástáil aonaid den scoth chuige seo ná a dhearbhú go dtugann dréachtphost blag teaghrán folamh ar ais ón modh `content`, ach nílimid chun tástálacha a scríobh don sampla seo.

Ansin, ba mhaith linn iarratas ar athbhreithniú ar an bpost a chumasú, agus ba mhaith linn go dtabharfadh `content` teaghrán folamh ar ais agus muid ag fanacht leis an athbhreithniú. Nuair a fhaigheann an post ceadú, ba chóir é a fhoilsiú, rud a chiallaíonn go dtabharfar téacs an phoist ar ais nuair a ghlaoitear ar `content`.

Tabhair faoi deara gurb é an t-aon chineál a bhfuilimid ag idirghníomhú leis ón gcliathbhosca ná an cineál `Post`. Úsáidfidh an cineál seo an patrún stáit agus coinneoidh sé luach a bheidh ar cheann de thrí réad stáit a léiríonn na stáit éagsúla a d'fhéadfadh post a bheith
i ndréacht, ag fanacht le hathbhreithniú, nó foilsithe. Déanfar athrú ó stát amháin go stát eile
a bhainistiú go hinmheánach laistigh den chineál `Post`. Athraíonn na stáit mar
fhreagra ar na modhanna a ghlaonn úsáideoirí ár leabharlainne ar an gcás `Post`,
ach ní gá dóibh na hathruithe stáit a bhainistiú go díreach. Chomh maith leis sin, ní féidir le húsáideoirí
botún a dhéanamh leis na stáit, mar shampla post a fhoilsiú sula ndéantar athbhreithniú air.

### Sainmhíniú `Post` agus Cás Nua a Chruthú sa Stádas Dréachta

Tosaímis ar chur i bhfeidhm na leabharlainne! Tá a fhios againn go bhfuil
struchtúr `Post` poiblí de dhíth orainn a bhfuil roinnt ábhair ann, mar sin tosóimid leis an
sainmhíniú ar an struchtúr agus feidhm phoiblí `nua` ghaolmhar chun cás de `Post` a chruthú, mar a thaispeántar i Liostáil 18-12. Déanfaimid tréith phríobháideach `State` freisin a shaineoidh an t-iompar a chaithfidh gach réad stáit le haghaidh `Post` a bheith aige.

Ansin coinneoidh `Post` réad tréithe de `Box<dyn State>` taobh istigh de `Option<T>` i réimse príobháideach darb ainm `state` chun an réad stáit a choinneáil. Feicfidh tú cén fáth go bhfuil an
`Option<T>` riachtanach i gceann tamaill.

<Listing number="18-12" file-name="src/lib.rs" caption="Definition of a `Post` struct and a `new` function that creates a new `Post` instance, a `State` trait, and a `Draft` struct">

```rust,noplayground
{{#rustdoc_include ../../listings/ch18-oop/listing-18-12/src/lib.rs}}
```

</Listing>

Sainmhíníonn an tréith `State` an t-iompar a roinneann stáit éagsúla poist. Is iad na réada stáit `Draft`, `PendingReview`, agus `Published`, agus cuirfidh siad go léir an tréith `State` i bhfeidhm. Faoi láthair, níl aon mhodhanna ag an tréith, agus
tosaímid tríd an stát `Draft` amháin a shainiú mar is é sin an stát inar mian linn
go dtosódh post.

Nuair a chruthaímid `Post` nua, socraímid a réimse `state` go luach `Some` a
shealbhaíonn `Box`. Pointíonn an `Box` seo chuig sampla nua den struchtúr `Draft`.
Cinntíonn sé seo aon uair a chruthaímid sampla nua de `Post`, go dtosóidh sé mar
dhréacht. Toisc go bhfuil réimse `state` an `Post` príobháideach, níl aon bhealach ann
`Post` a chruthú in aon stát eile! Sa fheidhm `Post::new`, socraímid an réimse
`content` go `String` nua, folamh.

### Stóráil Téacs Ábhar an Phoist

Chonaiceamar i Liostáil 18-11 gur mhaith linn a bheith in ann glaoch ar mhodh darb ainm `add_text` agus `&str` a chur air a chuirtear leis ansin mar ábhar téacs an
phoist bhlag. Cuirimid é seo i bhfeidhm mar mhodh, seachas an réimse `content` a nochtadh mar `pub`, ionas gur féidir linn modh a chur i bhfeidhm níos déanaí a rialóidh conas a
léitear sonraí an réimse `content`. Tá an modh `add_text` sách
simplí, mar sin cuirimis an cur i bhfeidhm i Liostáil 18-13 leis an mbloc `impl
Post`:

<Listing number="18-13" file-name="src/lib.rs" caption="Implementing the `add_text` method to add text to a post’s `content`">

```rust,noplayground
{{#rustdoc_include ../../listings/ch18-oop/listing-18-13/src/lib.rs:here}}
```

</Listing>

Glacann an modh `add_text` tagairt inathraithe do `self`, mar go bhfuilimid ag athrú an tsampla `Post` a bhfuilimid ag glaoch `add_text` air. Ansin glaoimid `push_str` ar an `String` i `content` agus cuirimid an argóint `text` ar aghaidh chun é a chur leis
an `content` sábháilte. Ní bhraitheann an t-iompar seo ar an staid ina bhfuil an post,
mar sin níl sé mar chuid den phatrún staide. Ní idirghníomhaíonn an modh `add_text`
leis an réimse `state` ar chor ar bith, ach is cuid den iompar é ar mhaith linn
tacaíocht a thabhairt dó.

### A Chinntiú go bhfuil Ábhar Dréachta-Poist Folamh

Fiú tar éis dúinn `add_text` a ghlaoch agus roinnt ábhair a chur lenár bpost, ba mhaith linn fós go dtabharfadh an modh `content` slisne teaghráin folamh ar ais mar go bhfuil an post
fós i staid an dréachta, mar a thaispeántar ar líne 7 de Liostáil 18-11. Faoi láthair, déanaimis an modh `ábhar` a chur i bhfeidhm leis an rud is simplí a chomhlíonfaidh an riachtanas seo: slisne teaghráin folamh a thabhairt ar ais i gcónaí. Athróimid é seo níos déanaí nuair a chuirfimid an cumas i bhfeidhm staid poist a athrú ionas gur féidir é a fhoilsiú.
Go dtí seo, ní féidir le poist a bheith ach i staid dréachta, mar sin ba chóir go mbeadh ábhar an phoist folamh i gcónaí. Taispeánann Liostáil 18-14 an cur i bhfeidhm áitchoinneálaí seo:

<Listing number="18-14" file-name="src/lib.rs" caption="Adding a placeholder implementation for the `content` method on `Post` that always returns an empty string slice">

```rust,noplayground
{{#rustdoc_include ../../listings/ch18-oop/listing-18-14/src/lib.rs:here}}
```

</Listing>

Leis an modh `ábhar` breise seo, oibríonn gach rud i Liostáil 18-11 suas go dtí líne 7 mar a bhí beartaithe.

### Athraíonn Athbhreithniú ar an bPost a Stádas

Ansin, ní mór dúinn feidhmiúlacht a chur leis chun athbhreithniú ar phost a iarraidh, agus ba cheart go n-athródh sé a staid ó `Draft` go `PendingReview`. Taispeánann Liostáil 18-15 an cód seo:

<Listing number="18-15" file-name="src/lib.rs" caption="Implementing `request_review` methods on `Post` and the `State` trait">

```rust,noplayground
{{#rustdoc_include ../../listings/ch18-oop/listing-18-15/src/lib.rs:here}}
```

</Listing>

Tugaimid modh poiblí darb ainm `request_review` do `Post` a ghlacfaidh tagairt inathraithe
do `self`. Ansin glaoimid ar mhodh inmheánach `request_review` ar an
stádas reatha de `Post`, agus ídíonn an dara modh `request_review` seo an
stádas reatha agus tugann sé staid nua ar ais.

Cuirimid an modh `request_review` leis an tréith `State`; beidh ar gach cineál a
chuireann an tréith i bhfeidhm an modh `request_review` a chur i bhfeidhm anois.
Tabhair faoi deara, seachas `self`, `&self`, nó `&mut self` a bheith mar an chéad
pharaiméadar den mhodh, go bhfuil `self: Box<Self>` againn. Ciallaíonn an comhréir seo nach bhfuil an
modh bailí ach amháin nuair a ghlaotar air ar `Box` ina bhfuil an cineál. Glacann an comhréir seo
úinéireacht ar `Box<Self>`, ag cur an tseanstaid ar neamhní ionas gur féidir luach stádais an
`Post` a athrú go staid nua.

Chun an seanstádas a ídiú, ní mór don mhodh `request_review` úinéireacht
a ghlacadh ar an luach stádais. Seo an áit a dtagann an `Option` sa réimse `state` de `Post` isteach: glaoimid ar an modh `take` chun an luach `Some` a bhaint as an réimse `state` agus `None` a fhágáil ina áit, mar ní ligeann Rust dúinn réimsí neamhlíonta a bheith againn i struchtúir. Ligeann sé seo dúinn an luach `state` a bhogadh amach as
`Post` seachas é a fháil ar iasacht. Ansin socróimid luach `state` an phoist mar
thoradh na hoibríochta seo.

Ní mór dúinn `state` a shocrú go `None` go sealadach seachas é a shocrú go díreach
le cód cosúil le `self.state = self.state.request_review();` chun úinéireacht a fháil ar
luach an `state`. Cinntíonn sé seo nach féidir le `Post` an seanluach `state` a úsáid tar éis
dúinn é a chlaochlú go stát nua.

Tugann an modh `request_review` ar `Draft` sampla nua, boscaithe de struchtúr nua `PendingReview` ar ais, a léiríonn an stát nuair a bhíonn post ag fanacht le
hathbhreithniú. Cuireann an struchtúr `PendingReview` an modh `request_review` i bhfeidhm freisin
ach ní dhéanann sé aon chlaochluithe. Ina áit sin, filleann sé é féin, mar nuair a
iarraimid athbhreithniú ar phost atá cheana féin sa stát `PendingReview`, ba chóir dó fanacht
sa stát `PendingReview`.

Anois is féidir linn tosú ag feiceáil buntáistí an phatrúin stáit: tá an
modh `request_review` ar `Post` mar an gcéanna is cuma cén luach `state` atá air. Tá gach
stádas freagrach as a rialacha féin.

Fágfaimid an modh `content` ar `Post` mar atá, ag filleadh slisne teaghráin folamh. Is féidir linn `Post` a bheith againn anois sa stát `PendingReview` chomh maith leis an
stádas `Draft`, ach ba mhaith linn an t-iompar céanna sa stát `PendingReview`.
Oibríonn Liostáil 18-11 anois suas go dtí líne 10!

<!-- Seancheannteidil. Ná bain iad nó d'fhéadfadh naisc briseadh. -->

<a id="adding-the-approve-method-that-changes-the-behavior-of-content"></a>

### Ag cur `approve` leis chun Iompar `content` a Athrú

Beidh an modh `approve` cosúil leis an modh `request_review`: socróidh sé `state` go dtí an luach a deir an staid reatha ba chóir a bheith aige nuair a cheadaítear an staid sin, mar a thaispeántar i Liostáil 18-16:

<Listing number="18-16" file-name="src/lib.rs" caption="Implementing the `approve` method on `Post` and the `State` trait">

```rust,noplayground
{{#rustdoc_include ../../listings/ch18-oop/listing-18-16/src/lib.rs:here}}
```

</Listing>

Cuirimid an modh `approve` leis an tréith `State` agus cuirimid struchtúr nua leis a chuireann `State` i bhfeidhm, an staid `Published`.

Cosúil leis an gcaoi a n-oibríonn `request_review` ar `PendingReview`, má ghlaonn muid ar an modh `approve` ar `Draft`, ní bheidh aon éifeacht aige mar go dtabharfaidh `approve` `self` ar ais. Nuair a ghlaonn muid ar `approve` ar `PendingReview`, tugann sé sampla nua, boscaithe, den struchtúr `Published` ar ais. Cuireann an struchtúr `Published` an tréith `State` i bhfeidhm, agus i gcás an mhodha `request_review` agus an mhodha `approve` araon, tugann sé é féin ar ais, mar ba chóir don phost fanacht sa staid `Published` sna cásanna sin.

Anois ní mór dúinn an modh `content` a nuashonrú ar `Post`. Ba mhaith linn go mbeadh an luach a thugtar ar ais ó `content` ag brath ar staid reatha an `Post`, mar sin beidh an `Post` toscaire chuig modh `content` atá sainmhínithe ar a `state`,
mar a thaispeántar i Liostáil 18-17:

<Listing number="18-17" file-name="src/lib.rs" caption="Updating the `content` method on `Post` to delegate to a `content` method on `State`">

```rust,ignore,does_not_compile
{{#rustdoc_include ../../listings/ch18-oop/listing-18-17/src/lib.rs:here}}
```

</Listing>

Ós rud é gurb é an sprioc na rialacha seo go léir a choinneáil laistigh de na struchtúir a chuireann `State` i bhfeidhm, glaoimid modh `content` ar an luach i `state` agus cuirimid an sampla `post` (is é sin, `self`) ar aghaidh mar argóint. Ansin, cuirimid an luach ar ais a
fhilleann trí úsáid a bhaint as an modh `content` ar an luach `state`.

Tugaimid an modh `as_ref` ar an `Option` mar ba mhaith linn tagairt don
luach laistigh den `Option` seachas úinéireacht an luacha. Ós rud é gur `Option<Box<dyn State>>` é `state`, nuair a ghlaonn muid ar `as_ref`, cuirtear `Option<&Box<dyn
State>>` ar ais. Mura nglaonn muid ar `as_ref`, gheobhaimis earráid mar
ní féidir linn `state` a bhogadh amach as an `&self` iasachta den pharaiméadar feidhme.

Ansin glaoimid ar an modh `unwrap`, rud nach mbeidh scaoll orainn choíche, mar tá a fhios againn go gcinntíonn na modhanna ar `Post` go mbeidh luach `Some` i `state` i gcónaí nuair a bheidh na modhanna sin déanta. Seo ceann de na cásanna a phléamar sa
chuid [“Cásanna ina bhfuil Tuilleadh Eolais Agat Ná an
Tiomsaitheoir”][more-info-than-rustc]<!-- ignore --> de Chaibidil 9 nuair a
bhfuil a fhios againn nach féidir luach `None` a bheith ann choíche, cé nach bhfuil an tiomsaitheoir in ann
é sin a thuiscint.

Ag an bpointe seo, nuair a ghlaonn muid ar `content` ar an `&Box<dyn State>`, beidh éifeacht ag deref coercion ar an `&` agus ar an `Box` agus mar sin glaofar ar an modh `content` sa deireadh ar an gcineál a chuireann an tréith `State` i bhfeidhm. Ciallaíonn sé sin go gcaithfimid `ábhar` a chur leis an sainmhíniú tréithe `State`, agus sin an áit a gcuirfimid an loighic maidir leis an ábhar atá le tabhairt ar ais ag brath ar an stát atá againn, mar a thaispeántar i Liostáil 18-18:

<Listing number="18-18" file-name="src/lib.rs" caption="Adding the `content` method to the `State` trait">

```rust,noplayground
{{#rustdoc_include ../../listings/ch18-oop/listing-18-18/src/lib.rs:here}}
```

</Listing>

Cuirimid cur i bhfeidhm réamhshocraithe leis don mhodh `content` a thugann slisne teaghrán folamh ar ais. Ciallaíonn sé sin nach gá dúinn `content` a chur i bhfeidhm ar na struchtúir `Draft` agus `PendingReview`. Sáróidh an struchtúr `Published` an modh `content` agus cuirfidh sé an luach i `post.content` ar ais.

Tabhair faoi deara go bhfuil nótaí saoil ag teastáil uainn ar an modh seo, mar a phléamar i
gCaibidil 10. Táimid ag glacadh tagairt do `post` mar argóint agus ag filleadh tagairt do chuid den `post` sin, mar sin tá saolré an tagartha a tugadh ar ais gaolmhar le saolré an argóint `post`.

Agus táimid críochnaithe—oibríonn Liosta 18-11 anois! Tá an patrún stáit curtha i bhfeidhm againn le rialacha shreabhadh oibre an phoist bhlag. Tá an loighic a bhaineann leis na
rialacha ina gcónaí sna réada stáit seachas a bheith scaipthe ar fud `Post`.

> #### Cén Fáth Nach bhfuil Enum ann? 
> B’fhéidir go raibh tú ag smaoineamh cén fáth nár úsáid muid `enum` leis na stáit phoist éagsúla
> mar athróga. Is réiteach féideartha é sin cinnte, bain triail as
> agus déan comparáid idir na torthaí deiridh chun a fheiceáil cé acu is fearr leat! Míbhuntáiste amháin a bhaineann le
> enum a úsáid ná go mbeidh gá le
> abairt `match` nó a leithéid i ngach áit a sheiceálann luach an enum chun gach athróg féideartha a láimhseáil. D’fhéadfadh sé seo a bheith níos athchleachtach ná an réiteach tréith réada seo.

### Comhbhabhtálacha an Phatrúin Stáit

Tá sé léirithe againn go bhfuil Rust in ann an patrún stáit atá dírithe ar réada a chur i bhfeidhm chun na cineálacha éagsúla iompair ba chóir a bheith ag post i
ngach stát a chuimsiú. Níl aon rud ar eolas ag na modhanna ar `Post` faoi na hiompraíochtaí éagsúla. An
tslí ar eagraíomar an cód, ní mór dúinn breathnú in aon áit amháin chun na
bealaí éagsúla a fháil amach inar féidir le post foilsithe iompar: cur i bhfeidhm an tréith `State`
ar an struchtúr `Published`.

Dá mbeadh orainn cur i bhfeidhm malartach a chruthú nach n-úsáidfeadh an patrún stáit, d'fhéadfaimis nathanna `match` a úsáid sna modhanna ar `Post` nó fiú sa chód `main` a sheiceálann staid an phoist agus a athraíonn iompar sna háiteanna sin. Chiallódh sé sin go mbeadh orainn breathnú i roinnt áiteanna chun
tuigbheáil a dhéanamh ar na himpleachtaí go léir a bhaineann le post a bheith sa staid fhoilsithe! Ní dhéanfadh sé seo ach méadú dá mhéad staid a chuirfimis leis: bheadh ​​​​lámh eile ag teastáil ó gach ceann de na nathanna `match` sin.

Leis an patrún stáit, níl nathanna `match` ag teastáil ó na modhanna `Post` agus na háiteanna ina n-úsáidimid `Post`, agus chun staid nua a chur leis, ní bheadh ​​​​ort ach
struchtúr nua a chur leis agus na modhanna tréithe a chur i bhfeidhm ar an struchtúr sin.

Is furasta an cur i bhfeidhm a úsáideann an patrún stáit a leathnú chun níos mó
feidhmiúlachta a chur leis. Chun simplíocht an chóid a chothabháil a úsáideann an
patrún stáit a fheiceáil, bain triail as cúpla ceann de na moltaí seo:

- Cuir modh `reject` leis a athraíonn staid an phoist ó 'Ag Feitheamh Athbhreithnithe' ar ais
go `Draft`. 
- Éilítear dhá ghlao chun `approve` a dhéanamh sula bhféadfar an stát a athrú go `Published`.
- Ceadaítear d'úsáideoirí ábhar téacs a chur leis ach amháin nuair atá post i stát `Draft`.
Leid: bíodh an réad stáit freagrach as a bhféadfadh athrú a dhéanamh faoin
ábhar ach ní bheidh sé freagrach as an `Post` a mhodhnú.

Míbhuntáiste amháin a bhaineann leis an bpatrún stáit ná, toisc go gcuireann na stáit na
haistrithe idir stáit i bhfeidhm, go bhfuil cuid de na stáit cúpláilte lena chéile. Dá
mbeadh
stát eile á chur againn idir `PendingReview` agus `Published`, amhail `Scheduled`,
bheadh ​​orainn an cód i `PendingReview` a athrú chun aistriú go
`Scheduled` ina ionad. Bheadh ​​​​sé níos lú oibre mura mbeadh ar `PendingReview`
athrú le stát nua a chur leis, ach chiallódh sé sin aistriú go
patrún dearaidh eile.

Míbhuntáiste eile is ea gur dhúblaíomar roinnt loighce. Chun cuid den
dúbláil a dhíchur, d'fhéadfaimis iarracht a dhéanamh cur i bhfeidhm réamhshocraithe a dhéanamh do na modhanna
`request_review` agus `approve` ar an tréith `State` a thugann `self` ar ais;
mar sin féin, ní bheadh ​​sé seo comhoiriúnach le dyn, mar níl a fhios ag an tréith cad
a bheidh sa `self` coincréiteach go díreach. Ba mhaith linn a bheith in ann `State` a úsáid mar
réad tréithe, mar sin ní mór dúinn a mhodhanna a bheith comhoiriúnach le dyn.

I measc dúbláil eile tá cur i bhfeidhm comhchosúla na modhanna `request_review`
agus `approve` ar `Post`. Déanann an dá mhodh tarmligean chuig cur i bhfeidhm
an mhodha chéanna ar an luach sa réimse `state` de `Option::take` agus socraíonn siad an luach
nua den réimse `state` don toradh. Dá mbeadh go leor modhanna againn ar `Post`
a lean an patrún seo, d'fhéadfaimis smaoineamh ar mhacra a shainiú chun an
athrá a dhíchur (féach an chuid [“Macros”][macros]<!-- ignore --> i gCaibidil 20).

Trí an patrún stáit a chur i bhfeidhm díreach mar atá sé sainmhínithe do theangacha réada-dhírithe, nílimid ag baint an leasa is mó as láidreachtaí Rust agus a d'fhéadfaimis.
Féachaimid ar roinnt athruithe is féidir linn a dhéanamh ar an gcliathbhosca `blog` a fhéadann stáit neamhbhailí agus aistrithe a dhéanamh ina n-earráidí ag am tiomsaithe.

#### Ionchódú Stáit agus Iompair mar Chineálacha

Taispeánfaimid duit conas athmhachnamh a dhéanamh ar an bpatrún stáit chun sraith dhifriúil de
chomhréitigh a fháil. In ionad na stáit agus na haistrithe a chuimsiú go hiomlán ionas nach mbeidh aon eolas ag an gcód seachtrach orthu, déanfaimid na stáit a ionchódú i gcineálacha
difriúla. Dá bhrí sin, cuirfidh córas seiceála cineáil Rust cosc ​​ar iarrachtaí chun
poist dréachta a úsáid i gcás nach gceadaítear ach poist fhoilsithe trí earráid tiomsaitheora a eisiúint.

Breithnímis an chéad chuid de `main` i Liostáil 18-11:

<Listing file-name="src/main.rs">

```rust,ignore
{{#rustdoc_include ../../listings/ch18-oop/listing-18-11/src/main.rs:here}}
```

</Listing>

Cuirimid ar ár gcumas fós poist nua a chruthú i riocht dréachta ag baint úsáide as `Post::new`
agus an cumas téacs a chur le hábhar an phoist. Ach in ionad modh `content` a bheith againn ar phost dréachta a thugann teaghrán folamh ar ais, déanfaimid amhlaidh nach mbeidh an modh `content` ar chor ar bith ag poist dréachta. Ar an mbealach sin, má dhéanaimid iarracht ábhar phost dréachta a fháil, gheobhaidh muid earráid tiomsaitheora ag insint dúinn nach bhfuil an modh ann. Mar thoradh air sin, beidh sé dodhéanta dúinn ábhar an phoist dréachta a thaispeáint de thaisme i dtáirgeadh, mar ní thiomsóidh an cód sin fiú.
Léiríonn liostú 18-19 sainmhíniú struchtúr `Post` agus struchtúr `DraftPost`,
chomh maith le modhanna ar gach ceann acu:

<Listing number="18-19" file-name="src/lib.rs" caption="A `Post` with a `content` method and `DraftPost` without a `content` method">

```rust,noplayground
{{#rustdoc_include ../../listings/ch18-oop/listing-18-19/src/lib.rs}}
```

</Listing>

Tá réimse príobháideach `content` ag an struchtúr `Post` agus `DraftPost` araon a
stórálann téacs an phoist bhlag. Níl an réimse `state` ag na struchtúir a thuilleadh mar
táimid ag bogadh ionchódú an stáit go dtí cineálacha na struchtúr. Léireoidh an struchtúr `Post` post foilsithe, agus tá modh `content` aige
a thugann an `content` ar ais.

Tá feidhm `Post::new` againn fós, ach in ionad sampla de
`Post` a thabhairt ar ais, tugann sé sampla de `DraftPost` ar ais. Ós rud é go bhfuil `content` príobháideach
agus nach bhfuil aon fheidhmeanna ann a thugann `Post` ar ais, ní féidir sampla de `Post` a chruthú faoi láthair.

Tá modh `add_text` ag an struchtúr `DraftPost`, mar sin is féidir linn téacs a chur le
`content` mar a bhí roimhe, ach tabhair faoi deara nach bhfuil modh `content` sainmhínithe ag `DraftPost`! Mar sin, cinntíonn an clár anois go dtosaíonn gach post mar dhréachtphoist, agus nach bhfuil a n-ábhar ar fáil le taispeáint i ndréachtphoist. Mar thoradh ar aon iarracht na srianta seo a sheachaint, beidh earráid tiomsaitheora ann.

#### Aistrithe a Chur i bhFeidhm mar Chlaochluithe i gCineálacha Éagsúla

Mar sin, conas a fhaighimid post foilsithe? Ba mhaith linn an riail a fhorfheidhmiú go gcaithfear dréachtphost a athbhreithniú agus a cheadú sula bhféadfar é a fhoilsiú. Níor cheart go mbeadh aon ábhar le feiceáil i bpost atá sa stát
athbhreithniú ar feitheamh. Cuirfimid na srianta seo i bhfeidhm trí struchtúr eile, `PendingReviewPost`, a chur leis, an modh `request_review` a shainiú ar `DraftPost` chun `PendingReviewPost` a thabhairt ar ais, agus modh `approve` a shainiú ar `PendingReviewPost` chun `Post` a thabhairt ar ais, mar a thaispeántar i Liostáil 18-20:

<Listing number="18-20" file-name="src/lib.rs" caption="A `PendingReviewPost` that gets created by calling `request_review` on `DraftPost` and an `approve` method that turns a `PendingReviewPost` into a published `Post`">

```rust,noplayground
{{#rustdoc_include ../../listings/ch18-oop/listing-18-20/src/lib.rs:here}}
```

</Listing>

Glacann na modhanna `request_review` agus `approve` úinéireacht ar `self`, agus ar an gcaoi sin
gáíonn siad na samplaí `DraftPost` agus `PendingReviewPost` agus claochlaíonn siad
iad ina `PendingReviewPost` agus ina `Post` foilsithe, faoi seach. Ar an mbealach seo,
ní bheidh aon samplaí `DraftPost` fágtha againn tar éis dúinn `request_review` a ghlaoch orthu, agus mar sin de. Níl modh `content` sainmhínithe ar struchtúr `PendingReviewPost`, mar sin bíonn earráid tiomsaithe mar thoradh ar iarracht a ábhar a léamh,
mar atá le `DraftPost`. Ós rud é gurb é an t-aon bhealach chun sampla `Post` foilsithe a fháil a bhfuil modh `content` sainmhínithe ann ná glaoch ar an modh `approve` ar `PendingReviewPost`, agus gurb é an t-aon bhealach chun `PendingReviewPost` a fháil ná glaoch ar an modh `request_review` ar `DraftPost`,
tá sreabhadh oibre an phoist bhlag ionchódaithe againn anois isteach sa chóras cineáil.

Ach ní mór dúinn roinnt athruithe beaga a dhéanamh ar `main` freisin. Tugann na modhanna `request_review` agus `approve` cásanna nua ar ais seachas an struchtúr a nglaotar orthu a mhodhnú, mar sin ní mór dúinn níos mó sannadh scáthaithe `let post =` a chur leis chun na cásanna a tugadh ar ais a shábháil. Ní féidir linn na dearbhuithe faoi ábhar an dréachta agus
ábhar na bpost athbhreithnithe atá ar feitheamh a bheith ina dteaghráin fholmha ach an oiread, agus níl siad de dhíth orainn ach an oiread: ní féidir linn
cód a thiomsú a dhéanann iarracht ábhar na bpost sna stáit sin a úsáid a thuilleadh.
Taispeántar an cód nuashonraithe i `main` i Liostáil 18-21:

<Listing number="18-21" file-name="src/main.rs" caption="Modifications to `main` to use the new implementation of the blog post workflow">

```rust,ignore
{{#rustdoc_include ../../listings/ch18-oop/listing-18-21/src/main.rs}}
```

</Listing>

Ciallaíonn na hathruithe a bhí orainn a dhéanamh ar `main` chun `post` a athshannadh nach leanann an
cur i bhfeidhm seo an patrún stáit atá dírithe ar réada a thuilleadh:
níl na claochluithe idir na stáit curtha i bhfeidhm go hiomlán a thuilleadh
laistigh den chur i bhfeidhm `Post`. Mar sin féin, is é an buntáiste atá againn ná go bhfuil stáit neamhbhailí
dodhéanta anois mar gheall ar an gcóras cineáil agus an tseiceáil cineáil a tharlaíonn ag
am an tiomsaithe! Cinntíonn sé seo go bhfaighfear fabhtanna áirithe, amhail taispeáint ábhar
post neamhfhoilsithe, sula sroicheann siad an táirgeadh.

Bain triail as na tascanna a mholtar ag tús an ailt seo ar an gcliathbhosca `blog` mar atá
sé tar éis Liostáil 18-21 chun a fheiceáil cad a cheapann tú faoi dhearadh an leagan seo
den chód. Tabhair faoi deara go bhféadfadh cuid de na tascanna a bheith críochnaithe cheana féin sa
dhearadh seo.

Tá feicthe againn, cé go bhfuil Rust in ann patrúin dearaidh atá dírithe ar réada a chur i bhfeidhm, go bhfuil patrúin eile, amhail ionchódú stáit isteach sa chóras cineáil,
ar fáil i Rust freisin. Tá comhbhabhtálacha éagsúla ag na patrúin seo. Cé go mb’fhéidir go bhfuil tú an-eolach ar phatrúin atá dírithe ar réada, is féidir le hathmhachnamh a dhéanamh ar an
fhadhb chun leas a bhaint as gnéithe Rust buntáistí a sholáthar, amhail
cosc a chur ar roinnt fabhtanna ag am tiomsaithe. Ní bheidh patrúin atá dírithe ar réada i gcónaí
an réiteach is fearr i Rust mar gheall ar ghnéithe áirithe, cosúil le húinéireacht, nach
bhfuil ag teangacha atá dírithe ar réada.

## Achoimre

Is cuma an gceapann tú gur teanga réada-dhírithe í Rust nó nach gceapann tar éis duit an chaibidil seo a léamh, tá a fhios agat anois gur féidir leat tréithe réada a úsáid chun roinnt gnéithe réada-dhírithe a fháil i Rust. Is féidir le seoladh dinimiciúil roinnt solúbthachta a thabhairt do do chód mar mhalairt ar fheidhmíocht rith-ama. Is féidir leat an tsolúbthacht seo a úsáid chun patrúin réada-dhírithe a chur i bhfeidhm a chabhróidh le hinchothabháil do chóid. Tá gnéithe eile ag Rust freisin, cosúil le húinéireacht, nach bhfuil ag teangacha réada-dhírithe. Ní bheidh patrún réada-dhírithe i gcónaí ar an mbealach is fearr chun leas a bhaint as láidreachtaí Rust, ach is rogha atá ar fáil é.

Ansin, féachfaimid ar phatrúin, arb iad gnéithe eile de chuid Rust iad a chuireann go leor solúbthachta ar fáil. Táimid tar éis breathnú orthu go hachomair ar fud an leabhair ach ní fhaca muid a gcumas iomlán fós. A ligean ar aghaidh linn!

[more-info-than-rustc]: ch09-03-to-panic-or-not-to-panic.html#cases-in-which-you-have-more-information-than-the-compiler
[macros]: ch20-05-macros.html#macros