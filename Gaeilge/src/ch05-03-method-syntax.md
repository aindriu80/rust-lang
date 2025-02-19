## Comhréir Modh

Tá _modhanna_ cosúil le feidhmeanna: dearbhaímid iad leis an eochairfhocal `fn` agus a
ainm, is féidir paraiméadair agus luach tuairisceáin a bheith acu, agus tá roinnt cód iontu
sin a rith nuair a ghlaoitear an modh ó áit éigin eile. Murab ionann agus feidhmeanna,
sainmhínítear modhanna i gcomhthéacs struchtúir (nó enum nó trait
réad, a chlúdaímid i [Caibidil 6][enums] <!-- neamhaird --> agus [Caibidil
17][trait-objects]<!-- déan neamhaird de -->, faoi seach), agus is é a gcéad pharaiméadar
i gcónaí `self`, a léiríonn an ásc ar an struchtúr an modh á
ar a dtugtar ar.

### Modhanna a Shainmhíniú

Athraímis an fheidhm `area` a bhfuil sampla `Rectangle` aici mar pharaiméadar
agus ina ionad sin déan modh `area` atá sainmhínithe ar an struchtúr `Rectangle`, mar a thaispeántar
i Liosta 5-13.

<Listing number="5-13" file-name="src/main.rs" caption="Defining an `area` method on the `Rectangle` struct">

```rust
{{#rustdoc_include ../../listings/ch05-using-structs-to-structure-related-data/listing-05-13/src/main.rs}}
```

</Listing>

Chun an fheidhm a shainiú laistigh de chomhthéacs `Rectangle`, cuirimid tús le `impl`
(cur i bhfeidhm) bloc le haghaidh `Rectangle`. Gach rud laistigh den bhloc `impl` seo
a bhaineann leis an gcineál `Rectangle`. Ansin bogaimid an fheidhm `area`
laistigh de na lúibíní chatach `impl` agus athraigh an chéad cheann (agus sa chás seo, amháin)
paraiméadar a bheith `self` sa síniú agus i ngach áit laistigh den chorp. I
`main`, áit ar thugamar an fheidhm `area` agus gur ritheamar `rect1` mar argóint,
ina ionad sin is féidir linn _method syntax_ a úsáid chun an modh `area` a ghlaoch ar ár `Rectangle`
shampla. Téann an modh comhréire tar éis sampla: cuirimid ponc leis ina dhiaidh sin
ainm an mhodha, lúibíní, agus aon argóintí.

Sa síniú le haghaidh `area`, úsáidimid `&self` in ionad `rectangle: &Rectangle`.
Tá an `&self` gearr i ndáiríre do `self: &Self`. Laistigh de bhloc `impl`, tá an
cineál Is ailias é `self` don chineál ar a bhfuil an bloc `impl`. Ní mór modhanna
bíodh paraiméadar darb ainm `self` den chineál `self` acu dá gcéad pharaiméadar, mar sin Meirge
ligeann sé duit é seo a ghiorrú gan ach an t-ainm `self` sa chéad láthair paraiméadar.
Tabhair faoi deara go gcaithfimid fós an `&` a úsáid os comhair na gearrscaireachta `self` chun
cuir in iúl go bhfaigheann an modh seo an sampla `self` ar iasacht, díreach mar a rinneamar i
`rectangle: &Rectangle`. Is féidir le modhanna úinéireacht a ghlacadh ar `self`, `self` a fháil ar iasacht
go do-athraithe, mar atá déanta againn anseo, nó 'self` a fháil ar iasacht go frithpháirteach, díreach mar is féidir leo
paraiméadar eile.

Roghnaigh muid `&self` anseo ar an gcúis chéanna a d'úsáid muid `&Rectangle` san fheidhm
leagan: nílimid ag iarraidh úinéireacht a ghlacadh, agus níl uainn ach na sonraí a léamh isteach
an struct, ní scríobh air. Dá mba mhian linn an cás atá againn a athrú
ar a dtugtar an modh ar mar chuid de cad a dhéanann an modh, d'úsáidfimid `&mut self` mar
an chéad pharaiméadar. Ag modh a ghlacann úinéireacht ar an gcás trí
ag baint úsáide as ach `self` mar go bhfuil an chéad paraiméadar annamh; tá an teicníc seo de ghnáth
a úsáidtear nuair a athraíonn an modh `self` isteach i rud éigin eile agus is mian leat a
cosc a chur ar an nglaoiteoir an t-ábhar bunaidh a úsáid tar éis an chlaochlaithe.

