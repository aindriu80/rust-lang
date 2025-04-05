## Sraith Míreanna a Phróiseáil le hIterators

Ceadaíonn an patrún atriator duit tasc éigin a dhéanamh ar sheicheamh míreanna i
cas. Bíonn iterator freagrach as loighic atriallta thar gach mír agus
ag cinneadh cathain a bheidh an seicheamh críochnaithe. Nuair a úsáideann tú atrialltóirí, ní dhéanann tú
caithfidh tú an loighic sin a chur i bhfeidhm duit féin.

I Rust, tá iterators _lazy_, rud a chiallaíonn nach bhfuil aon éifeacht acu go dtí go ghlaonn tú
modhanna a ídíonn an t-iterator chun é a úsáid suas. Mar shampla, an cód i
Cruthaíonn liostú 13-10 atrialltóir thar na míreanna sa veicteoir `v1` trí ghlaoch a chur air
an modh `iter` arna shainmhíniú ar `Vec<T>`. Ní dhéanann an cód seo ann féin rud ar bith
úsáideach.

<Listing number="13-10" file-name="src/main.rs" caption="Creating an iterator">

```rust
{{#rustdoc_include ../../listings/ch13-functional-features/listing-13-10/src/main.rs:here}}
```

</Listing>

Stóráiltear an t-iterator san athróg `v1_iter`. Chomh luath agus atá cruthaithe againn
iterator, is féidir linn é a úsáid ar bhealaí éagsúla. I Liosta 3-5 i gCaibidil 3, táimid
atriallta thar eagar ag baint úsáide as lúb `for` chun roinnt cód a fhorghníomhú ar gach ceann dá chuid
míreanna. Faoin gcochall chruthaigh sé seo go hintuigthe agus ansin d'ól sé iterator,
ach rinneamar glóir ar conas go díreach a oibríonn sé sin go dtí seo.

Sa sampla i Liostú 13-11, scaraimid cruthú an atriartóra ó
úsáid an iterator sa lúb `for`. Nuair a thugtar an lúb `for` ag baint úsáide as
an t-iterator in `v1_iter`, úsáidtear gach eilimint san aitreoir i gceann amháin
atriallta na lúb, a phriontaí amach gach luach.

<Listing number="13-11" file-name="src/main.rs" caption="Using an iterator in a `for` loop">

```rust
{{#rustdoc_include ../../listings/ch13-functional-features/listing-13-11/src/main.rs:here}}
```

</Listing>

I dteangacha nach bhfuil aitritheoirí curtha ar fáil ag a leabharlanna caighdeánacha,
is dócha go scríobhfá an fheidhmiúlacht chéanna seo trí athróg a thosú ag innéacs
0, ag baint úsáide as an athróg sin chun innéacsú isteach sa veicteoir chun luach a fháil, agus
ag incrimintiú an luach athraitheach i lúb go dtí go shroich sé líon iomlán na
míreanna sa veicteoir.

Láimhseálann iterators an loighic sin ar fad duit, ag gearradh síos ar chód athchleachtach duit
d'fhéadfadh praiseach a dhéanamh. Tugann iterators níos mó solúbthachta duit úsáid a bhaint as an gcéanna
loighic le go leor cineálacha éagsúla de sheichimh, ní hamháin struchtúir sonraí is féidir leat
innéacs isteach, cosúil le veicteoirí. Déanaimis scrúdú ar an gcaoi a ndéanann atrialltóirí é sin.

### An `Iterator` Trait agus an `next` Modh

Cuireann gach iterator trait darb ainm `Iterator` i bhfeidhm a shainmhínítear sa
leabharlann caighdeánach. Breathnaíonn an sainmhíniú ar an trait mar seo:

```rust
pub trait Iterator {
    type Item;

    fn next(&mut self) -> Option<Self::Item>;

    // methods with default implementations elided
}
```

Tabhair faoi deara go n-úsáideann an sainmhíniú seo roinnt comhréire nua: `type Item` agus `Self::Item`,
atá ag sainmhíniú cineál _a bhaineann_ leis an tréith seo. Labhróimid faoi
cineálacha gaolmhara go domhain i gCaibidil 20. Faoi láthair, níl a fhios agat ach go bhfuil
deir an cód seo go gcaithfidh tú sainmhíniú a thabhairt freisin chun an trait `Iterator` a chur i bhfeidhm cineál `Item`, agus úsáidtear an cineál `Item` seo sa chineál tuairisceáin den `next`
modh. I bhfocail eile, is é an cineál `Item` an cineál a sheoltar ar ais ón
iterator.

