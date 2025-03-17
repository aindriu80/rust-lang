## Tagairtí a Bhailíochtú le Saoil

Is cineál cineálach eile iad saolré atá in úsáid againn cheana féin. Ina ionad sin
ná a chinntiú go bhfuil an t-iompar a theastaíonn uainn ag cineál, cinntíonn an saolré sin
tá tagairtí bailí chomh fada agus a theastaíonn uainn iad a bheith.

Sonraí amháin nár phléigh muid sna [“Tagairtí agus
Iasachtaí a fháil”][references-and-borrowing]<!-- neamhaird a dhéanamh ar --> tá an roinn i gCaibidil 4
go bhfuil _lifetime_ ag gach tagairt i Rust, agus sin an raon feidhme dó
tá an tagairt sin bailí. An chuid is mó den am, bíonn saolta intuigthe agus tátal,
díreach mar an chuid is mó den am, tá tátal a bhaint as cineálacha. Ní mór dúinn cineálacha a anótáil amháin
nuair is féidir cineálacha iolracha. Ar an mbealach céanna, ní mór dúinn saolréanna a anótáil
nuair a d’fhéadfaí saolré na dtagairtí a cheangal ar roinnt bealaí éagsúla. Rust
éilíonn orainn na caidrimh a anótáil ag baint úsáide as paraiméadair chineálacha saoil chun
a chinntiú go mbeidh na tagairtí iarbhír a úsáidtear ag am rite bailí cinnte.

Ní coincheap é saolréanna anótála atá ag formhór na dteangacha ríomhchlárúcháin eile, mar sin de
beidh sé seo ag dul a bhraitheann neamhchoitianta. Cé nach gclúdóidh muid saolréanna ina gcuid
go hiomlán sa chaibidil seo, pléifimid bealaí coitianta a dtiocfadh leat teacht orthu
comhréir feadh an tsaoil ionas gur féidir leat a bheith compordach leis an gcoincheap.

### Tagairtí Dangling le Saoil a Chosc

Is í an phríomhaidhm le saolréanna ná _dangling references_ a chosc, a chuireann faoi deara a
clár chun sonraí a thagairt seachas na sonraí a bhfuil sé beartaithe tagairt a dhéanamh dóibh.
Smaoinigh ar an gclár i Liostú 10-16, a bhfuil raon feidhme seachtrach agus taobh istigh aige
scóip.

<Listing number="10-16" caption="An attempt to use a reference whose value has gone out of scope">

```rust,ignore,does_not_compile
{{#rustdoc_include ../../listings/ch10-generic-types-traits-and-lifetimes/listing-10-16/src/main.rs}}
```

</Listing>

> Nóta: Dearbhaíonn na samplaí i Liostú 10-16, 10-17, agus 10-23 athróga
> gan luach tosaigh a thabhairt dóibh, mar sin tá an t-ainm athróg ann ar an taobh amuigh
> scóip. Ar an gcéad amharc, d’fhéadfadh sé a bheith cosúil go bhfuil sé seo ag teacht salach ar a bhfuil ag Rust
> gan luachanna null. Mar sin féin, má dhéanaimid iarracht athróg a úsáid sula dtabharfar luach dó,
> gheobhaidh muid earráid ama tiomsaithe, rud a thaispeánann nach gceadaíonn Rust go deimhin
> luachanna null.

Dearbhaíonn an raon feidhme seachtrach athróg darb ainm `r` gan aon luach tosaigh, agus an
dearbhaíonn raon feidhme inmheánach athróg darb ainm `x` le luach tosaigh `5`. Laistigh
an scóip istigh, déanaimid iarracht luach `r` a shocrú mar thagairt do `x`. Ansin
críochnaíonn an scóip inmheánach, agus déanaimid iarracht an luach a phriontáil in `r`. Ní dhéanfaidh an cód seo
tiomsaigh toisc go bhfuil an luach a bhfuil `r` ag tagairt dó imithe as an scóip roimhe seo
déanaimid iarracht é a úsáid. Seo an teachtaireacht earráide:

```console
{{#include ../../listings/ch10-generic-types-traits-and-lifetimes/listing-10-16/output.txt}}
```

Deir an teachtaireacht earráide nach bhfuil an athróg `x` "beo fada go leor." Tá an
Is é an chúis go mbeidh `x` as an raon feidhme nuair a chríochnaíonn an raon feidhme istigh ar líne 7.
Ach tá `r` fós bailí don scóip sheachtrach; toisc go bhfuil a raon feidhme níos mó, deirimid
go mairfeadh sé "níos faide." Dá gceadódh Rust don chód seo oibriú, bheadh ​​`r`
cuimhne thagartha a bhí dealraitheach nuair a chuaigh `x` as raon feidhme, agus
ní bheadh ​​aon rud a rinneamar iarracht a dhéanamh le `r` ag obair i gceart. Mar sin, conas a dhéanann Rust
a chinneadh go bhfuil an cód seo neamhbhailí? Úsáideann sé seiceálaí iasachtaí.

### An Seiceálaí Iasachta

Tá _borrow checker_  ag an tiomsaitheoir Rust a dhéanann comparáid idir scóip chun a chinneadh
cibé an bhfuil gach iasacht bailí. Léiríonn Liostú 10-17 an cód céanna le Liostú
10-16 ach le nótaí a thaispeánann saolréanna na n-athróg.

