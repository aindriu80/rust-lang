## Áirimh a shainiú

Nuair a thugann struchtúir bealach duit réimsí agus sonraí gaolmhara a ghrúpáil le chéile, mar shampla
`Rectangle` lena `width` agus `height`, tugann enums bealach duit le rá a
tá luach ar cheann de shraith luachanna féideartha. Mar shampla, b’fhéidir gur mhaith linn é sin a rá
Tá `Rectangle` ar cheann de shraith cruthanna féideartha a chuimsíonn `Circle` agus
`Triangle`. Chun seo a dhéanamh, ligeann Rust dúinn na féidearthachtaí seo a ionchódú mar enum.

Breathnaímis ar chás b’fhéidir gur mhaith linn a chur in iúl i gcód agus féachaimis cén fáth a bhfuiltear ag súil leis
úsáideach agus níos oiriúnaí ná na struchtúir sa chás seo. Abair go gcaithfimid oibriú
le seoltaí IP. Faoi láthair, úsáidtear dhá mhórchaighdeán le haghaidh seoltaí IP:
leagan a ceathair agus leagan a sé. Toisc gurb iad seo na féidearthachtaí amháin le haghaidh an
Seoladh IP a dtiocfaidh ár gclár trasna air, is féidir linn _enurate_ gach is féidir
leagan, agus is é sin an áit a fhaigheann an áirimh a ainm.

Féadfaidh seoladh IP a bheith ina sheoladh a ceathair nó ina sheoladh leagan a sé, ach ní féidir
araon ag an am céanna. Déanann an mhaoin sin de sheoltaí IP na sonraí enum
struchtúr oiriúnach toisc nach féidir le luach enum ach a bheith mar cheann dá leagan.
Tá seoltaí leagan a ceathair agus leagan a sé fós go bunúsach IP
seoltaí, mar sin ba chóir iad a láimhseáil mar an cineál céanna nuair a bhíonn an cód á láimhseáil
cásanna a bhaineann le seoladh IP de chineál ar bith.

Is féidir linn an coincheap seo a chur in iúl i gcód trí áireamh `IpAddrKind` agus
ag liostú na cineálacha féideartha is féidir le seoladh IP a bheith, `V4` agus `V6`. Seo iad na
leaganacha den enum:

```rust
{{#rustdoc_include ../../listings/ch06-enums-and-pattern-matching/no-listing-01-defining-enums/src/main.rs:def}}
```

Is cineál sonraí saincheaptha é `IpAddrKind` anois is féidir linn a úsáid in áit eile dár gcód.

### Luachanna Enum

Is féidir linn cásanna a chruthú de gach ceann den dá leagan de `IpAddrKind` mar seo:

```rust
{{#rustdoc_include ../../listings/ch06-enums-and-pattern-matching/no-listing-01-defining-enums/src/main.rs:instance}}
```

Tabhair faoi deara go bhfuil leaganacha an enum spásáilte faoina aitheantóir, agus táimid
úsáid a bhaint as idirstad dúbailte chun an dá cheann a scaradh. Tá sé seo úsáideach mar anois an dá luachanna
Tá `IpAddrKind::V4` agus `IpAddrKind::V6` den chineál céanna: `IpAddrKind`. muid
is féidir ansin, mar shampla, feidhm a shainiú a ghlacann aon `IpAddrKind`:

```rust
{{#rustdoc_include ../../listings/ch06-enums-and-pattern-matching/no-listing-01-defining-enums/src/main.rs:fn}}
```

Agus is féidir linn an fheidhm seo a thabhairt le ceachtar den dá leagan:

```rust
{{#rustdoc_include ../../listings/ch06-enums-and-pattern-matching/no-listing-01-defining-enums/src/main.rs:fn_call}}
```

Tá buntáistí níos mó fós ag baint le húsáid enums. Ag smaoineamh níos mó ar ár gcineál seoladh IP,
faoi ​​láthair níl bealach againn chun an seoladh IP iarbhír _data_ a stóráil; againn
níl a fhios ach cén _chineál_ atá ann. Ós rud é gur fhoghlaim tú díreach faoi structs i
Caibidil 5, seans go mbeidh cathú ort dul i ngleic leis an bhfadhb seo le struchtúir mar a léirítear i
Liostáil 6-1.

<Listing number="6-1" caption="Storing the data and `IpAddrKind` variant of an IP address using a `struct`">

```rust
{{#rustdoc_include ../../listings/ch06-enums-and-pattern-matching/listing-06-01/src/main.rs:here}}
```

</Listing>

