## Athróga agus Inathraitheacht

Mar a luadh sa [“Luachanna Stórála le
Athróga”][storing-values-with-variables]<!-- ignore --> alt, de réir réamhshocraithe,
tá athróga do- immutable. Tá sé seo ar cheann de go leor nodanna a thugann Rust duit a scríobh
do chód ar bhealach a bhaineann leas as an concurrency sábháilteachta agus éasca go
Cuireann meirge. Mar sin féin, tá an rogha agat fós do chuid athróg a dhéanamh mutable.
Déanaimis iniúchadh ar conas agus cén fáth a spreagann Rust tú a bheith i bhfabhar do-mhothúchánacht agus cén fáth
uaireanta b'fhéidir gur mhaith leat rogha an diúltaithe.

Nuair a bhíonn athróg neamh-inchurtha, a luaithe a bhíonn luach ceangailte le hainm, ní féidir leat athrú
an luach sin. Chun é seo a léiriú, gintear tionscadal nua dar teideal _variables_ in
do _projects_ eolaire trí úsáid a bhaint as `cargo new variables`.

Ansin, i do eolaire _variables_ nua, oscail _src/main.rs_ agus cuir ceann ina áit
cód leis an gcód seo a leanas, nach dtiomsóidh fós:

<span class="filename">Ainm comhaid: src/main.rs</span>

```rust,ignore,does_not_compile
{{#rustdoc_include ../../listings/ch03-common-programming-concepts/no-listing-01-variables-are-immutable/src/main.rs}}
```

Sábháil agus rith an clár ag úsáid `cargo run`. Ba cheart go bhfaighfeá teachtaireacht earráide
maidir le hearráid neamh-luaineachta, mar a thaispeántar san aschur seo:

```console
{{#include ../../listings/ch03-common-programming-concepts/no-listing-01-variables-are-immutable/output.txt}}
```

Léiríonn an sampla seo conas a chuidíonn an tiomsaitheoir leat teacht ar earráidí i do chláir.
Is féidir le hearráidí tiomsaitheora a bheith frustrachas, ach i ndáiríre ní chiallaíonn siad ach do chlár
nach bhfuil tú ag déanamh a bhfuil uait go fóill go sábháilte; ní chiallaíonn siad go bhfuil tú
nach ríomhchláraitheoir maith é! Faigheann Rustaceans a bhfuil taithí acu earráidí tiomsaitheora fós.

Fuair ​​tú an teachtaireacht earráide `` cannot assign twice to immutable variable `x` `` toisc go ndearna tú iarracht an dara luach a shannadh don athróg do-ath-inchurtha `x`.

Tá sé tábhachtach go bhfaighimid earráidí maidir le ham tiomsaithe nuair a dhéanaimid iarracht a
luach atá sainithe mar neamh-luaineach mar go bhféadfadh an cás seo a bheith mar thoradh air
fabhtanna. Má oibríonn cuid amháin dár gcód ar an toimhde go mbeidh luach
choíche agus athraíonn cuid eile dár gcód an luach sin, is féidir
nach ndéanfaidh an chéad chuid den chód an rud a ceapadh dó a dhéanamh. An chúis
Is féidir leis an gcineál seo fabht a bheith deacair a rianú síos i ndiaidh an bhfíric, go háirithe
nuair a athraíonn an dara píosa cód an luach amháin _uaireanta_. An Meirge
ráthaíonn tiomsaitheoir nuair a luann tú nach n-athróidh luach, i ndáiríre
Ní athróidh, mar sin ní gá duit súil a choinneáil air féin. Tá do chód mar sin
níos éasca a réasúnú tríd.

Ach is féidir inathraitheacht a bheith an-úsáideach, agus is féidir cód a dhéanamh níos áisiúla a scríobh.
Cé go bhfuil athróga do-laghdaithe de réir réamhshocraithe, is féidir leat iad a dhéanamh comhshóite faoi
ag cur `mut` os comhair an ainm athróg mar a rinne tú i [Caibidil
2][storing-values-with-variables] <!-- neamhaird -->. Nuair a chuirfear `mut` tugann sé freisin
rún do léitheoirí an chóid amach anseo trí chodanna eile den chód a chur in iúl
ag athrú luach na hathróige seo.

Mar shampla, déanaimis _src/main.rs_ a athrú chuig an méid seo a leanas:

<span class="filename">Ainm comhaid: src/main.rs</span>

```rust
{{#rustdoc_include ../../listings/ch03-common-programming-concepts/no-listing-02-adding-mut/src/main.rs}}
```

