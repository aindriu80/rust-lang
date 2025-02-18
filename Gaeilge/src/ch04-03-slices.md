## An Cineál Slice

Ligeann _Slices_ duit tagairt a dhéanamh do sheicheamh comhtheagmhálach d’eilimintí in a
[collection](ch08-00-common-collections.md) seachas an cnuasach iomlán. A
Is cineál tagartha é slice, mar sin níl úinéireacht aige.

Seo fadhb bheag ríomhchláraithe: scríobh feidhm a ghlacann teaghrán de
focail scartha le spásanna agus seolann sé ar ais an chéad fhocal a aimsíonn sé sa téad sin.
Mura bhfaighidh an fheidhm spás sa téad, caithfidh an téad iomlán a bheith
focal amháin, mar sin ba chóir an teaghrán iomlán a chur ar ais.

Déanaimis oibriú tríd an gcaoi a scríobhfaimid síniú na feidhme seo gan úsáid a bhaint as
slices, chun an fhadhb a réiteoidh slisní a thuiscint:

```rust,ignore
fn first_word(s: &String) -> ?
```

Tá `&String` mar pharaiméadar ag an bhfeidhm `first_word`. Ní gá dúinn
úinéireacht, mar sin tá sé seo go breá. (I Rust idiomatic, ní feidhmeanna a ghlacadh úinéireacht
dá n-argóintí mura gá, agus tiocfaidh na cúiseanna leis sin
soiléir agus muid ag leanúint ar aghaidh!) Ach cad ba cheart dúinn filleadh? Níl bealach againn i ndáiríre
chun labhairt faoi chuid de shreang. Mar sin féin, d'fhéadfaimis an t-innéacs de dheireadh na
an focal, léirithe ag spás. Déanaimis iarracht é sin, mar a thaispeántar i Liostú 4-7.

<Listing number="4-7" file-name="src/main.rs" caption="The `first_word` function that returns a byte index value into the `String` parameter">

```rust
{{#rustdoc_include ../../listings/ch04-understanding-ownership/listing-04-07/src/main.rs:here}}
```

</Listing>

Toisc go gcaithfimid dul tríd an eilimint `String` de réir eiliminte agus seiceáil an bhfuil
Is spás é luach, déanfaimid ár `String` a thiontú go sraith beart ag baint úsáide as an
modh `as_bytes`.

```rust,ignore
{{#rustdoc_include ../../listings/ch04-understanding-ownership/listing-04-07/src/main.rs:as_bytes}}
```

Ansin, cruthaímid iterator thar an sraith beart ag baint úsáide as an modh `iter`:

```rust,ignore
{{#rustdoc_include ../../listings/ch04-understanding-ownership/listing-04-07/src/main.rs:iter}}
```

Déanfaimid plé níos mine ar atrialltóirí i [Caibidil 13][ch13]<!-- neamhaird -->.
Go dtí seo, bíodh a fhios agat gur modh é `iter` a thugann gach eilimint i mbailiúchán ar ais
agus go gcumhdaíonn `enumerate` toradh `iter` agus cuireann sé gach eilimint ar ais mar
cuid de tuple ina ionad. D'fhill an chéad eilimint den tuple ó
Is é `enumerate` an t-innéacs, agus is tagairt í an dara eilimint don eilimint.
Tá sé seo beagán níos áisiúla ná an t-innéacs a ríomh dúinn féin.

Toisc go dtugann an modh `áirimh` tuple ar ais, is féidir linn patrúin a úsáid chun
scrios an tuple sin. Beidh muid ag plé patrúin níos mó i [Caibidil
6][ch6] <!-- neamhaird a dhéanamh -->. Sa lúb `do`, sonraímid patrún a bhfuil `i` air
don innéacs sa tuple agus `&item` don bheart singil sa tuple.
Toisc go bhfaighimid tagairt don eilimint ó `.iter().enurate()`, úsáidimid
`&` sa phatrún.

Laistigh den lúb `do`, déanaimid cuardach don bheart a sheasann don spás trí
ag baint úsáide as an chomhréir liteartha beart. Má aimsímid spás, cuirimid an suíomh ar ais.
Seachas sin, cuirimid fad na sreinge ar ais trí úsáid a bhaint as `s.len()`.

```rust,ignore
{{#rustdoc_include ../../listings/ch04-understanding-ownership/listing-04-07/src/main.rs:inside_for}}
```

