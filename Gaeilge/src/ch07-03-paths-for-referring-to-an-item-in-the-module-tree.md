## Cosáin chun Tagairt a Dhéanamh do Mhír i gCrann an Mhodúil

Chun Rust a thaispeáint nuair is féidir mír a aimsiú i gcrann modúl, úsáidimid cosán mar an gcéanna
ar an mbealach a n-úsáidimid cosán agus córas comhaid á nascleanúint. Chun feidhm a ghlaoch, ní mór dúinn
fios a chosáin.

Is féidir le cosán a bheith i dhá fhoirm:

- Is é _absolute path_ an cosán iomlán a thosaíonn ó fhréamh gcliathbhosca; le haghaidh cód
 ó chliathbhosca seachtrach, tosaíonn an cosán iomlán le hainm an chliabháin, agus le haghaidh
 cód ón gcliathbhosca reatha, tosaíonn sé leis an `crate` litriúil.
- Tosaíonn cosán _relative_ ón modúl reatha agus úsáidtear `self`, `super`, nó
 aitheantóir sa mhodúl reatha.

Leanann aitheantóir amháin nó níos mó cosáin iomlána agus choibhneasta araon
scartha le coilíneachtaí dúbailte (`::`).

Ag filleadh ar Liostú 7-1, abair gur mhaith linn an fheidhm `add_to_waitlist` a ghlaoch.
Is ionann é seo agus fiafraí: cad é cosán na feidhme `add_to_waitlist`?
I Liostáil 7-3 tá Liosta 7-1 le roinnt de na modúil agus feidhmeanna
bhaintear.

Taispeánfaimid dhá bhealach chun an fheidhm `add_to_waitlist` a ghlaoch ó fheidhm nua,
`eat_at_restaurant`, sainmhínithe i bhfréamh an chliathbhosca. Tá na cosáin seo ceart, ach
tá fadhb eile fágtha a chuirfidh cosc ​​ar an sampla seo a chur le chéile
mar atá. Míneoimid cén fáth i mbeagán focal.

Tá an fheidhm `eat_at_restaurant` mar chuid d'API poiblí ár gcliathbhosca leabharlainne, mar sin
marcálann muid é leis an eochairfhocal `pub`. Sa [“Cosáin Nochtadh leis an `pub`
Eochairfhocal”][pub] <!-- neamhaird a dhéanamh ar --> alt, déanfaimid níos mó sonraí faoi `pub`.

<Listing number="7-3" file-name="src/lib.rs" caption="Calling the `add_to_waitlist` function using absolute and relative paths">

```rust,ignore,does_not_compile
{{#rustdoc_include ../../listings/ch07-managing-growing-projects/listing-07-03/src/lib.rs}}
```

</Listing>

An chéad uair a ghlaoimid an fheidhm `add_to_waitlist` i `eat_at_restaurant`,
úsáidimid cosán iomlán. Sainmhínítear an fheidhm `add_to_waitlist` mar an gcéanna
cliathbhosca mar `eat_at_restaurant`, rud a chiallaíonn gur féidir linn an eochairfhocal `crate` a úsáid chun
tús a chur le cosán iomlán. Áirímid ansin gach ceann de na modúil as a chéile go dtí go ndéanaimid
déan ár mbealach chuig `add_to_waitlist`. Is féidir leat córas comhaid a shamhlú leis an gcéanna
struchtúr: shonraigh muid an cosán `/front_of_house/hosting/add_to_waitlist` go dtí
reáchtáil an clár `add_to_waitlist`; ag baint úsáide as an ainm `crate` chun tosú as an
Is cosúil le fréamh an chliabháin úsáid a bhaint as `/` chun tosú ó fhréamh an chórais comhad i do bhlaosc.

An dara huair a ghlaoimid `add_to_waitlist` i `eat_at_restaurant`, úsáidimid
cosán coibhneasta. Tosaíonn an cosán le `front_of_house`, ainm an mhodúil
sainmhínithe ag an leibhéal céanna de chrann an mhodúil le `eat_at_restaurant`. Seo an
bheadh ​​​​coibhéis córas comhaid ag baint úsáide as an gcosán
`front_of_house/hosting/add_to_waitlist`. Ag tosú le hainm modúl ciallaíonn
go bhfuil an cosán coibhneasta.