Nuair a ritheann muid an clár anois, faigheann muid seo:

```console
{{#include ../../listings/ch03-common-programming-concepts/no-listing-02-adding-mut/output.txt}}
```

Tá cead againn an luach faoi cheangal go `x` a athrú ó `5` go `6` nuair is `mut`
úsáidtear. I ndeireadh na dála, is fút féin atá sé cinneadh a dhéanamh maidir le sócmhainneacht a úsáid nó gan é
ag brath ar cad a cheapann tú is soiléire sa chás áirithe sin.

### Tairiseacha

Cosúil le hathróga domhalartaithe, is luachanna iad _constants_ atá ceangailte d'ainm agus
nach bhfuil cead a athrú, ach tá roinnt difríochtaí idir tairisigh
agus athróga.

Ar dtús, níl cead agat `mut` a úsáid le tairisigh. Ní hamháin go bhfuil tairisigh
do-laghdaithe de réir réamhshocraithe - tá siad i gcónaí dochorraithe. Dearbhaíonn tú tairisigh ag baint úsáide as an
eochairfhocal `const` in ionad an eochairfhocail `let`, agus cineál an luacha _must_
a bheith anótáilte. Clúdóimid cineálacha agus clóscríobhfaimid nótaí sa chéad chuid eile,
[“Cineálacha Sonraí”][data-types]<!-- neamhaird a dhéanamh ar -->, mar sin ná bí buartha faoi na sonraí
ceart anois. Bíodh a fhios agat go gcaithfidh tú an cineál a anótáil i gcónaí.

Is féidir tairisigh a dhearbhú in aon raon feidhme, lena n-áirítear an raon feidhme domhanda, a dhéanann
úsáideach iad le haghaidh luachanna a gcaithfidh go leor codanna den chód a bheith ar an eolas fúthu.

Is é an difríocht dheireanach nach féidir tairisigh a shocrú ach do shloinneadh tairiseach,
ní toradh é sin ar luach nach bhféadfaí a ríomh ach ag am rite.

Seo sampla de dhearbhú seasta:

```rust
const THREE_HOURS_IN_SECONDS: u32 = 60 * 60 * 3;
```

Is é ainm an tairiseach ná `THREE_HOURS_IN_SECONDS` agus socraítear a luach go dtí an
toradh ar iolrú 60 (líon na soicind i nóiméid) faoi 60 (an uimhir
nóiméad in uair an chloig) faoi 3 (an líon uaireanta is mian linn a chomhaireamh sa
clár). Is é an gnás ainmniúcháin atá ag Rust maidir le tairisigh ná gach cás uachtair a úsáid le
béim idir focail. Tá an tiomsaitheoir in ann sraith theoranta de
oibríochtaí ag am tiomsaithe, a ligeann dúinn rogha a dhéanamh an luach seo a scríobh amach in a
bealach atá níos éasca a thuiscint agus a fhíorú, seachas an tairiseach seo a shocrú
go dtí an luach 10,800. Féach an rannán [Tagairt Meirge ar tairiseach
luacháil][const-eval] le haghaidh tuilleadh eolais ar na hoibríochtaí is féidir a úsáid
nuair a dhearbhaítear tairisigh.

Tá tairisigh bailí ar feadh an ama ar fad a ritheann clár, laistigh den raon feidhme i
a dearbhaíodh iad. Déanann an airí seo tairisigh úsáideach do luachanna i
d'fhearann ​​iarratais a bhféadfadh go mbeadh a fhios ag codanna éagsúla den chlár
thart ar, mar shampla an t-uaslíon pointí a cheadaítear d’aon imreoir cluiche
thuilleamh, nó luas an tsolais.

Tá sé úsáideach luachanna cruachódaithe a úsáidtear ar fud do chláir a ainmniú mar thairisigh
brí an luacha sin a chur in iúl do lucht cothabhála an chóid amach anseo. sé freisin
cabhraíonn sé le háit amháin a bheith i do chód bheadh ​​ort a athrú má tá an
ní mór luach cruachód a nuashonrú amach anseo.

### Scáthfhoghlaim