Ní éilíonn an tréith `Iterator` ach ar ghníomhaithe modh amháin a shainiú: an
modh `next`, a sheolann mír amháin den aterator ar ais ag am fillte isteach
`Some` agus, nuair a bhíonn an atriall thart, filleann sé `None`.

Is féidir linn an modh `next` a ghlaoch ar iterators go díreach; Léiríonn liostú 13-12
cad iad na luachanna a sheoltar ar ais ó ghlaonna arís agus arís eile go `next` ar an iterator a cruthaíodh
ón veicteoir.

<Listing number="13-12" file-name="src/lib.rs" caption="Calling the `next` method on an iterator">

```rust,noplayground
{{#rustdoc_include ../../listings/ch13-functional-features/listing-13-12/src/lib.rs:here}}
```

</Listing>

Tabhair faoi deara go gcaithfimid `v1_iter` mutable a dhéanamh: ag glaoch ar an modh `next` ar an
athraíonn iterator staid inmheánach a úsáideann an t-iterator chun súil a choinneáil ar cá háit
tá sé san ord. I bhfocail eile, _ídíonn an cód seo_, nó úsáideann suas, an
iterator. Itheann gach glao go dtí an chéad uair eile mír ón aterator. Ní raibh gá againn
chun `v1_iter` a dhéanamh mutable nuair a d'úsáideamar lúb `for` toisc gur ghlac an lúb
úinéireacht `v1_iter` agus rinne sé a athrú taobh thiar de na pictiúir.

Tabhair faoi deara freisin go bhfuil na luachanna a fhaighimid ó na glaonna go `next` neamh-inaistrithe
tagairtí do na luachanna sa veicteoir. Táirgeann an modh `iter` iterator
thar thagairtí domhalartaithe. Más mian linn a chruthú iterator a thógann
úinéireacht `v1` agus luachanna úinéireachta á dtabhairt ar ais, is féidir linn `into_iter` a thabhairt air ina ionad
`iter`. Ar an gcaoi chéanna, más mian linn tagairtí mutable a athrá, is féidir linn glaoch
`iter_mut` in ionad `iter`.

### Modhanna a ídíonn an t-Iterator

Tá roinnt modhanna éagsúla ag an tréith `Iterator` le réamhshocrú
feidhmiúcháin a sholáthraíonn an leabharlann chaighdeánach; is féidir leat eolas a fháil orthu seo
Tríd an doiciméadú caighdeánach API leabharlainne a chuardach don `Iterator`
trait. Tugann cuid de na modhanna seo an modh `next` ina sainmhíniú, a
is é sin an fáth go bhfuil ort an modh `next` a chur i bhfeidhm agus tú ag cur an tréith `Iterator`.

Tugtar _oiriúnóirí ídithe_ ar mhodhanna a dtugann `next` orthu, toisc iad a bheith ag glaoch orthu
úsáideann suas an t-iterator. Sampla amháin is ea an modh `sum`, a ghlacann úinéireacht air
an iterator agus atriates trí na míreanna trí ghlaoch arís agus arís eile `next`, mar sin
ag caitheamh an iterator. De réir mar a atrialltar tríd, cuireann sé gach mír le rith
iomlán agus cuireann sé an t-iomlán ar ais nuair a bhíonn atriall críochnaithe. I liostú 13-13 tá a
tástáil a léiríonn úsáid an mhodha `sum`:

<Listing number="13-13" file-name="src/lib.rs" caption="Calling the `sum` method to get the total of all items in the iterator">

```rust,noplayground
{{#rustdoc_include ../../listings/ch13-functional-features/listing-13-13/src/lib.rs:here}}
```

</Listing>

Níl cead againn `v1_iter` a úsáid tar éis an ghlao chun `sum` a dhéanamh toisc go dtógann `sum`
úinéireacht an iterator ar a dtugaimid é.

### Modhanna a Tháirgeann Iterators Eile

Is modhanna iad _Iterator adapters_ arna sainmhíniú ar an trait `Iterator` nach bhfuil
ithe an iterator. Ina áit sin, táirgeann siad iterators éagsúla trí athrú
gné éigin den iterator bunaidh.

Léiríonn liostú 13-14 sampla de ghlaoch ar an modh cuibheora iterator `map`,
a thógann dúnadh chun glaoch ar gach mír de réir mar a atrialltar na míreanna tríd.
Tugann an modh `map` atriar nua ar ais a tháirgeann na hearraí mionathraithe. Tá an
Cruthaíonn dúnadh anseo iterator nua ina mbeidh gach mír as an veicteoir
méadaithe ag 1:

<Listing number="13-14" file-name="src/main.rs" caption="Calling the iterator adapter `map` to create a new iterator">

```rust,not_desired_behavior
{{#rustdoc_include ../../listings/ch13-functional-features/listing-13-14/src/main.rs:here}}
```