Tá bealach againn anois le hinnéacs deireadh an chéad fhocail sa
teaghrán, ach tá fadhb ann. Táimid ag tabhairt 'usize' ar ais leis féin, ach tá
uimhir bhríoch amháin i gcomhthéacs an `&String`. I bhfocail eile,
toisc gur luach ar leith é ón `String`, níl aon ráthaíocht ann go mbeidh sé
beidh sé fós bailí sa todhchaí. Smaoinigh ar an gclár i Liosta 4-8 go
úsáideann an fheidhm `first_word` ó Liostú 4-7.

<Listing number="4-8" file-name="src/main.rs" caption="Storing the result from calling the `first_word` function and then changing the `String` contents">

```rust
{{#rustdoc_include ../../listings/ch04-understanding-ownership/listing-04-08/src/main.rs:here}}
```

</Listing>

Tiomsaítear an clár seo gan aon earráidí agus dhéanfadh sé é sin freisin dá mba rud é gur úsáideamar `word`
tar éis glaoch ar `s.clear()`. Toisc nach bhfuil `word` ceangailte le staid `s`
ar chor ar bith, tá an luach `5` fós i `word`. D'fhéadfaimis an luach sin `5` a úsáid le
an athróg `s` chun iarracht a dhéanamh an chéad fhocal a bhaint amach, ach bheadh ​​​​sé seo ina fhabht
mar tá ábhar `s` athraithe ó shábháil muid `5` i `word`.

Ní mór a bheith buartha faoin innéacs i `word` ag éirí as sioncronú leis na sonraí i
Tá `s` tedious agus seans maith go hearráid! Tá sé níos brí fós na hinnéacsanna seo a bhainistiú más rud é
scríobhaimid feidhm `second_word`. Chaithfeadh a shíniú breathnú mar seo:

```rust,ignore
fn second_word(s: &String) -> (usize, usize) {
```

Anois tá _agus_ innéacs tosaigh á rianú againn, agus tá níos mó fós againn
luachanna a ríomhadh ó shonraí i stát ar leith ach nach bhfuil ceangailte leo
an stát sin ar chor ar bith. Tá trí athróg neamhghaolmhara againn ag snámh thart ar an riachtanas sin
a choinneáil i sioncronú.

Ar ámharaí an tsaoil, tá réiteach ag Rust ar an bhfadhb seo: slisní teaghrán.

### Sliseanna Teaghrán

Tagairt is ea _string slice_ do chuid de `String`, agus tá an chuma air seo:

```rust
{{#rustdoc_include ../../listings/ch04-understanding-ownership/no-listing-17-slice/src/main.rs:here}}
```

Seachas tagairt don `String` iomlán, is tagairt é `hello` d'a
cuid den `String`, sonraithe sa ghiotán breise `[0..5]`. Cruthaímid slisní
ag baint úsáide as raon laistigh de lúibíní trí `[starting_index..ending_index]` a shonrú,
áit a bhfuil `starting_index` an chéad suíomh sa slice agus is é `ending_index`
ceann amháin níos mó ná an seasamh deireanach sa slice. Go hinmheánach, na sonraí slice
Stórálann struchtúr an suíomh tosaigh agus fad an slice, a
fhreagraíonn do `ending_index` lúide `starting_index`. Mar sin, i gcás `let
world = &s[6..11];`, bheadh ​​`world` ina shlis ina bhfuil pointeoir don
beart ag innéacs 6 de `s` le luach faid `5`.

Taispeánann Fíor 4-7 é seo i léaráid.

<img alt="Trí thábla: tábla a léiríonn sonraí cruachta s, a léiríonn
chuig an mbeart ag innéacs 0 i dtábla de na sonraí teaghrán &quot;hello world&quot; ar
an gcarn. Déanann an tríú tábla ionadaíocht ar shonraí cruachta an domhain slice, a
tá luach faid 5 aige agus pointí go beart 6 den tábla sonraí carn."
src="img/trpl04-07.svg" class="center" style="leithead: 50%;" />

<span class="caption">Fíor 4-7: Slis teaghrán a thagraíonn do chuid d’a
`String`</span>

Le comhréir raon `..` Rust, más mian leat tosú ag innéacs 0, is féidir leat titim
an luach roimh an dá thréimhse. I bhfocail eile, tá siad seo comhionann:

```rust
let s = String::from("hello");

let slice = &s[0..2];
let slice = &s[..2];
```

Ar an gcaoi chéanna, má chuimsíonn do shlis an beart deireanach den `String`, tusa
Is féidir titim ar an uimhir trailing. Ciallaíonn sé sin go bhfuil siad seo comhionann:

```rust
let s = String::from("hello");

let len = s.len();

let slice = &s[3..len];
let slice = &s[3..];
```

Is féidir leat an dá luach a laghdú freisin chun slice den teaghrán iomlán a ghlacadh. Mar sin iad seo
comhionann:

```rust
let s = String::from("hello");

let len = s.len();

let slice = &s[0..len];
let slice = &s[..];
```

> Tabhair faoi deara: Caithfidh innéacsanna raon slisne teaghráin a bheith ag carachtar bailí UTF-8
> teorainneacha. Má dhéanann tú iarracht sreangshlis a chruthú i lár a
> carachtar multibyte, scoirfidh do chlár le hearráid. Chun críocha
> ó thabhairt isteach slisní teaghrán, táimid ag glacadh leis ASCII amháin sa chuid seo; a
> tá plé níos críochnúla ar láimhseáil UTF-8 sa [“Storing UTF-8 Ionchódaithe
> Téacs le Teaghráin”][strings]<!-- neamhaird --> alt de Chaibidil 8.

Agus an fhaisnéis seo go léir san áireamh, athscríobhfaimid `first_word` chun a
slisne. Scríobhtar `&str` an cineál a chiallaíonn "slis teaghrán":

<Listing file-name="src/main.rs">

```rust
{{#rustdoc_include ../../listings/ch04-understanding-ownership/no-listing-18-first-word-slice/src/main.rs:here}}
```

</Listing>

Faighimid an t-innéacs do fhoirceann an fhocail mar a rinneamar i Liosta 4-7, de réir
ag lorg an chéad eachtra de spás. Nuair a aimsímid spás, filleann muid a
slisne teaghrán ag baint úsáide as tús na sreinge agus innéacs an spáis mar an
innéacsanna tosaigh agus deiridh.

Anois nuair a ghlaoimid `first_word`, faighimid ar ais luach amháin atá ceangailte leis an
sonraí bunúsacha. Tá an luach comhdhéanta de thagairt do phointe tosaigh na
an slice agus líon na n-eilimintí sa slice.

Bheadh ​​feidhm `second_word` ag baint le slisne a thabhairt ar ais freisin:

```rust,ignore
fn second_word(s: &String) -> &str {
```

Tá API simplí againn anois atá i bhfad níos deacra a praiseach a dhéanamh mar gheall ar an
cinnteoidh tiomsaitheoir go bhfanfaidh na tagairtí sa `String` bailí. Cuimhnigh
an fabht sa chlár i Liostú 4-8, nuair a fuair muid an t-innéacs go dtí deireadh an
chéad fhocal ach ansin glanta an teaghrán mar sin bhí ár n-innéacs neamhbhailí? Bhí an cód sin
mícheart go loighciúil ach níor léirigh sé aon earráidí láithreach. Bheadh ​​na fadhbanna
thaispeáint suas níos déanaí má choinnigh muid ag iarraidh úsáid a bhaint as an chéad fhocal innéacs le fholmhú
teaghrán. Déanann slisní an fabht seo dodhéanta agus cuirimid in iúl dúinn go bhfuil fadhb againn leis
ár gcód i bhfad níos luaithe. Ag baint úsáide as an leagan slise de `first_word` caithfear a
earráid ama tiomsaithe:

<Listing file-name="src/main.rs">

```rust,ignore,does_not_compile
{{#rustdoc_include ../../listings/ch04-understanding-ownership/no-listing-19-slice-error/src/main.rs:here}}
```

</Listing>

Seo é earráid an tiomsaitheora:

```console
{{#include ../../listings/ch04-understanding-ownership/no-listing-19-slice-error/output.txt}}
```

A thabhairt chun cuimhne ó na rialacha iasachtaithe go má tá tagairt do-inaistrithe againn do
rud éigin, ní féidir linn tagairt mutable a ghlacadh freisin. Toisc go bhfuil gá le `clear`
gearr an `String`, ní mór dó tagairt mutable a fháil. An `println!`
tar éis an ghlao go `clear` úsáideann an tagairt i `word`, mar sin an do-athlasach
ní mór tagairt a bheith gníomhach fós ag an bpointe sin. Dícheadaíonn meirge an mutable
tagairt in `clear` agus an tagairt do-athluaite i `word` as atá ann cheana féin ag an
am céanna, agus teipeann ar an tiomsú. Ní hamháin go bhfuil Rust tar éis ár n-API a dhéanamh níos éasca le húsáid,
ach chuir sé deireadh freisin le haicme iomlán earráidí ag am tiomsaithe!

<!-- Old heading. Do not remove or links may break. -->

<a id="string-literals-are-slices"></a>

#### Teaghrán Liteartha mar Slisní