Anseo, tá struchtúr `IpAddr` sainmhínithe againn a bhfuil dhá réimse ann: réimse `kind` a
is den chineál `IpAddrKind` (an enum a shainmhínigh muid roimhe seo) agus réimse `address`
den chineál `String`. Tá dhá chás den struchtúr seo againn. Is é an chéad cheann ná `home`,
agus tá an luach `IpAddrKind::V4` mar a `kind` agus seoladh gaolmhar aige
sonraí de `127.0.0.1`. Is é an dara cás ná `loopback`. Tá an ceann eile aige
leagan de `IpAddrKind` mar a luach `kind`, `V6`, agus tá seoladh `::1` aige
bhaineann leis. Bhaineamar úsáid as struchtúr chun an `kind` agus an `address` a chumhdach
luachanna le chéile, mar sin anois tá baint ag an malairt leis an luach.

Mar sin féin, tá sé níos gonta an coincheap céanna a léiriú ag baint úsáide as enum amháin:
seachas enum taobh istigh de struchtúr, is féidir linn sonraí a chur go díreach i ngach enum
athraitheach. Deir an sainmhíniú nua seo ar an `IpAddr` enum go bhfuil `V4` agus `V6` araon
beidh luachanna `String` gaolmhar ag leagan:

```rust
{{#rustdoc_include ../../listings/ch06-enums-and-pattern-matching/no-listing-02-enum-with-data/src/main.rs:here}}
```

Ceangaimid sonraí go díreach le gach leagan den enum, mar sin níl aon ghá le
struchtúr breise. Anseo, tá sé níos éasca sonraí eile a fheiceáil faoin gcaoi a n-oibríonn enums:
déantar feidhm freisin d'ainm gach athraitheach enum a shainímid
Tógann sampla den enum. Is é sin, is glao feidhme é `IpAddr::V4()`
a thógann argóint `String` agus a thugann sampla den chineál `IpAddr` ar ais. muid
a fháil go huathoibríoch an fheidhm cruthaitheoir sainithe mar thoradh ar shainiú an
áim.

Tá buntáiste eile ag baint le enum seachas struchtúr a úsáid: gach leagan
is féidir cineálacha agus méideanna éagsúla sonraí gaolmhara a bheith ann. Leagan a ceathair IP
beidh ceithre chomhpháirt uimhriúla ag seoltaí a mbeidh luachanna acu i gcónaí
idir 0 agus 255. Dá dteastódh uainn seoltaí `V4` a stóráil mar cheithre luach `u8` ach
fós seoltaí `V6` a chur in iúl mar luach `String` amháin, ní bheimis in ann é a dhéanamh
a struchtúr. Láimhseálann Enums an cás seo gan stró:

```rust
{{#rustdoc_include ../../listings/ch06-enums-and-pattern-matching/no-listing-03-variants-with-different-data/src/main.rs:here}}
```

Tá roinnt bealaí éagsúla léirithe againn chun struchtúir sonraí a shainiú chun an leagan a stóráil
ceithre agus leagan sé seoltaí IP. Mar sin féin, mar a casadh sé amach, ar mian leo a stóráil
Seoltaí IP agus ionchódaigh cén cineál iad atá chomh coitianta go bhfuil sainmhíniú ar [an leabharlann 
chaighdeánach is féidir linn a úsáid!][IpAddr]<!-- neamhaird a dhéanamh --> Breathnaímid ar conas
sainmhíníonn an leabharlann chaighdeánach `IpAddr`: tá an enum agus na leaganacha beacht aige sin
atá sainmhínithe agus úsáidte againn, ach neadaíonn sé na sonraí seolta laistigh de na leaganacha isteach
i bhfoirm dhá struchtúr éagsúla, atá sainmhínithe go difriúil do gach ceann acu
leagan:

```rust
struct Ipv4Addr {
    // --snip--
}

struct Ipv6Addr {
    // --snip--
}

enum IpAddr {
    V4(Ipv4Addr),
    V6(Ipv6Addr),
}
```

Léiríonn an cód seo gur féidir leat sonraí de chineál ar bith a chur taobh istigh de mhalairt enum:
teaghráin, cineálacha uimhriúla, nó struchtúir, mar shampla. Is féidir leat fiú ceann eile a áireamh
uaim! Chomh maith leis sin, is minic nach mbíonn cineálacha caighdeánacha leabharlainne i bhfad níos casta ná
cad a d'fhéadfá teacht suas leis.

Tabhair faoi deara, cé go bhfuil sainmhíniú ar `IpAddr` sa ghnáthleabharlann,
is féidir linn ár sainmhíniú féin a chruthú agus a úsáid go fóill gan coinbhleacht mar gheall orainn
nár thug muid sainmhíniú caighdeánach na leabharlainne isteach inár raon feidhme. Labhróimid
tuilleadh faoi chineálacha a thabhairt isteach sa raon feidhme i gCaibidil 7 .

