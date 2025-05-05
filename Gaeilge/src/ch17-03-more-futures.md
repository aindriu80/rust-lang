## Ag Obair le Líon ar bith de Thodhchaí

Nuair a d'athraíomar ó dhá thodhchaí a úsáid go trí cinn sa chuid roimhe seo, b'éigean dúinn
freisin aistriú ó `join` a úsáid go `join3`. Bheadh ​​sé cráite
feidhm dhifriúil a ghlaoch gach uair a d'athraíomar líon na dtodhchaí a theastaigh uainn a bheith páirteach. Ar ámharaí an tsaoil, tá foirm macra de `join` againn ar féidir linn líon treallach argóintí a chur chuici. Láimhseálann sé fanacht leis na todhchaí féin freisin.
Dá bhrí sin, d'fhéadfaimis an cód ó Liostáil 17-13 a athscríobh chun `join!` a úsáid in ionad `join3`, mar atá i Liostáil 17-14.

<Listing number="17-14" caption="Using `join!` to wait for multiple futures" file-name="src/main.rs">

```rust
{{#rustdoc_include ../../listings/ch17-async-await/listing-17-14/src/main.rs:here}}
```

</Listing>

Is cinnte gur feabhas é seo ar an malartú idir `join` agus
`join3` agus `join4` agus mar sin de! Mar sin féin, ní oibríonn an fhoirm macra seo ach amháin
nuair a bhíonn a fhios againn cé mhéad todhchaí atá ann roimh ré. I Rust sa saol réadúil,
áfach, is patrún coitianta é todhchaí a bhrú isteach i mbailiúchán agus ansin fanacht ar chuid nó ar
gach todhchaí díobh a bheith críochnaithe.

Chun na todhchaí go léir i mbailiúchán éigin a sheiceáil, beidh orainn athrá a dhéanamh orthu agus
join a dhéanamh orthu _uile_ acu. Glacann an fheidhm `trpl::join_all` le haon chineál a
chuireann an tréith `Iterator` i bhfeidhm, a d'fhoghlaim tú faoi i [An Tréith Iterator agus an Modh `next`][iterator-trait]<!-- ignore --> Caibidil 13, mar sin
is cosúil gurb é an ticéad ceart é. Déanaimis iarracht ár dtodhchaí a chur i veicteoir agus
`join!` a athsholáthar le `join_all` mar a thaispeántar i Liostáil 17-15.

<Listing  number="17-15" caption="Storing anonymous futures in a vector and calling `join_all`">

```rust,ignore,does_not_compile
{{#rustdoc_include ../../listings/ch17-async-await/listing-17-15/src/main.rs:here}}
```

</Listing>

Ar an drochuair, ní thiomsaíonn an cód seo. Ina áit sin, faighimid an earráid seo:

<!-- manual-regeneration
cd listings/ch17-async-await/listing-17-15/
cargo build
copy just the compiler error
-->

```text
error[E0308]: mismatched types
  --> src/main.rs:45:37
   |
10 |         let tx1_fut = async move {
   |                       ---------- the expected `async` block
...
24 |         let rx_fut = async {
   |                      ----- the found `async` block
...
45 |         let futures = vec![tx1_fut, rx_fut, tx_fut];
   |                                     ^^^^^^ expected `async` block, found a 
different `async` block
   |
   = note: expected `async` block `{async block@src/main.rs:10:23: 10:33}`
              found `async` block `{async block@src/main.rs:24:22: 24:27}`
   = note: no two async blocks, even if identical, have the same type
   = help: consider pinning your async block and casting it to a trait object
```

D’fhéadfadh sé seo a bheith ionadh. Tar éis an tsaoil, ní thugann aon cheann de na bloic asyncrónacha aon rud ar ais,
mar sin táirgeann gach ceann acu `Future<Output = ()>`. Cuimhnigh gur tréith í `Future`,
ach, agus go gcruthaíonn an tiomsaitheoir enum uathúil do gach bloc asyncrónach. Ní féidir leat dhá struchtúr lámhscríofa éagsúla a chur i `Vec`, agus baineann an riail chéanna
leis na enums éagsúla a ghineann an tiomsaitheoir.

Chun seo a chur ag obair, ní mór dúinn _trait objects_ a úsáid, díreach mar a rinneamar i [“Returning
Errors from the run function”][dyn]<!-- ignore --> i gCaibidil 12. (Clúdóimid
trait objects go mion i gCaibidil 18.) Trí úsáid a bhaint as réada tréithe, is féidir linn gach
ceann de na todhchaí gan ainm a tháirgeann na cineálacha seo a chóireáil mar an gcineál céanna, toisc go gcuireann siad uile an tréith `Future` i bhfeidhm.

> Nóta: I rannóg Chaibidil 8 [Úsáid Enum chun Illuachanna a Stóráil][enum-alt]<!-- ignore -->, phléamar bealach eile chun ilchineálacha a áireamh i `Vec`: enum a úsáid chun gach cineál a fhéadfaidh a bheith le feiceáil sa
> veicteoir a léiriú. Ní féidir linn é sin a dhéanamh anseo, áfach. Ar an gcéad dul síos, níl aon bhealach againn na cineálacha éagsúla a ainmniú, mar go bhfuil siad gan ainm. Ar an gcéad dul síos, ba é an chúis
> ar shroicheamar veicteoir agus `join_all` ar an gcéad dul síos ná go mbeimid in ann oibriú
> le bailiúchán dinimiciúil todhchaíochtaí nuair nach bhfuil cúram orainn ach go bhfuil an cineál
> aschuir chéanna acu.

Tosaímid trí gach todhchaí sa `vec!` a fhilleadh i `Box::new`, mar a thaispeántar i
Liostáil 17-16.

<Listing number="17-16" caption="Using `Box::new` to align the types of the futures in a `Vec`" file-name="src/main.rs">

```rust,ignore,does_not_compile
{{#rustdoc_include ../../listings/ch17-async-await/listing-17-16/src/main.rs:here}}
```

</Listing>


Ar an drochuair, ní thiomsaíonn an cód seo fós. Déanta na fírinne, faighimid an earráid bhunúsach chéanna a fuair muid roimhe seo don dara agus don tríú glao `Box::new` araon, chomh maith le
earráidí nua a thagraíonn don tréith `Unpin`. Fillfimid ar na hearráidí `Unpin` i gceann tamaill. Ar dtús, déanaimis na hearráidí cineáil ar na glaonna `Box::new` a shocrú trí
chineál an athróg `futures` a anótáil go sainráite (féach Liostáil 17-17).

