## Todhchaí agus an Comhréir Asyncrónach

Is iad _futures_ agus eochairfhocail Rust
`async` agus `await` príomhghnéithe na cláir asyncrónaí i Rust.

Is luach é _future_ nach bhfuil réidh anois ach a bheidh réidh ag pointe éigin sa todhchaí. (Feictear an coincheap céanna seo i go leor teangacha, uaireanta faoi ainmneacha eile ar nós _task_ nó _promise_.) Soláthraíonn Rust tréith `Future` mar bhloc tógála ionas gur féidir oibríochtaí asyncrónacha éagsúla a chur i bhfeidhm le
struchtúir sonraí éagsúla ach le comhéadan coiteann. I Rust, is cineálacha iad todhchaí a chuireann an tréith `Future` i bhfeidhm. Tá a fhaisnéis féin ag gach todhchaí faoin dul chun cinn atá déanta agus cad is brí le "réidh".

Is féidir leat an eochairfhocal `async` a chur i bhfeidhm ar bhloic agus ar fheidhmeanna chun a shonrú gur féidir iad a bhriseadh agus a atosú. Laistigh de bhloc asyncrónach nó de fheidhm asyncrónach, is féidir leat an eochairfhocal `await` a úsáid chun _await a dhéanamh ar thodhchaí_ (is é sin, fanacht go mbeidh sé
réidh). Aon phointe ina bhfuil tú ag fanacht le todhchaí laistigh de bhloc nó feidhm neamhshioncrónach is
áit fhéideartha é don bhloc nó don fheidhm neamhshioncrónach sin sos a chur air agus atosú. Tugtar
_polling_ ar an
próiseas seiceáil le todhchaí chun a fháil amach an bhfuil a luach ar fáil fós.

Úsáideann roinnt teangacha eile, amhail C# agus JavaScript, eochairfhocail `async` agus `await`
le haghaidh cláir neamhshioncrónach. Má tá tú eolach ar na teangacha sin, féadfaidh tú
roinnt difríochtaí suntasacha a thabhairt faoi deara i gcaoi a ndéanann Rust rudaí, lena n-áirítear conas a
láimhseálann sé an comhréir. Tá cúis mhaith leis sin, mar a fheicfimid!

Nuair a bhíonn Rust neamhshioncrónach á scríobh againn, úsáidimid na heochairfhocail `async` agus `await` an chuid is mó den
am. Tiomsaíonn Rust iad i gcód coibhéiseach ag baint úsáide as an tréith `Future`, díreach mar a
thiomsaíonn sé lúba `for` i gcód coibhéiseach ag baint úsáide as an tréith `Iterator`. Toisc
go soláthraíonn Rust an tréith `Future`, áfach, is féidir leat é a chur i bhfeidhm freisin do do chineálacha sonraí féin nuair is gá duit. Tugann go leor de na feidhmeanna a fheicfimid ar fud na caibidle seo cineálacha ar ais lena gcur i bhfeidhm féin de `Future`. Fillfimid ar
shainmhíniú an tréithe ag deireadh na caibidle agus déanfaimid iniúchadh níos doimhne ar conas
a oibríonn sé, ach is leor an méid seo chun sinn a choinneáil ag bogadh ar aghaidh.

D’fhéadfadh sé seo go léir a bheith beagáinín teibí, mar sin scríobhaimis ár gcéad chlár neamhshioncrónach:
scríobán gréasáin beag. Cuirfimid dhá URL isteach ón líne ordaithe, gheobhaimid an dá cheann acu ag an am céanna, agus cuirfimid toradh cibé ceann a chríochnaíonn ar ais ar dtús. Beidh go leor comhréir nua sa
shampla seo, ach ná bíodh imní ort - míneoimid
gach rud a theastaíonn uait a bheith ar eolas agat de réir mar a théimid ar aghaidh.

## Ár gCéad Chlár Neamhshioncrónach