Breathnaímid ar shampla eile d’enum i Liostú 6-2: tá réimse leathan ag an gceann seo
éagsúlacht na gcineálacha atá leabaithe ina leagan.

<Listing number="6-2" caption="A `Message` enum whose variants each store different amounts and types of values">

```rust
{{#rustdoc_include ../../listings/ch06-enums-and-pattern-matching/listing-06-02/src/main.rs:here}}
```

</Listing>

Tá ceithre leagan ag an enum seo le cineálacha éagsúla:

- Níl aon sonraí ag `Quit` a bhaineann leis ar chor ar bith.
- Tá réimsí ainmnithe ag `Move`, mar a dhéanann struchtúr.
- Cuimsíonn `Write` `String` singil.
- Áirítear le `ChangeColor` trí luach `i32`.

Tá sé cosúil le sainiú ainim le malairtí ar nós na cinn i Liosta 6-2
cineálacha éagsúla sainmhínithe struchtúir a shainmhíniú, ach amháin ní úsáideann an enum an
eochairfhocal `struct` agus déantar na leaganacha go léir a ghrúpáil le chéile faoin `Message`
cineál. D'fhéadfadh na sonraí céanna a bheith sna struchtúir seo a leanas agus a bhí sa enum roimhe seo
sealbhaíonn leagan:

```rust
{{#rustdoc_include ../../listings/ch06-enums-and-pattern-matching/no-listing-04-structs-similar-to-message-enum/src/main.rs:here}}
```

Ach má úsáidimid na struchtúir éagsúla, a bhfuil a chineál féin ag gach ceann acu, ní mór dúinn
Níorbh fhéidir feidhm a shainiú chomh héasca chun aon cheann de na cineálacha teachtaireachtaí seo a ghlacadh agus
d'fhéadfaimis leis an `Message` enum a shainmhínítear i Liostú 6-2, ar cineál amháin é.

Tá cosúlacht amháin eile idir enums agus struchtúir: díreach mar is féidir linn
modhanna a shainiú ar struchtúir ag baint úsáide as `impl`, táimid in ann modhanna a shainiú ar
éinim. Seo modh darb ainm ‘glaoch’ a d’fhéadfaimis a shainiú ar ár ‘Teachtaireacht’ enum:

```rust
{{#rustdoc_include ../../listings/ch06-enums-and-pattern-matching/no-listing-05-methods-on-enums/src/main.rs:here}}
```

D'úsáidfeadh corp an mhodha `self` chun an luach a thugamar ar an
modh ar. Sa sampla seo, chruthaíomar athróg `m` a bhfuil an luach aige
`Message::Write(String::from("hello"))`, agus sin an rud a bheidh `self` sa
corp an mhodha `call` nuair a ritheann `m.call()`.

Breathnaímid ar enum eile sa leabharlann chaighdeánach atá an-choitianta agus
úsáideach: `Option`.

### An `Option` Enum agus a Buntáistí thar Luachanna Neamhnithe

Scrúdaíonn an chuid seo cás-staidéar ar `Option`, a bhfuil sainmhíniú eile air
ag an leabharlann chaighdeánach. Ionchódaíonn an cineál `Option` an cás an-choitianta i
a d'fhéadfadh a bheith ina luach rud éigin nó d'fhéadfadh sé a bheith rud ar bith.

Mar shampla, má iarrann tú an chéad mhír ar liosta neamhfholamh, gheobhaidh tú
luach. Má iarrann tú an chéad mhír ar liosta folamh, ní bhfaighfeá rud ar bith.
Is féidir leis an tiomsaitheoir an coincheap seo a chur in iúl i dtéarmaí an chórais chineáil
seiceáil an bhfuil gach cás ba cheart duit a láimhseáil láimhseáilte agat; seo
is féidir le feidhmiúlacht cosc ​​a chur ar fhabhtanna atá thar a bheith coitianta i gcláir eile
teangacha.

Is minic a smaoinítear ar dhearadh teanga ríomhchláraithe i dtéarmaí na ngnéithe atá agat
san áireamh, ach tá na gnéithe a eisiamh tú tábhachtach freisin. Níl an meirge ag meirge
null gné atá ag go leor teangacha eile. Is luach é _Null_ a chiallaíonn ann
níl aon luach ann. I dteangacha le null, is féidir athróga a bheith i gceann de na hathróga i gcónaí
dhá stát: neamhní nó neamh-null.