Is é an cinneadh a dhéanfaidh tú maidir le conair ghaolmhar nó cosán iomlán a roghnú
bunaithe ar do thionscadal, agus braitheann sé ar cibé an bhfuil seans níos mó agat bogadh
cód sainmhínithe míre ar leithligh ó nó in éineacht leis an gcód a úsáideann an
mír. Mar shampla, má bhog muid an modúl `front_of_house` agus an
feidhmíonn `eat_at_restaurant` isteach i modúl darb ainm `customer_experience`, bheimis
gá an cosán iomlán chuig `add_to_waitlist` a nuashonrú, ach an cosán coibhneasta
bheadh ​​bailí fós. Mar sin féin, má bhog muid an fheidhm `eat_at_restaurant`
ar leithligh isteach i modúl darb ainm `dining`, an cosán iomlán chuig an
D'fhanfadh an glao `add_to_waitlist` mar a chéile, ach bheadh ​​gá leis an gcosán coibhneasta
a nuashonrú. Is é an rogha atá againn i gcoitinne ná cosáin iomlána a shonrú toisc go bhfuil
is dóichí go mbeidh muid ag iarraidh sainmhínithe cód agus glaonna míreanna a bhogadh go neamhspleách orthu
chéile.

Déanaimis iarracht Liostú 7-3 a thiomsú agus faigh amach cén fáth nach dtiomsóidh sé fós! Tá an
taispeántar na hearráidí a fhaighimid i Liostú 7-4.

<Listing number="7-4" caption="Compiler errors from building the code in Listing 7-3">

```console
{{#include ../../listings/ch07-managing-growing-projects/listing-07-03/output.txt}}
```

</Listing>

Deir na teachtaireachtaí earráide go bhfuil modúl `hosting` príobháideach. I bhfocail eile, táimid
bíodh na cosáin chearta agat don mhodúl `hosting` agus don `add_to_waitlist`
feidhm, ach ní ligfidh Rust dúinn iad a úsáid toisc nach bhfuil rochtain aige ar an
rannóga príobháideacha. I Rust, tá gach mír (feidhmeanna, modhanna, struchtúir, enums,
modúil, agus tairisigh) príobháideach do mhodúil tuismitheora de réir réamhshocraithe. Más mian leat
chun mír mar fheidhm nó struchtúr a dhéanamh príobháideach, cuireann tú i modúl é.

Ní féidir le míreanna i modúl tuismitheora na míreanna príobháideacha taobh istigh de mhodúil leanaí a úsáid, ach
is féidir le míreanna i modúil leanaí na míreanna i modúil a sinsear a úsáid. Tá sé seo
mar gheall ar mhodúil leanbh wrap agus a cheilt a gcuid sonraí cur chun feidhme, ach an leanbh
is féidir le modúil an comhthéacs ina bhfuil siad sainithe a fheiceáil. Chun leanúint ar aghaidh lenár
meafar, smaoinigh ar na rialacha príobháideachais mar chúloifig a
bialann: is príobháideach do chustaiméirí bialainne an rud a théann ar aghaidh ann, ach
is féidir le bainisteoirí oifige gach rud a fheiceáil agus a dhéanamh sa bhialann a oibríonn siad.

Roghnaigh Rust go mbeadh an córas modúil ag feidhmiú ar an mbealach seo ionas go gcuirfí i bhfolach taobh istigh
is é sonraí cur chun feidhme an réamhshocrú. Ar an mbealach sin, tá a fhios agat cé na codanna den
cód istigh is féidir leat a athrú gan an cód seachtrach a bhriseadh. Mar sin féin, tugann Rust
tá an rogha agat codanna istigh de chód na modúil leanaí a nochtadh don tsinsir sheachtrach
modúil tríd an eochairfhocal `pub` a úsáid chun mír a phoibliú.

### Conairí á Nochtadh leis an Eochairfhocal `pub`

Fillfimid ar an earráid i Liostú 7-4 a chuir in iúl dúinn gurb é an modúl `hosting`
príobháideach. Ba mhaith linn go mbeadh an fheidhm `eat_at_restaurant` sa mhodúl tuismitheora
rochtain ar an bhfeidhm `add_to_waitlist` sa mhodúl linbh, mar sin marcálann muid an
modúl `hosting` leis an eochairfhocal `pub`, mar a thaispeántar i Liosta 7-5.

<Listing number="7-5" file-name="src/lib.rs" caption="Declaring the `hosting` module as `pub` to use it from `eat_at_restaurant`">

```rust,ignore,does_not_compile
{{#rustdoc_include ../../listings/ch07-managing-growing-projects/listing-07-05/src/lib.rs}}
```

</Listing>

Ar an drochuair, tá earráidí tiomsaitheora fós mar thoradh ar an gcód i Liostú 7-5, mar
léirithe i Liosta 7-6.