<Listing number="10-17" caption="Annotations of the lifetimes of `r` and `x`, named `'a` and `'b`, respectively">

```rust,ignore,does_not_compile
{{#rustdoc_include ../../listings/ch10-generic-types-traits-and-lifetimes/listing-10-17/src/main.rs}}
```

</Listing>

Anseo, rinneamar saolré `r` a anótáil le `'a` agus saolré `x`
le `'b`. Mar a fheiceann tú, tá an bloc `' b` istigh i bhfad níos lú ná an bloc seachtrach
`'a` bloc saoil. Ag am tiomsaithe, déanann Rust comparáid idir méid an dá cheann
saoil agus feictear go bhfuil saolré `'a` ag `r` ach go dtagraíonn sé don chuimhne
le saolré `'b`. Diúltaítear don chlár toisc go bhfuil `'b` níos giorra ná
`'a`: ní mhaireann ábhar na tagartha chomh fada leis an tagairt.

Le liostú 10-18 socraítear an cód ionas nach mbeidh tagairt dhochrach aige agus é
thiomsaíonn gan aon earráidí.

<Listing number="10-18" caption="A valid reference because the data has a longer lifetime than the reference">

```rust
{{#rustdoc_include ../../listings/ch10-generic-types-traits-and-lifetimes/listing-10-18/src/main.rs}}
```

</Listing>

Anseo, tá an saolré `' b` ag `x`, atá sa chás seo níos mó ná `'a`. seo
ciallaíonn `r` is féidir tagairt a dhéanamh do `x` mar tá a fhios ag Rust go bhfuil an tagairt in `r` will
bheith bailí i gcónaí agus `x` bailí.

Anois go bhfuil a fhios agat cad iad saolré na dtagairtí agus conas a dhéanann Rust anailís
saolréanna chun a chinntiú go mbeidh teistiméireachtaí bailí i gcónaí, déanaimis iniúchadh cineálach
saolré paraiméadair agus luachanna toraidh i gcomhthéacs feidhmeanna.

### Saoil Cineálach i bhFeidhmeanna

Scríobhfaimid feidhm a thabharfaidh ar ais an ceann is faide de dhá shlisne téad. seo
Beidh feidhm a ghlacadh dhá shlisne teaghrán agus ar ais slice amháin teaghrán. Tar éis
tá an fheidhm `longest` curtha i bhfeidhm againn, ba cheart don chód i Liostú 10-19
cló `The longest string is abcd`.

<Listing number="10-19" file-name="src/main.rs" caption="A `main` function that calls the `longest` function to find the longer of two string slices">

```rust,ignore
{{#rustdoc_include ../../listings/ch10-generic-types-traits-and-lifetimes/listing-10-19/src/main.rs}}
```

</Listing>

Tabhair faoi deara gur mian linn an fheidhm a ghlacadh slisní teaghrán, a bhfuil tagairtí,
seachas teaghráin, mar nílimid ag iarraidh an fheidhm `longest` a ghlacadh
úinéireacht a paraiméadair. Déan tagairt don [“Slices Teaghrán mar
Paraiméadair”][string-slices-as-parameters]<!-- neamhaird --> an roinn i gCaibidil 4
le tuilleadh plé a fháil faoin bhfáth gurb iad na paraiméadair a úsáidimid i Liosta 10-19 ná na
cinn atá uainn.

Má dhéanaimid iarracht an fheidhm `longest` a chur i bhfeidhm mar a thaispeántar i Liostú 10-20, é
ní thiomsóidh.

<Listing number="10-20" file-name="src/main.rs" caption="An implementation of the `longest` function that returns the longer of two string slices but does not yet compile">

```rust,ignore,does_not_compile
{{#rustdoc_include ../../listings/ch10-generic-types-traits-and-lifetimes/listing-10-20/src/main.rs:here}}
```

</Listing>

Ina áit sin, faighimid an earráid seo a leanas a labhraíonn faoi shaolréanna:

```console
{{#include ../../listings/ch10-generic-types-traits-and-lifetimes/listing-10-20/output.txt}}
```

Léiríonn an téacs cabhrach go dteastaíonn paraiméadar cineálach saoil don chineál fillte
air mar ní féidir le Rust a rá an mbaineann an tagairt atá á thabhairt ar ais
`x` nó `y`. I ndáiríre, níl a fhios againn ach an oiread, mar gheall ar an `if` bloc sa chorp
den fheidhm seo filleann tagairt do `x` agus filleann an bloc `else` a
tagairt do `y`!

Agus an fheidhm seo á sainiú againn, níl a fhios againn na luachanna nithiúla a bheidh
a chur ar aghaidh isteach sa fheidhm seo, mar sin níl a fhios againn cé acu an cás `if` nó an
cuirfear cás `else` i gcrích. Níl a fhios againn freisin ar shaolréanna nithiúla an
tagairtí a sheolfar isteach, mar sin ní féidir linn breathnú ar na scóip mar a rinneamar
Liostaí 10-17 agus 10-18 chun a chinneadh an ndéanfaidh an tagairt a chuirimid ar ais
bheith bailí i gcónaí. Ní féidir leis an seiceálaí iasachtaí é seo a chinneadh ach an oiread, mar gheall air
Ní fios conas a bhaineann saolré `x` agus `y` le saolré an
luach aischuir. Chun an earráid seo a réiteach, cuirfimid paraiméadair chineálacha saoil leis sin
an gaol idir na tagairtí a shainiú ionas gur féidir leis an seiceálaí iasachtaí
a anailís a dhéanamh.

