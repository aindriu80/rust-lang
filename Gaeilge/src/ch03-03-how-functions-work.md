## Feidhmeanna

Tá feidhmeanna forleithne i gcód Rust. Tá ceann de na cinn is mó feicthe agat cheana féin
feidhmeanna tábhachtacha sa teanga: an `main`, is é sin an iontráil
pointe go leor clár. Tá an eochairfhocal `fn` feicthe agat freisin, a ligeann duit
feidhmeanna nua a dhearbhú.

Úsáideann cód meirge _nathair cás_ mar ghnáthstíl feidhme agus athróg
ainmneacha, ina bhfuil litreacha beaga go léir agus ina gcuirtear béim ar fhocail ar leith.
Seo clár ina bhfuil sainmhíniú ar fheidhm shamplach:

<span class="filename">Ainm comhaid: src/main.rs</span>

```rust
{{#rustdoc_include ../../listings/ch03-common-programming-concepts/no-listing-16-functions/src/main.rs}}
```

Sainmhínímid feidhm i Rust trí `fn` a iontráil agus ainm feidhme agus a
sraith lúibíní. Insíonn na lúibíní cuartha don tiomsaitheoir cá bhfuil an fheidhm
tosaíonn agus críochnaíonn an comhlacht.

Is féidir linn aon fheidhm atá sainithe againn a ghlaoch trína hainm a chur isteach agus sraith ina dhiaidh
de lúibíní. Toisc go bhfuil `another_function` sainmhínithe sa chlár, is féidir é a bheith
ar a dtugtar ón taobh istigh den `main`. Tabhair faoi deara gur shainmhíníomar `another_function`
_tar éis_ an fheidhm `main` sa chód foinse; d'fhéadfaimis é a shainiú roimhe seo
chomh maith. Is cuma le Rust cén áit a shainíonn tú do chuid feidhmeanna, ach amháin go bhfuil siad
sainithe áit éigin i raon feidhme atá le feiceáil ag an nglaoiteoir.

Cuirimis tús le tionscadal dénártha nua darb ainm _functions_ chun feidhmeanna a iniúchadh
a thuilleadh. Cuir an sampla `another_function` i _src/main.rs_ agus rith é. tu
Ba chóir go bhfeicfeadh sé an t-aschur seo a leanas:

```console
{{#include ../../listings/ch03-common-programming-concepts/no-listing-16-functions/output.txt}}
```

Feidhmíonn na línte san ord ina bhfuil siad le feiceáil sa `main`.
Ar dtús an "Dia duit, domhan!" priontaí an teachtaireacht, agus ansin tugtar `another_function`
agus tá a theachtaireacht clóbhuailte.

### Paraiméadair

Is féidir linn feidhmeanna a shainiú chun _parameters_ a bheith acu, ar athróga speisialta iad sin
mar chuid de shíniú feidhme. Nuair a bhíonn paraiméadair ag feidhm, is féidir leat
luachanna nithiúla a sholáthar dó le haghaidh na bparaiméadar sin. Go teicniúil, an coincréit
_arguments_ a thugtar ar luachanna, ach i gcomhrá ócáideach, is gnách go n-úsáideann daoine
na focail _parameter_ agus _argument_ go hidirmhalartaithe do cheachtar na hathróga
i sainmhíniú feidhme nó sna luachanna nithiúla a chuirtear isteach nuair a ghlaonn tú ar a
feidhm.

Sa leagan seo de `another_function` cuirimid paraiméadar leis:

<span class="filename">Ainm comhaid: src/main.rs</span>

```rust
{{#rustdoc_include ../../listings/ch03-common-programming-concepts/no-listing-17-functions-with-parameters/src/main.rs}}
```

Bain triail as an gclár seo a rith; ba cheart duit an t-aschur seo a leanas a fháil:

```console
{{#include ../../listings/ch03-common-programming-concepts/no-listing-17-functions-with-parameters/output.txt}}
```

Tá paraiméadar amháin darb ainm `x` sa dearbhú `another_function`. An cineál
Sonraítear `x` mar `i32`. Nuair a thugaimid `5` isteach go `another_function`, beidh an
`println!` cuireann macra `5` san áit a raibh an péire lúibíní cuartha ina raibh `x`
sa teaghrán formáide.

I sínithe feidhm, _ní mór duit_ cineál gach paraiméadar a dhearbhú. Tá sé seo
cinneadh d’aon ghnó i ndearadh Rust: nótaí clóite a éilíonn san fheidhm
sainmhínithe ciallaíonn an tiomsaitheoir beagnach riamh gá duit iad a úsáid in aon áit eile
an cód chun a dhéanamh amach cén cineál atá i gceist agat. Tá an tiomsaitheoir in ann a thabhairt freisin
teachtaireachtaí earráide níos cabhrach má tá a fhios aige cad iad na cineálacha a bhfuil an fheidhm ag súil leo.