<Listing number="17-17" caption="Fixing the rest of the type mismatch errors by using an explicit type declaration" file-name="src/main.rs">

```rust,ignore,does_not_compile
{{#rustdoc_include ../../listings/ch17-async-await/listing-17-17/src/main.rs:here}}
```

</Listing>


Tá an dearbhú cineáil seo beagáinín casta, mar sin déanaimis scrúdú air:

1. Is é an todhchaí féin an cineál is istigh. Tugaimid faoi deara go soiléir gurb é aschur an todhchaí an cineál aonaid `()` trí `Future<Output = ()>` a scríobh.

2. Ansin, cuirimid `dyn` leis an tréith chun é a mharcáil mar dhinimiciúil.

3. Tá an tagairt tréithe iomlán fillte i `Box`.

4. Ar deireadh, luaimid go soiléir gur `Vec` é `futures` ina bhfuil na míreanna seo.

Rinne sin difríocht mhór cheana féin. Anois nuair a ritheann muid an tiomsaitheoir, ní bhfaighimid ach
na hearráidí ina luaitear `Unpin`. Cé go bhfuil trí cinn acu ann, tá a n-ábhar
an-chosúil.

<!-- manual-regeneration
cd listings/ch17-async-await/listing-17-16
cargo build
# copy *only* the errors
# fix the paths
-->

```text
error[E0308]: mismatched types
   --> src/main.rs:46:46
    |
10  |         let tx1_fut = async move {
    |                       ---------- the expected `async` block
...
24  |         let rx_fut = async {
    |                      ----- the found `async` block
...
46  |             vec![Box::new(tx1_fut), Box::new(rx_fut), Box::new(tx_fut)];
    |                                     -------- ^^^^^^ expected `async` block, found a different `async` block
    |                                     |
    |                                     arguments to this function are incorrect
    |
    = note: expected `async` block `{async block@src/main.rs:10:23: 10:33}`
               found `async` block `{async block@src/main.rs:24:22: 24:27}`
    = note: no two async blocks, even if identical, have the same type
    = help: consider pinning your async block and casting it to a trait object
note: associated function defined here
   --> file:///home/.rustup/toolchains/1.82/lib/rustlib/src/rust/library/alloc/src/boxed.rs:255:12
    |
255 |     pub fn new(x: T) -> Self {
    |            ^^^

error[E0308]: mismatched types
   --> src/main.rs:46:64
    |
10  |         let tx1_fut = async move {
    |                       ---------- the expected `async` block
...
30  |         let tx_fut = async move {
    |                      ---------- the found `async` block
...
46  |             vec![Box::new(tx1_fut), Box::new(rx_fut), Box::new(tx_fut)];
    |                                                       -------- ^^^^^^ expected `async` block, found a different `async` block
    |                                                       |
    |                                                       arguments to this function are incorrect
    |
    = note: expected `async` block `{async block@src/main.rs:10:23: 10:33}`
               found `async` block `{async block@src/main.rs:30:22: 30:32}`
    = note: no two async blocks, even if identical, have the same type
    = help: consider pinning your async block and casting it to a trait object
note: associated function defined here
   --> file:///home/.rustup/toolchains/1.82/lib/rustlib/src/rust/library/alloc/src/boxed.rs:255:12
    |
255 |     pub fn new(x: T) -> Self {
    |            ^^^

error[E0277]: `{async block@src/main.rs:10:23: 10:33}` cannot be unpinned
   --> src/main.rs:48:24
    |
48  |         trpl::join_all(futures).await;
    |         -------------- ^^^^^^^ the trait `Unpin` is not implemented for `{async block@src/main.rs:10:23: 10:33}`, which is required by `Box<{async block@src/main.rs:10:23: 10:33}>: Future`
    |         |
    |         required by a bound introduced by this call
    |
    = note: consider using the `pin!` macro
            consider using `Box::pin` if you need to access the pinned value outside of the current scope
    = note: required for `Box<{async block@src/main.rs:10:23: 10:33}>` to implement `Future`
note: required by a bound in `join_all`
   --> file:///home/.cargo/registry/src/index.crates.io-6f17d22bba15001f/futures-util-0.3.30/src/future/join_all.rs:105:14
    |
102 | pub fn join_all<I>(iter: I) -> JoinAll<I::Item>
    |        -------- required by a bound in this function
...
105 |     I::Item: Future,
    |              ^^^^^^ required by this bound in `join_all`

error[E0277]: `{async block@src/main.rs:10:23: 10:33}` cannot be unpinned
  --> src/main.rs:48:9
   |
48 |         trpl::join_all(futures).await;
   |         ^^^^^^^^^^^^^^^^^^^^^^^ the trait `Unpin` is not implemented for `{async block@src/main.rs:10:23: 10:33}`, which is required by `Box<{async block@src/main.rs:10:23: 10:33}>: Future`
   |
   = note: consider using the `pin!` macro
           consider using `Box::pin` if you need to access the pinned value outside of the current scope
   = note: required for `Box<{async block@src/main.rs:10:23: 10:33}>` to implement `Future`
note: required by a bound in `futures_util::future::join_all::JoinAll`
  --> file:///home/.cargo/registry/src/index.crates.io-6f17d22bba15001f/futures-util-0.3.30/src/future/join_all.rs:29:8
   |
27 | pub struct JoinAll<F>
   |            ------- required by a bound in this struct
28 | where
29 |     F: Future,
   |        ^^^^^^ required by this bound in `JoinAll`

error[E0277]: `{async block@src/main.rs:10:23: 10:33}` cannot be unpinned
  --> src/main.rs:48:33
   |
48 |         trpl::join_all(futures).await;
   |                                 ^^^^^ the trait `Unpin` is not implemented for `{async block@src/main.rs:10:23: 10:33}`, which is required by `Box<{async block@src/main.rs:10:23: 10:33}>: Future`
   |
   = note: consider using the `pin!` macro
           consider using `Box::pin` if you need to access the pinned value outside of the current scope
   = note: required for `Box<{async block@src/main.rs:10:23: 10:33}>` to implement `Future`
note: required by a bound in `futures_util::future::join_all::JoinAll`
  --> file:///home/.cargo/registry/src/index.crates.io-6f17d22bba15001f/futures-util-0.3.30/src/future/join_all.rs:29:8
   |
27 | pub struct JoinAll<F>
   |            ------- required by a bound in this struct
28 | where
29 |     F: Future,
   |        ^^^^^^ required by this bound in `JoinAll`
```