### Comhréir Nótaí Saoil

Ní athraíonn nótaí saoil cé chomh fada agus a mhaireann aon cheann de na tagairtí. Ina ionad sin,
déanann siad cur síos ar na gaolmhaireachtaí a bhaineann le saolré na tagairtí iolracha do gach ceann acu
eile gan cur isteach ar an saolré. Díreach mar is féidir le feidhmeanna glacadh le haon chineál
nuair a shonraíonn an síniú paraiméadar cineál cineálach, is féidir le feidhmeanna glacadh leis
tagairtí le haon saolré trí pharaiméadar cineálach saoil a shonrú.

Tá comhréir beagán neamhghnách ag nótaí saoil: ainmneacha an tsaoil
ní mór do pharaiméadair tosú le haspail (`'`) agus de ghnáth is cás íochtair iad ar fad
agus an-ghearr, cosúil le cineálacha cineálacha. Úsáideann formhór na ndaoine an t-ainm `'a` ar an gcéad dul síos
nóta feadh an tsaoil. Cuirimid nótaí paraiméadar an tsaoil i ndiaidh `&` a
tagairt, ag baint úsáide as spás chun an nóta a scaradh ó chineál na tagartha.

Seo roinnt samplaí: tagairt do `i32` gan paraiméadar saoil, a
tagairt do `i32` a bhfuil paraiméadar saoil darb ainm `'a` aige, agus mutable
tagairt do `i32` a bhfuil an saolré `'a` aige freisin.

```rust,ignore
&i32        // tagairt
&'a i32     // tagairt le saolré follasach
&'a mut i32 // tagairt mutable le saolré follasach
```

Níl mórán brí ag baint le nóta saoil amháin ann féin toisc go bhfuil an
Tá anótálacha i gceist a insint do Rust conas paraiméadair chineálacha feadh an tsaoil il
baineann tagairtí lena chéile. Déanaimis scrúdú ar conas na nótaí saoil
a bhaineann le chéile i gcomhthéacs na feidhme `longest`.

### Anótálacha Saoil i Sínithe Feidhme

Chun nótaí saoil a úsáid i sínithe feidhm, ní mór dúinn an
paraiméadair cineálach _lifetime_ laistigh de lúibíní uillinne idir ainm na feidhme
agus an liosta paraiméadar, díreach mar a rinneamar le paraiméadair cineálach _type_.

Ba mhaith linn go gcuirfeadh an síniú an srian seo a leanas in iúl: an t-aischur
beidh an tagairt bailí fad is atá an dá pharaiméadar bailí. Is é seo an
an gaol idir saolré na bparaiméadar agus an luach toraidh. Déanfaimid
ainmnigh an saolré `'a` agus ansin cuir le gach tagairt é, mar a thaispeántar sa Liostú
10-21.

<Listing number="10-21" file-name="src/main.rs" caption="The `longest` function definition specifying that all the references in the signature must have the same lifetime `'a`">

```rust
{{#rustdoc_include ../../listings/ch10-generic-types-traits-and-lifetimes/listing-10-21/src/main.rs:here}}
```

</Listing>

Ba cheart don chód seo an toradh a theastaíonn uainn a thiomsú agus a tháirgeadh nuair a úsáidimid é leis an
`príomhfheidhm' i Liostú 10-19.

Insíonn síniú na feidhme do Rust anois go bhfuil `'a`, an fheidhm ar feadh an tsaoil
Bíonn dhá pharaiméadar, agus is slisní teaghrán iad araon a mhaireann ar a laghad mar
ar feadh an tsaoil `'a`. Insíonn an síniú feidhm freisin Rust go bhfuil an teaghrán
Beidh slice ar ais ón bhfeidhm beo ar a laghad chomh fada agus a saolré `'a`.
Go praiticiúil, ciallaíonn sé go bhfuil an saolré an tagairt ar ais ag an
tá an fheidhm `longest` mar an gcéanna leis an gceann is lú de shaolréanna na luachanna
dá dtagraítear ag na hargóintí feidhm. Is iad na caidrimh seo a theastaíonn uainn
Rust a úsáid agus an cód seo á anailísiú.

Cuimhnigh, nuair a shonraímid na paraiméadair saoil sa síniú feidhme seo,
níl muid ag athrú saolré aon luachanna a chuirtear isteach nó a thugtar ar ais. Ina ionad sin,
táimid ag sonrú gur cheart don seiceálaí iasachtaí diúltú d’aon luachanna nach ndéanann
cloí leis na srianta seo. Tabhair faoi deara nach gá an fheidhm `longest`
fios go cruinn cá fhad a mhairfidh `x` agus `y`, ach gur féidir le scóip éigin a bheith
in ionad `'a` a shásóidh an síniú seo.

