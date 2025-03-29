## Athmhacnamh chun Modúlacht agus Láimhseáil Earráidí a Fheabhsú

Chun ár gclár a fheabhsú, socróimid ceithre fhadhb a bhaineann leis an
struchtúr an chláir agus conas a láimhseáiltear earráidí féideartha. Ar dtús, ár `main`
Déanann Feidhm dhá thasc anois: parsálann sé argóintí agus léann sé comhaid. Mar ár
clár ag fás, líon na dtascanna ar leith Láimhseálann an `main` fheidhm Láimhseálann
méadú. De réir mar a ghnóthaíonn feidhm freagrachtaí, bíonn sé níos deacra
cúis faoi, níos deacra a thástáil, agus níos deacra a athrú gan briseadh ceann amháin dá
páirteanna. Is fearr feidhmiúlacht a scaradh ionas go mbeidh gach feidhm freagrach as
tasc amháin.

Tá baint ag an gceist seo leis an dara fadhb freisin: cé go bhfuil `query` agus `file_path`
is athróga cumraíochta iad dár gclár, úsáidtear athróga cosúil le `contents`
chun loighic an chláir a fheidhmiú. Dá fhaide a éiríonn `main`, is amhlaidh is mó athróg
beidh orainn scóip a thabhairt isteach; dá mhéad athróg atá againn i raon feidhme, is amhlaidh is deacra
beidh sé súil a choinneáil ar chuspóir gach ceann acu. Is fearr a ghrúpáil
athróga cumraíochta in aon struchtúr amháin chun a gcuspóir a dhéanamh soiléir.

Is í an tríú fadhb ná gur úsáideamar `expect` chun teachtaireacht earráide a phriontáil nuair a
theipeann ar léamh an chomhaid, ach ní phrionnaíonn an teachtaireacht earráide ach `Should have been
able to read the file`. Is féidir le léamh comhaid teip ar roinnt bealaí: do
mar shampla, seans go bhfuil an comhad ar iarraidh, nó seans nach bhfuil cead againn é a oscailt.
Faoi láthair, beag beann ar an gcás, ba mhaith linn an teachtaireacht earráide céanna a phriontáil lena haghaidh
gach rud, nach dtabharfadh an t-úsáideoir aon fhaisnéis!

Ceathrú, úsáidimid `expect` chun earráid a láimhseáil, agus má ritheann an t-úsáideoir ár gclár
gan dóthain argóintí a shonrú, gheobhaidh siad earráid `index out of bounds`
ó Rust nach míníonn go soiléir an fhadhb. B’fhearr dá mbeadh an
bhí an cód láimhseála earráidí in aon áit amháin agus mar sin ní raibh ach áit amháin ag cothóirí sa todhchaí
dul i gcomhairle leis an gcód más gá an loighic láimhseála earráidí a athrú. Tar éis na
Cinnteoidh cód láimhseála earráidí in aon áit amháin go bhfuilimid ag priontáil teachtaireachtaí
beidh brí leis sin dár n-úsáideoirí deiridh.

Rachaimid i ngleic leis na ceithre fhadhb seo trínár dtionscadal a athmhonarú.

### Imní maidir le Tionscadail Dhénártha a Scaradh

An fhadhb eagraíochtúil a bhaineann le freagracht as tascanna iolracha a leithdháileadh ar
tá an fheidhm `main` coitianta i go leor tionscadal dénártha. Mar thoradh air sin, an Rust
pobail i ndiaidh treoirlínte a fhorbairt chun na hábhair imní ar leith a roinnt a
clár dénártha nuair a thosaíonn `main` ag éirí mór. Tá an méid seo a leanas ag an bpróiseas seo
céimeanna:

- Roinn do chlár i gcomhad _main.rs_ agus i gcomhad _lib.rs_ agus bog do
 loighic an chláir chun _lib.rs_.
- Chomh fada agus a bhfuil do loighic parsála ordú beag, féadfaidh sé fanacht i
 _main.rs_.
- Nuair a thosaíonn loighic parsála na n-orduithe ag éirí níos casta, bain amach í
 ó _main.rs_ agus bog é go _lib.rs_.

Na freagrachtaí a fhanann sa `main` tar éis an phróisis seo
ba chóir a bheith teoranta dóibh seo a leanas:

- Ag glaoch ar an líne ordaithe loighic parsála leis na luachanna argóint
- Aon chumraíocht eile a chur ar bun
- Ag glaoch ar fheidhm `run` in _lib.rs_
- An earráid a láimhseáil má fhilleann `run` earráid

Baineann an patrún seo le hábhair imní a scaradh: _main.rs_ handles running the
Láimhseálann an clár agus _lib.rs_ loighic uile an taisc atá idir lámha. Mar gheall ort
ní féidir an fheidhm `main` a thástáil go díreach, ligeann an struchtúr seo duit gach ceann díobh a thástáil
loighic do chláir trí é a aistriú go feidhmeanna in _lib.rs_. An cód a
Beidh iarsmaí i _main.rs_ beag go leor chun a cruinneas a fhíorú trí léamh
é. Déanaimis ár gclár a athoibriú tríd an bpróiseas seo a leanúint.

#### Parsálaí Argóint a Bhaint as

Bainfimid an fheidhmiúlacht chun argóintí a pharsáil isteach in fheidhm a
Glaofaidh `main` chun ullmhú le haghaidh loighic parsála na n-orduithe a bhogadh go dtí
_src/lib.rs_. Léiríonn liostú 12-5 tús nua `main` a ghlaonn ceann nua
feidhm `parse_config`, a shaineoimid in _src/main.rs_ faoi láthair.

<Listing number="12-5" file-name="src/main.rs" caption="Extracting a `parse_config` function from `main`">

```rust,ignore
{{#rustdoc_include ../../listings/ch12-an-io-project/listing-12-05/src/main.rs:here}}
```

</Listing>

Táimid fós ag bailiú na n-argóintí ordú i veicteoir, ach ina ionad sin
an luach argóinte ag innéacs 1 a shannadh don athróg `query` agus an
luach argóinte ag innéacs 2 leis an athróg `file_path` laistigh den `main`
fheidhm, cuirimid an veicteoir iomlán ar aghaidh chuig an fheidhm `parse_config`. Tá an
Coinníonn feidhm `parse_config` an loighic a shocraíonn cén argóint
ina athróg agus a théann na luachanna ar ais go dtí `main`. Cruthaímid fós
na hathróga `query` agus `file_path` i `main`, ach níl na hathróga `main` a thuilleadh
freagracht as cinneadh a dhéanamh ar an gcaoi a ndéanann na hargóintí agus na hathróga ceannlíne
comhfhreagras.

Seans go bhfuil an chosúlacht ar an scéal go bhfuil an t-athoibriú seo ró-mhillte dár gclár beag, ach táimid ag athmhacrú
i gcéimeanna beaga incriminteacha. Tar éis an t-athrú seo a dhéanamh, rith an clár arís go
deimhnigh go n-oibríonn an pharsáil argóinte fós. Is maith do dhul chun cinn a sheiceáil
go minic, chun cuidiú le cúis fadhbanna a aithint nuair a tharlaíonn siad.

#### Luachanna Cumraíochta a Ghrúpáil

Is féidir linn céim bheag eile a ghlacadh chun an fheidhm `parse_config` a fheabhsú tuilleadh.
Faoi láthair, táimid ag filleadh tuple, ach ansin briseann muid é sin láithreach
tuple i gcodanna aonair arís. Is comhartha é seo b’fhéidir nach bhfuil againn
an astarraingt ceart fós.

Táscaire eile a thaispeánann go bhfuil spás le feabhsú ná an chuid `config`
de `parse_config`, a thugann le tuiscint go bhfuil gaol idir an dá luach a thabharfaimid ar ais agus
tá an dá chuid mar chuid de luach cumraíochta amháin. Nílimid á chur in iúl seo faoi láthair
brí i struchtúr na sonraí seachas an dá luach a ghrúpáil isteach
tuple; ina ionad sin cuirfimid an dá luach in aon struchtúr amháin agus tabharfaidh muid gach ceann de na
struct réimsí ainm brí. Déanfaidh sé sin níos fusa don todhchaí
lucht cothabhála an chóid seo chun tuiscint a fháil ar an gcaoi a mbaineann na luachanna difriúla le gach ceann acu
eile agus cad é an cuspóir atá leo.

Léiríonn liostú 12-6 na feabhsuithe ar an bhfeidhm `parse_config`.

<Listing number="12-6" file-name="src/main.rs" caption="Refactoring `parse_config` to return an instance of a `Config` struct">

