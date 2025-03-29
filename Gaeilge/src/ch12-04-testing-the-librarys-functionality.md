## Feidhmiúlacht na Leabharlainne a Fhorbairt le Forbairt Thrialaithe

Anois go bhfuil an loighic bainte amach againn i _src/lib.rs_ agus d'fhág muid an argóint
bailiú agus láimhseáil earráidí in _src/main.rs_, tá sé i bhfad níos éasca tástálacha a scríobh
le haghaidh feidhmiúlacht lárnach ár gcód. Is féidir linn feidhmeanna a ghlaoch go díreach le
argóintí éagsúla agus seiceáil luachanna tuairisceáin gan gá a ghlaoch ar ár dénártha
ón líne ordaithe.

Sa chuid seo, cuirfimid an loighic chuardaigh leis an gclár `minigrep` ag baint úsáide as
an próiseas forbartha tástála-tiomáinte (TDD) leis na céimeanna seo a leanas:

1. Scríobh tástáil a theipeann ort agus é a rith chun a chinntiú go dteipeann uirthi ar an gcúis leat
 ag súil.
2. Scríobh nó modhnaigh go leor cód chun pas a fháil sa tástáil nua.
3. Déan an cód a chuir tú leis nó a d'athraigh tú a athchur agus cinntigh go leanann na tástálacha ar aghaidh
 chun pas a fháil.
4. Déan arís ó chéim 1!

Cé nach bhfuil ann ach ceann amháin de go leor bealaí chun bogearraí a scríobh, is féidir le TDD cabhrú le cód a thiomáint
dearadh. An triail a scríobh sula scríobhann tú an cód a fhágann go n-éireoidh leis an triail
cuidíonn sé le clúdach tástála ard a choinneáil ar feadh an phróisis.

Déanfaimid tástáil ar chur i bhfeidhm na feidhmiúlachta a dhéanfaidh i ndáiríre
an teaghrán ceiste a chuardach in inneachar an chomhaid agus déan liosta de
línte a mheaitseálann an cheist. Cuirfimid an fheidhmiúlacht seo leis an bhfeidhm ar a dtugtar
`search`.

### Scriobh teist theip

Toisc nach bhfuil siad de dhíth orainn a thuilleadh, bainimis na ráitis `println!` ó
_src/lib.rs_ agus _src/main.rs_ a d’úsáideamar chun iompar an chláir a sheiceáil.
Ansin, in _src/lib.rs_, cuirfimid modúl `tests` le feidhm tástála, agus muid ag
rinne i [Caibidil 11][ch11-anatomy] <!-- neamhaird -->. Sonraíonn an fheidhm tástála
an iompar ba mhaith linn a bheith ag an fheidhm `search`: tógfaidh sé ceist agus
an téacs a chuardach, agus beidh sé ar ais ach na línte as an téacs a
an cheist a chuimsiú. Léiríonn liostú 12-15 an tástáil seo, nach dtiomsóidh fós.

<Listing number="12-15" file-name="src/lib.rs" caption="Creating a failing test for the `search` function we wish we had">

```rust,ignore,does_not_compile
{{#rustdoc_include ../../listings/ch12-an-io-project/listing-12-15/src/lib.rs:here}}
```

</Listing>

Déanann an tástáil seo cuardach don teaghrán `"duct"`. Is é an téacs atá á chuardach againn ná trí
línte, ach ceann amháin acu ina bhfuil `"duct"` (tabhair faoi deara go bhfuil an cúlslais i ndiaidh an
Insíonn oscailt luachan dúbailte do Rust gan carachtar nua-líne a chur ag an tús
den ábhar atá sa teaghrán seo litriúil). Dearbhaímid gur tháinig an luach ar ais ó
Níl san fheidhm `search` ach an líne a mbeimid ag súil leis.

Nílimid in ann an tástáil seo a rith go fóill agus féachaint uirthi go dteipeann uirthi mar ní amhlaidh a dhéanann an tástáil
fiú tiomsú: níl an fheidhm `search` ann fós! De réir TDD
prionsabail, cuirfimid díreach go leor cód leis chun an tástáil a chur le chéile agus a reáchtáil
ag cur sainmhíniú ar an bhfeidhm `search` a thugann folamh ar ais i gcónaí
veicteoir, mar a thaispeántar i Liostú 12-16. Ansin ba chóir an tástáil a thiomsú agus a theipeann
toisc nach meaitseálann veicteoir folamh veicteoir a bhfuil an líne `"safe,
fast, productive."`

<Listing number="12-16" file-name="src/lib.rs" caption="Defining just enough of the `search` function so our test will compile">

```rust,noplayground
{{#rustdoc_include ../../listings/ch12-an-io-project/listing-12-16/src/lib.rs:here}}
```

</Listing>