Nuair a bhíonn saolréanna i bhfeidhmeanna á anótáil, téann na nótaí isteach san fheidhm
síniú, nach bhfuil sa chomhlacht feidhme. Is cuid de na nótaí saoil
conradh na feidhme, mórán cosúil leis na cineálacha sa síniú. Ag
go bhfuil sínithe feidhm ciallaíonn an conradh saolré an anailís ar an meirge
Is féidir le tiomsaitheoir a bheith níos simplí. Má tá fadhb ann leis an gcaoi a bhfuil feidhm
anótáilte nó an bealach ar a dtugtar é, is féidir leis an earráidí tiomsaitheoir pointe go dtí an chuid de
ár gcód agus na srianta níos cruinne. Más rud é, ina ionad sin, an tiomsaitheoir Rust
rinneamar níos mó tátail faoi na caidrimh a bhí i gceist againn ar feadh an tsaoil
le bheith, b'fhéidir nach mbeadh an tiomsaitheoir in ann ach go leor céimeanna a úsáid chun ár gcód a úsáid
ar shiúl ó chúis na faidhbe.

Nuair a thugaimid tagairtí nithiúla don `longest`, is é sin an saolré nithiúil
in ionad `'a` is ea an chuid de scóip `x` a fhorluíonn leis an
scóip `y`. I bhfocail eile, beidh an saolré cineálach `'a` a fháil ar an nithiúla
saolré atá comhionann leis an gceann is lú de shaolré `x` agus `y`. Toisc
rinneamar an tagairt ar ais a anótáil leis an bparaiméadar saoil céanna `'a`,
beidh an tagairt ar ais bailí freisin ar feadh an fhad is lú de na
saolré `x` agus `y`.

Breathnaímid ar an gcaoi a gcuireann nótaí saoil srian ar an bhfeidhm `longest` trí
tagairtí a bhfuil saolréanna coincréiteacha éagsúla acu a rith. Tá liosta 10-22
sampla simplí.

<Listing number="10-22" file-name="src/main.rs" caption="Using the `longest` function with references to `String` values that have different concrete lifetimes">

```rust
{{#rustdoc_include ../../listings/ch10-generic-types-traits-and-lifetimes/listing-10-22/src/main.rs:here}}
```

</Listing>

Sa sampla seo, tá `string1` bailí go dtí deireadh an scóip sheachtraigh, `string2`
bailí go dtí deireadh an scóip istigh, agus déanann `result` tagairt do rud éigin
atá bailí go dtí deireadh an raon feidhme laistigh. Rith an cód seo agus feicfidh tú
go gceadaíonn an seiceálaí iasachtaí; tiomsóidh agus priontálfaidh sé `The longest string
is long string is long`.

Ansin, déanaimis iarracht sampla a thaispeánann go bhfuil saolré na tagartha i
caithfidh gurb é `result` saolré níos lú an dá argóint. Bogfaimid an
dearbhú na hathróige `result` lasmuigh den scóip inmheánach ach fág an
sannadh an luacha don athróg `result` taobh istigh den scóip le
`string2`. Ansin bogfaimid an `println!` a úsáideann `result` chuig taobh amuigh de
raon feidhme istigh, tar éis an raon feidhme istigh dar críoch. Beidh an cód i Liostú 10-23
gan tiomsú.

<Listing number="10-23" file-name="src/main.rs" caption="Attempting to use `result` after `string2` has gone out of scope">

```rust,ignore,does_not_compile
{{#rustdoc_include ../../listings/ch10-generic-types-traits-and-lifetimes/listing-10-23/src/main.rs:here}}
```

</Listing>

Nuair a dhéanaimid iarracht an cód seo a thiomsú, faighimid an earráid seo:

```console
{{#include ../../listings/ch10-generic-types-traits-and-lifetimes/listing-10-23/output.txt}}
```

Léiríonn an earráid le haghaidh `result` a bheith bailí don ráiteas `println!`,
Ba ghá go mbeadh `string2` bailí go dtí deireadh an scóip sheachtraigh. Tá a fhios ag meirge
seo toisc gur thugamar anótáil ar shaolré na bparaiméadar feidhme agus ar ais
luachanna ag baint úsáide as an bparaiméadar saoil céanna `'a`.

Mar dhaoine, is féidir linn breathnú ar an gcód seo agus a fheiceáil go bhfuil `string1` níos faide ná
`string2`, agus mar sin, beidh tagairt do `string1` i `result`.
Toisc nach bhfuil `string1` imithe as an scóip go fóill, déanfar tagairt do `string1`
fós bailí don ráiteas `println!`. Mar sin féin, ní féidir leis an tiomsaitheoir a fheiceáil
go bhfuil an tagairt bailí sa chás seo. Táimid tar éis a dúirt Rust go bhfuil an saolré
tá an tagairt a thugann an fheidhm `longest` ar ais mar an gcéanna leis an gceann is lú de
saolré na dtagairtí a cuireadh isteach. Dá bhrí sin, an seiceálaí iasachtaí
dícheadaítear an cód i Liostú 10-23 mar go bhféadfadh tagairt neamhbhailí a bheith aige.

Déan iarracht níos mó turgnaimh a dhearadh a athraíonn luachanna agus saolré an
tagairtí a cuireadh ar aghaidh chuig an bhfeidhm `longest` agus conas a cuireadh an tagairt ar ais
úsáidtear. Déan hipitéisí faoi cé acu an rachaidh nó nach rachaidh do thurgnaimh thar an
seiceálaí iasachtaí sula ndéanann tú tiomsú; seiceáil ansin féachaint an bhfuil an ceart agat!