Agus paraiméadair iolracha á sainiú, deighil na dearbhuithe paraiméadar le
camóga, mar seo:

<span class="filename">Ainm comhaid: src/main.rs</span>

```rust
{{#rustdoc_include ../../listings/ch03-common-programming-concepts/no-listing-18-functions-with-multiple-parameters/src/main.rs}}
```

Cruthaíonn an sampla seo feidhm darb ainm `print_labeled_measurement` le dhá cheann
paraiméadair. Tugtar `value` ar an gcéad pharaiméadar agus is `i32` é. Is é an dara
darb ainm `unit_label` agus is cineál `char` é. Ansin priontaí an fheidhm téacs ina bhfuil
an `value` agus an `unit_label` araon.

Déanaimis iarracht an cód seo a rith. Ionadaigh an ríomhchlár atá i do _functions_ faoi láthair
comhad _src/main.rs_ an tionscadail leis an sampla roimhe seo agus é a rith ag baint úsáide as `cargo
run`:

```console
{{#include ../../listings/ch03-common-programming-concepts/no-listing-18-functions-with-multiple-parameters/output.txt}}
```

Toisc gur thugamar an fheidhm le `5` mar luach `value` agus `' h'` mar
an luach le haghaidh `unit_label`, tá na luachanna sin in aschur an chláir.

### Ráitis agus Léirithe

Tá comhlachtaí feidhme comhdhéanta de shraith ráiteas a chríochnaíonn go roghnach le
léiriú. Go dtí seo, níor cuireadh deireadh leis na feidhmeanna atá clúdaithe againn
abairt, ach tá slonn feicthe agat mar chuid de ráiteas. Toisc
Is teanga bunaithe ar chaint í meirge, is idirdhealú tábhachtach é seo
thuiscint. Níl na hidirdhealú céanna ag teangacha eile, mar sin breathaimis orthu
cad iad ráitis agus nathanna cainte agus conas a théann a ndifríochtaí i bhfeidhm ar na coirp
of feidhmeanna.

- Is treoracha iad **Ráitis** a dhéanann gníomh éigin agus nach bhfilleann
 luach.
- Déanann **léirithe** luach iarmhartach. Breathnaímid ar roinnt samplaí.

Tá ráitis agus nathanna cainte úsáidte againn cheana féin. Athróg a chruthú agus
is ráiteas é luach a shannadh dó leis an eochairfhocal `let`. I Liosta 3-1,
`let y = 6;` is ráiteas é.

<Listing number="3-1" file-name="src/main.rs" caption="A `main` function declaration containing one statement">

```rust
{{#rustdoc_include ../../listings/ch03-common-programming-concepts/listing-03-01/src/main.rs}}
```

</Listing>

Is ráitis iad sainmhínithe feidhmeanna freisin; is é an sampla iomlán roimhe seo a
ráiteas ann féin. (Mar a fheicfimid thíos, ní feidhm _calling_ a
ráiteas.)

Ní thugann ráitis luachanna ar ais. Mar sin, ní féidir leat ráiteas `let` a shannadh
chuig athróg eile, mar a dhéanann an cód seo a leanas iarracht; gheobhaidh tú earráid:

<span class="filename">Ainm comhaid: src/main.rs</span>

```rust,ignore,does_not_compile
{{#rustdoc_include ../../listings/ch03-common-programming-concepts/no-listing-19-statements-vs-expressions/src/main.rs}}
```

Nuair a bheidh an clár seo á rith agat, beidh cuma mar seo ar an earráid a gheobhaidh tú:

```console
{{#include ../../listings/ch03-common-programming-concepts/no-listing-19-statements-vs-expressions/output.txt}}
```

Ní thugann an ráiteas `let y = 6` luach ar ais, mar sin níl aon rud ann
`x` chun ceangal a dhéanamh. Tá sé seo difriúil ón méid a tharlaíonn i dteangacha eile, mar
C agus Ruby, áit a dtugann an tasc ar ais luach an taisc. Sna
teangacha, is féidir leat `x = y = 6` a scríobh agus tá an luach ag `x` agus `y` araon
`6`; ní hé sin an cás i Rust.

Measúnaíonn na habairtí go luach agus is ionann iad agus an chuid is mó den chuid eile den chód a
scríobhfaidh tú i Rust. Smaoinigh ar oibríocht matamaitice, mar `5 + 6`, atá ina
slonn a dhéanann luacháil ar an luach `11`. Is féidir le habairtí a bheith mar chuid de
ráitis: i Liostú 3-1, is é an `6` sa ráiteas `let y = 6;`
slonn a dhéanann luacháil ar an luach `6`. Is éard atá i gceist le glaoch ar fheidhm ná
léiriú. Is léiriú é macra a ghlaoch. Cruthaíodh bloc scóip nua le
Is slonn é lúibíní curly, mar shampla:

<span class="filename">Ainm comhaid: src/main.rs</span>