```rust,should_panic,noplayground
{{#rustdoc_include ../../listings/ch12-an-io-project/listing-12-06/src/main.rs:here}}
```

</Listing>

Tá struchtúr darb ainm `Config` curtha leis againn le go mbeidh réimsí darb ainm `query` agus
`file_path`. Léiríonn síniú `parse_config` anois go bhfilleann sé a
luach `Config`. I gcorp `parse_config`, áit a raibh muid ag filleadh
slisní teaghrán a dhéanann tagairt do luachanna teaghrán in `args`, sainímid anois `Config`
luachanna `String` faoi úinéireacht a bheith ann. Is é an athróg `args` i `main` úinéir
luachanna na hargóintí agus níl sé ach ag ligean don fheidhm `parse_config` a fháil ar iasacht
orthu, rud a chiallaíonn go sáródh muid rialacha iasachtaithe Rust dá ndéanfadh `Config` iarracht a dhéanamh
úinéireacht na luachanna in `args`.

Tá roinnt bealaí inar féidir linn na sonraí `String` a bhainistiú; an éasca,
Cé go bhfuil sé beagán mí-éifeachtach, is é an bealach an modh `clone` a ghlaoch ar na luachanna.
Déanfaidh sé seo cóip iomlán de na sonraí don sampla `Config` is féidir a bheith agat, cé acu
tógann sé níos mó ama agus cuimhne ná tagairt do na sonraí teaghrán a stóráil.
Mar sin féin, déanann chlónáil na sonraí ár gcód an-simplí mar gheall orainn
ní gá saolré na dtagairtí a bhainistiú; sa chás seo,
Is fiú comhbhabhtáil fiúntach é feidhmíocht bheag a thabhairt suas chun simplíocht a bhaint amach.

> ### Na Comhshóiteanna a bhaineann le `clone` a Úsáid
>
> Tá an claonadh ann i measc go leor Rustaceans gan úsáid a bhaint as `clone` lena dheisiú
> fadhbanna úinéireachta mar gheall ar a chostas ama rite. I
> [Caibidil 13][ch13]<!-- neamhaird a dhéanamh -->, beidh tú ag foghlaim conas é a úsáid níos éifeachtaí
> modhanna sa chineál seo cásanna. Ach faoi láthair, tá sé ceart go leor cúpla a chóipeáil
> teaghráin chun leanúint ar aghaidh ag déanamh dul chun cinn mar ní dhéanfaidh tú ach na cóipeanna seo
> uair amháin agus tá cosán do chomhaid agus teaghrán na gceisteanna an-bheag. Is fearr a bheith agat
> clár oibre atá beagán mí-éifeachtach ná iarracht a dhéanamh cód hyperoptimize
> ar do chéad phas. De réir mar a éiríonn tú níos mó taithí le Rust, beidh sé
> níos éasca tosú leis an réiteach is éifeachtaí, ach faoi láthair, tá
> breá inghlactha `clone` a ghlaoch.

Tá `main` nuashonraithe againn agus mar sin cuireann sé an t-ús `Config` ar ais ag
`parse_config` isteach in athróg darb ainm `config`, agus nuashonraíomar an cód sin
d'úsáidtí na hathróga ar leith `query` agus `file_path` roimhe seo mar sin úsáideann sé anois
na réimsí ar an struchtúr `Config` ina ionad sin.

Anois cuireann ár gcód in iúl níos soiléire go bhfuil baint ag `query` agus `file_path` agus
gurb é an cuspóir atá leo ná conas a oibreoidh an clár a chumrú. Cód ar bith a
úsáideann a fhios na luachanna seo chun iad a fháil sa chás `config` sna réimsí
ainmnithe as a gcuspóir.

#### Cruthaitheoir á Chruthú do `Config`

Go dtí seo, tá an loighic atá freagrach as an líne ordaithe a pharsáil bainte amach againn
argóintí ó `main` agus é a chur san fheidhm `parse_config`. Ag déanamh amhlaidh
chabhraigh sé linn a fheiceáil go raibh gaol idir na luachanna `query` agus `file_path`, agus sin
Ba cheart caidreamh a chur in iúl inár gcód. Chuireamar struchtúr `Config` leis ansin
ainmnigh an cuspóir gaolmhar le `query` agus `file_path` agus a bheith in ann an
ainmneacha luachanna mar struchtúr ainmneacha réimse ón bhfeidhm `parse_config`.