### Smaointeoireacht i dTéarmaí Saoil

Braitheann an bealach inar gá duit paraiméadair an tsaoil a shonrú ar an méid atá agat
feidhm ag déanamh. Mar shampla, má d’athraigh muid cur i bhfeidhm an
feidhm `longest` chun an chéad pharaiméadar a thabhairt ar ais i gcónaí seachas an ceann is faide
slisne teaghrán, ní bheadh ​​​​gá dúinn saolré a shonrú ar an bparaiméadar `y`. Tá an
tiomsóidh an cód seo a leanas:

<Listing file-name="src/main.rs">

```rust
{{#rustdoc_include ../../listings/ch10-generic-types-traits-and-lifetimes/no-listing-08-only-one-reference-with-lifetime/src/main.rs:here}}
```

</Listing>

Tá paraiméadar saoil `'a` sonraithe againn don pharaiméadar `x` agus don tuairisceán
cineál, ach ní le haghaidh an pharaiméadar `y`, toisc nach bhfuil an saolré `y` acu
gaol ar bith le saolré `x` nó luach an aischuir.

Nuair a bheidh tagairt ó fheidhm á filleadh ar ais, is é an paraiméadar saoil don
ní mór an cineál fillte a mheaitseáil leis an bparaiméadar saoil do cheann de na paraiméadair. Más rud é
tagraíonn an tagairt ar ais _not_ do cheann de na paraiméadair, caithfidh sé tagairt a dhéanamh
go luach a chruthaítear laistigh den fheidhm seo. Mar sin féin, bheadh ​​​​sé seo ina dangling
tagairt mar go rachaidh an luach as raon feidhme ag deireadh na feidhme.
Smaoinigh ar an iarracht seo an fheidhm `longest` nach ndéanfaidh
tiomsaigh:

<Listing file-name="src/main.rs">

```rust,ignore,does_not_compile
{{#rustdoc_include ../../listings/ch10-generic-types-traits-and-lifetimes/no-listing-09-unrelated-lifetime/src/main.rs:here}}
```

</Listing>

Anseo, cé go bhfuil paraiméadar saoil `'a` sonraithe againn don tuairisceán
cineál, beidh an cur i bhfeidhm theipeann a thiomsú mar gheall ar an luach ar ais
níl baint ag an saolré le saolré na bparaiméadar ar chor ar bith. Seo é an
teachtaireacht earráide a fhaighimid:

```console
{{#include ../../listings/ch10-generic-types-traits-and-lifetimes/no-listing-09-unrelated-lifetime/output.txt}}
```

Is í an fhadhb atá ann go dtéann `result` as an scóip agus go ndéantar é a ghlanadh ag an deireadh
den fheidhm `longest`. Táimid ag iarraidh tagairt a thabhairt ar ais do `result` freisin
ón bhfeidhm. Níl aon bhealach is féidir linn paraiméadair shaolré a shonrú go
d’athródh sé an tagairt dhochrach, agus ní ligfidh Rust dúinn cliseadh a chruthú
tagairt. Sa chás seo, is é an socrú is fearr ná cineál sonraí faoi úinéireacht a thabhairt ar ais
seachas tagairt agus mar sin tá an fheidhm ghlao freagrach as
ag glanadh suas an luach.

Ar deireadh thiar, baineann comhréir saoil le saolréanna éagsúla a nascadh
paraiméadair agus luachanna aischuir feidhmeanna. Nuair a bheidh siad ceangailte, tá Rust
dóthain faisnéise chun oibríochtaí cuimhne-sábháilte a cheadú agus oibríochtaí a dhícheadú
a chruthódh leideanna buailte nó a sháródh sábháilteacht na cuimhne ar shlí eile.

### Nótaí Saoil i Sainmhínithe Struchtúr

Go dtí seo, na struchtúir atá sainmhínithe againn go léir faoi úinéireacht sealúchais. Is féidir linn struchtúir a shainiú
chun tagairtí a choinneáil, ach sa chás sin bheadh ​​orainn nóta saoil a chur leis
ar gach tagairt i sainmhíniú an struchtúir. I liostú 10-24 tá struchtúr ainmnithe
`ImportantExcerpt` a choinníonn slisne teaghrán.

<Listing number="10-24" file-name="src/main.rs" caption="A struct that holds a reference, requiring a lifetime annotation">

```rust
{{#rustdoc_include ../../listings/ch10-generic-types-traits-and-lifetimes/listing-10-24/src/main.rs}}
```

</Listing>

Tá an `part` réimse singil ag an struchtúr seo a choinníonn slisne teaghrán, is é sin a
tagairt. Mar is amhlaidh le cineálacha sonraí cineálach, dearbhaímid ainm an chineál cineálach
paraiméadar feadh an tsaoil taobh istigh lúibíní uillinn tar éis ainm an struct ionas gur féidir linn
úsáid a bhaint as an paraiméadar saoil i gcorp an tsainmhínithe struct. seo
Ciallaíonn anótáil nach féidir le `ImportantExcerpt` a bheith níos faide ná an tagairt
coinníonn sé ina réimse `part`.

