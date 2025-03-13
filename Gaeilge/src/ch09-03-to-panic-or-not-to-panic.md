## Go `panic!` nó Gan `panic!`

Mar sin, conas a shocraíonn tú cathain ba cheart duit `panic!` a ghlaoch agus cathain ba cheart duit filleadh
`Result`? Nuair a scaoll cód, níl aon bhealach a ghnóthú. D’fhéadfá `panic!` a ghlaoch
i gcás aon earráide, cibé an bhfuil bealach féideartha ann chun aisghabháil nó nach bhfuil, ach
ansin tá tú ag déanamh an chinnidh nach féidir cás a aisghabháil ar son
an cód glaonna. Nuair a roghnaíonn tú luach `Result` a thabhairt ar ais, tugann tú an
roghanna cód glaonna. D'fhéadfadh an cód glaonna a roghnú chun iarracht a dhéanamh a ghnóthú i
ar bhealach atá feiliúnach dá chás, nó d’fhéadfadh sé a chinneadh go ndéanfaí ‘Earráid’
Tá luach sa chás seo do-aisghabhála, mar sin is féidir glaoch ar `panic!` agus cas do
earráid in-aisghabhála isteach i gceann do-aisghabhála. Mar sin, is éard atá i gceist le `Result` a thabhairt ar ais
rogha réamhshocraithe maith nuair a bhíonn feidhm á sainiú agat a d’fhéadfadh teip a bheith uirthi.

I gcásanna mar shamplaí, cód fréamhshamhail, agus tástálacha, tá sé níos mó
cuí cód a scríobh a scanraíonn seachas `Result` a thabhairt ar ais. Déanaimis
fiosraigh cén fáth, ansin pléigh cásanna nach féidir leis an tiomsaitheoir é sin a insint
Tá teip dodhéanta, ach is féidir leat mar an duine. Críochnóidh an chaibidil le
roinnt treoirlínte ginearálta maidir le conas a chinneadh cé acu an scaoll i gcód na leabharlainne.

### Samplaí, Cód Fréamhshamhail, agus Tástálacha

Agus sampla á scríobh agat chun coincheap éigin a léiriú, lena n-áirítear freisin
is féidir le cód láidir láimhseála earráidí an sampla a dhéanamh níos soiléire. I samplaí, tá
thuigtear gurb é atá i gceist le glao ar mhodh cosúil le `unwrap` a d'fhéadfadh scaoll a dhéanamh ná a
ionadsealbhóir don tslí ar mhaith leat go láimhseálfadh d’iarratas earráidí, is féidir
difriúil bunaithe ar a bhfuil an chuid eile de do chód a dhéanamh.

Mar an gcéanna, bíonn na modhanna `unwrap` agus `expect` an-áisiúil agus fréamhshamhaltú á dhéanamh,
sula mbeidh tú réidh chun cinneadh a dhéanamh conas earráidí a láimhseáil. Fágann siad marcóirí soiléire isteach
do chód le haghaidh nuair a bheidh tú réidh chun do chlár a dhéanamh níos láidre.

Má theipeann ar ghlao modha i dtástáil, ba mhaith leat go dteipfeadh ar an tástáil iomlán, fiú dá mbeadh
ní hé an modh sin an fheidhmiúlacht atá á thástáil. Toisc go bhfuil `panic!` mar thástáil
marcáilte mar theip, agus is é `unwrap` nó `expect` go díreach cad ba cheart
tarlú.

### Cásanna ina Bhfuil Breis Eolais Agat Ná An Tiomsaitheoir

Bheadh ​​sé oiriúnach freisin `unwrap` nó `expect` a ghlaoch nuair a bhíonn roinnt agat
loighic eile a chinntíonn go mbeidh luach `Ok` ag an `Result`, ach an loighic
nach rud é a thuigeann an tiomsaitheoir. Beidh luach `Result` fós agat
nach mór duit a láimhseáil: is cuma cén oibríocht atá á glaoch agat fós
féidearthacht teip i gcoitinne, cé go bhfuil sé dodhéanta go loighciúil
do chás ar leith. Más féidir leat a chinntiú tríd an gcód a iniúchadh de láimh
nach mbeidh leagan `Err` agat choíche, tá sé breá inghlactha glaoch a chur air
`unwrap`, agus níos fearr fós a dhoiciméadú ar an gcúis a cheapann tú nach mbeidh riamh agat
Leagan `Err` sa téacs `expect`. Seo sampla:

```rust
{{#rustdoc_include ../../listings/ch09-error-handling/no-listing-08-unwrap-that-cant-fail/src/main.rs:here}}
```

Táimid ag cruthú sampla `IpAddr` trí teaghrán crua-chóid a pharsáil. Is féidir linn a fheiceáil
gur seoladh IP bailí é `127.0.0.1`, mar sin tá sé inghlactha `expect` a úsáid
anseo. Mar sin féin, le teaghrán bailí, códaithe, ní athraíonn an cineál tuairisceáin
den mhodh `parse`: faigheann muid luach `Result` fós, agus gheobhaidh an tiomsaitheoir
déanaimid fós an `Result` a láimhseáil amhail is gur féidir an leagan `Err` a dhéanamh
mar nach bhfuil an tiomsaitheoir cliste go leor chun a fheiceáil go bhfuil an teaghrán seo i gcónaí a
seoladh IP bailí. Má tháinig an teaghrán seoladh IP ó úsáideoir seachas a bheith
hardcoded isteach sa chlár agus mar sin _raibh_ seans teipe,
Is cinnte gur mhaith linn an `Result` a láimhseáil ar bhealach níos láidre ina ionad sin.
Má luann tú an toimhde go bhfuil an seoladh IP seo códaithe crua, spreagfar sinn é sin a dhéanamh
athrú `expect` go cód láimhseála earráidí níos fearr más rud é, sa todhchaí, ní mór dúinn a fháil
an seoladh IP ó fhoinse éigin eile ina ionad sin.

### Treoirlínte do Láimhseáil Earráidí

Tá sé inmholta go mbeadh do chód scaoll nuair is féidir go bhféadfadh do chód
deireadh suas i droch-staid. Sa chomhthéacs seo, is éard atá i _droch-staid_ ná nuair a bhíonn roinnt toimhde ann,
Tá ráthaíocht, conradh, nó malairtí briste, mar shampla nuair a bhíonn luachanna neamhbhailí,
cuirtear luachanna contrártha, nó luachanna atá in easnamh ar aghaidh chuig do chód - móide ceann amháin nó
níos mó díobh seo a leanas:

- Is é an droch-staid rud éigin gan choinne, i gcomparáid le rud éigin go
 is dócha go dtarlóidh sé ó am go chéile, cosúil le húsáideoir sonraí a iontráil mícheart
 formáid.
- Ní mór do chód tar éis an phointe seo a bheith ag brath ar gan a bheith sa droch-staid seo,
 seachas seiceáil le haghaidh na faidhbe ag gach céim.
- Níl bealach maith ann chun an fhaisnéis seo a ionchódú sna cineálacha a úsáideann tú. Déanfaimid
 oibriú trí shampla dá bhfuil i gceist againn sna [“Stáit Ionchódaithe agus Iompar
 mar Cineálacha”][encoding]<!-- neamhaird --> alt de Chaibidil 18.

Má ghlaonn duine éigin ar do chód agus má chuireann sé/sí luachanna isteach nach bhfuil ciall leo, beidh
is fearr earráid a thabhairt ar ais más féidir leat ionas gur féidir le húsáideoir na leabharlainne cinneadh a dhéanamh ar cad é
ba mhaith leo a dhéanamh sa chás sin. Mar sin féin, i gcásanna ina bhféadfaí leanúint ar aghaidh
neamhchinnte nó díobhálach, b’fhéidir gurb é an rogha is fearr `panic!` a ghlaoch agus foláireamh a thabhairt do na
duine a úsáideann do leabharlann chun an fabht ina gcód ionas gur féidir leo é a dheisiú le linn
forbartha. Mar an gcéanna, is minic a bhíonn `panic!` oiriúnach má tá tú ag glaoch
cód seachtrach atá as do smacht agus tugann sé ar ais staid neamhbhailí go
níl aon bhealach agat le socrú.