Is _a lán_ é sin le díleá, mar sin déanaimis é a scaradh óna chéile. Insíonn an chéad chuid den teachtaireacht dúinn nach gcuireann an chéad bhloc asyncrónach (`src/main.rs:8:23: 20:10`)
an tréith `Unpin` i bhfeidhm agus molann sé `pin!` nó `Box::pin` a úsáid chun
é a réiteach. Níos déanaí sa chaibidil, déanfaimid tochailt isteach i roinnt sonraí eile faoi `Pin` agus
`Unpin`. I láthair na huaire, áfach, is féidir linn comhairle an tiomsaitheora a leanúint chun
dícheangal. I Liostáil 17-18, tosaímid tríd an nóta cineáil do
`futures` a nuashonrú, le `Pin` ag timfhilleadh gach `Box`. Ar an dara dul síos, úsáidimid `Box::pin` chun
na todhchaí féin a phionáil.

<Listing number="17-18" caption="Using `Pin` and `Box::pin` to make the `Vec` type check" file-name="src/main.rs">

```rust
{{#rustdoc_include ../../listings/ch17-async-await/listing-17-18/src/main.rs:here}}
```

</Listing>

Má dhéanaimid é seo a thiomsú agus a rith, gheobhaimid an t-aschur a raibh súil againn leis sa deireadh:

<!-- Not extracting output because changes to this output aren't significant;
the changes are likely to be due to the threads running differently rather than
changes in the compiler -->

```text
received 'hi'
received 'more'
received 'from'
received 'messages'
received 'the'
received 'for'
received 'future'
received 'you'
```

Ó, a Dhia!

Tá beagán eile le fiosrú anseo. Ar an gcéad dul síos, cuireann úsáid a bhaint as `Pin<Box<T>>` beagán forchostais leis ó na todhchaí seo a chur ar an gcarn le `Box`—agus
nílimid ag déanamh sin ach chun na cineálacha a ailíniú. Ní _gá_ linn i ndáiríre an
leithdháileadh carn, tar éis an tsaoil: tá na todhchaí seo áitiúil don fheidhm seo.
Mar a luadh cheana, is cineál fillteáin é `Pin` féin, mar sin is féidir linn leas a bhaint as
cineál amháin a bheith againn sa `Vec`—an chúis bhunaidh ar shroicheamar `Box`—gan leithdháileadh carn a dhéanamh. Is féidir linn `Pin` a úsáid go díreach le gach
todhchaí, ag baint úsáide as an macra `std::pin::pin`.

Mar sin féin, ní mór dúinn a bheith soiléir fós faoin gcineál tagartha bioráilte;
seach sin, ní bheidh a fhios ag Rust fós conas iad seo a léirmhíniú mar réada tréithe dinimiciúla,
agus sin an rud a theastaíonn uainn uathu a bheith sa `Vec`. Dá bhrí sin, déanaimid gach todhchaí a phionáil nuair a shainmhínímid í, agus sainmhínímid `futures` mar `Vec` ina bhfuil tagairtí inathraithe bioráilte don chineál todhchaí dinimiciúil, mar atá i Liostáil 17-19.

<Listing number="17-19" caption="Using `Pin` directly with the `pin!` macro to avoid unnecessary heap allocations" file-name="src/main.rs">

```rust
{{#rustdoc_include ../../listings/ch17-async-await/listing-17-19/src/main.rs:here}}
```

</Listing>

Shroicheamar an méid seo trí neamhaird a dhéanamh den fhíric go bhféadfadh cineálacha éagsúla `Output` a bheith againn. Mar shampla, i Liosta 17-20, cuireann an todhchaí gan ainm le haghaidh `a` `Future<Output = u32>` i bhfeidhm, cuireann an todhchaí gan ainm le haghaidh `b` `Future<Output =
&str>` i bhfeidhm, agus cuireann an todhchaí gan ainm le haghaidh `c` `Future<Output = bool>` i bhfeidhm.

<Listing number="17-20" caption="Three futures with distinct types" file-name="src/main.rs">

```rust
{{#rustdoc_include ../../listings/ch17-async-await/listing-17-20/src/main.rs:here}}
```

</Listing>


Is féidir linn `trpl::join!` a úsáid chun fanacht leo, mar go gceadaíonn sé dúinn cineálacha éagsúla todhchaí a chur isteach agus táirgeann sé tuple de na cineálacha sin. Ní féidir linn `trpl::join_all` a úsáid, mar éilíonn sé go mbeidh an cineál céanna ag na todhchaí go léir a chuirtear isteach. Cuimhnigh, is é an earráid sin a chuir tús linn ar an eachtra seo le
`Pin`!

Is comhbhabhtáil bhunúsach í seo: is féidir linn déileáil le líon dinimiciúil
todhchaí le `join_all`, fad is atá an cineál céanna acu go léir, nó is féidir linn déileáil
le líon socraithe todhchaí leis na feidhmeanna `join` nó leis an macra `join!`,
fiú má tá cineálacha difriúla acu. Is é seo an cás céanna a mbeadh orainn aghaidh a thabhairt air agus muid
ag obair le haon chineálacha eile i Rust. Níl todhchaí speisialta, cé go bhfuil
roinnt comhréir deas againn chun oibriú leo, agus is rud maith é sin.

### Todhchaí Rásaíochta

Nuair a "cheanglaímid" todhchaí leis an teaghlach feidhmeanna agus macraí `join`,
ní mór dúinn _gach_ ceann acu a chríochnú sula mbogann muid ar aghaidh. Uaireanta, áfach, ní gá ach _roinnt_ todhchaí ó shraith a chríochnú sula mbogann muid ar aghaidh—rud beag cosúil le
rásaíocht a dhéanamh idir todhchaí amháin agus todhchaí eile.

I Liostáil 17-21, úsáidimid `trpl::race` arís chun dhá thodhchaí, `slow` agus
`fast`, a rith i gcoinne a chéile.

<Listing number="17-21" caption="Using `race` to get the result of whichever future finishes first" file-name="src/main.rs">

```rust
{{#rustdoc_include ../../listings/ch17-async-await/listing-17-21/src/main.rs:here}}
```

</Listing>