Cruthaíonn an fheidhm `main` anseo sampla den struchtúr `ImportantExcerpt`
a choinníonn tagairt don chéad abairt den `String` atá ar úinéireacht ag an
athróg `novel`. Tá na sonraí san `novel` ann roimh an `ImportantExcerpt`
cruthaítear shampla. Ina theannta sin, ní théann `novel` as raon feidhme go dtí ina dhiaidh sin
téann an `ImportantExcerpt` amach as an scóip, mar sin tá an tagairt sa
Tá sampla `ImportantExcerpt` bailí.

### Elision ar feadh an tSaoil

D'fhoghlaim tú go bhfuil saolré ag gach tagairt agus gur gá duit a shonrú
paraiméadair shaolré le haghaidh feidhmeanna nó struchtúir a úsáideann tagairtí. Mar sin féin, táimid
Bhí feidhm aige i Liostú 4-9, a thaispeántar arís i Liostú 10-25, a cuireadh le chéile
gan nótaí saoil.

<Listing number="10-25" file-name="src/lib.rs" caption="A function we defined in Listing 4-9 that compiled without lifetime annotations, even though the parameter and return type are references">

```rust
{{#rustdoc_include ../../listings/ch10-generic-types-traits-and-lifetimes/listing-10-25/src/main.rs:here}}
```

</Listing>

Is cúis stairiúil an chúis a thiomsaíonn an fheidhm seo gan nótaí saoil:
i leaganacha luatha (réamh-1.0) de Rust, ní bheadh ​​an cód seo tiomsaithe toisc
bhí saolré follasach ag teastáil ó gach tagairt. Ag an am sin, an fheidhm
bheadh ​​síniú scríofa mar seo:

```rust,ignore
fn first_word<'a>(s: &'a str) -> &'a str {
```

Tar éis a lán de chód Rust a scríobh, fuair an fhoireann Rust go ríomhchláraitheoirí Rust
go raibh na nótaí saoil céanna á gcur isteach arís agus arís eile go háirithe
cásanna. Bhí na cásanna seo intuartha agus lean siad roinnt cinntitheach
patrúin. Rinne na forbróirí na patrúin seo a ríomhchlárú isteach i gcód an tiomsaitheora amhlaidh
d’fhéadfadh an seiceálaí iasachtaí tátal a bhaint as na saolréanna sna cásanna seo agus ní bheadh
nótaí soiléire de dhíth.

Tá an píosa seo de stair Rust ábhartha mar is féidir go bhfuil níos mó
tiocfaidh patrúin cinntitheacha chun cinn agus cuirfear leis an tiomsaitheoir iad. Sa todhchaí,
d'fhéadfadh go mbeadh níos lú nótaí saoil de dhíth.

Tugtar an
_rialacha éalaithe saoil_. Ní rialacha iad seo atá le leanúint ag ríomhchláraitheoirí; siad
sraith cásanna ar leith a bhreithneoidh an tiomsaitheoir, agus más rud é do chód
oiriúnach do na cásanna seo, ní gá duit na saolréanna a scríobh go sainráite.

Ní thugann na rialacha díothaithe tátal iomlán. Má tá débhríocht fós mar
cad iad na saolréanna atá ag na tagairtí tar éis do Rust na rialacha a chur i bhfeidhm, an
ní dhéanfaidh an tiomsaitheoir buille faoi thuairim cén saolré ba cheart a bheith sna tagairtí atá fágtha.
In ionad buille faoi thuairim a thabhairt, tabharfaidh an tiomsaitheoir earráid duit is féidir leat a réiteach
trí na nótaí saoil a chur leis.

Tugtar _ionchur saoil_ ar fhad saoil ar pharaiméadair feidhme nó modha, agus
tugtar _saolréanna aschuir_ ar shaolréanna ar luachanna aischuir.

Úsáideann an tiomsaitheoir trí riail chun saolré na dtagairtí a dhéanamh amach
nuair nach bhfuil nótaí soiléire ann. Baineann an chéad riail le hionchur
saolréanna, agus tá feidhm ag an dara agus an tríú riail maidir le saolréanna aschuir. Má tá an
Faigheann tiomsaitheoir go dtí deireadh na dtrí rialacha agus tá tagairtí do
rud nach féidir leis saolréanna a dhéanamh amach, stopfaidh an tiomsaitheoir le hearráid.
Baineann na rialacha seo le sainmhínithe `fn` chomh maith le bloic `impl`.

Is é an chéad riail go sannann an tiomsaitheoir paraiméadar saoil do gach ceann acu
paraiméadar atá ina thagairt. I bhfocail eile, feidhm le paraiméadar amháin
faigheann sé paraiméadar saoil amháin: `fn foo<'a>(x: &'a i32)`; feidhm le dhá
faigheann paraiméadair dhá pharaiméadair saoil ar leith: `fn foo<'a, 'b>(x: &'a i32,
y: &'b i32)`; agus mar sin de.

Is é an dara riail, má tá go díreach paraiméadar saoil ionchuir amháin, go
sanntar an saolré do gach paraiméadair shaolré aschuir: `fn foo<'a>(x: &'a i32)
-> &'a i32`.