Mar sin anois gurb é cuspóir na feidhme `parse_config` `Config` a chruthú
mar shampla, is féidir linn `parse_config` a athrú ó fheidhm shimplí go feidhm
darb ainm `new` a bhaineann leis an struchtúr `Config`. Ag déanamh an athraithe seo
beidh an cód níos idiomatic. Is féidir linn cásanna de chineálacha a chruthú sa
leabharlann caighdeánach, mar `String`, trí `String::new` a ghlaoch. Mar an gcéanna, le
ag athrú `parse_config` go feidhm `new` a bhaineann le `Config`, déanfaimid
bheith in ann cásanna de `Config` a chruthú trí `Config::new` a ghlaoch. Liostáil 12-7
léiríonn sé na hathruithe is gá dúinn a dhéanamh.

<Listing number="12-7" file-name="src/main.rs" caption="Changing `parse_config` into `Config::new`">

```rust,should_panic,noplayground
{{#rustdoc_include ../../listings/ch12-an-io-project/listing-12-07/src/main.rs:here}}
```

</Listing>

Tá `main` nuashonraithe againn mar a raibh muid ag glaoch `parse_config` chun glaoch a chur air ina ionad sin
`Config::new`. D'athraigh muid an t-ainm `parse_config` go `new` agus bhogamar é
laistigh de bhloc `impl`, a nascann an fheidhm `new` le `Config`. Bain triail as
an cód seo a thiomsú arís chun a chinntiú go n-oibríonn sé.

### Láimhseáil Earráidí a Shocrú

Anois oibreoimid ar ár láimhseáil earráidí a shocrú. Tabhair chun cuimhne go bhfuil iarracht á dhéanamh rochtain a fháil
is iad na luachanna sa veicteoir `args` ag innéacs 1 nó innéacs 2 a chuirfidh an ríomhchlár faoi deara
scaoll má tá níos lú ná trí mhír sa veicteoir. Bain triail as an gclár a rith
gan aon argóintí; beidh sé cuma mar seo:

```console
{{#include ../../listings/ch12-an-io-project/listing-12-07/output.txt}}
```

An líne `index out of bounds: the len is 1 but the index is 1` an t-innéacs earráid
teachtaireacht atá beartaithe le haghaidh ríomhchláraitheoirí. Ní chuideoidh sé lenár n-úsáideoirí deiridh a thuiscint cad é
ba chóir dóibh a dhéanamh ina ionad. Déanaimis é sin a shocrú anois.

#### An Teachtaireacht Earráide a Fheabhsú

I Liostú 12-8, cuirimid seic san fheidhm `new` a dheimhneoidh go bhfuil an
tá an tslis fada go leor roimh rochtain a fháil ar innéacs 1 agus innéacs 2. Mura bhfuil
fada go leor, scaoileann an clár agus taispeánann sé teachtaireacht earráide níos fearr.

<Listing number="12-8" file-name="src/main.rs" caption="Adding a check for the number of arguments">

```rust,ignore
{{#rustdoc_include ../../listings/ch12-an-io-project/listing-12-08/src/main.rs:here}}
```

</Listing>

Tá an cód seo cosúil le [an fheidhm `Guess::new` a scríobhamar sa Liostú
9-13][ch9-custom-types] <!-- neamhaird -->, nuair a thugamar `panic!` nuair a
Bhí argóint `value` as raon na luachanna bailí. In ionad a sheiceáil le haghaidh
raon luachanna anseo, táimid ag seiceáil go bhfuil fad na `args` ar a laghad
Is féidir le `3` agus an chuid eile den fheidhm a oibriú ar an toimhde go seo
Tá an coinníoll comhlíonta. Má tá níos lú ná trí mhír ag `args`, an coinníoll seo
beidh sé `true`, agus tugaimid an macra `panic!` chun deireadh a chur leis an gclár láithreach.

Leis na línte breise cód seo i `new`, rithfimid an clár gan aon cheann
argóintí arís féachaint cén chuma atá ar an earráid anois:

```console
{{#include ../../listings/ch12-an-io-project/listing-12-08/output.txt}}
```