Ina chur i láthair in 2009 “Null References: The Billion Dollar Mistake,” Tony
Tá sé seo le rá ag Hoare, aireagóir null:

> Tugaim mo bhotún billiún dollar air. Ag an am sin, bhí mé ag dearadh an chéad cheann
> cineál córas cuimsitheach le haghaidh tagairtí i dteanga atá dírithe ar oibiachtaí. Mo
> Ba é an sprioc ná a chinntiú gur chóir go mbeadh gach úsáid a bhaintear as teistiméireachtaí go hiomlán sábháilte, le
> seiceáil a dhéanann an tiomsaitheoir go huathoibríoch. Ach ní raibh mé in ann cur i gcoinne
> temptation tagairt ar neamhní a chur isteach, go simplí toisc go raibh sé chomh héasca sin
> chur i bhfeidhm. Mar thoradh air seo tá líon mór earráidí, leochaileachtaí agus córais
> tuairteanna, a ba chúis dócha billiún dollar de pian agus damáiste i
> daichead bliain anuas.

Is í an fhadhb le luachanna nialasach ná má dhéanann tú iarracht luach nialasach a úsáid mar
luach neamh-null, gheobhaidh tú earráid de chineál éigin. Mar gheall ar seo ar neamhní nó-null
tá an mhaoin forleatach, tá sé thar a bheith éasca earráid den chineál seo a dhéanamh.

Mar sin féin, tá an coincheap atá null ag iarraidh a chur in iúl fós úsáideach: a
Is luach é null atá neamhbhailí faoi láthair nó atá as láthair ar chúis éigin.

Ní bhaineann an fhadhb leis an gcoincheap i ndáiríre ach leis an ábhar ar leith
cur i bhfeidhm. Mar sin, níl nulls ag Rust, ach tá enum aige
ar féidir leis an gcoincheap luach a bheith i láthair nó as láthair a ionchódú. Tá an enum seo
`Rogha<T>`, agus [sainmhínítear é sa ghnáthleabharlann][option]<!-- neamhaird a dhéanamh ar -->
mar seo a leanas:

```rust
enum Option<T> {
    None,
    Some(T),
}
```

Tá an `Option<T>` enum chomh húsáideach sin go bhfuil sé san áireamh fiú sa réamhrá; leat
ní gá é a thabhairt isteach sa raon feidhme go sainráite. Tá a leagan san áireamh freisin i
an réamhrá: is féidir leat `Some` agus `None` a úsáid go díreach gan an `Option::`
réimír. Níl sa `Option<T>` enum fós ach áithne rialta, agus `Some(T)` agus
Is leaganacha den chineál `Option<T>` iad `none` fós.

Is gné de Rust é an chomhréir `<T>` nár labhair muid faoi go fóill. Tá sé a
paraiméadar cineálach, agus clúdóimid cineálacha níos mionsonraithe i gCaibidil 10.
Faoi láthair, níl a fhios agat ach go gciallaíonn `<T>` gurb é an leagan `Some` de
is féidir leis an enum `Option` píosa amháin sonraí a choinneáil d'aon chineál, agus go bhfuil gach ceann acu
de chineál coincréite a úsáidtear in ionad `T` a dhéanann an cineál foriomlán `Option<T>`
cineál difriúil. Seo roinnt samplaí de luachanna `Option` a úsáid le coinneáil
cineálacha uimhreacha agus cineálacha ruaille:

```rust
{{#rustdoc_include ../../listings/ch06-enums-and-pattern-matching/no-listing-06-option-examples/src/main.rs:here}}
```

Is é `Option<i32>` an ​​cineál `some_number`. Is é an cineál `some_char`
`Option<char>`, ar cineál difriúil é. Is féidir le meirge tátal a bhaint as na cineálacha seo toisc
tá luach sonraithe againn laistigh den leagan `Some`. Le haghaidh `absent_number`, Rust
éilíonn orainn an cineál foriomlán `Option` a anó: ní féidir leis an tiomsaitheoir an tátal a bhaint as
clóscríobh go gcoimeádfaidh an leagan comhfhreagrach `Some` trí bhreathnú ar a
luach `none`. Anseo, insíonn muid do Rust go bhfuil i gceist againn go mbeadh `absent_number` de chineál
`Option<i32>`.

Nuair a bhíonn luach `Some` againn, tá a fhios againn go bhfuil luach i láthair agus go bhfuil an luach ann
ar siúl laistigh den `Some`. Nuair a bhíonn luach `None` againn, i gciall éigin ciallaíonn sé an
rud céanna le null: níl luach bailí againn. Mar sin cén fáth a bhfuil `Option<T>` agat
ar bith níos fearr ná null a bheith agat?