```rust
{{#rustdoc_include ../../listings/ch03-common-programming-concepts/no-listing-20-blocks-are-expressions/src/main.rs}}
```

An slonn seo:

```rust,ignore
{
    let x = 3;
    x + 1
}
```

is bloc é a dhéanann, sa chás seo, meastóireacht ar `4`. Tá an luach sin ceangailte le `y`
mar chuid den ráiteas `let`. Tabhair faoi deara nach bhfuil a
leathstad ag an deireadh, rud nach ionann agus an chuid is mó de na línte atá feicthe agat go dtí seo.
Ní fholaíonn na habairtí dar críoch leathchoilín. Má chuireann tú leathstad go dtí an deireadh
de slonn, déanann tú ráiteas é, agus ní fhillfidh sé ansin a
luach. Coinnigh seo san áireamh agus tú ag iniúchadh luachanna agus nathanna tuairisceáin fheidhme
seo chugainn.

### Feidhmeanna le Luachanna Tuairisceáin

Is féidir le feidhmeanna luachanna a chur ar ais chuig an gcód a ghlaonn orthu. Ní thugaimid ainm ar ais
luachanna, ach ní mór dúinn a gcineál a dhearbhú tar éis saighead (`->`). I Rust, an
Tá luach aischuir na feidhme comhchiallach le luach an deiridh
léiriú i mbloic an choirp feidhm. Is féidir leat filleadh go luath ó a
feidhmiú trí úsáid a bhaint as an eochairfhocal `return` agus luach a shonrú, ach an chuid is mó
filleann feidhmeanna an slonn deiridh go hintuigthe. Seo sampla de a
feidhm a thugann luach ar ais:

<span class="filename">Ainm comhaid: src/main.rs</span>

```rust
{{#rustdoc_include ../../listings/ch03-common-programming-concepts/no-listing-21-function-return-values/src/main.rs}}
```

Níl aon ghlaonna feidhme, macraí, nó fiú ráitis `let` sna `five`
feidhm - gan ach an uimhir `5` leis féin. Sin feidhm fhíor-bhailí i
Meirge. Tabhair faoi deara go sonraítear cineál aischuir na feidhme freisin, mar `-> i32`. Bain triail as
an cód seo a rith; ba cheart go mbeadh cuma mar seo ar an aschur:

```console
{{#include ../../listings/ch03-common-programming-concepts/no-listing-21-function-return-values/output.txt}}
```

Is é an `5` i `five` luach aischuir na feidhme, agus sin an fáth a bhfuil an cineál tuairisceáin
tá `i32`. Déanaimis é seo a scrúdú níos mine. Tá dhá mhír thábhachtacha ann:
ar dtús, léiríonn an líne `let x = five();` go bhfuil luach aischuir a
feidhm chun athróg a thúsú. Toisc go dtugann an fheidhm `five` `5` ar ais,
is ionann an líne sin agus an méid seo a leanas:

```rust
let x = 5;
```

Sa dara háit, níl aon pharaiméadair ag an bhfeidhm `five` agus sainmhíníonn sé cineál an
luach ar ais, ach tá an comhlacht ar an fheidhm a uaigneach `5` gan aon leathstad
mar is léiriú é ar mian linn a luach a thabhairt ar ais.

Breathnaímis ar shampla eile:

<span class="filename">Ainm comhaid: src/main.rs</span>

```rust
{{#rustdoc_include ../../listings/ch03-common-programming-concepts/no-listing-22-function-parameter-and-return/src/main.rs}}
```

Má ritheann tú an cód seo, priontálfar `The value of x is: 6`. Ach má chuirimid a
leathstad ag deireadh na líne ina bhfuil `x + 1`, ag athrú ó an
léiriú ar ráiteas, gheobhaidh muid earráid:

<span class="filename">Ainm comhaid: src/main.rs</span>

```rust,ignore,does_not_compile
{{#rustdoc_include ../../listings/ch03-common-programming-concepts/no-listing-23-statements-dont-return-values/src/main.rs}}
```

Cruthaíonn an cód seo earráid, mar a leanas:

```console
{{#include ../../listings/ch03-common-programming-concepts/no-listing-23-statements-dont-return-values/output.txt}}
```

Nochtann an phríomhtheachtaireacht earráide, `mismatched types`, an phríomhcheist leis seo
cód. Deir an sainmhíniú ar an bhfeidhm `plus_one` go dtabharfaidh sé ar ais an
`i32`, ach ní luachálann ráitis go luach, a chuirtear in iúl le `()`,
an cineál aonaid. Dá bhrí sin, ní chuirtear aon rud ar ais, rud a thagann salach ar an bhfeidhm
sainmhíniú agus déantar earráid dá bharr. San aschur seo, cuireann Rust teachtaireacht chuig
b'fhéidir cabhrú leis an tsaincheist seo a cheartú: molann sé an leathstad a bhaint, a
dheisiú an earráid.