Tá an t-aschur seo níos fearr: tá teachtaireacht earráide réasúnta againn anois. Mar sin féin, táimid freisin
bíodh faisnéis sheachtrach againn nach dteastaíonn uainn a thabhairt dár n-úsáideoirí. B'fhéidir go bhfuil an
ní hé an teicníc a d’úsáideamar i Liostú 9-13 an ceann is fearr le húsáid anseo: glao chuig
Tá `panic!` níos oiriúnaí d'fhadhb ríomhchláraithe ná d'fhadhb úsáide,
[mar a pléadh i gCaibidil 9][ch9-error-guidelines] <!-- neamhaird -->. Ina ionad sin,
úsáidfimid an teicníocht eile ar fhoghlaim tú faoi i gCaibidil 9—[ag filleadh a
`Result`][ch9-result] <!-- neamhaird --> a thugann le fios gur éirigh nó go bhfuil earráid ann.

<!-- Old headings. Do not remove or links may break. -->

<a id="returning-a-result-from-new-instead-of-calling-panic"></a>

#### `Result` a Fhilleadh In ionad `panic!` a ghlaoch

Is féidir linn ina ionad sin luach `Result` a thabhairt ar ais ina mbeidh sampla `Config` istigh
an cás rathúil agus déanfaidh sé cur síos ar an bhfadhb sa chás earráide. Táimid freisin
ag dul a athrú ainm na feidhme ó `new` go `build` mar go leor
tá ríomhchláraitheoirí ag súil nach dteipfidh ar fheidhmeanna `new` choíche. Nuair a bhíonn `Config::build`'
Ag cumarsáid le `main`, is féidir linn an cineál `Result` a úsáid chun a chur in iúl go raibh a
fadhb. Ansin is féidir linn `main` a athrú chun malairt `Err` a thiontú ina leagan eile
earráid phraiticiúil dár n-úsáideoirí gan an téacs máguaird faoi `thread
'main'` agus `RUST_BACKTRACE` is cúis le glaoch chun `panic!`.

Léiríonn liostú 12-9 na hathruithe is gá dúinn a dhéanamh ar luach aischuir an
feidhm a bhfuilimid ag tabhairt 'Cumraíocht::build' air anois agus corp na feidhme atá ag teastáil
chun `Result` a thabhairt ar ais. Tabhair faoi deara nach tiomsófar é seo go dtí go nuashonróimid `main` mar
Bhuel, rud a dhéanfaimid sa chéad liostú eile.

<Listing number="12-9" file-name="src/main.rs" caption="Returning a `Result` from `Config::build`">

```rust,ignore,does_not_compile
{{#rustdoc_include ../../listings/ch12-an-io-project/listing-12-09/src/main.rs:here}}
```

</Listing>

Tugann ár bhfeidhm `build` `Result` ar ais agus sampla `Config` sa rath
cás agus teaghrán litriúil sa chás earráide. Beidh ár luachanna earráide i gcónaí
téadlitreacha a bhfuil an saolré `'static` acu.

Tá dhá athrú déanta againn i gcorp na feidhme: in ionad ‘scaoll!’ a ghlaoch
nuair nach n-éiríonn leis an úsáideoir go leor argóintí a dhéanamh, tugaimid luach `Err` ar ais anois, agus
tá an luach aischuir `Config` fillte againn i `OK`. Déanann na hathruithe seo an
feidhm cloí lena síniú cineáil nua.

Má chuirtear luach `Err` ar ais ó `Config::build`' ceadaíonn sé don phríomhfheidhm
láimhseáil an luach `Result` a cuireadh ar ais ón bhfeidhm `build` agus scoir an
próiseáil níos glaine i gcás earráide.

<!-- Old headings. Do not remove or links may break. -->

<a id="calling-confignew-and-handling-errors"></a>

#### Ag glaoch `Config::build` agus ag Láimhseáil Earráidí

Chun an cás earráide a láimhseáil agus teachtaireacht atá éasca le húsáid a phriontáil, ní mór dúinn nuashonrú a dhéanamh
`main` chun an `Result` atá á chur ar ais ag `Config::build` a láimhseáil, mar a thaispeántar in
Liostáil 12-10. Glacfaimid an fhreagracht as an líne ceannais a fhágáil freisin
uirlis le cód earráide nonzero ar shiúl ó `panic!` agus ina ionad sin a chur i bhfeidhm ag
lámh. Is gnás é stádas scoir nonzero chun comhartha a thabhairt don phróiseas sin
ar a dtugtar ár gclár gur scoir an clár le staid earráide.

<Listing number="12-10" file-name="src/main.rs" caption="Exiting with an error code if building a `Config` fails">