Nuair a bhíonntear ag súil le teip, áfach, tá sé níos oiriúnaí `Result` a thabhairt ar ais
ná glaoch `panic!` a dhéanamh. I measc na samplaí tá parsálaí míchumtha a thabhairt
sonraí nó iarratas HTTP a thugann stádas ar ais a thugann le fios go bhfuil ráta bainte amach agat
teorainn. Sna cásanna seo, nuair a chuirtear `Result` ar ais, léirítear gur teip é
an fhéidearthacht a bhfuiltear ag súil leis go gcaithfidh an cód glaonna cinneadh a dhéanamh maidir le conas déileáil leis.

Nuair a dhéanann do chód oibríocht a d’fhéadfadh úsáideoir a chur i mbaol má tá
ar a dtugtar ag baint úsáide as luachanna neamhbhailí, ba chóir do chód a fhíorú go bhfuil na luachanna bailí ar dtús
agus scaoll mura bhfuil na luachanna bailí. Is ar chúiseanna sábháilteachta is mó a dhéantar é seo:
Má dhéanann tú iarracht oibriú ar shonraí neamhbhailí is féidir do chód a nochtadh d'leochaileachtaí.
Is é seo an phríomhchúis go nglaofaidh an leabharlann chaighdeánach `panic!` má dhéanann tú iarracht
rochtain chuimhne as-theorainneacha: ag iarraidh rochtain a fháil ar chuimhne nach léi
is fadhb choitianta slándála é an struchtúr sonraí reatha. Is minic a bhíonn feidhmeanna
_contracts_: ní ráthaítear a n-iompraíocht ach amháin má shásaíonn na hionchuir ar leith
riachtanais. Tá ciall ag baint le panicking nuair a sháraítear an conradh mar a
léiríonn sárú conartha fabht ar thaobh an ghlaoiteora i gcónaí, agus ní cineál é
earráid is mian leat go mbeadh ar an gcód glaonna a láimhseáil go sainráite. Go deimhin, tá
aon bhealach réasúnta chun glaoch cód a ghnóthú; an _ríomhchláraitheoirí_ glaonna ag teastáil
chun an cód a shocrú. Conarthaí le haghaidh feidhm, go háirithe nuair a bheidh sárú
ina chúis le scaoll, a mhíniú sa doiciméadú API don fheidhm.

Mar sin féin, bheadh go leor seiceálacha earráide i do chuid feidhmeanna go léir briathar
agus annoying. Go fortunately, is féidir leat córas cineál Rust a úsáid (agus mar sin an cineál
seiceáil a rinne an tiomsaitheoir) go leor de na seiceálacha a dhéanamh ar do shon. Má tá do
tá cineál áirithe ag feidhm mar pharaiméadar, is féidir leat dul ar aghaidh le do chóid
loighic a fhios agam gur chinntigh an tiomsaitheoir cheana féin go bhfuil luach bailí agat. Le haghaidh
Mar shampla, má tá cineál agat seachas `Option`, tá súil ag do chlár
bíodh _rud éigin_ agat seachas _rud ar bith_. Ní gá do chód a láimhseáil mar sin
dhá chás do na leaganacha `Some` agus `None`: ní bheidh ach cás amháin ann do
cinnte go bhfuil luach. Ní bheidh cód ag iarraidh rud ar bith a chur ar aghaidh chuig d'fheidhm
fiú tiomsú, mar sin ní gá d'fheidhm a sheiceáil don chás sin ag am rite.
Sampla eile is ea úsáid a bhaint as cineál slánuimhir gan síniú mar `u32`, rud a chinntíonn
ní bhíonn an paraiméadar diúltach riamh.