<Listing number="7-6" caption="Compiler errors from building the code in Listing 7-5">

```console
{{#include ../../listings/ch07-managing-growing-projects/listing-07-05/output.txt}}
```

</Listing>

Cad a tharla? Nuair a chuirtear an eochairfhocal `pub` os comhair `mod hosting` déanann an
modúl poiblí. Leis an athrú seo, más féidir linn rochtain a fháil ar `front_of_house`, is féidir linn
rochtain a fháil ar `hosting`. Ach tá na _contents_ de `hosting` fós príobháideach; ag déanamh an
ní dhéanann an modúl poiblí a bhfuil ann. An eochairfhocal `pub` ar mhodúl
ní ligeann sé ach tagairt a dhéanamh do chód ina mhodúil sinsear, ní rochtain a fháil ar a chód istigh.
Toisc gur coimeádáin iad modúil, níl mórán ar féidir linn a dhéanamh ach an
modúl poiblí; caithfimid dul níos faide agus rogha a dhéanamh ceann amháin nó níos mó de na
míreanna laistigh den mhodúl poiblí chomh maith.

Deir na hearráidí i Liostú 7-6 go bhfuil an fheidhm `add_to_waitlist` príobháideach.
Baineann na rialacha príobháideachais le struchtúir, ainmneacha, feidhmeanna agus modhanna chomh maith
modúil.

Déanaimis an fheidhm `add_to_waitlist` a phoibliú freisin tríd an `pub` a chur leis
eochairfhocal roimh a shainmhíniú, mar atá i Liostú 7-7.

<Listing number="7-7" file-name="src/lib.rs" caption="Adding the `pub` keyword to `mod hosting` and `fn add_to_waitlist` lets us call the function from `eat_at_restaurant`">

```rust,noplayground,test_harness
{{#rustdoc_include ../../listings/ch07-managing-growing-projects/listing-07-07/src/lib.rs}}
```

</Listing>

Anois beidh an cód le chéile! Chun a fháil amach cén fáth a ligeann dúinn úsáid a bhaint as an eochairfhocal `pub`
na cosáin seo i `eat_at_restaurant` maidir leis na rialacha príobháideachais, breathaimis
ag na cosáin iomlána agus coibhneasta.

Ar an mbealach iomlán, cuirimid tús le `crate`, fréamh modúl ár gcliathbhosca
crann. Sainmhínítear an modúl `front_of_house` i bhfréamh an chliathbhosca. Cé go
Níl `front_of_house` poiblí, toisc go bhfuil an fheidhm `eat_at_restaurant` ann
sainithe sa mhodúl céanna le `front_of_house` (is é sin, `eat_at_restaurant`
agus is siblíní iad `front_of_house`), is féidir linn tagairt a dhéanamh do `front_of_house` ó
`eat_at_restaurant`. Ar aghaidh tá an modúl `hosting` marcáilte le `pub`. Is féidir linn
rochtain a fháil ar an modúl tuismitheora de `hosting`, ionas gur féidir linn rochtain a fháil ar `hosting`. Ar deireadh, an
marcáiltear an fheidhm `add_to_waitlist` le `pub` agus is féidir linn rochtain a fháil ar a thuismitheoir
modúl, mar sin oibríonn an glao feidhm seo!

Sa chonair choibhneasta, tá an loighic mar an gcéanna leis an gcosán iomlán ach amháin i gcás an
chéad chéim: seachas tosú ó fhréamh an gcliathbhosca, tosaíonn an cosán ó
`front_of_house`. Sainmhínítear an modúl `front_of_house` laistigh den mhodúl céanna
mar `eat_at_restaurant`, mar sin an cosán coibhneasta ag tosú ón modúl ina bhfuil
Is saothair shainithe é `eat_at_restaurant`. Ansin, mar gheall ar `hosting` agus
marcáiltear `add_to_waitlist` le `pub`, oibríonn an chuid eile den chosán, agus seo
Tá glao feidhm bailí!

Má tá sé ar intinn agat do chliabhán leabharlainne a chomhroinnt ionas gur féidir le tionscadail eile do chód a úsáid,
is é do API poiblí do chonradh le húsáideoirí do chliabhán a chinneann conas
is féidir leo idirghníomhú le do chód. Tá go leor cúinsí maidir le bainistiú
athruithe ar do API poiblí chun é a dhéanamh níos éasca do dhaoine brath ar do
cliathbhosca. Tá na breithnithe seo lasmuigh de scóip an leabhair seo; má tá tú
suim agat san ábhar seo, féach [Treoirlínte Rust API][api-guidelines].

