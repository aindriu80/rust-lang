## Leideanna Cliste a Chaitheamh Cosúil le Tagairtí Rialta leis an dTréith `Deref`

Nuair a chuirtear an trait `Deref` i bhfeidhm is féidir leat iompar an
_dereference operator_ `*` (gan a chur amú leis an iolrú nó glob
oibreoir). Trí `Deref` a chur i bhfeidhm sa chaoi is gur féidir pointeoir cliste a bheith ann
cóireáilte cosúil le tagairt rialta, is féidir leat scríobh cód a oibríonn ar
tagairtí agus úsáid an cód sin le leideanna cliste freisin.

Breathnaímid ar dtús ar an gcaoi a n-oibríonn an t-oibreoir díreference le tagairtí rialta.
Ansin déanfaimid iarracht cineál saincheaptha a shainiú a iompraíonn mar `Box<T>`, agus féach cén fáth
ní oibríonn an t-oibreoir díreference mar thagairt ar ár nua-shainithe
cineál. Déanfaimid iniúchadh ar an gcaoi a bhféadfar é seo a dhéanamh má chuirtear an tréith 'Deref' i bhfeidhm
leideanna cliste a bheith ag obair ar bhealaí cosúil le tagairtí. Ansin féachfaimid ar
Gné _deref coercion_ Rust agus conas a ligeann sé dúinn oibriú le ceachtar tagairt
nó leideanna cliste.

> Nóta: Tá difríocht mhór amháin idir an cineál `MyBox<T>` atáimid ar tí
> build and the real `Box<T>`: ní stórálfaidh ár leagan a shonraí ar an gcarn.
> Táimid ag díriú an sampla seo ar `Deref`, mar sin áit a bhfuil na sonraí stóráilte i ndáiríre
> nach bhfuil chomh tábhachtach leis an iompar atá cosúil le pointeoir.

<!-- Seannasc, ná bain -->

<a id="following-the-pointer-to-the-value-with-the-dereference-operator"></a>

### Tar éis an Pointeoir don Luach

Is cineál pointeoir é tagairt rialta, agus bealach amháin chun smaoineamh ar phointeoir
mar shaighead le luach atá stóráilte in áit éigin eile. I Liostú 15-6, cruthaímid a
tagairt do luach `i32` agus ansin úsáid an t-oibreoir díreference chun an
tagairt don luach:

<Listing number="15-6" file-name="src/main.rs" caption="Using the dereference operator to follow a reference to an `i32` value">

```rust
{{#rustdoc_include ../../listings/ch15-smart-pointers/listing-15-06/src/main.rs}}
```

</Listing>

Tá luach `i32` `5` ag an athróg `x`. Leagamar `y` comhionann le tagairt do
`x`. Is féidir linn a dhearbhú go bhfuil `x` cothrom le `5`. Mar sin féin, más mian linn a dhéanamh ar
dearbhú faoin luach in `y`, caithfimid `*y` a úsáid chun an tagairt a leanúint
chuig an luach a bhfuil sé ag díriú air (mar sin _dereference_) ionas gur féidir leis an tiomsaitheoir comparáid a dhéanamh
an luach iarbhír. Nuair a dhírímid `y`, tá rochtain againn ar an luach slánuimhir
Tá `y` ag cur in iúl gur féidir linn comparáid a dhéanamh le `5`.

Dá ndéanfaimis iarracht `assert_eq!(5, y);` a scríobh ina ionad sin, gheobhaimid an tiomsú seo
earráid:

```console
{{#include ../../listings/ch15-smart-pointers/output-only-01-comparing-to-reference/output.txt}}
```

Ní cheadaítear uimhir a chur i gcomparáid agus tagairt d’uimhir toisc go bhfuil siad
cineálacha éagsúla. Ní mór dúinn an t-oibreoir díreference a úsáid chun an tagairt a leanúint
leis an luach atá á lua aige.

### Ag baint úsáide as `Box<T>` Cosúil le Tagairt