Chun fócas na caibidle seo a choinneáil ar fhoghlaim neamhshioncrónach seachas páirteanna
den éiceachóras a mheascadh, chruthaíomar an cliathbhosca `trpl` (is giorrúchán é `trpl` do “The Rust
Programming Language”). Déanann sé ath-onnmhairiú ar na cineálacha, tréithe agus feidhmeanna go léir
a bheidh uait, go príomha ó na cliathbhoscaí [`futures`][futures-crate]<!-- ignore --> agus
[`tokio`][tokio]<!-- ignore -->. Is baile oifigiúil é an cliathbhosca `futures`
le haghaidh turgnamhaíochta Rust le haghaidh cód asyncrónach, agus is ann a dearadh an tréith `Future`
ar dtús. Is é Tokio an t-am rith asyncrónach is mó a úsáidtear i
Rust inniu, go háirithe le haghaidh feidhmchlár gréasáin. Tá amanna rith iontacha eile amuigh
ann, agus d'fhéadfadh siad a bheith níos oiriúnaí do do chuspóirí. Úsáidimid an cliathbhosca `tokio`
faoin gcochall le haghaidh `trpl` toisc go bhfuil sé tástáilte go maith agus in úsáid go forleathan.

I gcásanna áirithe, athainmníonn nó fillteann `trpl` na APIanna bunaidh freisin chun tú a choinneáil dírithe ar na sonraí a bhaineann leis an gcaibidil seo. Más mian leat tuiscint a fháil ar cad
a dhéanann an cliathbhosca, molaimid duit [a chód
foinse][crate-source]<!-- ignore --> a sheiceáil. Beidh tú in ann a fheiceáil cén cliathbhosca as a dtagann gach
ath-onnmhairiú, agus tá tráchtanna fairsinge fágtha againn ag míniú cad a dhéanann an
cliathbhosca.

Cruthaigh tionscadal dénártha nua darb ainm `hello-async` agus cuir an cliathbhosca `trpl` leis mar
spleáchas:

```console
$ cargo new hello-async
$ cd hello-async
$ cargo add trpl
```

Anois is féidir linn na píosaí éagsúla a sholáthraíonn `trpl` a úsáid chun ár gcéad chlár neamhshioncrónach a scríobh. Tógfaimid uirlis bheag líne ordaithe a bhailíonn dhá leathanach gréasáin, a tharraingíonn an eilimint `<title>` ó gach ceann acu, agus a phriontálann teideal cibé leathanach a chríochnaíonn an próiseas iomlán sin ar dtús.

### An Fheidhm page_title a Shainmhíniú

Tosaímid trí fheidhm a scríobh a ghlacann URL leathanaigh amháin mar pharaiméadar, a dhéanann iarratas air, agus a thugann téacs an eilimint teidil ar ais (féach Liostáil 17-1).

<Listing number="17-1" file-name="src/main.rs" caption="Defining an async function to get the title element from an HTML page">

```rust
{{#rustdoc_include ../../listings/ch17-async-await/listing-17-01/src/main.rs:all}}
```

</Listing>


Ar dtús, sainmhínímid feidhm darb ainm `page_title` agus marcálaimid í leis an eochairfhocal `async`. Ansin úsáidimid an fheidhm `trpl::get` chun cibé URL a chuirtear isteach a fháil agus cuirimid an eochairfhocal `await` leis chun fanacht leis an bhfreagra. Chun téacs an
fhreagra a fháil, glaoimid ar a mhodh `text`, agus fanfaimid air arís leis an eochairfhocal `await`. Tá an dá chéim seo asincrónach. Maidir leis an bhfeidhm `get`, caithfimid
fanacht go seolfaidh an freastalaí an chéad chuid dá fhreagra ar ais, lena n-áirítear
ceanntásca HTTP, fianáin, agus mar sin de, agus is féidir é a sheachadadh ar leithligh ó
chorp an fhreagra. Go háirithe má tá an corp an-mhór, féadfaidh sé tamall a thógáil
chun go dtiocfaidh sé ar fad. Toisc go gcaithfimid fanacht go dtiocfaidh _iomlán_ an fhreagra, tá an modh `text` asincrónach freisin. Caithfimid fanacht go sainráite leis an dá thodhchaí seo, mar go bhfuil todhchaí i Rust
_leisciúil_: ní dhéanann siad aon rud go dtí go n-iarrann tú orthu é sin a dhéanamh leis an eochairfhocal `await`.
(Go deimhin, taispeánfaidh Rust rabhadh tiomsaitheora mura n-úsáideann tú todhchaí.)