An phríomhchúis le modhanna a úsáid in ionad feidhmeanna, sa bhreis ar
ag soláthar comhréire modhanna agus gan a bheith athrá ar an gcineál `self` i ngach
síniú an mhodha, is don eagraíocht é. Chuireamar gach rud is féidir linn a dhéanamh
le sampla de chineál i mbloc `impl` amháin seachas úsáideoirí a dhéanamh amach anseo
dár gcuardach cód le haghaidh cumais `Rectangle` in áiteanna éagsúla sa
leabharlann a chuirimid ar fáil.

Tabhair faoi deara gur féidir linn a roghnú modh a thabhairt ar an ainm céanna le ceann de na struchtúir
réimsí. Mar shampla, is féidir linn modh a shainiú ar `Rectangle` atá ainmnithe freisin
`width`:

<Listing file-name="src/main.rs">

```rust
{{#rustdoc_include ../../listings/ch05-using-structs-to-structure-related-data/no-listing-06-method-field-interaction/src/main.rs:here}}
```

</Listing>

Anseo, táimid ag roghnú an modh `width` a thabhairt ar ais `true` má tá an luach isteach
tá réimse `width` an ásc níos mó ná `0` agus `false` más luach é
`0`: is féidir linn réimse a úsáid laistigh de mhodh den ainm céanna chun críche ar bith. I
`main`, nuair a leanaimid `rect1.width` le lúibíní, tá a fhios ag Rust gurb éard atá i gceist againn
modh `width`. Nuair nach n-úsáidimid lúibíní, tá a fhios ag Rust go bhfuil an réimse i gceist againn
`width`.

Go minic, ach ní i gcónaí, nuair a thugaimid modh an t-ainm céanna le réimse ba mhaith linn
é a thabhairt ar ais ach an luach sa réimse agus rud ar bith eile a dhéanamh. Modhanna mar seo
Tugtar _getters_ orthu, agus ní chuireann Rust i bhfeidhm iad go huathoibríoch le haghaidh struchtúr
réimsí mar a dhéanann roinnt teangacha eile. Tá getters úsáideach mar is féidir leat an
réimse príobháideach ach an modh poiblí, agus dá bhrí sin cumasaigh rochtain inléite amháin air sin
réimse mar chuid den chineál API poiblí. Déanfaimid plé ar cad poiblí agus príobháideach
atá agus conas réimse nó modh a ainmniú mar phoiblí nó príobháideach i [Caibidil
7][public] <!-- neamhaird a dhéanamh -->.

> ### Cá bhfuil an t-oibreoir `->`?
>
> In C agus C++, úsáidtear dhá oibreoir éagsúla chun modhanna glaonna a úsáid: úsáideann tú
> `.` má tá tú ag glaoch modh ar an réad go díreach agus `->` má tá tú
> an modh a ghlaoch ar phointeoir don réad agus is gá díthagairt a dhéanamh don
> pointeoir ar dtús. I bhfocail eile, más pointeoir é `object`,
> Tá `object->something()` cosúil le `(*object).something()`.
>
> Níl coibhéis ag meirge leis an oibreoir `->`; ina ionad sin, tá Rust a
> gné ar a dtugtar _tagairtí uathoibríocha agus dereferencing_. Tá modhanna glaonna
> ceann de na cúpla áit i Rust leis an iompar seo.
>
> Seo mar a oibríonn sé: nuair a ghlaonn tú ar mhodh le `object.something()`, Rust
> cuireann sé isteach `&`, `&mut`, nó `*` go huathoibríoch ionas go meaitseálann `object` síniú
> an modh. I bhfocail eile, tá na rudaí seo a leanas mar an gcéanna:
>
> <!-- CAN'T EXTRACT SEE BUG https://github.com/rust-lang/mdBook/issues/1127 -->
>
> ```rust
> # #[derive(Debug,Copy,Clone)]
> # struct Point {
> #     x: f64,
> #     y: f64,
> # }
> #
> # impl Point {
> #    fn distance(&self, other: &Point) -> f64 {
> #        let x_squared = f64::powi(other.x - self.x, 2);
> #        let y_squared = f64::powi(other.y - self.y, 2);
> #
> #        f64::sqrt(x_squared + y_squared)
> #    }
> # }
> # let p1 = Point { x: 0.0, y: 0.0 };
> # let p2 = Point { x: 5.0, y: 6.5 };
> p1.distance(&p2);
> (&p1).distance(&p2);
> ```
>
> Breathnaíonn an chéad cheann i bhfad níos glaine. Oibríonn an t-iompar tagartha uathoibríoch seo
> toisc go bhfuil glacadóir soiléir ag modhanna - an cineál `self`. I bhfianaise an ghlacadóra
> agus ainm an mhodha, is féidir le Rust a dhéanamh amach go cinntitheach an bhfuil an modh
> ag léamh (`&self`), ag mutating (`&mut self`), nó ag ithe (`self`). An bhfíric
> go dtugann Rust iasachtaíocht intuigthe do ghlacadóirí modhanna is cuid mhór de
> úinéireacht a dhéanamh eirgeanamaíochta go praiticiúil.