Is féidir linn an cód a athscríobh i Liostú 15-6 chun `Box<T>` a úsáid in ionad a
tagairt ; an t-oibreoir díreference a úsáidtear ar an `Box<T>` i Liostú 15-7
feidhmeanna ar an mbealach céanna leis an oibreoir dereference a úsáidtear ar an tagairt i
Liostáil 15-6:

<Listing number="15-7" file-name="src/main.rs" caption="Using the dereference operator on a `Box<i32>`">

```rust
{{#rustdoc_include ../../listings/ch15-smart-pointers/listing-15-07/src/main.rs}}
```

</Listing>

Is é an príomhdhifríocht idir Liostú 15-7 agus Liostú 15-6 ná gur anseo a shocraímid
`y` a bheith ina shampla de `Box<T>` ag tagairt do luach cóipeáilte de `x` in áit
ná tagairt a dhíríonn ar luach `x`. Sa dearbhú deireanach, is féidir linn
úsáid an t-oibreoir díreference chun pointeoir an `Box<T>` a leanúint mar an gcéanna
bealach a rinne muid nuair a bhí `y` mar thagairt. Ansin, déanfaimid iniúchadh ar a bhfuil speisialta
faoi ​​`Box<T>` a chuireann ar ár gcumas an t-oibreoir díthagartha a úsáid trí ár n-
cineál féin.

### Ár Pointeoir Cliste Féin a Shainmhíniú

Déanaimis pointeoir cliste a thógáil cosúil leis an gcineál `Box<T>` a sholáthraíonn an
leabharlann caighdeánach chun taithí a fháil ar an gcaoi a n-iompraíonn leideanna cliste difriúil ó
tagairtí de réir réamhshocraithe. Ansin féachfaimid ar conas an cumas a úsáid chun an
oibreoir dereference.

Sainmhínítear an cineál `Box<T>` ar deireadh mar struchtúr tuple le eilimint amháin, mar sin
Sainmhíníonn liostú 15-8 cineál `MyBox<T>` ar an mbealach céanna. Déanfaimid sainmhíniú freisin ar a
feidhm `new` chun an fheidhm `new` a shainmhínítear ar `Box<T>` a mheaitseáil.

<Listing number="15-8" file-name="src/main.rs" caption="Defining a `MyBox<T>` type">

```rust
{{#rustdoc_include ../../listings/ch15-smart-pointers/listing-15-08/src/main.rs:here}}
```

</Listing>

Sainmhínímid struchtúr darb ainm `MyBox` agus dearbhaímid paraiméadar cineálach `T`, mar gheall ar
ba mhaith linn go mbeadh luachanna d'aon chineál ag ár gcineál. Is struchtúr tuple é an cineál `MyBox`
le gné amháin den chineál `T`. Glacann an fheidhm `MyBox::new` paraiméadar amháin de
clóscríobh `T` agus seolann tú sampla `MyBox` a choinníonn an luach a cuireadh isteach.

Déanaimis iarracht an `main` i Liostú 15-7 a chur le Liostú 15-8 agus
é a athrú chun an cineál `MyBox<T>` a shainmhínigh muid a úsáid in ionad `Box<T>`. Tá an
ní thiomsóidh an cód i Liostú 15-9 toisc nach bhfuil a fhios ag Rust conas díthagairt a dhéanamh
`MyBox`.

<Listing number="15-9" file-name="src/main.rs" caption="Attempting to use `MyBox<T>` in the same way we used references and `Box<T>`">

```rust,ignore,does_not_compile
{{#rustdoc_include ../../listings/ch15-smart-pointers/listing-15-09/src/main.rs:here}}
```

</Listing>

Here’s the resulting compilation error:

```console
{{#include ../../listings/ch15-smart-pointers/listing-15-09/output.txt}}
```

Ní féidir ár gcineál `MyBox<T>` a dhímheas toisc nach bhfuil sé sin curtha i bhfeidhm againn
cumas ar ár gcineál. Chun díthagairt a dhéanamh leis an oibreoir `*`, déanaimid
an trait `Deref` a chur i bhfeidhm.