D’fhéadfadh sé seo
go gcuirfeadh sé seo i gcuimhne duit plé Chaibidil 13 ar athráiteoirí sa chuid
[Sraith Míreanna a Phróiseáil le hAthráiteoirí][iterators-lazy]<!-- neamhaird a dhéanamh -->.

Ní dhéanann athráiteoirí aon rud mura nglaonn tú ar a modh `next`—bíodh sé go díreach nó trí
lúba `for` nó modhanna ar nós `map` a úsáideann `next` faoin gcochall a úsáid.

Mar an gcéanna, ní dhéanann todhchaí aon rud mura n-iarrann tú go sainráite orthu é sin a dhéanamh. Ligeann an leisciúlacht seo
do Rust gan cód neamhshioncrónach a rith go dtí go mbeidh gá leis i ndáiríre.

> Nóta: Tá sé seo difriúil ón iompar a chonaiceamar sa chaibidil roimhe seo agus
> ag úsáid `thread::spawn` i [Snáithe Nua a Chruthú le
> spawn][thread-spawn]<!--ignore-->, áit ar thosaigh an dúnadh a thugamar chuig snáithe eile
> ag rith láithreach. Tá sé difriúil freisin ón gcaoi a dtéann go leor teangacha eile
> i ngleic le neamhshioncrónach. Ach tá sé tábhachtach do Rust, agus feicfimid cén fáth
> níos déanaí.

Nuair a bheidh `response_text` againn, is féidir linn é a pharsáil i gcás den chineál `Html`
ag baint úsáide as `Html::parse`. In ionad teaghrán amh, tá cineál sonraí againn anois
is féidir linn a úsáid chun oibriú leis an HTML mar struchtúr sonraí níos saibhre. Go háirithe, is féidir linn
an modh `select_first` a úsáid chun an chéad chás de roghnóir CSS ar leith a aimsiú. Trí an teaghrán `"title"` a rith, gheobhaimid an chéad eilimint `<title>`
sa doiciméad, más ann dó. Ós rud é nach bhféadfadh aon eilimint chomhoiriúnach a bheith ann, tugann `select_first` `Option<ElementRef>` ar ais. Ar deireadh, úsáidimid an modh
`Option::map`, rud a ligeann dúinn oibriú leis an mír sa `Option` má tá sé
i láthair, agus gan aon rud a dhéanamh mura bhfuil. (D'fhéadfaimis abairt `match` a úsáid
anseo freisin, ach tá `map` níos idiomataí.) I gcorp na feidhme a sholáthraímid do
`map`, glaoimid ar `inner_html` ar an `title_element` chun a ábhar a fháil, arb é
`String` é. Nuair a bheidh gach rud ráite agus déanta, tá `Option<String>` againn.

Tabhair faoi deara go dtéann eochairfhocal `await` Rust _i ndiaidh_ an abairt atá tú ag fanacht leis,
ní roimhe. Is é sin, is eochairfhocal _postfix_ é. D'fhéadfadh sé seo a bheith difriúil ón méid
a bhfuil tú cleachtaithe leis má d'úsáid tú `async` i dteangacha eile, ach i Rust déanann sé
slabhraí modhanna i bhfad níos deise le hoibriú leo. Mar thoradh air sin, is féidir linn corp `page_url_for` a athrú chun glaonna feidhme `trpl::get` agus `text` a shlabhrú le chéile
le `await` eatarthu, mar a thaispeántar i Liostáil 17-2.

<Listing number="17-2" file-name="src/main.rs" caption="Chaining with the `await` keyword">

```rust
{{#rustdoc_include ../../listings/ch17-async-await/listing-17-02/src/main.rs:chaining}}
```

</Listing>

Leis sin, tá ár gcéad fheidhm neamhshioncrónach scríofa againn go rathúil! Sula gcuirfimid
roinnt cóid i `main` chun glaoch air, labhraimis beagán níos mó faoi na rudaí atá
scríofa againn agus cad is brí leis.