Priontálann gach todhchaí teachtaireacht nuair a thosaíonn sé ag rith, sosann sé ar feadh tamaill
trí ghlaoch agus fanacht le `sleep`, agus ansin priontálann sé teachtaireacht eile nuair a
chríochnaíonn sé. Ansin, cuirimid `slow` agus `fast` araon chuig `trpl::race` agus fanfaimid go gcríochnóidh ceann
dóibh. (Níl an toradh anseo ró-iontach: buaileann `fast`.) Murab ionann agus
nuair a d'úsáideamar `race` ar ais in [“Ár gCéad Chlár Asyncrónach”][async-program]<!--
ignore -->, ní dhéanaimid ach neamhaird den chás `Either` a thugann sé ar ais anseo, toisc go dtarlaíonn an t-iompar suimiúil go léir i gcorp na mbloc asyncrónach.

Tabhair faoi deara má athraíonn tú ord na n-argóintí go `race`, athraíonn ord na
dteachtaireachtaí “tosaithe”, cé go gcríochnaíonn an todhchaí `fast` i gcónaí
ar dtús. Sin toisc nach bhfuil cur i bhfeidhm na feidhme `race` seo cothrom. Ritheann sé na todhchaí a chuirtear isteach mar argóintí i gcónaí san ord ina
ritheann siad. Tá cur i bhfeidhm eile _cóir_ agus roghnóidh siad go randamach
cé acu todhchaí le vótaíocht ar dtús. Beag beann ar cibé an bhfuil cur i bhfeidhm an chine
atá á úsáid againn cothrom, áfach, rithfidh _ceann_ de na todhchaí suas go dtí an chéad
`await` ina chorp sula bhféadfar tasc eile a thosú.

Meabhraigh ó [Ár gCéad Chlár Asyncrónach][async-program]<!-- ignore --> go dtugann Rust deis d'am rith an tasc a chur ar sos agus aistriú go
ceann eile mura bhfuil an todhchaí atá á fanacht réidh. Tá an rud eile fíor freisin:
Cuireann Rust _only_ sos ar bhloic asyncrónacha agus tugann sé an rialú ar ais go ham rith ag pointe feithimh.
Tá gach rud idir pointí feithimh sioncrónach.

Ciallaíonn sé sin má dhéanann tú go leor oibre i mbloc asyncrónach gan pointe feithimh,
go gcuirfidh an todhchaí sin bac ar aon todhchaí eile ó dhul chun cinn a dhéanamh. Uaireanta, d'fhéadfá
é seo a chloisteáil mar thodhchaí amháin ag _ocras_ todhchaí eile. I gcásanna áirithe,
b'fhéidir nach mbeadh sé sin ina mhórcheist. Mar sin féin, má tá tú ag déanamh cineál éigin oibre costasaí
suite nó oibre fadtréimhseach, nó má tá todhchaí agat a leanfaidh ort ag déanamh tasc áirithe
go deo, beidh ort smaoineamh ar cathain agus cá háit le rialú a thabhairt ar ais don am rith.

Ar an gcaoi chéanna, má tá oibríochtaí blocála fadtréimhseacha agat, is féidir le haisioncrónach a bheith ina
uirlis úsáideach chun bealaí a sholáthar do chodanna éagsúla den chlár baint a bheith acu
le chéile.

Ach _conas_ a thabharfá rialú ar ais don am rith sna cásanna sin?

<!-- Seancheannteidil. Ná bain iad nó d'fhéadfadh naisc briseadh. -->

<a id="yielding"></a>

### Rialú a Thabhairt don Am Rith

Déanaimis oibríocht fhada a insamhladh. Tugann liostú 17-22 feidhm `slow` isteach.

<Listing number="17-22" caption="Using `thread::sleep` to simulate slow operations" file-name="src/main.rs">

```rust
{{#rustdoc_include ../../listings/ch17-async-await/listing-17-22/src/main.rs:slow}}
```

</Listing>

Úsáideann an cód seo `std::thread::sleep` in ionad `trpl::sleep` ionas go gcuirfidh glaoch ar `slow` bac ar an snáithe reatha ar feadh roinnt milleasoicindí. Is féidir linn `slow` a úsáid chun seasamh in ionad oibríochtaí fíorshaoil ​​atá ag rith ar feadh i bhfad agus
ag blocáil.

I Liosta 17-23, úsáidimid `slow` chun aithris a dhéanamh ar an gcineál seo oibre atá ceangailte le LAP i
béire todhchaí.

<Listing number="17-23" caption="Using `thread::sleep` to simulate slow operations" file-name="src/main.rs">

```rust
{{#rustdoc_include ../../listings/ch17-async-await/listing-17-23/src/main.rs:slow-futures}}
```

</Listing>

Ar dtús, ní thugann gach todhchaí ach an rialú ar ais chuig an am rite _tar éis_ roinnt oibríochtaí mall a dhéanamh. Má ritheann tú an cód seo, feicfidh tú an t-aschur seo:

<!-- manual-regeneration
cd listings/ch17-async-await/listing-17-23/
cargo run
copy just the output
-->

```text
'a' started.
'a' ran for 30ms
'a' ran for 10ms
'a' ran for 20ms
'b' started.
'b' ran for 75ms
'b' ran for 10ms
'b' ran for 15ms
'b' ran for 350ms
'a' finished.
```

Mar atá lenár sampla níos luaithe, críochnaíonn `race` a luaithe is a bhíonn `a` críochnaithe.
Níl aon idirnascadh idir an dá thodhchaí, áfach. Déanann an todhchaí `a` a chuid oibre go léir go dtí go bhfanann an glao `trpl::sleep`, ansin déanann an todhchaí `b` a chuid oibre go léir go dtí go bhfanann a glao `trpl::sleep` féin, agus ar deireadh críochnaíonn an todhchaí `a`. Chun ligean don dá thodhchaí dul chun cinn a dhéanamh idir a gcuid tascanna mall, teastaíonn pointí feithimh uainn ionas gur féidir linn an rialú a thabhairt ar ais don am rite. Ciallaíonn sé sin go
gceann muid rud éigin ar féidir linn fanacht leis!

Is féidir linn an cineál seo láimhseála a fheiceáil ag tarlú cheana féin i Liostáil 17-23: dá
mbaineamar an `trpl::sleep` ag deireadh thodhchaí `a`, chríochnódh sé
gan an todhchaí `b` ag rith _ar chor ar bith_. Déanaimis iarracht an fheidhm `sleep` a úsáid mar
phointe tosaigh chun ligean d'oibríochtaí múchadh agus dul chun cinn á dhéanamh, mar a thaispeántar i
Liostáil 17-24.

<Listing number="17-24" caption="Using `sleep` to let operations switch off making progress" file-name="src/main.rs">