### Caitheamh Cineál Cosúil le Tagairt tríd an Trait `Deref` a Chur i bhFeidhm

Mar a pléadh sa [“Tréith a Chur i bhFeidhm ar Chineál”][impl-trait]<!-- neamhaird a dhéanamh
--> alt de Chaibidil 10, a chur i bhfeidhm tréith, ní mór dúinn a chur ar fáil
cur i bhfeidhm do mhodhanna riachtanacha an trait. An trait `Deref`, ar fáil
ag an leabharlann chaighdeánach, éilíonn orainn modh amháin darb ainm `deref` sin a chur i bhfeidhm
faigheann sé `self` ar iasacht agus cuireann sé tagairt ar ais do na sonraí istigh. Liostáil 15-10
ina bhfuil `Deref` curtha i bhfeidhm le cur leis an sainmhíniú ar `MyBox`:

<Listing number="15-10" file-name="src/main.rs" caption="Implementing `Deref` on `MyBox<T>`">

```rust
{{#rustdoc_include ../../listings/ch15-smart-pointers/listing-15-10/src/main.rs:here}}
```

</Listing>

Sainmhíníonn an chomhréir `type Target = T;` cineál gaolmhar don `Deref`
tréithe a úsáid. Is bealach beagán difriúil iad cineálacha comhlachaithe chun a
paraiméadar cineálach, ach ní gá duit a bheith buartha fúthu faoi láthair; clúdóidh muid
iad go mion i gCaibidil 20.

Líonaimid corp an mhodha `deref` le `&self.0` mar sin filleann `deref` a
tagairt don luach a theastaíonn uainn a rochtain leis an oibreoir `*`; aisghairm ó na
[“Úsáid Struchtúir Tuple gan Réimsí Ainmnithe chun Éagsúla a Chruthú
Cineálacha”][tuple-structs]<!-- neamhaird --> roinn de Chaibidil 5 a bhfuil rochtain ag `.0` air
an chéad luach i struchtúr tuple. An fheidhm `main` i Liostú 15-9 go
glaonna `*` ar an luach `MyBox<T>` le chéile anois, agus na dearbhuithe pas!

Gan an tréithe `Deref`, ní féidir leis an tiomsaitheoir ach tagairtí `&` a dhímheas.
Tugann an modh `deref` an cumas don tiomsaitheoir luach d'aon chineál a ghlacadh
a chuireann `Deref` i bhfeidhm agus a ghlaonn an modh `deref` chun tagairt `&` a fháil go
tá a fhios aige conas dereference.

Nuair a chuamar isteach `* y` i Liosta 15-9, rith Rust é seo taobh thiar de na cásanna
cód:

``` meirge, neamhaird
*(y.deref())
```

Cuireann Rust glaoch chuig an modh `deref` in ionad an oibreora `*` agus ansin a
tagairt shimplí ionas nach mbeidh orainn smaoineamh ar cé acu an gcaithfimid nó nach gá
glaoigh ar an modh `deref`. Ligeann an ghné Rust seo dúinn cód a scríobh a fheidhmíonn
mar an gcéanna cibé an bhfuil tagairt rialta againn nó cineál a chuireann i bhfeidhm
`Deref`.

Is é an fáth go dtugann an modh `deref` tagairt ar ais do luach, agus go bhfuil an
tá gá le tagairt shimplí lasmuigh de na lúibíní in `*(y.deref())` fós,
a bhaineann leis an gcóras úinéireachta. Má thug an modh `deref` an luach ar ais
go díreach in ionad tagairt don luach, bhogfaí an luach amach as
`self`. Nílimid ag iarraidh úinéireacht a ghlacadh ar an luach inmheánach taobh istigh de `MyBox<T>` in
sa chás seo nó i bhformhór na gcásanna ina n-úsáidimid an t-oibreoir díreference.