Nuair a fheiceann Rust bloc atá marcáilte leis an eochairfhocal `async`, tiomsaíonn sé é i
gcineál sonraí uathúil, gan ainm a chuireann an tréith `Future` i bhfeidhm. Nuair a fheiceann Rust
feidhm atá marcáilte le `async`, tiomsaíonn sé í i bhfeidhm neamh-neamhshioncrónach a bhfuil a
corp ina bhloc neamhshioncrónach. Is é cineál an
chineáil sonraí gan ainm a chruthaíonn an tiomsaitheoir don bhloc neamhshioncrónach sin cineál tuairisceáin feidhme neamhshioncrónach.

Dá bhrí sin, is ionann `async fn` a scríobh agus feidhm a scríobh a thugann
_future_ den chineál tuairisceáin ar ais. Don tiomsaitheoir, is ionann sainmhíniú feidhme amhail an
`async fn page_title` i Liosta 17-1 agus feidhm neamh-neamhshioncrónach
sainmhínithe mar seo:

```rust
# extern crate trpl; // required for mdbook test
use std::future::Future;
use trpl::Html;

fn page_title(url: &str) -> impl Future<Output = Option<String>> + '_ {
    async move {
        let text = trpl::get(url).await.text().await;
        Html::parse(&text)
            .select_first("title")
            .map(|title| title.inner_html())
    }
}
```

Siúlaimis trí gach cuid den leagan claochlaithe:

- Úsáideann sé comhréir `impl Trait` a phléamar siar i gCaibidil 10 sa chuid
[“Traits as Parameters”][impl-trait]<!-- ignore -->.
- Is é an tréith a chuirtear ar ais ná `Future` le cineál gaolmhar de `Output`. Tabhair faoi deara
gurb é an cineál `Output` ná `Option<String>`, atá mar an gcéanna leis an mbunchineál tuairisceáin ón leagan `async fn` de `page_title`.
- Tá an cód ar fad a ghlaoitear i gcorp na feidhme bunaidh fillte i mbloc `async move`. Cuimhnigh gur léirithe iad na bloic. Is é an bloc iomlán seo an léiriú a chuirtear ar ais ón bhfeidhm.

- Ginfidh an bloc async seo luach leis an gcineál `Option<String>`, mar a thuairiscítear díreach. Meaitseálann an luach sin leis an gcineál `Output` sa chineál tuairisceáin. Tá sé seo díreach cosúil le bloic eile a chonaic tú.
- Is bloc `async move` an corp feidhme nua mar gheall ar an gcaoi a n-úsáideann sé an paraiméadar `url`. (Labhróimid i bhfad níos mó faoi `async` i gcoinne `async move` níos déanaí sa chaibidil.)
- Tá cineál saoil ag an leagan nua den fheidhm nach bhfacamar cheana sa chineál aschuir: `'_`. Toisc go dtugann an fheidhm todhchaí ar ais a thagraíonn do thagairt—sa chás seo, an tagairt ón bparaiméadar `url`—ní mór dúinn a rá le Rust gur mian linn an tagairt sin a chur san áireamh. Ní gá dúinn ainm a thabhairt don saolré anseo, mar tá Rust cliste go leor chun a fhios a bheith aige nach bhfuil ach tagairt amháin ann a d'fhéadfadh a bheith i gceist, ach _caithfimid_ a bheith soiléir go bhfuil an todhchaí mar thoradh air sin ceangailte leis an saolré sin.

Anois is féidir linn glaoch ar `page_title` i `main`.

## Teideal Leathanach Aonair a Chinneadh

Chun tús a chur leis, gheobhaimid teideal do leathanach aonair. I Liosta 17-3, leanann muid an patrún céanna a d'úsáideamar i gCaibidil 12 chun argóintí líne ordaithe a fháil sa chuid
[Ag Glacadh le hArgóintí Líne Ordaithe][cli-args]<!-- neamhaird a dhéanamh -->. Ansin, cuirimid an chéad URL `page_title` ar aghaidh agus fanfaimid ar an toradh. Ós rud é gur `Option<String>` an ​​luach
a tháirgeann an todhchaí, úsáidimid abairt `match` chun
teachtaireachtaí éagsúla a phriontáil chun cuntas a thabhairt ar cibé an raibh `<title>` ar an leathanach.

<Listing number="17-3" file-name="src/main.rs" caption="Calling the `page_title` function from `main` with a user-supplied argument">