```rust,ignore
{{#rustdoc_include ../../listings/ch12-an-io-project/listing-12-10/src/main.rs:here}}
```

</Listing>

Sa liostú seo, d’úsáideamar modh nár chlúdaigh muid go mion go fóill:
`unwrap_or_else`, a shainmhínítear ar `Result<T, E>` ag an ngnáthleabharlann.
Trí úsáid a bhaint as `unwrap_or_else` is féidir linn earráid shaincheaptha éigin nach mbaineann le `panic!` a shainiú
láimhseáil. Más luach `OK` é an `Result`, tá iompar an mhodha seo cosúil
go `unwrap`: tugann sé ar ais an luach inmheánach atá á chumhdach ag `Ok`. Mar sin féin, má tá an
Is luach `Err` é an luach, glaonn an modh seo an cód sa _closure_, is é sin
feidhm gan ainm a shainímid agus a thabharaimid mar argóint go `unwrap_or_else`.
Clúdóimid dúnadh níos mine i [Caibidil 13][ch13]<!-- neamhaird -->. Le haghaidh
anois, níl le déanamh agat ach fios a bheith agat go rachaidh `unwrap_or_else` thar luach inmheánach
an `Err`, arb í sa chás seo an teaghrán statach `"not enough arguments"`
a chuireamar i Liosta 12-9, lenár ndúnadh san argóint `err` that
dealraitheach idir na píopaí ingearach. Is féidir an cód sa dúnadh a úsáid ansin an
luach `err` nuair a ritheann sé.

Chuireamar líne ‘úsáide’ nua leis chun `process` a thabhairt ón ngnáthleabharlann isteach
scóip. Níl sa chód sa dúnadh a reáchtálfar sa chás earráide ach dhá
línte: priontáilimid an luach `err` agus ansin glaoimid `process::exit`. Tá an
stopfaidh an fheidhm `process::exit` an clár láithreach agus seolfaidh sé an
uimhir a ritheadh ​​mar chód stádais scoir. Tá sé seo cosúil leis an
Láimhseáil bunaithe ar `panic!` a d'úsáideamar i Liosta 12-8, ach ní fhaighimid an lámh in uachtar ar fad a thuilleadh
aschur breise. Déanaimis iarracht é:

```console
{{#include ../../listings/ch12-an-io-project/listing-12-10/output.txt}}
```

Go hiontach! Tá an t-aschur seo i bhfad níos cairdiúla dár n-úsáideoirí.

### Loighic á baint as `main`

Anois go bhfuil an parsáil cumraíochta críochnaithe againn, déanaimis dul chuig
loighic an chláir. Mar a dúirt muid in [“Imní a Scaradh maidir le Dénártha
Tionscadail”](#scaradh-imní-do-thionscadail-dénártha)<!-- neamhaird a dhéanamh -->, déanfaimid
bain feidhm darb ainm `run` a choinneoidh an loighic ar fad atá sa
`main` nach bhfuil baint aici le cumraíocht nó láimhseáil a shocrú
earráidí. Nuair a bheidh muid críochnaithe, beidh `main` gonta agus éasca le fíorú
iniúchadh, agus beimid in ann tástálacha a scríobh don loighic eile ar fad.

Léiríonn liostú 12-11 an fheidhm `run` asbhainte. Faoi láthair, nílimid ach ag déanamh
feabhas beag, incriminteach ar bhaint na feidhme. Táimid fós
ag sainiú na feidhme in _src/main.rs_.

<Listing number="12-11" file-name="src/main.rs" caption="Extracting a `run` function containing the rest of the program logic">

```rust,ignore
{{#rustdoc_include ../../listings/ch12-an-io-project/listing-12-11/src/main.rs:here}}
```

</Listing>

Cuimsíonn an fheidhm `run` an loighic ar fad atá fágtha ó `main`, ag tosú
ó léamh an chomhaid. Glacann an fheidhm `run` an sampla `Config` mar
argóint.

#### Earráidí Ag Filleadh ón bhFeidhm `run`

Leis an loighic cláir atá fágtha scartha isteach san fheidhm `run`, is féidir linn
feabhas a chur ar láimhseáil earráidí, mar a rinneamar le `Config::build` i Liostú 12-9.
In ionad ligean don chlár scaoll a dhéanamh ach glaoch ar `expect`, an `run`
tabharfaidh feidhm `Result<T, E>` ar ais nuair a théann rud éigin mícheart. Beidh sé seo in iúl
Déanaimid an loighic a bhaineann le láimhseáil earráidí a chomhdhlúthú tuilleadh i `main` in a
bealach éasca le húsáid. Léiríonn liostú 12-12 na hathruithe is gá dúinn a dhéanamh ar an
síniú agus corp `run`.

<Listing number="12-12" file-name="src/main.rs" caption="Changing the `run` function to return `Result`">

```rust,ignore
{{#rustdoc_include ../../listings/ch12-an-io-project/listing-12-12/src/main.rs:here}}
```

</Listing>

Tá trí athrú shuntasacha déanta againn anseo. Ar dtús, d'athraigh muid an cineál tuairisceáin de
an fheidhm `run` go `Result<(), Box<dyn Error>>`. An fheidhm seo roimhe seo
ar ais an cineál aonaid, `()`, agus a choinneáil orainn mar an luach ar ais sa
Cás `OK`.

Don chineál earráide, d'úsáideamar an _trait object_ `Box<dyn Error>` (agus tá
thug `std::error::Error` isteach sa scóip le ráiteas `use` ag an mbarr).
Clúdóimid réada trait i [Caibidil 18][ch18]<!-- neamhaird -->. Chun anois, díreach
Bíodh a fhios agat go gciallaíonn `Box<dyn Error>` go dtabharfaidh an fheidhm cineál ar ais a
cuireann sé an trait `Error` i bhfeidhm, ach ní gá dúinn cén cineál ar leith a shonrú
beidh an luach tuairisceáin. Tugann sé seo solúbthacht dúinn chun luachanna earráide a thabhairt ar ais
d’fhéadfadh sé a bheith de chineálacha éagsúla i gcásanna earráide éagsúla. Tá an eochairfhocal `dyn` gearr
le haghaidh _dinimiciúil_.