Is é an tríú riail, má tá paraiméadair shaolré ionchuir iolracha, ach
duine acu is `&self` nó `&mut self` toisc gur modh é seo, saolré
sanntar `self` ar gach paraiméadair shaolré aschuir. Déanann an tríú riail seo
modhanna i bhfad níos deise a léamh agus a scríobh mar go bhfuil níos lú siombailí riachtanach.

Ligean orainn gur muid an tiomsaitheoir. Cuirfimid na rialacha seo i bhfeidhm chun na
saolré na dtagairtí i síniú na feidhme `first_word` i
Liostáil 10-25. Tosaíonn an síniú gan aon saolréanna a bhaineann leis an
tagairtí:

```rust,ignore
fn first_word(s: &str) -> &str {
```

Ansin tá feidhm ag an tiomsaitheoir an chéad riail, a shonraíonn go bhfuil gach paraiméadar
faigheann a shaolré féin. Tabharfaimid `'a` air mar is gnách, mar sin anois tá an síniú
seo:

```rust,ignore
fn first_word<'a>(s: &'a str) -> &str {
```

Tá feidhm ag an dara riail toisc go bhfuil go díreach saolré ionchuir amháin. An dara ceann
sonraíonn an riail go sanntar saolré an pharaiméadar ionchuir amháin
saolré an aschuir, mar sin is é an síniú anois:

```rust,ignore
fn first_word<'a>(s: &'a str) -> &'a str {
```

Anois tá saolréanna ag na tagairtí go léir sa síniú feidhme seo, agus tá an
is féidir leis an tiomsaitheoir leanúint lena anailís gan gá don ríomhchláraitheoir anótáil a dhéanamh
na saolréanna sa síniú feidhme seo.

Breathnaímid ar shampla eile, an uair seo ag baint úsáide as an bhfeidhm `longest` a raibh
gan aon pharaiméadair saoil nuair a thosaigh muid ag obair leis i Liostú 10-20:

```rust,ignore
fn longest(x: &str, y: &str) -> &str {
```

Cuirfimid an chéad riail i bhfeidhm: faigheann gach paraiméadar a shaolré féin. An uair seo táimid
bíodh dhá pharaiméadair againn seachas ceann amháin, agus mar sin tá dhá shaolré againn:

```rust,ignore
fn longest<'a, 'b>(x: &'a str, y: &'b str) -> &str {
```

Is féidir leat a fheiceáil nach bhfuil feidhm ag an dara riail toisc go bhfuil níos mó ná ceann amháin ann
shaolré ionchuir. Níl feidhm ag an tríú riail ach an oiread, mar is é an `longest` ná a
feidhm seachas modh, mar sin níl aon cheann de na paraiméadair `self`. Tar éis
ag obair trí na trí rialacha, níl a fhios againn go fóill cad é an toradh
Is é saolré an chineáil. Sin é an fáth go bhfuaireamar earráid agus muid ag iarraidh an cód a thiomsú isteach
Liostú 10-20: d’oibrigh an tiomsaitheoir trí na rialacha éalaithe ar feadh an tsaoil ach fós féin
níorbh fhéidir fad saoil na dtagairtí sa síniú a dhéanamh amach.

Toisc nach mbaineann an tríú riail ach le sínithe modhanna, féachfaimid
saolréanna sa chomhthéacs sin taobh le taobh féachaint cén fáth a gciallaíonn an tríú riail nach gá dúinn
anótáil saolréanna i sínithe modha go minic.

### Anótálacha Saoil i Sainmhínithe Modh

Nuair a chuirimid modhanna i bhfeidhm ar struchtúr le saolréanna, bainimid úsáid as an chomhréir chéanna agus atá
paraiméadair chineálacha a thaispeántar i Liosta 10-11. I gcás ina ndearbhaímid agus
Braitheann úsáid paraiméadair an tsaoil ar cibé an bhfuil baint acu leis an struchtúr
réimsí nó paraiméadair an mhodha agus na luachanna tuairisceáin.

Ní mór ainmneacha saoil do réimsí struchtúir a dhearbhú i gcónaí tar éis an `impl`
eochairfhocal agus ansin úsáidtear é tar éis ainm an struchtúir toisc go bhfuil na saolréanna sin páirteach
den chineál struchtúir.

I sínithe modha taobh istigh den bhloc `impl`, d'fhéadfadh tagairtí a bheith ceangailte leis an
saolré na dtagairtí i réimsí an struchtúir, nó d'fhéadfadh siad a bheith neamhspleách. I
Ina theannta sin, is minic a fhágann rialacha éalaithe an tsaoil é ionas go mbeidh nótaí saoil ann
nach bhfuil riachtanach i sínithe modh. Breathnaímid ar roinnt samplaí ag baint úsáide as an
struchtúr darb ainm `ImportantExcerpt` a shainmhíomar i Liostú 10-24.