```rust
{{#rustdoc_include ../../listings/ch17-async-await/listing-17-24/src/main.rs:here}}
```

</Listing>

I Liosta 17-24, cuirimid glaonna `trpl::sleep` le pointí await idir gach glao le `slow`. Anois tá obair an dá thodhchaí fite fuaite:

<!-- manual-regeneration
cd listings/ch17-async-await/listing-17-24
cargo run
copy just the output
-->

```text
'a' started.
'a' ran for 30ms
'b' started.
'b' ran for 75ms
'a' ran for 10ms
'b' ran for 10ms
'a' ran for 20ms
'b' ran for 15ms
'a' finished.
```

Ritheann an todhchaí `a` ar feadh tamaill fós sula dtugann sé an smacht do `b`, mar gheall ar `slow` sula nglaonn sé ar `trpl::sleep` riamh, ach ina dhiaidh sin malartaíonn na todhchaí
ar ais agus amach gach uair a bhuaileann ceann acu pointe fanachta. Sa chás seo, rinneamar é sin tar éis gach glao ar `slow`, ach d'fhéadfaimis an obair a bhriseadh suas ar
cibé bealach is ciallmhaire dúinn.

Ní mian linn _sleep_ anseo i ndáiríre, áfach: ba mhaith linn dul chun cinn a dhéanamh chomh tapa
agus is féidir linn. Ní mór dúinn ach an smacht a thabhairt ar ais don am rith. Is féidir linn é sin a dhéanamh
go díreach, ag baint úsáide as an bhfeidhm `yield_now`. I Liosta 17-25, cuirimid `yield_now` in ionad na nglaonna `sleep` sin go léir.

<Listing number="17-25" caption="Using `yield_now` to let operations switch off making progress" file-name="src/main.rs">

```rust
{{#rustdoc_include ../../listings/ch17-async-await/listing-17-25/src/main.rs:yields}}
```

</Listing>

Tá an cód seo níos soiléire faoin aidhm iarbhír agus is féidir leis a bheith i bhfad níos tapúla ná `codladh` a úsáid, mar is minic a bhíonn teorainneacha ag lasc ama cosúil leis an gceann a úsáideann `codladh` maidir le cé chomh mionsonraithe is féidir leo a bheith. Codlaíonn an leagan de `codladh` atá á úsáid againn,
mar shampla, i gcónaí ar feadh milleasoicind ar a laghad, fiú má thugaimid `Fad` nana-soicind amháin dó. Arís, tá ríomhairí nua-aimseartha _tapa_: is féidir leo
go leor a dhéanamh i milleasoicind amháin!

Is féidir leat é seo a fheiceáil duit féin trí thagarmharc beag a shocrú, mar shampla an ceann
i Liostáil 17-26. (Ní bealach thar a bheith dian é seo chun tástáil feidhmíochta a dhéanamh,
ach is leor é chun an difríocht a thaispeáint anseo.)

<Listing number="17-26" caption="Comparing the performance of `sleep` and `yield_now`" file-name="src/main.rs">

```rust
{{#rustdoc_include ../../listings/ch17-async-await/listing-17-26/src/main.rs:here}}
```

</Listing>

Anseo, scipeáilimid an priontáil stádais go léir, cuirimid `Duration` aon-nana-soicind chuig
`trpl::sleep`, agus ligimid do gach todhchaí rith leis féin, gan aon athrú idir na
todhchaí. Ansin rithimid ar feadh 1,000 athrá agus feicimid cé chomh fada a thógann an todhchaí ag baint úsáide as
`trpl::sleep` i gcomparáid leis an todhchaí ag baint úsáide as `trpl::yield_now`.

Tá an leagan le `yield_now` _i bhfad_ níos tapúla!

Ciallaíonn sé seo gur féidir le haisioncrónú a bheith úsáideach fiú le haghaidh tascanna atá ceangailte le ríomh, ag brath ar
cad eile atá á dhéanamh ag do chlár, toisc go soláthraíonn sé uirlis úsáideach chun
na caidrimh idir codanna éagsúla den chlár a struchtúrú. Is
foirm _iltascála comhoibríoch_ é seo, áit a bhfuil an chumhacht ag gach todhchaí a chinneadh
cathain a thugann sé smacht trí phointí feithimh. Dá bhrí sin, tá an
fhreagracht ar gach todhchaí freisin bac a sheachaint ar feadh ró-fhada. I roinnt córas oibriúcháin leabaithe bunaithe ar Rust,
is é seo an _t-aon_ cineál iltascála!

I gcód an tsaoil réadaigh, ní bheidh tú ag malartú glaonna feidhme le pointí feithimh ar gach líne aonair de ghnáth, ar ndóigh. Cé go bhfuil sé réasúnta saor rialú a thabhairt ar an mbealach seo, níl sé saor in aisce. I go leor cásanna, d'fhéadfadh iarracht tasc atá ceangailte le ríomhaireacht a bhriseadh suas é a dhéanamh i bhfad níos moille, mar sin uaireanta is fearr
don fheidhmíocht fhoriomlán ligean d'oibríocht blocáil go hachomair. Déan
tomhais i gcónaí chun a fheiceáil cad iad na bacainní feidhmíochta iarbhír atá i do chód. Tá sé tábhachtach an
dinimic bhunúsach a choinneáil i gcuimhne, áfach, má _tá_ tú ag feiceáil
go leor oibre ag tarlú i sraitheach a raibh súil agat a tharlódh ag an am céanna!

### Ár nAistarraingtí Aisioncrónacha Féin a Thógáil

Is féidir linn todhchaí a chumadh le chéile freisin chun patrúin nua a chruthú. Mar shampla, is féidir linn
feidhm 'am scoir' a thógáil le bloic thógála aisioncrónacha atá againn cheana féin. Nuair
a bheidh muid críochnaithe, beidh an toradh ina bhloc tógála eile a d'fhéadfaimis a úsáid chun
níos mó aistarraingtí aisioncrónacha a chruthú.

Léiríonn liostú 17-27 conas a bheimid ag súil go n-oibreodh an 'tréimhse scoir' seo le todhchaí mall.