> #### Dea-Chleachtais maidir le Pacáistí le Dénártha agus Leabharlann
>
> Luaigh muid gur féidir le cliathbhosca dénártha _src/main.rs_ a bheith i bpacáiste
> fréamh chomh maith le fréamh gcliathbhosca leabharlainne _src/lib.rs_, agus beidh an dá chliathbhosca
> ainm an phacáiste de réir réamhshocraithe. De ghnáth, pacáistí leis an bpatrún seo de
> ina mbeidh leabharlann agus cliathbhosca dénártha araon, beidh go leor cód sa
> cliathbhosca dénártha chun inrite a thosú a ghlaonn cód laistigh de chliathán na leabharlainne.
> Ligeann sé seo do thionscadail eile leas a bhaint as an gcuid is mó den fheidhmiúlacht a chuireann an
> soláthraíonn pacáiste toisc gur féidir cód an chliabháin leabharlainne a roinnt.
>
> Ba cheart crann an mhodúil a shainiú in _src/lib.rs_. Ansin, is féidir aon nithe poiblí
> a úsáid sa chliabhán dénártha trí chosáin a thosú le hainm an phacáiste.
> Bíonn an cliathbhosca dénártha ina úsáideoir ar an gcliathbhosca leabharlainne díreach mar a bheadh ​​go hiomlán
> d’úsáidfeadh cliathbhosca seachtrach cliathbhosca na leabharlainne: ní féidir leis ach an API poiblí a úsáid.
> Cuidíonn sé seo leat API maith a dhearadh; ní hamháin gur tusa an t-údar, is tusa freisin
> cliant!
>
> I [Caibidil 12][ch12]<!-- neamhaird a dhéanamh -->, léireoimid an eagraíocht seo
> cleachtadh le clár ordaithe ina mbeidh cliathbhosca dénártha araon
> agus cliathbhosca leabharlainne.

### Ag tosú Cosáin Choibhneasta le `super`

Is féidir linn cosáin choibhneasta a thógáil a thosaíonn sa mhodúl tuismitheora, seachas
an modúl reatha nó an fhréamh cliathbhosca, trí úsáid a bhaint as `super` ag tús an
cosán. Tá sé seo cosúil le cosán córais comhad a thosú leis an gcomhréir `..`. Ag baint úsáide as
ligeann `super` dúinn tagairt a dhéanamh do mhír a bhfuil a fhios againn atá sa mhodúl tuismitheora,
rud a d'fhéadfadh an crann modúl a atheagrú níos éasca nuair a bhíonn an modúl go dlúth
a bhaineann leis an tuismitheoir ach d’fhéadfaí an tuismitheoir a aistriú chuig áit eile sa mhodúl
crann lá éigin.

Smaoinigh ar an gcód i Liosta 7-8 a mhúnlaíonn an cás ina bhfuil cócaire
socraíonn sé ordú mícheart agus tugann sé amach go pearsanta don chustaiméir é. Tá an
feidhm `fix_incorrect_order` a shainmhínítear sa mhodúl `back_of_house` ar a dtugtar an
feidhm `deliver_order` arna shainiú sa mhodúl tuismitheora tríd an gcosán chuig a shonrú
`deliver_order`, ag tosú le `super`.

<Listing number="7-8" file-name="src/lib.rs" caption="Calling a function using a relative path starting with `super`">

```rust,noplayground,test_harness
{{#rustdoc_include ../../listings/ch07-managing-growing-projects/listing-07-08/src/lib.rs}}
```

</Listing>

Tá an fheidhm `fix_incorrect_order` sa mhodúl `back_of_house`, ionas gur féidir linn
úsáid `super` chun dul go dtí an modúl tuismitheora de `back_of_house`, atá sa chás seo
is `crate`, an fhréamh. Ón áit sin, lorgaímid `deliver_order` agus faighimid é.
Rath! Is dóigh linn go bhfuil an modúl `back_of_house` agus an fheidhm `deliver_order`
is dócha go bhfanfaidh siad sa chaidreamh céanna lena chéile agus go n-aistreofar iad
le chéile ar cheart dúinn cinneadh a dhéanamh crann modúl an chliathbhosca a atheagrú. Dá bhrí sin, táimid
úsáid as `super` mar sin beidh níos lú áiteanna againn chun cód a nuashonrú amach anseo más amhlaidh
bogtar an cód go modúl eile.

### Struchtúir agus Enums a Dhéanamh go Poiblí