I mbeagán focal, toisc go bhfuil `Option<T>` agus `T` (áit ar féidir `T` a bheith de chineál ar bith) difriúil
cineálacha, ní ligfidh an tiomsaitheoir dúinn luach `Option<T>` a úsáid amhail is dá mba é
cinnte luach bailí. Mar shampla, ní thiomsóidh an cód seo, toisc go bhfuil
ag iarraidh `i8` a chur le `Option<i8>`:

```rust,ignore,does_not_compile
{{#rustdoc_include ../../listings/ch06-enums-and-pattern-matching/no-listing-07-cant-use-option-directly/src/main.rs:here}}
```

Má rithimid an cód seo, faighimid teachtaireacht earráide mar an gceann seo:

```console
{{#include ../../listings/ch06-enums-and-pattern-matching/no-listing-07-cant-use-option-directly/output.txt}}
```

Go dian! Go bunúsach, ciallaíonn an teachtaireacht earráide seo nach dtuigeann Rust conas
chun `i8` agus `Option<i8>` a chur leis, toisc gur cineálacha éagsúla iad. Nuair a bheidh muid
a bhfuil luach de chineál cosúil le `i8` i Rust, cinnteoidh an tiomsaitheoir go mbeidh muid
luach bailí i gcónaí. Is féidir linn dul ar aghaidh go muiníneach gan seiceáil a dhéanamh
le haghaidh null roimh an luach sin a úsáid. Go dtí go bhfuil `Option<i8>` againn (nó
cibé cineál luacha a bhfuilimid ag obair leis) an gcaithfidh muid a bheith buartha faoi b'fhéidir
gan luach, agus cinnteoidh an tiomsaitheoir go ndéileálfaimid leis an gcás sin roimhe seo
ag baint úsáide as an luach.

I bhfocail eile, caithfidh tú `Option<T>` a thiontú go `T` sular féidir leat
oibríochtaí `T` a dhéanamh leis. Go ginearálta, cuidíonn sé seo le breith ar cheann de na cinn is mó
ceisteanna coitianta le null: ag glacadh leis nach bhfuil rud éigin ar neamhní nuair atá sé i ndáiríre.

Má dhéantar an baol a bhaineann le luach neamhneal a ghlacadh go mícheart, cabhraíonn sé leat a bheith
níos mó muiníne i do chód. D'fhonn go mbeadh luach is féidir a bheith b'fhéidir
null, ní mór duit liostáil go sainráite tríd an gcineál luacha sin a dhéanamh `Option<T>`.
Ansin, nuair a úsáideann tú an luach sin, ceanglaítear ort an cás a láimhseáil go sainráite
nuair a bhíonn an luach nialasach. I ngach áit go bhfuil luach ag cineál nach bhfuil
`Option<T>`, glacann tú leis go sábháilte nach bhfuil an luach ar neamhní. Bhí sé seo a
cinneadh dearaidh d’aon ghnó do Rust teorainn a chur le forleatach agus méadú null
sábháilteacht an chóid meirge.

Mar sin, conas a fhaigheann tú an luach `T` as leagan `Some` nuair a bhíonn luach agat
den chineál `Option<T>` ionas gur féidir leat an luach sin a úsáid? Tá a
líon mór modhanna atá úsáideach i gcásanna éagsúla; is féidir leat
seiceáil iad ina [a cháipéisíocht][docs] <!-- neamhaird -->. Ag éirí eolach
leis na modhanna ar `Option<T>` beidh siad thar a bheith úsáideach i do thuras le
Meirge.

Go ginearálta, chun luach `Option<T>` a úsáid, ba mhaith leat cód a bheith agat
láimhseálfaidh gach leagan. Ba mhaith leat roinnt cód a bheidh ar siúl ach amháin nuair a bheidh agat
Luach `Some(T)`, agus ceadaítear don chód seo an `T` istigh a úsáid. Ba mhaith leat roinnt
cód eile le rith mura bhfuil luach `None` agat, agus mura bhfuil a
luach `T` ar fáil. Is éard atá sa slonn `match` ná tógáil ar shreabhadh rialaithe a dhéanann
déanann sé seo go díreach nuair a úsáidtear é le enums: beidh sé ag rith cód difriúil ag brath ar
cén leagan den enum atá aige, agus is féidir leis an gcód sin úsáid a bhaint as na sonraí taobh istigh den
luach meaitseála.

[IpAddr]: ../std/net/enum.IpAddr.html
[option]: ../std/option/enum.Option.html
[docs]: ../std/option/enum.Option.html