Tá an cód seo níos soiléire faoin aidhm iarbhír agus is féidir leis a bheith i bhfad níos tapúla ná `codladh` a úsáid, mar is minic a bhíonn teorainneacha ag lasc ama cosúil leis an gceann a úsáideann `codladh` maidir le cé chomh mionsonraithe is féidir leo a bheith. Codlaíonn an leagan de `codladh` atá á úsáid againn,
mar shampla, i gcónaí ar feadh milleasoicind ar a laghad, fiú má thugaimid `Fad` nana-soicind amháin dó. Arís, tá ríomhairí nua-aimseartha _tapa_: is féidir leo
go leor a dhéanamh i milleasoicind amháin!

Is féidir leat é seo a fheiceáil duit féin trí thagarmharc beag a shocrú, mar shampla an ceann
i Liostáil 17-26. (Ní bealach thar a bheith dian é seo chun tástáil feidhmíochta a dhéanamh,
ach is leor é chun an difríocht a thaispeáint anseo.)




Priontálann gach todhchaí teachtaireacht nuair a thosaíonn sé ag rith, sosann sé ar feadh tamaill
trí ghlaoch agus fanacht le `sleep`, agus ansin priontálann sé teachtaireacht eile nuair a
chríochnaíonn sé. Ansin, cuirimid `slow` agus `fast` araon chuig `trpl::race` agus fanfaimid go gcríochnóidh ceann
dóibh. (Níl an toradh anseo ró-iontach: buaileann `fast`.) Murab ionann agus
nuair a d'úsáideamar `race` ar ais in [“Ár gCéad Chlár Asyncrónach”][async-program]<!--
ignore -->, ní dhéanaimid ach neamhaird den chás `Either` a thugann sé ar ais anseo, toisc go dtarlaíonn an t-iompar suimiúil go léir i gcorp na mbloc asyncrónach.

Tabhair faoi deara má athraíonn tú ord na n-argóintí go `race`, athraíonn ord na
dteachtaireachtaí “tosaithe”, cé go gcríochnaíonn an todhchaí `fast` i gcónaí
ar dtús. Sin toisc nach bhfuil cur i bhfeidhm na feidhme `race` seo cothrom. Ritheann sé na todhchaí a chuirtear isteach mar argóintí i gcónaí san ord ina
ritheann siad. Tá cur i bhfeidhm eile _cóir_ agus roghnóidh siad go randamach
cé acu todhchaí le vótaíocht ar dtús. Beag beann ar cibé an bhfuil cur i bhfeidhm an chine
atá á úsáid againn cothrom, áfach, rithfidh _ceann_ de na todhchaí suas go dtí an chéad
`await` ina chorp sula bhféadfar tasc eile a thosú.

Meabhraigh ó [Ár gCéad Chlár Asyncrónach][async-program]<!-- ignore --> go dtugann Rust deis d'am rith an tasc a chur ar sos agus aistriú go
ceann eile mura bhfuil an todhchaí atá á fanacht réidh. Tá an rud eile fíor freisin:
Cuireann Rust _only_ sos ar bhloic asyncrónacha agus tugann sé an rialú ar ais go ham rith ag pointe feithimh.
Tá gach rud idir pointí feithimh sioncrónach.

Ciallaíonn sé sin má dhéanann tú go leor oibre i mbloc asyncrónach gan pointe feithimh,
go gcuirfidh an todhchaí sin bac ar aon todhchaí eile ó dhul chun cinn a dhéanamh. Uaireanta, d'fhéadfá
é seo a chloisteáil mar thodhchaí amháin ag _ocras_ todhchaí eile. I gcásanna áirithe,
b'fhéidir nach mbeadh sé sin ina mhórcheist. Mar sin féin, má tá tú ag déanamh cineál éigin oibre costasaí
suite nó oibre fadtréimhseach, nó má tá todhchaí agat a leanfaidh ort ag déanamh tasc áirithe
go deo, beidh ort smaoineamh ar cathain agus cá háit le rialú a thabhairt ar ais don am rith.

Ar an gcaoi chéanna, má tá oibríochtaí blocála fadtréimhseacha agat, is féidir le haisioncrónach a bheith ina
uirlis úsáideach chun bealaí a sholáthar do chodanna éagsúla den chlár baint a bheith acu
le chéile.

Ach _conas_ a thabharfá rialú ar ais don am rith sna cásanna sin?

<!-- Old headings. Do not remove or links may break. -->

<a id="yielding"></a>

### Rialú a Thabhairt don Am Rith

Déanaimis oibríocht fhadtréimhseach a insamhladh. Tugann liostú 17-22 feidhm `slow` isteach.

<Listing number="17-22" caption="Using `thread::sleep` to simulate slow operations" file-name="src/main.rs">

```rust
{{#rustdoc_include ../../listings/ch17-async-await/listing-17-22/src/main.rs:slow}}
```

</Listing>

Úsáideann an cód seo `std::thread::sleep` in ionad `trpl::sleep` ionas go gcuirfidh glaoch ar `slow` bac ar an snáithe reatha ar feadh roinnt milleasoicindí. Is féidir linn `slow` a úsáid chun seasamh in ionad oibríochtaí fíorshaoil ​​atá ag rith ar feadh i bhfad agus
ag blocáil.

I Liosta 17-23, úsáidimid `slow` chun aithris a dhéanamh ar an gcineál seo oibre atá ceangailte le LAP i
béire todhchaí.

<Listing number="17-23" caption="Using `thread::sleep` to simulate slow operations" file-name="src/main.rs">

```rust
{{#rustdoc_include ../../listings/ch17-async-await/listing-17-23/src/main.rs:slow-futures}}
```

</Listing>

Ar dtús, ní thugann gach todhchaí ach an rialú ar ais chuig an am rite _tar éis_ roinnt oibríochtaí mall a dhéanamh. Má ritheann tú an cód seo, feicfidh tú an t-aschur seo:

<!-- manual-regeneration
cd listings/ch17-async-await/listing-17-23/
cargo run
copy just the output
-->

```text
'a' started.
'a' ran for 30ms
'a' ran for 10ms
'a' ran for 20ms
'b' started.
'b' ran for 75ms
'b' ran for 10ms
'b' ran for 15ms
'b' ran for 350ms
'a' finished.
```

Mar atá lenár sampla níos luaithe, críochnaíonn `race` a luaithe is a bhíonn `a` críochnaithe.
Níl aon idirnascadh idir an dá thodhchaí, áfach. Déanann an todhchaí `a` a chuid oibre go léir go dtí go bhfanann an glao `trpl::sleep`, ansin déanann an todhchaí `b` a chuid oibre go léir go dtí go bhfanann a glao `trpl::sleep` féin, agus ar deireadh críochnaíonn an todhchaí `a`. Chun ligean don dá thodhchaí dul chun cinn a dhéanamh idir a gcuid tascanna mall, teastaíonn pointí feithimh uainn ionas gur féidir linn an rialú a thabhairt ar ais don am rite. Ciallaíonn sé sin go
gceann muid rud éigin ar féidir linn fanacht leis!