Thabhairt chun cuimhne gur labhair muid faoi litreacha teaghrán á stóráil taobh istigh den dénártha. Anois
go bhfuil a fhios againn faoi slisní, is féidir linn a thuiscint i gceart litreacha teaghrán:

```rust
let s = "Hello, world!";
```

Is é an cineál `s` anseo ná `&str`: is slice é a dhíríonn ar an bpointe sonrach sin de
an dénártha. Is é seo freisin an fáth go bhfuil sreang-litreacha do-athlasach; Is é `&str`
tagairt do- immutable.

#### Sliseanna Teaghrán mar Pharaiméadair

Má bhíonn a fhios agat gur féidir leat slisní liteartha a ghlacadh agus luachanna `String` is féidir linn
feabhas amháin eile ar `first_word`, agus sin é a shíniú:

```rust,ignore
fn first_word(s: &String) -> &str {
```

Scríobhfadh Rustacean le níos mó taithí an síniú a thaispeántar i Liostú 4-9
ina ionad sin toisc go ligeann sé dúinn an fheidhm chéanna a úsáid ar an dá luach `&String`
agus luachanna `&str`.

<Listing number="4-9" caption="Improving the `first_word` function by using a string slice for the type of the `s` parameter">

```rust,ignore
{{#rustdoc_include ../../listings/ch04-understanding-ownership/listing-04-09/src/main.rs:here}}
```

</Listing>

Má tá slisne teaghrán againn, is féidir linn é sin a chur ar aghaidh go díreach. Má tá `String` againn, táimid
is féidir leat slice den `String` nó tagairt don `String` a chur ar aghaidh. seo
baineann solúbthacht leas as _deref coercions_, gné a chlúdóimid sa
[“Comhéigeantais Fóirne intuigthe le Feidhmeanna agus
Modhanna”][deref-coercions]<!-- neamhaird--> alt de Chaibidil 15.

Feidhm a shainiú chun sreangshlis a ghlacadh in ionad tagairt do `String`
a dhéanann ár n-API níos ginearálta agus níos úsáidí gan aon fheidhmiúlacht a chailliúint:

<Listing file-name="src/main.rs">

```rust
{{#rustdoc_include ../../listings/ch04-understanding-ownership/listing-04-09/src/main.rs:usage}}
```

</Listing>

### Sliseanna Eile

Baineann slisní teaghrán, mar a d'fhéadfá a shamhlú, go sonrach le teaghráin. Ach tá a
cineál slice níos ginearálta freisin. Smaoinigh ar an eagar seo:

```rust
let a = [1, 2, 3, 4, 5];
```

Díreach mar a d’fhéadfadh gur mhaith linn tagairt a dhéanamh do chuid de shraith, b’fhéidir gur mhaith linn tagairt a dhéanamh
chuid d'eagar. Dhéanfaimis mar seo:

```rust
let a = [1, 2, 3, 4, 5];

let slice = &a[1..3];

assert_eq!(slice, &[2, 3]);
```

Tá an cineál `&[i32]` ar an sliseog seo. Oibríonn sé ar an mbealach céanna is a dhéanann slisní teaghrán, trí
ag stóráil tagairt don chéad eilimint agus fad. Bainfidh tú úsáid as an gcineál seo
slice do gach cineál bailiúcháin eile. Déanfaimid plé ar na bailiúcháin seo i
mionsonraí nuair a labhraímid faoi veicteoirí i gCaibidil 8.

## Achoimre

Cinntíonn coincheapa na húinéireachta, na hiasachta, agus na slisní sábháilteacht cuimhne i Rust
cláir ag am tiomsaithe. Tugann an teanga Rust smacht duit ar do chuimhne
úsáid ar an mbealach céanna le teangacha ríomhchláraithe córais eile, ach a bhfuil an
úinéir na sonraí a ghlanadh suas go huathoibríoch na sonraí sin nuair a théann an t-úinéir as raon feidhme
ciallaíonn sé seo nach gá duit cód breise a scríobh agus a dhífhabhtú chun an rialú seo a fháil.

Bíonn tionchar ag úinéireacht ar an gcaoi a n-oibríonn go leor codanna eile de Rust, mar sin labhróimid faoi
na coincheapa seo níos faide ar fud an chuid eile den leabhar. Bogaimis ar aghaidh go dtí
Caibidil 5 agus féach ar phíosaí sonraí a ghrúpáil le chéile i `struct`.

[ch13]: ch13-02-iterators.html
[ch6]: ch06-02-match.html#patterns-that-bind-to-values
[strings]: ch08-02-strings.html#storing-utf-8-encoded-text-with-strings
[deref-coercions]: ch15-02-deref.html#implicit-deref-coercions-with-functions-and-methods