Tabhair faoi deara go gcaithfimid saolré sainráite `'a` a shainiú i síniú
`search` agus úsáid an tsaoil sin leis an argóint `contents` agus an tuairisceán
luach. Athghairm i [Caibidil 10][ch10-lifetimes]<!-- neamhaird --> go bhfuil an saolré
sonróidh paraiméadair cén saolré argóint atá ceangailte le saolré an
luach aischuir. Sa chás seo, tugaimid le fios gur chóir go mbeadh an veicteoir ar ais
slisní teaghrán a dhéanann tagairt do shlisní den argóint `contents` (seachas an
argóint `query`).

I bhfocail eile, inseoimid do Rust go bhfuil na sonraí ar ais ag an fheidhm `search`
beidh sé beo chomh fada agus a chuirtear na sonraí isteach san fheidhm `search` sa
argóint `contents`. Tá sé seo tábhachtach! Teastaíonn na sonraí dá dtagraítear _by_ a slice
a bheith bailí chun an tagairt a bheith bailí; má ghlacann an tiomsaitheoir leis go bhfuil muid ag déanamh
slices teaghrán de `query` seachas `contents`, déanfaidh sé a sheiceáil sábháilteachta
mícheart.

Má dhéanaimid dearmad ar na nótaí saoil agus iarracht a dhéanamh an fheidhm seo a thiomsú, déanfaimid
faigh an earráid seo:

```console
{{#include ../../listings/ch12-an-io-project/output-only-02-missing-lifetimes/output.txt}}
```

Ní fhéadfaidh Rust a fhios a bheith againn cé acu den dá argóint a theastaíonn uainn, mar sin ní mór dúinn a insint
é go follasach. Toisc gurb é `contents` an argóint a chuimsíonn ár dtéacs ar fad
agus ba mhaith linn na codanna den téacs sin a mheaitseáil, tá a fhios againn go bhfuil `contents` ar ais
an argóint ba chóir a bheith ceangailte leis an luach tuairisceáin ag baint úsáide as an saolré
comhréir.

Ní éilíonn teangacha ríomhchlárúcháin eile ort argóintí a nascadh le filleadh
luachanna sa síniú, ach beidh an cleachtas seo níos éasca le himeacht ama. D'fhéadfá
Ba mhaith liom an sampla seo a chur i gcomparáid leis na samplaí sa [“Tagairtí Bailíochtú
le Lifetimes”][validating-references-with-lifetimes]<!-- neamhaird --> alt
i gCaibidil 10 .

Anois déanaimis an tástáil:

```console
{{#include ../../listings/ch12-an-io-project/listing-12-16/output.txt}}
```

Go hiontach, teipeann ar an tástáil, díreach mar a bhí súil againn. Go n-éirí an t-ádh linn!

### Cód a Scríobh chun an Tástáil a Phas

Faoi láthair, tá ag teip ar ár dtástáil toisc go gcuirimid veicteoir folamh ar ais i gcónaí. A shocrú
go gcaithfidh ár gclár na céimeanna seo a leanas a leanúint agus `search` a chur i bhfeidhm:

1. Atriall trí gach líne den ábhar.
2. Seiceáil an bhfuil ár teaghrán fiosrúcháin sa líne.
3. Má dhéanann, cuir leis an liosta luachanna atá á thabhairt ar ais againn.
4. Mura ndéanann, déan faic.
5. Tabhair ar ais liosta na dtorthaí a mheaitseálann.

Oibrímid trí gach céim, ag tosú le atriall trí línte.

#### Atriall Trí Línte leis an Modh `lines`

Tá modh cabhrach ag meirge chun atriallta líne-ar-líne teaghráin a láimhseáil,
`lines` ainmnithe go caothúil, a oibríonna mar a thaispeántar i Liosta 12-17. Tabhair faoi deara go
ní bheidh sé seo le chéile fós.

<Listing number="12-17" file-name="src/lib.rs" caption="Iterating through each line in `contents`">

```rust,ignore,does_not_compile
{{#rustdoc_include ../../listings/ch12-an-io-project/listing-12-17/src/lib.rs:here}}
```

</Listing>

Tugann an modh `lines` atrialltóir ar ais. Labhróimid go domhain faoi iterators
[Caibidil 13][ch13-iterators]<!-- déan neamhaird de -->, ach chun cuimhne go bhfaca tú mar seo
as iterator a úsáid i [Liostú 3-5][ch3-iter]<!-- neamhaird -->, áit ar úsáideamar a
lúb `for` le iterator chun cód éigin a rith ar gach mír i mbailiúchán.

#### Ag Cuardach Gach Líne don Cheist

Ansin, seiceálfaimid an bhfuil ár teaghrán ceisteanna sa líne reatha.
Ar ámharaí an tsaoil, tá modh cabhrach ag teaghráin darb ainm `contains` a dhéanann é seo le haghaidh
linn! Cuir glao leis an modh `contains` san fheidhm `search`, mar a thaispeántar i
Liostáil 12-18. Tabhair faoi deara nach mbeidh sé seo le chéile fós.

<Listing number="12-18" file-name="src/lib.rs" caption="Adding functionality to see whether the line contains the string in `query`">