Is féidir linn an cineál seo láimhseála a fheiceáil ag tarlú cheana féin i Liostáil 17-23: dá
mbaineamar an `trpl::sleep` ag deireadh thodhchaí `a`, chríochnódh sé
gan an todhchaí `b` ag rith _ar chor ar bith_. Déanaimis iarracht an fheidhm `sleep` a úsáid mar
phointe tosaigh chun ligean d'oibríochtaí múchadh agus dul chun cinn á dhéanamh, mar a thaispeántar i
Liostáil 17-24.

<Listing number="17-24" caption="Using `sleep` to let operations switch off making progress" file-name="src/main.rs">

```rust
{{#rustdoc_include ../../listings/ch17-async-await/listing-17-24/src/main.rs:here}}
```

</Listing>

I Liosta 17-24, cuirimid glaonna `trpl::sleep` le pointí await idir gach glao le `slow`. Anois tá obair an dá thodhchaí fite fuaite:

<!-- manual-regeneration
cd listings/ch17-async-await/listing-17-24
cargo run
copy just the output
-->

```text
'a' started.
'a' ran for 30ms
'b' started.
'b' ran for 75ms
'a' ran for 10ms
'b' ran for 10ms
'a' ran for 20ms
'b' ran for 15ms
'a' finished.
```

Ritheann an todhchaí `a` ar feadh tamaill fós sula dtugann sé an smacht do `b`, mar gheall ar `slow` sula nglaonn sé ar `trpl::sleep` riamh, ach ina dhiaidh sin malartaíonn na todhchaí
ar ais agus amach gach uair a bhuaileann ceann acu pointe fanachta. Sa chás seo, rinneamar é sin tar éis gach glao ar `slow`, ach d'fhéadfaimis an obair a bhriseadh suas ar
cibé bealach is ciallmhaire dúinn.

Ní mian linn _sleep_ anseo i ndáiríre, áfach: ba mhaith linn dul chun cinn a dhéanamh chomh tapa
agus is féidir linn. Ní mór dúinn ach an smacht a thabhairt ar ais don am rite. Is féidir linn é sin a dhéanamh
go díreach, ag baint úsáide as an bhfeidhm `yield_now`. I Liosta 17-25, cuirimid `yield_now` in ionad na nglaonna `sleep` sin go léir.

<Listing number="17-25" caption="Using `yield_now` to let operations switch off making progress" file-name="src/main.rs">

```rust
{{#rustdoc_include ../../listings/ch17-async-await/listing-17-25/src/main.rs:yields}}
```

</Listing>

Tá an cód seo níos soiléire faoin aidhm iarbhír agus is féidir leis a bheith i bhfad níos tapúla ná `sleep` a úsáid, mar is minic a bhíonn teorainneacha ag lasc ama cosúil leis an gceann a úsáideann `sleep` maidir le cé chomh mionsonraithe is féidir leo a bheith. Codlaíonn an leagan de `sleep` atá á úsáid againn,
mar shampla, i gcónaí ar feadh milleasoicind ar a laghad, fiú má thugaimid `Fad` nana-soicind amháin dó. Arís, tá ríomhairí nua-aimseartha _tapa_: is féidir leo
go leor a dhéanamh i milleasoicind amháin!

Is féidir leat é seo a fheiceáil duit féin trí thagarmharc beag a shocrú, mar shampla an ceann
i Liostáil 17-26. (Ní bealach thar a bheith dian é seo chun tástáil feidhmíochta a dhéanamh,
ach is leor é chun an difríocht a thaispeáint anseo.)

<Listing number="17-26" caption="Comparing the performance of `sleep` and `yield_now`" file-name="src/main.rs">

```rust
{{#rustdoc_include ../../listings/ch17-async-await/listing-17-26/src/main.rs:here}}
```

</Listing>


Anseo, scipeáilimid an priontáil stádais go léir, cuirimid `Duration` aon-nana-soicind chuig
`trpl::sleep`, agus ligimid do gach todhchaí rith leis féin, gan aon athrú idir na
todhchaí. Ansin rithimid ar feadh 1,000 athrá agus feicimid cé chomh fada a thógann an todhchaí ag baint úsáide as
`trpl::sleep` i gcomparáid leis an todhchaí ag baint úsáide as `trpl::yield_now`.

Tá an leagan le `yield_now` _i bhfad_ níos tapúla!

Ciallaíonn sé seo gur féidir le haisioncrónú a bheith úsáideach fiú le haghaidh tascanna atá ceangailte le ríomhairí, ag brath ar
cad eile atá á dhéanamh ag do chlár, toisc go soláthraíonn sé uirlis úsáideach chun
na caidrimh idir codanna éagsúla den chlár a struchtúrú. Is
foirm _iltascála comhoibríoch_ é seo, áit a bhfuil an chumhacht ag gach todhchaí a chinneadh
cathain a thugann sé smacht trí phointí feithimh. Dá bhrí sin, tá an
fhreagracht ar gach todhchaí freisin bac a sheachaint ar feadh ró-fhada. I roinnt córas oibriúcháin leabaithe bunaithe ar Rust,
is é seo an _t-aon_ cineál iltascála!

I gcód an tsaoil réadaigh, ní bheidh tú ag malartú glaonna feidhme le pointí feithimh ar gach líne aonair de ghnáth, ar ndóigh. Cé go bhfuil sé réasúnta saor rialú a thabhairt ar an mbealach seo, níl sé saor in aisce. I go leor cásanna, d'fhéadfadh iarracht tasc atá ceangailte le ríomhaireacht a bhriseadh suas é a dhéanamh i bhfad níos moille, mar sin uaireanta is fearr
don fheidhmíocht fhoriomlán ligean d'oibríocht blocáil go hachomair. Déan
tomhais i gcónaí chun a fheiceáil cad iad na bacainní feidhmíochta iarbhír atá i do chód. Tá sé tábhachtach an
dinimic bhunúsach a choinneáil i gcuimhne, áfach, má _tá_ tú ag feiceáil
go leor oibre ag tarlú i sraitheach a raibh súil agat a tharlódh ag an am céanna!

### Ár nAistarraingtí Aisioncrónacha Féin a Thógáil