Mar a chonaic tú sa rang teagaisc cluiche buille faoi thuairim i [Caibidil
2][comparing-the-guess-to-the-secret-number]<!-- neamhaird a dhéanamh ar -->, is féidir leat a dhearbhú
athróg nua leis an ainm céanna leis an athróg roimhe seo. Deir Rustaceans go bhfuil an
Is é an chéad athróg _shadowed_ ag an dara, rud a chiallaíonn go bhfuil an dara
Is é an t-athróg a fheicfidh an tiomsaitheoir nuair a úsáideann tú ainm na hathróige.
Go bunúsach, déanann an dara athróg scáthú ar an gcéad cheann, ag glacadh aon úsáidí a bhaintear as an
ainm inathraithe dó féin go dtí go scáthaítear é féin nó go gcríochnaítear an raon feidhme.
Is féidir linn athróg a scáthú trí úsáid a bhaint as ainm na hathróige céanna agus an t-athróg a athrá
úsáid an eochairfhocail `let` mar seo a leanas:

<span class="filename">Ainm comhaid: src/main.rs</span>

```rust
{{#rustdoc_include ../../listings/ch03-common-programming-concepts/no-listing-03-shadowing/src/main.rs}}
```

Ceanglaíonn an clár seo `x` ar luach `5` ar dtús. Ansin cruthaíonn sé athróg nua
`x` trí `let x =` a athrá, ag tógáil an luach bunaidh agus ag cur `1` leis mar sin de
Is é luach `x` ansin `6`. Ansin, laistigh de raon feidhme istigh a cruthaíodh leis an curly
lúibíní, scáthaíonn an tríú ráiteas `let` `x` freisin agus cruthaíonn sé ráiteas nua
athróg, ag iolrú an luach roimhe faoi `2` chun luach `12` a thabhairt do `x`.
Nuair a bhíonn an scóip sin thart, cuirtear deireadh leis an scáthú istigh agus filleann `x` ar a bheith `6`.
Nuair a bheidh an clár seo á rith againn, aschuirfidh sé an méid seo a leanas:

```console
{{#include ../../listings/ch03-common-programming-concepts/no-listing-03-shadowing/output.txt}}
```

Ní hionann an scáthú agus athróg a mharcáil mar `mut` mar gheobhaidh muid a
earráid ama tiomsaithe má dhéanaimid iarracht de thaisme athshannadh don athróg seo gan
ag baint úsáide as an eochairfhocal `let`. Trí úsáid a bhaint as `let`, is féidir linn cúpla claochlú a dhéanamh
ar luach ach an bhfuil an t-athróg do-athlasta tar éis na claochluithe sin
curtha i gcrích.

Is é an difríocht eile idir `mut` agus scáthfhoghlaim ná toisc go bhfuilimid
ag cruthú athróg nua go héifeachtach nuair a úsáidimid an eochairfhocal `let` arís, is féidir linn
cineál an luacha a athrú ach an t-ainm céanna a athúsáid. Mar shampla, abair ár
Iarrann an clár ar úsáideoir a thaispeáint cé mhéad spás atá uathu idir téacs éigin
ag ionchur carachtair spáis, agus ansin ba mhaith linn an t-ionchur sin a stóráil mar uimhir:

```rust
{{#rustdoc_include ../../listings/ch03-common-programming-concepts/no-listing-04-shadowing-can-change-types/src/main.rs:here}}
```

Is cineál teaghrán é an chéad athróg `spaces` agus an dara hathróg `spaces`
is cineál uimhreach é. Fágann scáthú mar sin nach gá dúinn teacht suas leis
ainmneacha éagsúla, mar `spaces_str` agus `spaces_num`; ina ionad sin, is féidir linn a athúsáid
an t-ainm `spaces` níos simplí. Mar sin féin, má dhéanaimid iarracht `mut` a úsáid le haghaidh seo, mar a thaispeántar
anseo, gheobhaidh muid earráid ama tiomsaithe:

```rust,ignore,does_not_compile
{{#rustdoc_include ../../listings/ch03-common-programming-concepts/no-listing-05-mut-cant-change-types/src/main.rs:here}}
```

Deir an earráid nach bhfuil cead againn cineál athróige a athrú:

```console
{{#include ../../listings/ch03-common-programming-concepts/no-listing-05-mut-cant-change-types/output.txt}}
```

Anois go bhfuil iniúchadh déanta againn ar an gcaoi a n-oibríonn athróga, breathnaímid ar níos mó cineálacha sonraí iad
is féidir a bheith.

[comparing-the-guess-to-the-secret-number]: ch02-00-guessing-game-tutorial.html#comparing-the-guess-to-the-secret-number
[data-types]: ch03-02-data-types.html#data-types
[storing-values-with-variables]: ch02-00-guessing-game-tutorial.html#storing-values-with-variables
[const-eval]: ../reference/const_eval.html