</Listing>

Mar sin féin, tugann an cód seo rabhadh:

```console
{{#include ../../listings/ch13-functional-features/listing-13-14/output.txt}}
```

Ní dhéanann an cód i Liostú 13-14 faic; an dúnadh atá sonraithe againn
ní chuirtear glaoch riamh air. Cuireann an rabhadh i gcuimhne dúinn cén fáth: tá cuibheoirí iterator leisciúil, agus
caithfimid an iterator a ithe anseo.

Chun an rabhadh seo a shocrú agus an t-iteadóir a ithe, úsáidfimid an modh `collect`,
a d’úsáideamar i gCaibidil 12 le `env::args` i Liostú 12-1. An modh seo
ídíonn sé an t-iterator agus bailíonn sé na luachanna mar thoradh air i mbailiúchán sonraí
cineál.

I Liostáil 13-15, bailímid torthaí atriallta thar an atriallta sin
ar ais ón nglao go dtí `map` isteach i veicteoir. Beidh deireadh leis an veicteoir seo
ina bhfuil gach ítim as an veicteoir bunaidh méadaithe faoi 1.

<Listing number="13-15" file-name="src/main.rs" caption="Calling the `map` method to create a new iterator and then calling the `collect` method to consume the new iterator and create a vector">

```rust
{{#rustdoc_include ../../listings/ch13-functional-features/listing-13-15/src/main.rs:here}}
```

</Listing>

Toisc go dtógann `map` dúnadh, is féidir linn aon oibríocht ba mhaith linn a dhéanamh a shonrú
ar gach mír. Is sampla iontach é seo ar an gcaoi a ligeann dúnadh duit roinnt a shaincheapadh
iompar agus an t-iompar atriallta á athúsáid ag an trait `Iterator`
soláthraíonn.

Is féidir leat glaonna iolracha a shlabhra ar oiriúntóirí atrialach chun gníomhartha casta a dhéanamh iontu
ar bhealach inléite. Ach toisc go bhfuil gach iterators leisciúil, caithfidh tú glaoch ar cheann de na
modhanna oiriúnaitheora a ídiú chun torthaí a fháil ó ghlaonna ar oiriúntóirí iterator.

### Ag Úsáid Dúnta a Ghabhann A dTimpeallacht

Glacann go leor oiriúntóirí iterator dúnadh mar argóintí, agus go coitianta na dúnta
sonróidh muid mar argóintí d’oiriúnóirí atriallta a bheidh ina ndúntaí a ghabhfaidh
a dtimpeallacht.

Mar shampla seo, úsáidfimid an modh `filter` a thógann dúnadh. Tá an
faigheann dúnadh mír ón atrialltóir agus tugann sé `bool` ar ais. Má tá an dúnadh
tuairisceáin `true`, cuirfear an luach san áireamh san atriall a tháirgtear trí
`filter`. Má thugann an dúnadh 'bréagach' ar ais, ní chuirfear an luach san áireamh.

I Liostú 13-16, úsáidimid `filter` le dúnadh a ghlacann an `shoe_size`
athróg óna thimpeallacht chun athrá a dhéanamh thar bhailiúchán de struchtúr `Shoe`
cásanna. Tabharfaidh sé ar ais ach bróga go bhfuil an méid sonraithe.

<Listing number="13-16" file-name="src/lib.rs" caption="Using the `filter` method with a closure that captures `shoe_size`">

```rust,noplayground
{{#rustdoc_include ../../listings/ch13-functional-features/listing-13-16/src/lib.rs}}
```

</Listing>

Glacann an fheidhm `shoes_in_size` úinéireacht ar veicteoir bróga agus bróg
méid mar pharaiméadair. Filleann sé veicteoir nach bhfuil ann ach bróga den mhéid sonraithe
méid.

I gcorp `shoes_in_size`, tugaimid `into_iter` chun atriaradóir a chruthú
a ghlacann úinéireacht ar an veicteoir. Ansin tugaimid `filter` chun é sin a oiriúnú
iterator isteach i iterator nua go bhfuil ach gnéithe a dhúnadh
Filleann `true`.

Gabhann an dúnadh an paraiméadar `shoe_size` ón timpeallacht agus
comparáid a dhéanamh idir an luach agus méid gach bróg, gan ach bróga den mhéid a choinneáil
sonraithe. Ar deireadh, trí `collect` a ghlaoch bailítear na luachanna a thugann an
iterator oiriúnaithe isteach i veicteoir atá tugtha ar ais ag an bhfeidhm.

Léiríonn an tástáil nuair a thugaimid `shoes_in_size`, nach bhfaighimid ach bróga ar ais
go bhfuil an méid céanna leis an luach e shonraigh muid.