### Cineálacha Saincheaptha á gCruthú le haghaidh Bailíochtú

Glacaimis an smaoineamh córas cineál Rust a úsáid chun a chinntiú go bhfuil luach bailí againn
céim amháin eile agus féach ar chineál saincheaptha a chruthú le haghaidh bailíochtaithe. Athghairm an
cluiche buille faoi thuairim i gCaibidil 2 inar iarr ár gcód ar an úsáideoir buille faoi thuairim a thabhairt ar uimhir
idir 1 agus 100. muid ndeimhnithe riamh go raibh buille faoi thuairim an úsáideora eatarthu siúd
uimhreacha roimh é a sheiceáil i gcoinne ár n-uimhir rúnda; ní dhearnamar ach é sin a bhailíochtú
bhí an buille faoi thuairim dearfach. Sa chás seo, ní raibh na hiarmhairtí an-dona: ár
bheadh ​​an t-aschur “Ró-ard” nó “Ró-íseal” fós ceart. Ach bheadh ​​​​sé a
feabhsú úsáideach chun an t-úsáideoir a threorú i dtreo tomhais bhailí agus a bhfuil éagsúlachtaí acu
iompar nuair a dhéanann an t-úsáideoir buille faoi thuairim uimhir atá as raon i gcomparáid le nuair a bhíonn an
cineálacha úsáideoirí, mar shampla, litreacha ina ionad.

Bealach amháin chun é seo a dhéanamh ná an buille faoi thuairim a pharsáil mar `i32` in ionad ach a
`u32` chun uimhreacha a d'fhéadfadh a bheith diúltach a cheadú, agus ansin cuir seic le haghaidh an
uimhir a bheith i raon, mar sin:

<Listing file-name="src/main.rs">

```rust,ignore
{{#rustdoc_include ../../listings/ch09-error-handling/no-listing-09-guess-out-of-range/src/main.rs:here}}
```

</Listing>

Seiceálann an slonn `if` cibé an bhfuil ár luach as raon, insíonn sé don úsáideoir
faoin bhfadhb, agus glaonna `continue` chun tús a chur leis an gcéad atriall eile den lúb
agus iarr buille faoi thuairim eile. Tar éis an abairt `if`, is féidir linn dul ar aghaidh leis an
comparáidí idir `guess` agus an uimhir rúnda a fhios agam go bhfuil `guess`
idir 1 agus 100.