Ar dtús úsáidfimid modh darb ainm `level` a bhfuil an t-aon pharaiméadar ina thagairt dó
`self` agus arb é i32` a luach aischuir, nach tagairt d'aon rud é:

```rust
{{#rustdoc_include ../../listings/ch10-generic-types-traits-and-lifetimes/no-listing-10-lifetimes-on-methods/src/main.rs:1st}}
```

An dearbhú paraiméadar saoil tar éis `impl` agus a úsáid tar éis ainm an chineáil
ag teastáil, ach ní gá dúinn saolré na tagartha a anótáil
go `self` mar gheall ar riail an chéad elision.

Seo sampla ina bhfuil feidhm ag an tríú riail éalaithe saoil:

```rust
{{#rustdoc_include ../../listings/ch10-generic-types-traits-and-lifetimes/no-listing-10-lifetimes-on-methods/src/main.rs:3rd}}
```

Tá dhá shaolré ionchuir ann, mar sin cuireann Rust an chéad riail éalaithe saoil i bhfeidhm
agus tugann sé a saolta féin idir `&self` agus `announcement`. Ansin, mar gheall ar
ceann de na paraiméadair is ea `&self`, faigheann an cineál tuairisceáin saolré `&self`,
agus tá cuntas déanta ar gach saolré.

### An Saol Statach

Saolré speisialta amháin a chaithfimid a phlé ná `'static`, rud a léiríonn go bhfuil an
tagairt difear _can_ beo ar feadh ré iomlán an chláir. Gach
tá an saolré `'static` ag sreanglitreacha, agus is féidir linn anótáil a dhéanamh mar seo a leanas:

```rust
let s: &'static str = "I have a static lifetime.";
```

Stóráiltear téacs na teaghrán seo go díreach i ndénártha an chláir, mar atá
ar fáil i gcónaí. Dá bhrí sin, tá saolré gach teaghráin-liteartha `'static`.

Seans go bhfeicfeá moltaí i dteachtaireachtaí earráide chun an saolré `'static` a úsáid. Ach
sula sonrófar `'static` mar an saolré le haghaidh tagartha, smaoinigh ar
cibé an bhfuil an tagairt atá agat i do chónaí i ndáiríre ar feadh shaolré iomlán do
clár nó nach ea, agus cibé acu is mian leat é. An chuid is mó den am, teachtaireacht earráide
ag moladh na dtorthaí saoil `'static` as iarracht a dhéanamh ar dhrong a chruthú
tagairt nó neamhréir idir na saolréanna atá ar fáil. I gcásanna den sórt sin, an réiteach
is é sin na fadhbanna sin a réiteach, gan an saolré `'static` a shonrú.

## Paraiméadair Chineálacha Cineálacha, Teorainneacha Trait, agus Saoil le Chéile

Breathnaímid go hachomair ar an chomhréir a bhaineann le paraiméadair cineálacha cineálacha, tréithe a shonrú
teorainneacha, agus saolréanna ar fad in aon fheidhm amháin!

``` meirge
{{#rustdoc_include ../../listings/ch10-generic-types-traits-and-lifetimes/no-listing-11-generics-traits-and-lifetimes/src/main.rs:here}}
```

Seo í an fheidhm `longest` ó Liostú 10-21 a fhilleann an ceann is faide de
dhá shlisne teaghrán. Ach anois tá paraiméadar breise aige darb ainm `ann` den chineálach
clóscríobh `T`, ar féidir é a líonadh isteach de réir cineáil ar bith a chuireann an `Display` i bhfeidhm
tréith mar atá sonraithe ag an gclásal `áit`. Déanfar an paraiméadar breise seo a phriontáil
ag baint úsáide as `{}`, agus sin an fáth a bhfuil an tréithe `Display` faoi cheangal riachtanach. Toisc
is cineál cineálach iad saolréanna, dearbhuithe an pharaiméadar saoil
Téann `'a` agus an cineál paraiméadar cineálach `T` sa liosta céanna taobh istigh den uillinn
lúibíní i ndiaidh ainm na feidhme.

## Achoimre

Chlúdaigh muid go leor sa chaibidil seo! Anois go bhfuil a fhios agat faoi chineál cineálach
paraiméadair, tréithe agus teorainneacha tréithe, agus paraiméadair chineálacha saoil, tá tú
réidh le cód a scríobh gan athrá a oibríonn i go leor cásanna éagsúla.
Ligeann paraiméadair chineálacha duit an cód a chur i bhfeidhm ar chineálacha éagsúla. Tréithe agus
cinntíonn teorainneacha tréithe, cé go bhfuil na cineálacha cineálacha, go mbeidh an
iompar a theastaíonn ón gcód. D'fhoghlaim tú conas nótaí saoil a úsáid lena chinntiú
nach mbeidh aon tagairtí dochloíte ag an gcód solúbtha seo. Agus seo go léir
tarlaíonn anailís ag am tiomsaithe, rud nach gcuireann isteach ar fheidhmíocht am rite!

Creid é nó ná creid, tá i bhfad níos mó le foghlaim ar na hábhair a phléamar
sa chaibidil seo: Pléann Caibidil 18 réada trait, ar bealach eile iad a úsáid
tréithe. Tá cásanna níos casta ann freisin a bhaineann le nótaí saoil
nach mbeidh de dhíth ort ach i gcásanna sárfhorbartha; dóibh siúd, ba cheart duit léamh
an [Tagairt Rust][reference]. Ach ina dhiaidh sin, beidh tú ag foghlaim conas trialacha a scríobh isteach
Rust ionas gur féidir leat a chinntiú go bhfuil do chód ag obair mar ba chóir dó.

[references-and-borrowing]: ch04-02-references-and-borrowing.html#references-and-borrowing
[string-slices-as-parameters]: ch04-03-slices.html#string-slices-as-parameters
[reference]: ../reference/index.html