```rust,ignore,does_not_compile
{{#rustdoc_include ../../listings/ch17-async-await/listing-17-03/src/main.rs:main}}
```

</Listing>


Ar an drochuair, ní thiomsaíonn an cód seo. Is i bhfeidhmeanna nó i mbloic async amháin is féidir linn an eochairfhocal `await` a úsáid, agus ní ligfidh Rust dúinn an fheidhm `main` speisialta a mharcáil mar `async`.


<!-- manual-regeneration
cd listings/ch17-async-await/listing-17-03
cargo build
copy just the compiler error
-->

```text
error[E0752]: `main` function is not allowed to be `async`
 --> src/main.rs:6:1
  |
6 | async fn main() {
  | ^^^^^^^^^^^^^^^ `main` function is not allowed to be `async`
```

Is é an fáth nach féidir `main` a mharcáil mar `async` ná go bhfuil _runtime_ ag teastáil ó chód asyncrónach: cliathbhosca Rust a bhainistíonn sonraí fhorghníomhú cód asyncrónach. Is féidir le feidhm `main` cláir am rith a _thosú_, ach ní am rith é
_féin_. (Feicfimid tuilleadh faoin gcúis atá leis seo i gceann tamaill.) Tá áit amháin ar a laghad ag gach clár Rust
a fhorghníomhaíonn cód asyncrónach ina socraíonn sé
am rith agus ina bhforghníomhaíonn sé na todhchaí.

Déanann formhór na dteangacha a thacaíonn le async am rith a phacáistiú, ach ní dhéanann Rust. Ina áit sin,
tá go leor am rith asyncrónach éagsúil ar fáil, agus déanann gach ceann acu
malairtí éagsúla oiriúnach don chás úsáide a spriocdhíríonn sé air. Mar shampla, tá riachtanais an-difriúla ag freastalaí gréasáin ard-tréchur le go leor croíthe LAP agus méid mór RAM ná mar atá ag micrea-rialaitheoir le croí amháin, méid beag RAM, agus gan
chumas leithdháilte carn. Is minic a sholáthraíonn na cliathbhoscaí a sholáthraíonn na hamanna rith sin leaganacha neamhshioncrónacha de fheidhmiúlacht choitianta amhail comhad nó líonra I/O.

Anseo, agus ar fud an chuid eile den chaibidil seo, úsáidfimid an fheidhm `run` ón gcliathbhosca `trpl`, a ghlacann todhchaí mar argóint agus a ritheann go dtí go gcríochnaítear é.
Taobh thiar de na radhairc, socraíonn glaoch ar `run` am rith a úsáidtear chun an todhchaí a rith
a chuirtear isteach. Nuair a chríochnaíonn an todhchaí, tugann `run` cibé luach a tháirg an todhchaí ar ais.

D’fhéadfaimis an todhchaí a thugann `page_title` ar ais a chur go díreach chuig `run`, agus nuair a chríochnaíonn sé, d’fhéadfaimis meaitseáil a dhéanamh ar an `Option<String>` mar thoradh air sin, mar a rinneamar iarracht a dhéanamh i Liosta 17-3. Mar sin féin, i gcás fhormhór na samplaí sa chaibidil (agus formhór an chóid asyncrónaigh sa saol réadúil), beidh níos mó ná glao feidhme asyncrónach amháin á dhéanamh againn, mar sin ina ionad sin cuirfimid bloc `async` ar aghaidh agus fanfaimid go sainráite ar thoradh an ghlao `page_title`, mar atá i Liostáil 17-4.


<Listing number="17-4" caption="Awaiting an async block with `trpl::run`" file-name="src/main.rs">

<!-- should_panic,noplayground because mdbook test does not pass args -->

```rust,should_panic,noplayground
{{#rustdoc_include ../../listings/ch17-async-await/listing-17-04/src/main.rs:run}}
```

</Listing>

Nuair a ritheann muid an cód seo, faighimid an t-iompar a raibh súil againn leis ar dtús:


<!-- manual-regeneration
cd listings/ch17-async-await/listing-17-04
cargo build # skip all the build noise
cargo run https://www.rust-lang.org
# copy the output here
-->