Is féidir linn `pub` a úsáid freisin chun struchtúir agus enums a ainmniú go poiblí, ach tá a
roinnt sonraí breise maidir le húsáid `pub` le struchtúir agus enums. Má úsáidimid `pub`
roimh shainmhíniú struchtúr, déanaimid an struchtúr poiblí, ach réimsí an struchtúir
beidh sé fós príobháideach. Is féidir linn gach réimse a dhéanamh poiblí nó gan a bheith bunaithe ar chás
bonn. I Liostú 7-9, shainmhíomar struchtúr poiblí `back_of_house::Breakfast`
le réimse poiblí `toast` ach réimse príobháideach `seasonal_fruit`. Samhlacha seo
an cás i mbialann inar féidir leis an gcustaiméir an cineál aráin sin a phiocadh
Tagann béile le béile, ach socraíonn an cócaire cé na torthaí a théann leis an mbéile atá bunaithe
ar cad atá i séasúr agus i stoc. Athraíonn na torthaí atá ar fáil go tapa, mar sin
ní féidir le custaiméirí na torthaí a roghnú nó fiú na torthaí a gheobhaidh siad a fheiceáil.

<Listing number="7-9" file-name="src/lib.rs" caption="A struct with some public fields and some private fields">

```rust,noplayground
{{#rustdoc_include ../../listings/ch07-managing-growing-projects/listing-07-09/src/lib.rs}}
```

</Listing>

Toisc go bhfuil an réimse `toast` sa struchtúr `back_of_house::Breakfast` poiblí,
i `eat_at_restaurant` is féidir linn scríobh agus léamh chuig an réimse `toast` ag baint úsáide as ponc
nodaireacht. Tabhair faoi deara nach féidir linn an réimse `seasonal_fruit` a úsáid i
`eat_at_restaurant`, toisc go bhfuil `seasonal_fruit` príobháideach. Bain triail as uncommenting an
líne ag modhnú an luach réimse `seasonal_fruit` féachaint cén earráid a gheobhaidh tú!

Chomh maith leis sin, tabhair faoi deara toisc go bhfuil réimse príobháideach ag `back_of_house::Breakfast`, ní mór an
Ní mór do struchtúr feidhm a bhaineann leis an bpobal a sholáthar a fhoirgníonn an
mar shampla `Bricfeasta` (tá `summer` tugtha againn anseo). Mura raibh `Breakfast`
a leithéid d’fheidhm a bheith againn, níorbh fhéidir linn sampla de `Breakfast` a chruthú i
`eat_at_restaurant` mar níorbh fhéidir linn luach an phríobháidigh a shocrú
réimse `seasonal_fruit` i `eat_at_restaurant`.

I gcodarsnacht leis sin, má dhéanaimid enum poiblí, tá gach leagan dá chuid poiblí ansin. muid
níl de dhíth ach an `pub` roimh an eochairfhocal `enum`, mar a thaispeántar i Liosta 7-10.

<Listing number="7-10" file-name="src/lib.rs" caption="Designating an enum as public makes all its variants public">

```rust,noplayground
{{#rustdoc_include ../../listings/ch07-managing-growing-projects/listing-07-10/src/lib.rs}}
```

</Listing>

Toisc go ndearnamar an `Appetizer` enum poiblí, is féidir linn an `Soup` agus `Salad` a úsáid
leaganacha i `eat_at_restaurant`.

Ní bhíonn enums an-úsáideach mura bhfuil a gcuid leaganacha poiblí; bheadh ​​sé annoying
ní mór gach leagan enum a anótáil le `pub` i ngach cás, mar sin an réamhshocrú
le haghaidh leagan enum le bheith poiblí. Is minic a bhíonn struchtúir úsáideach gan a gcuid
réimsí a bheith poiblí, mar sin réimsí struct leanúint riail ghinearálta gach rud
a bheith príobháideach de réir réamhshocraithe ach amháin má tá `pub` anótáilte air.

Tá cás amháin eile a bhaineann le ‘teach tábhairne’ nár chlúdaigh muid, agus is é sin
an ghné dheireanach den chóras modúil atá againn: an eochairfhocal `use`. Clúdóidh muid `use` leis féin
ar dtús, agus ansin taispeánfaimid conas `pub` agus `use` a chur le chéile.

[pub]: ch07-03-paths-for-referring-to-an-item-in-the-module-tree.html#exposing-paths-with-the-pub-keyword
[api-guidelines]: https://rust-lang.github.io/api-guidelines/
[ch12]: ch12-00-an-io-project.html