Ar an dara dul síos, tá deireadh curtha againn leis an nglao chun súil a chaitheamh i bhfabhar an oibreora `?`, agus muidne
labhair faoi i [Caibidil 9][ch9-question-mark] <!-- neamhaird -->. Seachas
`panic!` ar earráid, cuirfidh `?` luach na hearráide ar ais ón bhfeidhm reatha
don té atá ag glaoch a láimhseáil.

Ar an tríú dul síos, tugann an fheidhm `run` luach `OK` ar ais anois sa chás ratha.
D'fhógair muid cineál ratha na feidhme `run` mar `()` sa síniú,
rud a chiallaíonn go gcaithfimid luach an chineáil aonaid a fhilleadh sa luach `Ok`. seo
`Ok(())` seans go bhféachfadh comhréir beagán aisteach ar dtús, ach úsáid á baint as `()` mar seo
an gnáthbhealach lena chur in iúl go bhfuilimid ag glaoch `run` as a fo-iarmhairtí
amháin; ní thugann sé luach a theastaíonn uainn ar ais.

Nuair a ritheann tú an cód seo, tiomsóidh sé ach taispeánfaidh sé rabhadh:

```console
{{#include ../../listings/ch12-an-io-project/listing-12-12/output.txt}}
```

Insíonn Rust dúinn gur thug ár gcód neamhaird ar an luach `Result` agus ar an luach `Result`
d’fhéadfadh sé a léiriú gur tharla earráid. Ach nílimid ag seiceáil féachaint an bhfuil nó
ní raibh earráid ann, agus cuireann an tiomsaitheoir i gcuimhne dúinn gur dócha go raibh sé i gceist againn
tá roinnt cód láimhseála earráidí anseo! Déanaimis an fhadhb sin a réiteach anois.

#### Earráidí Láimhseála Ar ais ó `run` sa `main`

Déanfaimid seiceáil le haghaidh earráidí agus láimhseálfaimid iad ag baint úsáide as teicníc cosúil leis an gceann a d'úsáideamar
le `Config::build` i Liostú 12-10, ach le difríocht bheag:

<span class="filename">Filename: src/main.rs</span>

```rust,ignore
{{#rustdoc_include ../../listings/ch12-an-io-project/no-listing-01-handling-errors-in-main/src/main.rs:here}}
```