```console
$ cargo run -- https://www.rust-lang.org
    Finished `dev` profile [unoptimized + debuginfo] target(s) in 0.05s
     Running `target/debug/async_await 'https://www.rust-lang.org'`
The title for https://www.rust-lang.org was
            Rust Programming Language
```

Ó, tá cód neamhshioncrónach ag obair againn faoi dheireadh! Ach sula gcuirfimid an cód leis chun rás a dhéanamh idir an dá shuíomh, déanaimis ár n-aird a dhíriú go hachomair ar an gcaoi a n-oibríonn
todhchaí.

Léiríonn gach pointe _await_—is é sin, gach áit a n-úsáideann an cód an eochairfhocal `await`—áit ina dtugtar smacht ar ais don am rith. Chun
sin a chur ag obair, ní mór do Rust súil a choinneáil ar an staid atá i gceist sa bhloc neamhshioncrónach
ionas gur féidir leis an am rith obair eile a thosú agus ansin teacht ar ais nuair
a bhíonn sé réidh chun iarracht a dhéanamh an chéad cheann a chur chun cinn arís. Is meaisín stáit dofheicthe é seo,
amhail is dá mba rud é go raibh enum mar seo scríofa agat chun an staid reatha a shábháil ag gach pointe
await:

```rust
{{#rustdoc_include ../../listings/ch17-async-await/no-listing-state-machine/src/lib.rs:enum}}
```

Bheadh ​​sé leadránach agus seans maith go mbeadh earráidí ann an cód a scríobh de láimh chun aistriú idir gach stát, áfach, go háirithe nuair is gá duit níos mó feidhmiúlachta agus
níos mó stát a chur leis an gcód níos déanaí. Ar ámharaí an tsaoil, cruthaíonn agus bainistíonn an tiomsaitheoir Rust struchtúir sonraí an mheaisín stáit le haghaidh cód neamhshioncrónach go huathoibríoch. Tá feidhm fós ag na
gnáthrialacha iasachta agus úinéireachta maidir le struchtúir sonraí, agus
ar ámharaí an tsaoil, láimhseálann an tiomsaitheoir iad sin a sheiceáil dúinn agus soláthraíonn sé
teachtaireachtaí earráide úsáideacha. Oibreoimid trí chúpla ceann díobh sin níos déanaí sa chaibidil.

Sa deireadh thiar, caithfidh rud éigin an meaisín stáit seo a fhorghníomhú, agus is
am rith an rud sin. (Sin é an fáth gur féidir leat teacht ar thagairtí do _fhorghníomhaithe_
agus tú ag féachaint ar amanna rith: is é forghníomhaitheoir an chuid den am rith atá freagrach as
an cód neamhshioncrónach a fhorghníomhú.)

Anois is féidir leat a fheiceáil cén fáth ar stop an tiomsaitheoir sinn ó `main` féin a dhéanamh ina fheidhm neamhshioncrónach ar ais i Liostáil 17-3. Dá mba fheidhm neamhshioncrónach í `main`, bheadh ​​ar rud éigin eile an meaisín stáit a bhainistiú le haghaidh cibé `main` todhchaíoch a sheoltar ar ais, ach is é `main` pointe tosaigh an chláir! Ina áit sin, thugamar ar an bhfeidhm `trpl::run` i `main` chun am rith a bhunú agus an todhchaí a sheoltar ar ais ag an mbloc
`async` a rith go dtí go seoltar `Ready` ar ais.

> Tabhair faoi deara: Soláthraíonn roinnt am rith macraí ionas gur féidir leat feidhm neamhshioncrónach `main` a scríobh. Athscríobhann na macraí sin `async fn main() { ... }` le bheith ina `fn
> main` gnáth, rud a dhéanann an rud céanna a rinneamar de láimh i Liosta 17-5: glaoigh ar fheidhm
> a ritheann todhchaí go dtí go gcríochnófar é ar an mbealach a dhéanann `trpl::run`.

Anois cuirfimid na píosaí seo le chéile agus féachfaimid conas is féidir linn cód comhuaineach a scríobh.

### Ag Rásaíocht Ár nDhá URL in Aghaidh a gCéile