```rust,ignore,does_not_compile
{{#rustdoc_include ../../listings/ch12-an-io-project/listing-12-18/src/lib.rs:here}}
```

</Listing>

Faoi láthair, táimid ag cur le feidhmiúlacht. Chun an cód a fháil le tiomsú, táimid
gá luach a thabhairt ar ais ón gcomhlacht mar a léirigh muid ba mhaith linn san fheidhm
síniú.

#### Línte Meaitseála á Stóráil

Chun an fheidhm seo a chríochnú, ní mór dúinn bealach chun na línte meaitseála a theastaíonn uainn a stóráil
a thabhairt ar ais. Ar an ábhar sin, is féidir linn veicteoir mutable a dhéanamh roimh an lúb `for` agus
glaoigh ar an modh `push` chun `line` a stóráil sa veicteoir. Tar éis an lúb `for`,
cuirimid ar ais an veicteoir, mar a thaispeántar i Liostú 12-19.

<Listing number="12-19" file-name="src/lib.rs" caption="Storing the lines that match so we can return them">

```rust,ignore
{{#rustdoc_include ../../listings/ch12-an-io-project/listing-12-19/src/lib.rs:here}}
```

</Listing>

Anois níor cheart don fheidhm `search` ach na línte ina bhfuil `query` a thabhairt ar ais,
agus ba chóir go n-éireodh lenár dtástáil. Déanaimis an tástáil a rith:

```console
{{#include ../../listings/ch12-an-io-project/listing-12-19/output.txt}}
```

Ár tástáil a rith, mar sin tá a fhios againn go n-oibríonn sé!

Ag an bpointe seo, d'fhéadfaimis deiseanna a bhreithniú chun an
feidhmiú na feidhme cuardaigh agus na tástálacha a choinneáil ag dul go dtí
an fheidhmiúlacht chéanna a choinneáil. Níl an cód san fheidhm chuardaigh ró-olc,
ach ní bhaineann sé leas as roinnt gnéithe úsáideacha de iterators. Déanfaimid
fill ar an sampla seo i [Caibidil 13][ch13-iterators]<!-- neamhaird a dhéanamh ar -->, áit a bhfuil
déanfaimid mionscrúdú ar atrialltóirí, agus féachfaimid ar conas é a fheabhsú.

#### Ag baint úsáide as an fheidhm `search` san Fheidhm `run`

Anois go bhfuil an fheidhm `search` ag obair agus á thástáil, ní mór dúinn `search` a thabhairt air
ónár bhfeidhm `run`. Ní mór dúinn pas a fháil sa luach `config.query` agus an
`contents` a léann `run` ón gcomhad go dtí an fheidhm `search`. Ansin `run`
priontálfaidh sé gach líne a sheoltar ar ais ó `search`:

<span class="filename">Filename: src/lib.rs</span>

```rust,ignore
{{#rustdoc_include ../../listings/ch12-an-io-project/no-listing-02-using-search-in-run/src/lib.rs:here}}
```

Táimid fós ag baint úsáide as lúb `for` chun gach líne ó `search` a thabhairt ar ais agus é a phriontáil.

Anois ba chóir an clár ar fad ag obair! Bainimis triail as, ar dtús le focal a
líne amháin go beacht a thabhairt ar ais ó dhán Emily Dickinson: _frog_.

```console
{{#include ../../listings/ch12-an-io-project/no-listing-02-using-search-in-run/output.txt}}
```

Cool! Anois bainimis triail as focal a mheaitseálann línte iolracha, mar _body_:

```console
{{#include ../../listings/ch12-an-io-project/output-only-03-multiple-matches/output.txt}}
```

Agus ar deireadh, déanaimis deimhin de nach bhfaighimid aon línte nuair a chuardaíonn muid a
focal nach bhfuil áit ar bith sa dán, mar _monomorphization_:

```console
{{#include ../../listings/ch12-an-io-project/output-only-04-no-matches/output.txt}}
```

Ar fheabhas! Tá ár mionleagan féin tógtha againn d’uirlis chlasaiceach agus tá go leor foghlamtha againn
faoi ​​conas feidhmchláir a struchtúrú. Tá beagán foghlamtha againn freisin faoi ionchur comhaid
agus aschur, saolréanna, tástáil, agus parsáil na n-orduithe.

Chun an tionscadal seo a chríochnú, taispeánfaimid go hachomair conas oibriú leis
athróga timpeallachta agus conas a phriontáil go hearráid chaighdeánach, atá sa dá cheann
úsáideach agus tú ag scríobh cláir orduithe.

[validating-references-with-lifetimes]: ch10-03-lifetime-syntax.html#validating-references-with-lifetimes
[ch11-anatomy]: ch11-01-writing-tests.html#the-anatomy-of-a-test-function
[ch10-lifetimes]: ch10-03-lifetime-syntax.html
[ch3-iter]: ch03-05-control-flow.html#looping-through-a-collection-with-for
[ch13-iterators]: ch13-02-iterators.html
