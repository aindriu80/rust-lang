## Pacáistí agus cliathbhoscaí

Is iad na chéad chodanna den chóras modúil a chlúdóidh muid ná pacáistí agus cliathbhoscaí.

Is é _crate_ an méid cód is lú a mheasann an tiomsaitheoir Rust ag a
am. Fiú má ritheann tú `rustc` seachas `rust` agus má éiríonn leat cód foinse amháin
comhad (mar a rinne muid an bealach ar fad ar ais sa "Scríobh agus Rith Clár Meirge"
alt de Chaibidil 1), measann an tiomsaitheoir gur cliathbhosca an comhad sin. cliathbhoscaí
Is féidir modúil a bheith iontu, agus féadfar na modúil a shainiú i gcomhaid eile a fhaigheann
curtha le chéile leis an gcliathbhosca, mar a fheicfimid sna hailt atá le teacht.

Is féidir le cliathbhosca teacht i gceann de dhá fhoirm: cliathbhosca dénártha nó cliathbhosca leabharlainne.
Is cláir iad _dénártha cliathbhoscaí_ is féidir leat a thiomsú d'inrite is féidir leat a rith,
cosúil le clár ordú-líne nó freastalaí. Caithfidh feidhm a bheith ag gach ceann acu ar a dtugtar
`main` a shainmhíníonn cad a tharlaíonn nuair a ritheann an inrite. Na cliathbhoscaí go léir atá againn
Cruthaíodh go dtí seo cliathbhoscaí dénártha.

Níl `main` ag cliathbhoscaí na leabharlainne_, agus ní thiomsaíonn siad chuig an
inrite. Ina áit sin, sainíonn siad feidhmiúlacht a bheartaítear a roinnt leo
tionscadail iolracha. Mar shampla, an gcliathbhosca `rand` a d'úsáideamar i [Caibidil
2][rand] Soláthraíonn <!-- neamhaird --> feidhmiúlacht a ghineann uimhreacha randamacha.
An chuid is mó den am nuair a deir Rustaceans “cliathbhosca”, ciallaíonn siad cliathbhosca leabharlainne, agus siad
“Cliathbhosca” a úsáid go hidirmhalartaithe le coincheap ginearálta ríomhchláraithe na “leabharlainne”.

Is comhad foinse é an _crate root_ a thosaíonn agus a dhéanann an tiomsaitheoir Rust
suas bunmhodúl do chliathbhosca (míneoimid modúil go domhain sa
[“Modúil a Shainmhíniú chun Scóip agus Príobháideacht a Rialú”][modules]<!-- neamhaird a dhéanamh ar -->
alt).

Is éard atá i _pacáiste_ ná beart cliathbhoscaí amháin nó níos mó a sholáthraíonn sraith de
feidhmiúlacht. Tá comhad _Cargo.toml_ i bpacáiste a chuireann síos ar conas
na cliathbhoscaí sin a thógáil. Is pacáiste é lasta i ndáiríre ina bhfuil an cliathbhosca dénártha
don uirlis ordú-líne a bhí in úsáid agat chun do chód a thógáil. An Lasta
pacáiste freisin tá cliathbhosca leabharlainne ar a mbraitheann an gcliathbhosca dénártha. Eile
is féidir le tionscadail a bheith ag brath ar an gcliathbhosca leabharlainne lasta chun an loighic chéanna a úsáid leis an Lasta
úsáidí uirlis ordú-líne. Is féidir an oiread cliathbhoscaí dénártha is tú féin a bheith i bpacáiste
cosúil le, ach ar a mhéad ach cliathbhosca leabharlainne amháin. Caithfidh pacáiste amháin ar a laghad a bheith ann
cliathbhosca, cibé an leabharlann nó cliathbhosca dénártha é.

Siúlfaimid cad a tharlaíonn nuair a chruthaímid pacáiste. Ar dtús cuirimid isteach an
ordú `cargo new my-project`:

```console
$ cargo new my-project
     Created binary (application) `my-project` package
$ ls my-project
Cargo.toml
src
$ ls my-project/src
main.rs
```

Tar éis dúinn `cargo new my-project` a rith, úsáidimid `ls` chun a fheiceáil cad a chruthaíonn Cargo. I
eolaire an tionscadail, tá comhad _Cargo.toml_ ann, rud a thugann pacáiste dúinn.
Tá eolaire _src_ ann freisin ina bhfuil _main.rs_. Oscail _Cargo.toml_ isteach
d’eagarthóir téacs, agus tabhair faoi deara nach bhfuil aon tagairt do _src/main.rs_. Leanann lasta a
coinbhinsiún gurb é _src/main.rs_ an fhréamh cliathbhosca de chliathbhosca dhénártha leis an gcéanna
ainm mar an bpacáiste. Mar an gcéanna, tá a fhios ag lasta go bhfuil an t-eolaire pacáiste
ina bhfuil _src/lib.rs_, tá cliathbhosca leabharlainne leis an ainm céanna sa phacáiste
mar an bpacáiste, agus is é _src/lib.rs_ a fhréamh gcliathbhosca. Gabhann lasta fréamh an chliathbhosca
comhaid chuig `rustc` chun an leabharlann nó an dénártha a thógáil.

Anseo, tá pacáiste againn nach bhfuil ach _src/main.rs_, rud a chiallaíonn sé amháin
tá cliathbhosca dénártha darb ainm `my-project`. Má tá _src/main.rs_ i bpacáiste
agus _src/lib.rs_, tá dhá chliathbhosca aige: dénártha agus leabharlann, an dá cheann acu mar an gcéanna
ainm mar an bpacáiste. Is féidir le cliathbhoscaí dénártha iolracha a bheith ag pacáiste trí chomhaid a chur
san eolaire _src/bin_: beidh gach comhad ina chliathbhosca dhénártha ar leith.

[modules]: ch07-02-defining-modules-to-control-scope-and-privacy.html
[rand]: ch02-00-guessing-game-tutorial.html#generating-a-random-number