Tabhair faoi deara go gcuirtear glao chuig an modh `deref` in ionad an oibreora `*` agus
ansin cuir glaoch chuig an oibreoir `*` uair amháin, gach uair a úsáidimid `*` inár gcód.
Toisc nach dtagann ionadú an oibreora `*` arís gan teorainn, ní mór dúinn
deireadh suas le sonraí den chineál `i32`, a mheaitseálann an `5` in `assert_eq!` i
Liostáil 15-9.

### Comhéigeantais Fhoréigthe intuigthe le Feidhmeanna agus Modhanna

Tiontaíonn _Deref coercion_ tagairt do chineál a chuireann an `Deref` i bhfeidhm
tréith isteach i dtagairt do chineál eile. Mar shampla, is féidir comhéigean deref a thiontú
`&String` go `&str` toisc go gcuireann `String` an trait `Deref` i bhfeidhm ionas go mbeidh sé
Filleann `&str`. Is áis é comhéigean deref a fheidhmíonn Rust ar argóintí chun
feidhmeanna agus modhanna, agus ní oibríonn sé ach ar chineálacha a chuireann an `Deref` i bhfeidhm
trait. Tarlaíonn sé go huathoibríoch nuair a thugaimid tagairt do chineál áirithe
luach mar argóint le feidhm nó modh nach bhfuil ag teacht leis an bparaiméadar
clóscríobh an sainmhíniú ar fheidhm nó modh. Seicheamh glaonna chuig an `deref`
athraíonn modh an cineál a sholáthraíomar isteach sa chineál a theastaíonn ón bparaiméadar.

Cuireadh comhéigean deref le Rust ionas go mbeidh feidhm ag ríomhchláraitheoirí ag scríobh agus
ní gá an oiread tagairtí agus díthagairtí follasacha a chur isteach i nglaonna modha
le `&` agus `*`. Ligeann an ghné comhéigean deref dúinn níos mó cód a scríobh freisin
is féidir oibriú le haghaidh tagairtí nó leideanna cliste.

Chun comhéigean deref a fheiceáil i ngníomh, bainimis úsáid as an gcineál `MyBox<T>` a shainmhíníomar ann
Liostáil 15-8 chomh maith le cur i bhfeidhm `Deref` a chuireamar leis sa Liostú
15-10. Léiríonn liosta 15-11 an sainmhíniú ar fheidhm a bhfuil sreangshleasa aici
paraiméadar:

<Listing number="15-11" file-name="src/main.rs" caption="A `hello` function that has the parameter `name` of type `&str`">

```rust
{{#rustdoc_include ../../listings/ch15-smart-pointers/listing-15-11/src/main.rs:here}}
```

</Listing>

Is féidir linn an fheidhm `hello` a thabhairt le slisne teaghrán mar argóint, mar shampla
`hello("Rust");` mar shampla. Trí chomhéigean deref is féidir `hello` a thabhairt air
le tagairt do luach cineáil `MyBox<String>`, mar a thaispeántar i Liostú 15-12:

<Listing number="15-12" file-name="src/main.rs" caption="Calling `hello` with a reference to a `MyBox<String>` value, which works because of deref coercion">

```rust
{{#rustdoc_include ../../listings/ch15-smart-pointers/listing-15-12/src/main.rs:here}}
```

</Listing>

Anseo táimid ag glaoch ar an bhfeidhm `hello` leis an argóint `&m`, is é sin a
tagairt do luach `MyBox<String>`. Toisc gur chuireamar an trait `Deref` i bhfeidhm
ar `MyBox<T>` i Liostú 15-10, is féidir le Rust `&MyBox <String>` a iompú ina `&String`
trí ghlaoch ar `deref`. Soláthraíonn an leabharlann chaighdeánach cur i bhfeidhm `Deref`
ar `String` a sheolann sreangán ar ais, agus tá sé seo i gcáipéisíocht an API
le haghaidh `Deref`. Glaonn Rust ar `deref` arís chun an `&String` a iompú ina `&str`, a
ag teacht le sainmhíniú na feidhme `hello`.