Bainimid úsáid as `if let` seachas `unwrap_or_else` le seiceáil an bhfilleann `run` an
`Error` luach agus cuir glaoch ar `process::exit(1)` má dhéanann sé. An fheidhm `run`
Ní thugann sé ar ais luach a theastaíonn uainn a `unwrap` ar an mbealach céanna
Filleann `Config::build` an sampla `Config`. Toisc go dtagann `run` ar ais `()` isteach
an cás ratha, is cúram linn ach earráid a bhrath, mar sin ní gá dúinn
`unwrap_or_else` chun an luach neamhfhillte a thabhairt ar ais, nach mbeadh ann ach `()`.

Tá coirp na bhfeidhmeanna `if let` agus `unwrap_or_else` mar an gcéanna i
an dá chás: priontáilimid an earráid agus scoir.

### Cód a scoilteadh isteach i gcliathbhosca leabharlainne

Tá ár dtionscadal `minigrep` ag breathnú go maith go dtí seo! Anois scoiltfimid an
_src/main.rs_ agus cuir roinnt cód isteach sa chomhad _src/lib.rs_. Ar an mbealach sin, táimid
in ann an cód a thástáil agus comhad _src/main.rs_ a bheith aige le níos lú freagrachtaí.

Bogfaimid an cód ar fad nach bhfuil sa `main` ó _src/main.rs_ go
_src/lib.rs_:

- An sainmhíniú ar fheidhm `run`
- Na ráitis `use` ábhartha
- An sainmhíniú ar `Config`
- An sainmhíniú ar fheidhm `Config::build`

Ba cheart go mbeadh na sínithe a thaispeántar i Liostú 12-13 ag inneachar _src/lib.rs_
(D’fhágamar coirp na bhfeidhmeanna ar lár go gairid). Tabhair faoi deara nach ndéanfaidh sé seo
tiomsaigh go dtí go modhnaimid _src/main.rs_ i Liostú 12-14.

<Listing number="12-13" file-name="src/lib.rs" caption="Moving `Config` and `run` into *src/lib.rs*">

```rust,ignore,does_not_compile
{{#rustdoc_include ../../listings/ch12-an-io-project/listing-12-13/src/lib.rs:here}}
```

</Listing>

Bhaineamar úsáid liobrálach as an eochairfhocal: `pub` ar `Config`, ar a réimsí agus a chuid
modh `build`, agus ar an bhfeidhm `run`. Tá cliathbhosca leabharlainne againn anois a bhfuil
API poiblí is féidir linn a thástáil!

Anois caithfimid an cód a bhog muid go _src/lib.rs_ a thabhairt isteach i scóip an
cliathbhosca dénártha in _src/main.rs_, mar a thaispeántar i Liostú 12-14.

<Listing number="12-14" file-name="src/main.rs" caption="Using the `minigrep` library crate in *src/main.rs*">

```rust,ignore
{{#rustdoc_include ../../listings/ch12-an-io-project/listing-12-14/src/main.rs:here}}
```

</Listing>

Cuirimid líne `use minigrep::Config` leis chun an cineál `Config` a thabhairt ón
cliathbhosca leabharlainne isteach i raon feidhme an chliabháin dhénártha, agus déanaimid réimír don fheidhm `run`
lenár n-ainm cliathbhosca. Anois ba chóir go mbeadh an fheidhmiúlacht go léir ceangailte agus ba chóir
oibre. Rith an clár le `cargo run` agus cinntigh go n-oibríonn gach rud i gceart.

Whew! Ba mhór an obair é sin, ach tá rath orainn féin curtha ar bun againn sa
todhchaí. Anois tá sé i bhfad níos éasca earráidí a láimhseáil, agus tá an cód níos mó déanta againn
modúlach. Déanfar beagnach ár gcuid oibre ar fad in _src/lib.rs_ as seo amach.

Bainimis leas as an modúlacht nua seo trí rud éigin a dhéanamh a dhéanfadh
a bheith deacair leis an seanchód ach tá sé éasca leis an gcód nua: déanfaimid
scríobh roinnt tástálacha!

[ch13]: ch13-00-functional-features.html
[ch9-custom-types]: ch09-03-to-panic-or-not-to-panic.html#creating-custom-types-for-validation
[ch9-error-guidelines]: ch09-03-to-panic-or-not-to-panic.html#guidelines-for-error-handling
[ch9-result]: ch09-02-recoverable-errors-with-result.html
[ch18]: ch18-00-oop.html
[ch9-question-mark]: ch09-02-recoverable-errors-with-result.html#a-shortcut-for-propagating-errors-the--operator