### Modhanna le Tuilleadh Paraiméadair

Déanaimis modhanna a chleachtadh trí mhodh eile a chur i bhfeidhm ar an `Rectangle`
struchtúr. An uair seo ba mhaith linn sampla de `Rectangle` a ghlacadh mar shampla eile
de `Rectangle` agus seol ar ais `true` más féidir leis an dara `Rectangle` oiriúnach go hiomlán
laistigh de `self` (an chéad `Rectangle`); ar shlí eile, ba cheart go dtabharfadh sé `false` ar ais.
Is é sin, nuair a bheidh an modh `can_hold` sainmhínithe againn, ba mhaith linn a bheith in ann scríobh
an clár a thaispeántar i Liosta 5-14.

<Listing number="5-14" file-name="src/main.rs" caption="Using the as-yet-unwritten `can_hold` method">

```rust,ignore
{{#rustdoc_include ../../listings/ch05-using-structs-to-structure-related-data/listing-05-14/src/main.rs}}
```

</Listing>

Bheadh ​​cuma mar seo a leanas ar an aschur a bhfuiltear ag súil leis toisc go bhfuil an dá thoise de
tá `rect2` níos lú ná toisí `rect1`, ach tá `rect3` níos leithne ná
`rect1`:

```text
Can rect1 hold rect2? true
Can rect1 hold rect3? false
```

Tá a fhios againn gur mhaith linn modh a shainiú, mar sin beidh sé laistigh den `impl Rectangle`
bloc. Is é an t-ainm modha `can_hold`, agus tógfaidh sé iasacht neamh-inmhalartaithe
de `Rectangle` eile mar pharaiméadar. Is féidir linn a insint cad é an cineál an
Déanfar paraiméadar trí bhreathnú ar an gcód a ghlaonn an modh:
Gabhann `rect1.can_hold(&rect2)` isteach in `&rect2`, ar iasacht do-inmheasúnaithe é
`rect2`, sampla de `Rectangle`. Déanann sé seo ciall mar ní gá dúinn ach
léigh `rect2` (seachas scríobh, rud a chiallódh go mbeadh iasacht sho-shóite de dhíth orainn),
agus ba mhaith linn go gcoimeádfadh `main` úinéireacht ar `rect2` ionas gur féidir linn é a úsáid arís ina dhiaidh sin
ag glaoch ar an modh `can_hold`. Is é luach aischuir `can_hold` ná a
Beidh Boole, agus an cur i bhfeidhm a sheiceáil cibé an leithead agus airde
tá `self` níos mó ná leithead agus airde an `Rectangle` eile,
faoi ​​seach. Cuirimis an modh nua `can_hold` leis an mbloc `impl` ó
Liostú 5-13, léirithe i Liostú 5-15.

<Listing number="5-15" file-name="src/main.rs" caption="Implementing the `can_hold` method on `Rectangle` that takes another `Rectangle` instance as a parameter">

```rust
{{#rustdoc_include ../../listings/ch05-using-structs-to-structure-related-data/listing-05-15/src/main.rs:here}}
```

</Listing>

Nuair a rithimid an cód seo leis an `main` i Liostú 5-14, gheobhaidh muid ár
aschur inmhianaithe. Is féidir le modhanna a ghlacadh paraiméadair iolracha a chuirimid leis an
síniú tar éis an pharaiméadar `self`, agus oibríonn na paraiméadair sin díreach mar a chéile
paraiméadair i bhfeidhmeanna.

### Feidhmeanna Gaolmhara