Murar chuir Rust comhéigean deref i bhfeidhm, bheadh ​​orainn an cód a scríobh isteach
Liostáil 15-13 in ionad an chóid i Liostú 15-12 chun `hello` a ghlaoch le luach
den chineál `&MyBox<String>`.

<Listing number="15-13" file-name="src/main.rs" caption="The code we would have to write if Rust didn’t have deref coercion">

```rust
{{#rustdoc_include ../../listings/ch15-smart-pointers/listing-15-13/src/main.rs:here}}
```

</Listing>

Déanann an `(*m)` tagairt don `MyBox<String>` mar `String`. Ansin tá an `&` agus
`[..]` glac sliseog teaghrán den `String` atá comhionann leis an teaghrán iomlán go
mheaitseáil síniú `hello`. Tá sé níos deacra an cód seo gan comhéigeantais deref a dhéanamh
léamh, scríobh, agus tuiscint leis na siombailí seo go léir atá i gceist. Deref comhéigean
ligeann do Rust na tiontuithe seo a láimhseáil dúinn go huathoibríoch.

Nuair a shainmhínítear an tréith `Deref` do na cineálacha atá i gceist, déanfaidh Rust anailís ar an
cineálacha agus úsáid `Deref::deref` a mhéad uair is gá chun tagairt a fháil
mheaitseáil le cineál an pharaiméadar. An líon uaireanta is gá go mbeadh `Deref::deref`
a cuireadh isteach réitithe ag am tiomsaithe, mar sin níl aon phionós ama rite as a ghlacadh
buntáiste a bhaint as comhéigean deref!

### Mar a Idirghníomhaíonn Comhéigean Deref le Mutability

Cosúil leis an gcaoi a n-úsáideann tú an tréith `Deref` chun an t-oibreoir `*` a shárú
tagairtí domhalartaithe, is féidir leat an tréith `DerefMut` a úsáid chun an `*` a shárú
oibreoir ar thagairtí mutable.

Déanann Rust comhéigean a dhíspreagadh nuair a aimsíonn sé cineálacha agus cur i bhfeidhm tréithe i dtrí cinn
cásanna:

- Ó `&T` go `&U` nuair a `T: Deref <Target=U>`
- Ó `&mut T` go `&mut U` nuair `T: DerefMut<Target=U>`
- Ó `&mut T` go `&U` nuair a `T: Deref <Target=U>`

Is ionann an chéad dá chás agus a chéile ach amháin an dara cás
feidhmíonn mutability. Deir an chéad chás má tá `&T`, agus `T` agat
cuireann sé `Deref` i bhfeidhm do chineál éigin `U`, is féidir leat `&U` a fháil go trédhearcach. Tá an
deir an dara cás go dtarlaíonn an comhéigean deref céanna le haghaidh tagairtí mutable.

Tá an tríú cás níos deacra: comhleanfaidh meirge tagairt chomhshóite do chás
do-mhothúchánach. Ach is _not_ a mhalairt is féidir: beidh tagairtí do-laghdaithe
riamh iallach a chur ar thagairtí mutable. Mar gheall ar na rialacha iasachtaithe, má tá
tagairt sho-shóite, ní mór gurb í an tagairt sho-shó-shamhail sin an t-aon tagairt dó sin
sonraí (ar shlí eile, ní thiomsódh an clár). Comhshó amháin a thiontú
ní sháróidh tagairt do thagairt neamh-inmhalartaithe amháin na rialacha iasachtaíochta.
Chun tagairt do-ath-inmheánach a thiontú go tagairt shochorraithe, bheadh ​​gá leis an
is í an tagairt tosaigh do- immutable an t-aon tagairt domhalartaithe do na sonraí sin, ach
ní ráthaíonn na rialacha iasachtaíochta é sin. Mar sin, ní féidir le Rust an
toimhde gur tagairt do-ath-inmheánach a thiontú go tagairt shochorraithe
is féidir.

[impl-trait]: ch10-02-traits.html#implementing-a-trait-on-a-type
[tuple-structs]: ch05-01-defining-structs.html#using-tuple-structs-without-named-fields-to-create-different-types	