Is féidir linn todhchaí a chumadh le chéile freisin chun patrúin nua a chruthú. Mar shampla, is féidir linn
feidhm `timeout` a thógáil le bloic thógála aisioncrónacha atá againn cheana féin. Nuair
a bheidh muid críochnaithe, beidh an toradh ina bhloc tógála eile a d'fhéadfaimis a úsáid chun
níos mó aistarraingtí aisioncrónacha a chruthú.

Léiríonn liostú 17-27 conas a bheimid ag súil go n-oibreodh an `timeout` seo le todhchaí
mhall.

<Listing number="17-27" caption="Using our imagined `timeout` to run a slow operation with a time limit" file-name="src/main.rs">

```rust,ignore
{{#rustdoc_include ../../listings/ch17-async-await/listing-17-27/src/main.rs:here}}
```

</Listing>

Cuirimis seo i bhfeidhm! Chun tús a chur leis, smaoinímis ar an API don `timeout`:

- Caithfidh sé a bheith ina fheidhm neamhshioncrónach féin ionas gur féidir linn fanacht leis.
- Ba chóir go mbeadh a chéad pharaiméadar ina thodhchaí le rith. Is féidir linn é a dhéanamh cineálach chun ligean dó oibriú le haon thodhchaí.
- Is é an dara paraiméadar an t-uasmhéid ama le fanacht. Má úsáidimid `Duration`,
cuirfidh sé sin ar aghaidh go héasca chuig `trpl::sleep`.
- Ba chóir dó `Result` a thabhairt ar ais. Má chríochnaíonn an todhchaí go rathúil, beidh an `Result` ina `Ok` leis an luach a tháirg an todhchaí. Má théann an t-am scoir thart ar dtús, beidh an `Result` ina `Err` leis an ré a d'fhan an t-am scoir leis.

Taispeánann Liostáil 17-28 an dearbhú seo.

<!-- This is not tested because it intentionally does not compile. -->

<Listing number="17-28" caption="Defining the signature of `timeout`" file-name="src/main.rs">

```rust,ignore
{{#rustdoc_include ../../listings/ch17-async-await/listing-17-28/src/main.rs:declaration}}
```

</Listing>

Sásaíonn sé sin ár spriocanna do na cineálacha. Anois smaoinímis ar an _iompar_ atá de dhíth orainn: ba mhaith linn rás a dhéanamh idir an todhchaí a chuirtear isteach agus an fad ama. Is féidir linn `trpl::sleep` a úsáid chun todhchaí lasc ama a chruthú ón fad ama, agus `trpl::race` a úsáid chun
an lasc ama sin a rith leis an todhchaí a chuireann an glaoiteoir isteach.

Tá a fhios againn freisin nach bhfuil `race` cothrom, ag bailiú argóintí san ord ina
ritheann siad. Dá bhrí sin, cuirimid `future_to_try` chuig `race` ar dtús ionas go mbeidh
seans aige a chríochnú fiú má tá fad an-ghearr ag `max_time`. Má chríochnaíonn `future_to_try` ar dtús, cuirfidh `race` `Left` ar ais leis an aschur ó
`future_to_try`. Má chríochnaíonn `timer` ar dtús, cuirfidh `race` `Right` ar ais le
aschur an lasc ama de `()`.

I Liostáil 17-29, déanaimid meaitseáil ar thoradh fanacht le `trpl::race`.

<Listing number="17-29" caption="Defining `timeout` with `race` and `sleep`" file-name="src/main.rs">

```rust
{{#rustdoc_include ../../listings/ch17-async-await/listing-17-29/src/main.rs:implementation}}
```

</Listing>

Má éiríonn leis an `future_to_try` agus má fhaighimid `Left(output)`, cuirimid `Ok(output)` ar ais. Má théann an lasc ama codlata thart ina ionad sin agus má fhaighimid `Right(())`, déanaimid neamhaird den `()` le `_` agus cuirimid `Err(max_time)` ar ais ina ionad.

Leis sin, tá `timeout` oibre againn atá tógtha as dhá chúntóir neamhshioncrónach eile. Má
rithimid ár gcód, priontáilfidh sé an modh teipe tar éis an ama deiridh:

```text
Failed after 2 seconds
```

Ós rud é go gcuireann todhchaí le chéile todhchaí eile, is féidir leat uirlisí an-chumhachtacha a thógáil
ag baint úsáide as bloic thógála níos lú neamhshioncrónacha. Mar shampla, is féidir leat an cur chuige céanna seo a úsáid
chun sosanna ama a chomhcheangal le hathiarrachtaí, agus iad sin a úsáid le hoibríochtaí ar nós
glaonna líonra (ceann de na samplaí ó thús na caibidle).

Go praiticiúil, is gnách go n-oibreoidh tú go díreach le `async` agus `await`, agus
sa dara háit le feidhmeanna agus macraí ar nós `join`, `join_all`, `race`, agus mar sin de. Ní bheidh ort ach teacht ar `pin` anois is arís chun todhchaí a úsáid leis na
APIanna sin.

Tá roinnt bealaí feicthe againn anois chun oibriú le todhchaí iolracha ag an am céanna.
An chéad rud eile, féachfaimid ar an gcaoi a bhféadfaimid oibriú le todhchaí iolracha i
seicheamh thar am le _streams_. Seo cúpla rud eile a d'fhéadfá a mheas ar dtús, áfach:

- D'úsáideamar `Vec` le `join_all` chun fanacht go gcríochnóidh na todhchaí go léir i ngrúpa éigin
le chéile. Conas a d'fhéadfá `Vec` a úsáid chun grúpa todhchaíochtaí a phróiseáil in ord ina ionad? Cad iad na comhbhabhtálacha a bhaineann leis sin a dhéanamh?

- Féach ar an gcineál `futures::stream::FuturesUnordered` ón gcliathbhosca `futures`. Cén chaoi a mbeadh sé difriúil idir é a úsáid agus `Vec` a úsáid? (Ná bíodh imní ort faoin bhfíric go bhfuil sé ón gcuid `stream` den chliathbhosca; oibríonn sé go breá le haon bhailiúchán todhchaíochtaí.)

[dyn]: ch12-03-improving-error-handling-and-modularity.html
[enum-alt]: ch12-03-improving-error-handling-and-modularity.html#returning-errors-from-the-run-function
[async-program]: ch17-01-futures-and-syntax.html#our-first-async-program
[iterator-trait]: ch13-02-iterators.html#the-iterator-trait-and-the-next-method