Tugtar _feidhmeanna gaolmhara_ ar gach feidhm a shainítear laistigh de bhloc `impl`
toisc go bhfuil baint acu leis an gcineál atá ainmnithe i ndiaidh an `impl`. Is féidir linn a shainiú
feidhmeanna gaolmhara nach bhfuil `self` mar a gcéad pharaiméadar acu (agus mar sin
nach modhanna iad) toisc nach bhfuil sampla den chineál ag teastáil uathu le bheith ag obair leo.
Tá feidhm amháin mar seo úsáidte againn cheana féin: an fheidhm `String::from` .Tá feidhm amháin 
mar seo úsáidte againn cheana féin: an fheidhm `String::from` a shainmhínítear ar an gcineál `String`.

Is minic a úsáidtear feidhmeanna gaolmhara nach modhanna iad le haghaidh tógálaithe a
tabharfaidh sé sampla nua den struchtúr ar ais. Is minic a dtugtar `new` orthu seo, ach
Ní ainm speisialta é ‘nua’ agus níl sé fite fuaite sa teanga. Mar shampla, táimid
d'fhéadfadh sé a roghnú feidhm ghaolmhar darb ainm `square` a sholáthar a bheadh ​​aici
paraiméadar toise amháin agus é sin a úsáid mar leithead agus airde araon, rud a fhágann go bhfuil sé
níos éasca `Rectangle` cearnach a chruthú seachas a bheith ag sonrú an rud céanna
luach faoi dhó:

<span class="filename">Filename: src/main.rs</span>

```rust
{{#rustdoc_include ../../listings/ch05-using-structs-to-structure-related-data/no-listing-03-associated-functions/src/main.rs:here}}
```

Is iad na heochairfhocail `self` sa chineál tuairisceáin agus i gcorp na feidhme
ailiasanna don chineál a thagann i ndiaidh an eochairfhocail `impl`, atá sa chás seo
is `Rectangle`.

Chun an fheidhm ghaolmhar seo a ghlaoch, úsáidimid an chomhréir `::` leis an ainm struct;
Is sampla é `let sq = Rectangle::square(3);`. Tá an fheidhm seo spásáilte le
an struct: úsáidtear an chomhréir `::` don dá fheidhm chomhcheangailte agus
spásanna ainmneacha cruthaithe ag modúil. Déanfaimid modúil a phlé i [Caibidil
7][modules] <!-- neamhaird a dhéanamh -->.

### Bloic `impl` iolracha

Ceadaítear bloic iolracha `impl` a bheith ag gach struchtúr. Mar shampla, Liostú
Tá 5-15 comhionann leis an gcód a thaispeántar i Liosta 5-16, a bhfuil gach modh ann
a bhloc `impl` féin.

<Listing number="5-16" caption="Rewriting Listing 5-15 using multiple `impl` blocks">

```rust
{{#rustdoc_include ../../listings/ch05-using-structs-to-structure-related-data/listing-05-16/src/main.rs:here}}
```

</Listing>

Níl aon chúis leis na modhanna seo a dheighilt ina mbloic `impl` iolracha anseo,
ach is comhréir bailí é seo. Feicfimid cás ina bhfuil bloic `impl` iolracha
úsáideach i gCaibidil 10, ina bpléimid cineálacha agus tréithe cineálacha.

## Achoimre

Ligeann struchtúir duit cineálacha saincheaptha a chruthú a bhfuil brí leo do d'fhearann. Le
ag baint úsáide as struchtúir, is féidir leat píosaí sonraí gaolmhara a choinneáil ceangailte lena chéile
agus ainmnigh gach píosa chun do chód a dhéanamh soiléir. I mbloic `impl`, is féidir leat a shainiú
feidhmeanna a bhaineann le do chineál, agus modhanna atá ar chineál an
fheidhm ghaolmhar a ligeann duit a shonrú ar an iompar go cásanna de do
tá struchtúir.

Ach ní hiad struchtúir an t-aon bhealach ar féidir leat cineálacha saincheaptha a chruthú: déanaimis iompú orthu
Gné Rust's enum chun uirlis eile a chur le do bhosca uirlisí.

[enums]: ch06-00-enums.html
[trait-objects]: ch18-02-trait-objects.md
[public]: ch07-03-paths-for-referring-to-an-item-in-the-module-tree.html#exposing-paths-with-the-pub-keyword
[modules]: ch07-02-defining-modules-to-control-scope-and-privacy.html