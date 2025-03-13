## Earráidí do-aisghabhála le `panic!`

Uaireanta tarlaíonn rudaí dona i do chód, agus níl aon rud ar féidir leat a dhéanamh faoi
é. Sna cásanna seo, tá an macra `panic!` ag Rust. Tá dhá bhealach a chur faoi deara a
scaoll i gcleachtas: trí ghníomh a dhéanamh a chuireann scaoll ar ár gcód (amhail
rochtain a fháil ar eagar thar an deireadh) nó trí ghlaoch go sainráite ar an macra `panic!`.
Sa dá chás, is cúis le scaoll inár gclár. De réir réamhshocraithe, déanfaidh na scaoll seo
cló teachtaireacht teip, unwind, glan suas an chairn, agus scor. Tríd an
athróg timpeallacht, is féidir leat freisin Rust taispeáint an chairn glaoch nuair a
tarlaíonn scaoll chun é a dhéanamh níos éasca foinse an scaoll a rianú.

> ### An Cruach a Dhíscaoileadh nó Tobscoir mar Fhreagairt ar Scaoill
>
> De réir réamhshocraithe, nuair a tharlaíonn scaoll tosaíonn an clár _unwinding_, rud a chiallaíonn
> Siúlann Rust cúltaca an chairn agus glanann sé suas na sonraí ó gach feidhm é
> cruinnithe. Mar sin féin, tá go leor oibre ag siúl siar agus ag glanadh suas. Rust,
> mar sin, is féidir leat rogha eile a roghnú láithreach _aborting_,
> a chríochnaíonn an clár gan glanadh suas.
>
> Beidh gá ansin an chuimhne a bhí in úsáid ag an gclár a ghlanadh suas ag an
> córas oibriúcháin. Más rud é i do thionscadal ní mór duit an dénártha iarmhartach a dhéanamh mar
> beag agus is féidir, is féidir leat athrú ó scaoileadh go dtí deireadh a chur le scaoll ag
> ag cur `panic = 'abort'` leis na rannáin `[profile]` cuí i do
> _Cargo.toml_ comhad. Mar shampla, más mian leat deireadh a chur le scaoll i mód scaoileadh,
> cuir é seo leis:
>
> ```toml
> [profile.release]
> scaoll = 'abort'
>

Déanaimis iarracht `panic!` a ghlaoch i gclár simplí:

<Listing file-name="src/main.rs">

```rust,should_panic,panics
{{#rustdoc_include ../../listings/ch09-error-handling/no-listing-01-panic/src/main.rs}}
```

</Listing>

Nuair a bheidh an clár á rith agat, feicfidh tú rud éigin mar seo:

```console
{{#include ../../listings/ch09-error-handling/no-listing-01-panic/output.txt}}
```

Is cúis leis an nglao go `panic!` an teachtaireacht earráide atá sa dá líne dheireanacha.
Taispeánann an chéad líne ár dteachtaireacht scaoll agus an áit inár gcód foinse
tharla an scaoll: léiríonn _src/main.rs:2:5_ gurb í an dara líne í,
an cúigiú carachtar dár gcomhad _src/main.rs_.

Sa chás seo, tá an líne a luaitear mar chuid dár gcód, agus má théann muid chuige sin
líne, feicimid an glao macra `panic!`. I gcásanna eile, d'fhéadfadh an glaoch `panic!`
bheith sa chód a ghlaonn ár gcód air, agus ainm an chomhaid agus uimhir na líne arna dtuairisciú ag
cód duine éigin eile a bheidh sa teachtaireacht earráide ina bhfuil an macra `panic!`
ar a dtugtar, ní líne ár gcód ba chúis leis an nglao scaoll ar deireadh thiar.

<!-- Old heading. Do not remove or links may break. -->

<a id="using-a-panic-backtrace"></a>

Is féidir linn úsáid a bhaint as aisrian na bhfeidhmeanna a tháinig an glaoch `panic!` uathu go figiúr
amach an chuid dár gcód atá ag cruthú na faidhbe. Chun tuiscint a fháil ar conas é a úsáid
cúl-lorg `panic!`, breathnaímis ar shampla eile agus féachaimis cén chaoi a bhfuil sé
tagann glao `panic!` ó leabharlann mar gheall ar fhabht inár gcód seachas
ónár gcód ag glaoch ar an macra go díreach. Tá cód éigin ag baint le liostú 9-1
iarrachtaí rochtain a fháil ar innéacs i veicteoir atá thar raon na n-innéacsanna bailí.

<Listing number="9-1" file-name="src/main.rs" caption="Attempting to access an element beyond the end of a vector, which will cause a call to `panic!`">

```rust,should_panic,panics
{{#rustdoc_include ../../listings/ch09-error-handling/listing-09-01/src/main.rs}}
```

</Listing>

Anseo, táimid ag iarraidh rochtain a fháil ar an 100ú eilimint dár veicteoir (atá ag
innéacs 99 toisc go dtosaíonn an t-innéacsú ag nialas), ach níl ach trí cinn ag an veicteoir
eilimintí. Sa chás seo, beidh Rust scaoll. Ag baint úsáide as `[]` atá ceaptha a thabhairt ar ais
eilimint, ach má éiríonn leat innéacs neamhbhailí, níl aon eilimint a chuireann Rust
d'fhéadfadh filleadh anseo a bheadh ​​ceart.

In C, níl aon sainmhíniú ar iarracht léamh thar dheireadh struchtúir sonraí
iompar. D'fhéadfá a fháil cibé rud atá ag an suíomh i gcuimhne a bheadh
fhreagraíonn don eilimint sin sa struchtúr sonraí, cé go bhfuil an chuimhne
nach mbaineann leis an struchtúr sin. Tugtar _buffer overread_ air seo agus is féidir
leochaileachtaí slándála a bheith mar thoradh air má tá ionsaitheoir in ann an t-innéacs a ionramháil
sa chaoi is gur féidir sonraí a léamh níor cheart ligean dóibh a stóráiltear ina dhiaidh sin
an struchtúr sonraí.

Chun do chlár a chosaint ar an gcineál seo leochaileachta, má dhéanann tú iarracht an
eilimint ag innéacs nach bhfuil ann, stopfaidh Rust a fhorghníomhú agus diúltóidh sé
ar aghaidh. Déanaimis iarracht é agus féach:

```console
{{#include ../../listings/ch09-error-handling/listing-09-01/output.txt}}
```

Léiríonn an earráid seo líne 4 dár _main.rs_ áit a ndéanaimid iarracht an t-innéacs a rochtain
`99` den veicteoir in `v`.

Insíonn an líne `nóta:` dúinn gur féidir linn an timpeallacht `RUST_BACKTRACE` a shocrú
athróg chun aisrian a fháil ar cad go díreach a tharla chun an earráid a chur faoi deara. A
Is éard atá i _backtrace_ ná liosta de na feidhmeanna go léir a glaodh chun é seo a bhaint amach
pointe. Oibríonn backtraces in Rust mar a dhéanann siad i dteangacha eile: an eochair do
Is é an t-aisrian a léamh ná tosú ón mbarr agus léamh go dtí go bhfeiceann tú comhaid leat
scríobh. Sin an áit a dtáinig an fhadhb. Na línte os cionn an spota sin
an cód a d'iarr do chód; tá na línte thíos cód a dtugtar do
cód. D'fhéadfadh go n-áireofaí ar na línte roimh agus tar éis croíchód Rust, caighdeánach
cód leabharlainne, nó cliathbhoscaí atá in úsáid agat. Déanaimis iarracht cúl-lorg a fháil
ag socrú an athróg timpeallachta `RUST_BACKTRACE` chuig aon luach seachas `0`.
Léiríonn liostú 9-2 aschur atá cosúil leis an méid a fheicfidh tú.

<!-- manual-regeneration
cd listings/ch09-error-handling/listing-09-01
RUST_BACKTRACE=1 cargo run
copy the backtrace output below
check the backtrace number mentioned in the text below the listing
-->

<Listing number="9-2" caption="The backtrace generated by a call to `panic!` displayed when the environment variable `RUST_BACKTRACE` is set">

```console
$ RUST_BACKTRACE=1 cargo run
thread 'main' panicked at src/main.rs:4:6:
index out of bounds: the len is 3 but the index is 99
stack backtrace:
   0: rust_begin_unwind
             at /rustc/f6e511eec7342f59a25f7c0534f1dbea00d01b14/library/std/src/panicking.rs:662:5
   1: core::panicking::panic_fmt
             at /rustc/f6e511eec7342f59a25f7c0534f1dbea00d01b14/library/core/src/panicking.rs:74:14
   2: core::panicking::panic_bounds_check
             at /rustc/f6e511eec7342f59a25f7c0534f1dbea00d01b14/library/core/src/panicking.rs:276:5
   3: <usize as core::slice::index::SliceIndex<[T]>>::index
             at /rustc/f6e511eec7342f59a25f7c0534f1dbea00d01b14/library/core/src/slice/index.rs:302:10
   4: core::slice::index::<impl core::ops::index::Index<I> for [T]>::index
             at /rustc/f6e511eec7342f59a25f7c0534f1dbea00d01b14/library/core/src/slice/index.rs:16:9
   5: <alloc::vec::Vec<T,A> as core::ops::index::Index<I>>::index
             at /rustc/f6e511eec7342f59a25f7c0534f1dbea00d01b14/library/alloc/src/vec/mod.rs:2920:9
   6: panic::main
             at ./src/main.rs:4:6
   7: core::ops::function::FnOnce::call_once
             at /rustc/f6e511eec7342f59a25f7c0534f1dbea00d01b14/library/core/src/ops/function.rs:250:5
note: Some details are omitted, run with `RUST_BACKTRACE=full` for a verbose backtrace.
```

</Listing>

Sin go leor aschur! D'fhéadfadh an t-aschur cruinn a fheiceann tú a bheith difriúil ag brath
ar do chóras oibriúcháin agus leagan Rust. D'fhonn backtracks a fháil leis seo
faisnéis, ní mór siombailí dífhabhtaithe a chumasú. Tá siombailí dífhabhtaithe cumasaithe ag
réamhshocraithe nuair a úsáidtear `cargo build` nó `cargo run` gan an bhratach `--release`,
mar atá againn anseo.

San aschur i Liostú 9-2, léiríonn líne 6 den chúlrian go dtí an líne inár
tionscadal is cúis leis an bhfadhb: líne 4 de _src/main.rs_. Más rud é nach bhfuil muid ag iarraidh
ár gclár chun scaoll, ba chóir dúinn tús a chur lenár n-imscrúdú ag an suíomh a luaitear
go dtí an chéad líne ina luaitear comhad a scríobh muid. I Liosta 9-1, áit a bhfuilimid
scríobh d'aon ghnó cód a bheadh ​​scaoll, is é an bealach a shocrú ar an scaoll gan
iarraidh eilimint thar raon na n-innéacsanna veicteora. Nuair a bheidh do cód
scaoll amach anseo, beidh ort a dhéanamh amach cén gníomh atá á dhéanamh ag an gcód
cad iad na luachanna is cúis leis an scaoll agus cad ba cheart don chód a dhéanamh ina ionad sin.

Tiocfaidh muid ar ais chuig `panic!` agus nuair ba cheart agus nár cheart dúinn `panic!` a úsáid chun
láimhseáil coinníollacha earráide sa [“Chun `panic!` nó Gan
`panic!`”][go-scaoll-nó-ní-scaoll]<!-- neamhaird a dhéanamh ar --> alt níos déanaí sa mhír seo
caibidil. Ansin, féachfaimid ar conas a ghnóthú ó earráid ag baint úsáide as `Result`.

[to-panic-or-not-to-panic]: ch09-03-to-panic-or-not-to-panic.html#to-panic-or-not-to-panic