Mar sin féin, ní réiteach idéalach é seo: dá mba rud é go raibh sé ríthábhachtach go ndéanfaí an
níor fheidhmigh an clár ach ar luachanna idir 1 agus 100, agus bhí go leor feidhmeanna aige
leis an riachtanas seo, go mbeadh seiceáil mar seo i ngach feidhm
tedious (agus d'fhéadfadh tionchar a imirt ar fheidhmíocht).

Ina áit sin, is féidir linn cineál nua a dhéanamh agus na bailíochtaithe a chur i bhfeidhm le cruthú
sampla den chineál seachas na bailíochtaithe a athrá i ngach áit. Sin
mar sin, tá sé sábháilte d'fheidhmeanna an cineál nua a úsáid ina sínithe agus
úsáid go muiníneach as na luachanna a fhaigheann siad. Léiríonn liostú 9-13 bealach amháin chun a
Cineál `Guess` nach gcruthóidh ach sampla de `Guess` má tá an fheidhm `new`
a fhaigheann luach idir 1 agus 100.

<Listing number="9-13" caption="A `Guess` type that will only continue with values between 1 and 100">

```rust
{{#rustdoc_include ../../listings/ch09-error-handling/listing-09-13/src/lib.rs}}
```

</Listing>

Ar dtús déanaimid sainmhíniú ar struchtúr darb ainm `Guess` a bhfuil réimse darb ainm `value` sin
tá `i32` aige. Seo an áit a stórálfar an uimhir.

Ansin cuirimid feidhm ghaolmhar i bhfeidhm darb ainm `new` ar `Guess` a chruthaíonn
samplaí de luachanna `Guess`. Sainmhínítear an fheidhm `new` go bhfuil ceann aici
paraiméadar darb ainm `value` den chineál `i32` agus `Guess` a thabhairt ar ais. An cód sa
Déanann corp na feidhme `new` tástáil ar 'luach' lena chinntiú go bhfuil sé idir 1 agus 100.
Mura n-éiríonn le ‘value’ an triail seo, déanaimid glao `panic!` a chuirfidh foláireamh
an ríomhchláraitheoir atá ag scríobh an cód glaonna go bhfuil fabht a theastaíonn uathu
a shocrú, mar go gcruthófaí `Guess` le `value` lasmuigh den raon seo
an conradh a bhfuil `Guess::new` ag brath air a shárú. Na coinníollacha ina
Seans gur cheart `Guess::new` a phlé ina API poiblí
doiciméadú; clúdóimid coinbhinsiúin doiciméadaithe a léiríonn an fhéidearthacht
de `panic!` sna doiciméid API a chruthaíonn tú i gCaibidil 14. Más rud é
éiríonn le `value` an triail, cruthaímid `Guess` nua lena shraith réimse `value`
chuig an bparaiméadar `value` agus seol ar ais an `Guess`.

Ansin, cuirimid modh darb ainm `value` i bhfeidhm a fhaigheann `self` ar iasacht, nach bhfuil aon cheann aige
paraiméadair eile, agus tuairisceáin `i32`. Uaireanta tugtar modh den chineál seo
a _getter_ toisc go bhfuil sé mar chuspóir aige roinnt sonraí a fháil óna réimsí agus iad a sheoladh ar ais
é. Tá an modh poiblí seo riachtanach toisc go bhfuil réimse `value` an `Guess`
Tá struchtúr príobháideach. Tá sé tábhachtach go mbeadh an réimse `value` príobháideach mar sin cód
ag baint úsáide as an struchtúr `Guess` ní cheadaítear `value` a shocrú go díreach: cód lasmuigh
caithfidh an modúl an fheidhm `Guess::new` a úsáid chun sampla de
`Guess`, ag cinntiú mar sin nach bhfuil aon bhealach le `Guess` `value` a bheith aige sin
nach bhfuil seiceáilte ag na coinníollacha san fheidhm `Guess::new`.

D'fhéadfadh feidhm a bhfuil paraiméadar aici nó nach dtugann ach uimhreacha idir 1 agus 100 ar ais
ansin dearbhaigh ina shíniú go nglacann sé nó go dtugann sé ar ais `Guess` seachas
`i32` agus ní bheadh ​​air aon seiceálacha breise a dhéanamh ina chorp.

## Achoimre

Tá gnéithe láimhseála earráidí Rust deartha chun cabhrú leat cód níos daingne a scríobh.
Léiríonn an macra `panic!` go bhfuil do chlár i riocht nach féidir leis a láimhseáil agus
ligeann duit insint don phróiseas chun stop a chur in ionad iarracht a dhéanamh dul ar aghaidh le neamhbhailí nó
luachanna míchearta. Úsáideann an enum `Result` córas cineáil Rust chun é sin a chur in iúl
seans go dteipfidh ar oibríochtaí ar bhealach a d'fhéadfadh do chód a ghnóthú. Is féidir leat úsáid a bhaint as
`Result` chun cód a ghlaonn do chód a insint go gcaithfidh sé acmhainneacht a láimhseáil
rath nó teip chomh maith. Ag baint úsáide as `panic!` agus `Result` sa chuí
Déanfaidh cásanna do chód níos iontaofa i bhfianaise fadhbanna dosheachanta.

Anois go bhfuil bealaí úsáideacha feicthe agat a n-úsáideann an leabharlann chaighdeánach generics leo
sna huimhreacha `Option` agus `Result`, labhróimid faoin gcaoi a n-oibríonn generics agus conas a oibríonn tú
Is féidir iad a úsáid i do chód.

[encoding]: ch18-03-oo-design-patterns.html#encoding-states-and-behavior-as-types