I Liosta 17-5, glaoimid ar `page_title` le dhá URL éagsúla a chuirtear isteach ón líne ordaithe agus déanaimid rásaíocht eatarthu.

<Listing number="17-5" caption="" file-name="src/main.rs">

<!-- should_panic,noplayground because mdbook does not pass args -->

```rust,should_panic,noplayground
{{#rustdoc_include ../../listings/ch17-async-await/listing-17-05/src/main.rs:all}}
```

</Listing>

Tosaímid trí ghlaoch ar `page_title` do gach ceann de na URLanna arna soláthar ag an úsáideoir. Sábhálaimid na todhchaí mar thoradh air sin mar `title_fut_1` agus `title_fut_2`. Cuimhnigh, ní dhéanann siad seo aon rud fós, mar go bhfuil todhchaí leisciúil agus nílimid tar éis fanacht leo fós. Ansin, cuirimid na todhchaí chuig `trpl::race`, a thugann luach ar ais chun a léiriú cé acu de na todhchaí a tugadh dó a chríochnaíonn ar dtús.

> Nóta: Faoin gcochall, tá `race` bunaithe ar fheidhm níos ginearálta, `select`,
> a chasfaidh tú níos minice air i gcód Rust sa saol réadúil. Is féidir le feidhm `select`
> a lán rudaí a dhéanamh nach féidir leis an bhfeidhm `trpl::race` a dhéanamh, ach tá roinnt castachta breise aici freisin ar féidir linn a scipeáil tharstu faoi láthair.

Is féidir le ceachtar todhchaí "bua" go dlisteanach, mar sin níl ciall le `Result` a thabhairt ar ais. Ina áit sin, tugann `race` cineál ar ais nár chonaiceamar cheana, `trpl::Either`. Tá an cineál `Either` cosúil le `Result` sa mhéid is go bhfuil dhá chás aige. Murab ionann agus `Result`, áfach, níl aon choincheap rath nó teip bácáilte isteach i `Either`. Ina áit sin, úsáideann sé `Left` agus `Right` chun "ceann amháin nó an ceann eile" a léiriú:

```rust
enum Either<A, B> {
    Left(A),
    Right(B),
}
```

Tugann an fheidhm `race` `Left` ar ais le haschur an todhchaí sin má bhuaigh an chéad
argóint, agus `Deas` le haschur an dara hargóint todhchaí má bhuaigh an _sin_
ceann. Meaitseálann sé seo an t-ord ina bhfuil na hargóintí le feiceáil agus an fheidhm á glaoch: tá an chéad argóint ar chlé ón dara hargóint.

Nuashonraímid `page_title` freisin chun an URL céanna a cuireadh isteach a thabhairt ar ais. Ar an mbealach sin, mura bhfuil `<title>` ar an leathanach a fhilleann ar dtús is féidir linn a réiteach, is féidir linn
teachtaireacht bhríoch a phriontáil fós. Agus an fhaisnéis sin ar fáil, críochnaímid trí
ár n-aschur `println!` a nuashonrú chun a léiriú cé acu URL a chríochnaigh ar dtús agus
cad é, más ann dó, an `<title>` don leathanach gréasáin ag an URL sin.

Tá scraper gréasáin beag oibre tógtha agat anois! Roghnaigh cúpla URL agus rith an
uirlis líne ordaithe. B’fhéidir go bhfaighidh tú amach go bhfuil roinnt suíomhanna níos tapúla ná
chéile, agus i gcásanna eile athraíonn an suíomh níos tapúla ó rith go rith. Níos tábhachtaí fós, tá bunghnéithe oibre le todhchaí foghlamtha agat, mar sin anois is féidir linn iniúchadh níos doimhne a dhéanamh ar a bhféadfaimid a dhéanamh le haisioncrónach.

[impl-trait]: ch10-02-traits.html#traits-as-parameters
[iterators-lazy]: ch13-02-iterators.html
[thread-spawn]: ch16-01-threads.html#creating-a-new-thread-with-spawn
[cli-args]: ch12-01-accepting-command-line-arguments.html

<!-- TODO: map source link version to version of Rust? -->

[crate-source]: https://github.com/rust-lang/book/tree/main/packages/trpl
[futures-crate]: https://crates.io/crates/futures
[tokio]: https://tokio.rs
